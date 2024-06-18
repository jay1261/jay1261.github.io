---
title: Spring (4) - Controller 테스트
author: jay
date: 2024-06-18
categories:
  - Spring
tags:
  - Java
  - Spring
source:
---

## 컨트롤러 테스트
---

컨트롤러를 테스트하기 위해서는 몇가지 신경써줘야 하는 것이 있다. MocMvc, WebApplicationContext, 시큐리티 관련 세팅을 해주어야한다.


### 시큐리티 제외 테스트

먼저 처음에는 프로젝트에서 사용하는 시큐리티를 제외시키고 테스트를 하는 방법으로 테스트 코드를 작성했다.
excludeFilters를 작성하고, SecurityConfig 클래스를 지정해주어 기존에 사용하는 시큐리티를 테스트에서 제외시킬 수 있다.

```java
@WebMvcTest(  
        controllers = CommentController.class,  
        excludeFilters = {  
                @ComponentScan.Filter(  
                        type = FilterType.ASSIGNABLE_TYPE,  
                        classes = SecurityConfig.class  
                )  
        }  
)
class CommentControllerTest {
	...
}
```

<br/>

이후 껍데기만 있는 시큐리티 필터를 만들어서 @BeforeEach로 MockMvc를 테스트 시작 전마다 세팅해주는 setup함수를 만들었다. 그리고 유저 정보가 필요한 테스트에서 사용할 테스트 유저 객체를 만들고, mockPrincipal에 넣어주는 mockUserSetup() 함수를 작성했다.

```java
...
class CommentControllerTest {  
    // MockMvc 사용  
    private MockMvc mvc;  
    // 가짜 인증을 위한 Principal 필요  
    private Principal mockPrincipal;  
  
    @Autowired  
    private ObjectMapper objectMapper;  
  
    @Autowired  
    private WebApplicationContext context;  
  
    @MockBean  
    CommentService commentService;  
  
    @BeforeEach  
    public void setup() {  
        mvc = MockMvcBuilders.webAppContextSetup(context)  
                .apply(springSecurity(new MockSpringSecurityFilter())) // 테스트용으로 만든 가짜 필터를 넣어줌  
                .build();  
    }
    
    private void mockUserSetup() {  
    // 컨트롤러에서 @AuthenticationPrincipal에서 유저를 뽑아오기 위해 가짜 유저를 만들어서 Principal에  넣어준다  
    // Mock 테스트 유저 생성  
    SignupRequestDto requestDto = new SignupRequestDto("user111111", "1q2w3e4r!@#$", "tester", "test@mail.com");  
    PasswordEncoder passwordEncoder = new BCryptPasswordEncoder();  
    String encoded = passwordEncoder.encode(requestDto.getPassword());  
  
    User testUser = new User(requestDto, encoded);  
    testUser.setUserRole(UserRole.USER);  
  
    UserDetailsImpl testUserDetails = new UserDetailsImpl(testUser);  
    mockPrincipal = new UsernamePasswordAuthenticationToken(testUserDetails, "", testUserDetails.getAuthorities());  
}
```


<br/>

댓글 등록에 대한 테스트로, this.mockUserSetup() 함수를 사용해서 mockPrincipal에 테스트 유저 정보를 넣어준다. mvc.perform으로 url을 지정해주고 데이터는 objectMapper를 사용해 json을 string 타입으로 만들어 전달한다. .principal을 지정해주어서 mockUserSetup() 함수에서 세팅해준 mockPrincipal을 사용해주어야한다.

```java
@Test  
void 댓글_등록_성공() throws Exception {  
    //given  
    this.mockUserSetup();  
    CommentRequestDto requestDto = new CommentRequestDto("description");  
  
    String data = objectMapper.writeValueAsString(requestDto);  
  
    //when then  
    mvc.perform(post("/posts/1/comments")  
                    .content(data)  
                    .contentType(MediaType.APPLICATION_JSON)  
                    .principal(mockPrincipal)  
            )  
            .andExpect(status().isOk())  
            .andDo(print());  
}
```



--- 

### 시큐리티 포함 테스트

처음엔 시큐리티를 제외시켜야지만 테스트를 할 수 있는 줄 알았다. 하지만 시큐리티를 포함해서 테스트를 할 수 있는 방법이 있다는 것을 알게 되었고, 이를 적용시켜보았다.

ControllerTest라는 클래스를 따로 만들었고, 이는 MockMvc, WebApplicationContext, objectMapper를 필드로 가지고 있다. getTestUser() 메서드는 테스트 유저를 생성해주는 메서드이고, @BeforeEach로 만든 setup() 함수는 MockMvc를 세팅해주고, 시큐리티에 직접 UserDetails를 추가해주는 메서드이다. 이제 다른 컨트롤러 테스트에서는 이 클래스를 상속받아서 사용하면 된다.

```java
public class ControllerTest {  
    // MockMvc 사용  
    @Autowired  
    protected MockMvc mvc;  
    @Autowired  
    private WebApplicationContext context;  
    @Autowired  
    protected ObjectMapper objectMapper;  
  
  
    User getTestUser(){  
        SignupRequestDto requestDto = new SignupRequestDto("user111111", "1q2w3e4r!@#$", "tester", "test@mail.com");  
        PasswordEncoder encoder = new BCryptPasswordEncoder();  
        String encodedPassword = encoder.encode("1q2w3e4r!@#$");  
  
        return new User(requestDto, encodedPassword);  
    }  
  
    @BeforeEach  
    public void setup() {  
        mvc = MockMvcBuilders  
                .webAppContextSetup(context)  
                .build();  
  
        User user = getTestUser();  
        UserDetailsImpl userDetails = new UserDetailsImpl(user);  
  
        // 시큐리티 authentication 에 UserDetails 객체 추가  
        SecurityContextHolder.getContext().setAuthentication(new UsernamePasswordAuthenticationToken(userDetails,userDetails.getPassword(), userDetails.getAuthorities()));  
    }  
}
```

<br/>

시큐리티를 제외시켰을 때랑 다르게 @WebMvcTest() 부분에서 excludeFilters를 지정하지 않고, mvc.perform에서 .principla로 mockPrincipal을 넣어주지 않는다.

```java
  
@WebMvcTest(controllers = CommentController.class)  
class CommentControllerTest extends ControllerTest {  
  
    @MockBean  
    CommentService commentService;  
  
    @Test  
    void 댓글_등록_성공() throws Exception {  
        //given  
        CommentRequestDto requestDto = new CommentRequestDto("description");  
  
        String data = objectMapper.writeValueAsString(requestDto);  
  
        //when then  
        mvc.perform(post("/posts/1/comments")  
                        .content(data)  
                        .contentType(MediaType.APPLICATION_JSON)  
                )  
                .andExpect(status().isOk())  
                .andDo(print());  
    }
    
    ...
}
```

