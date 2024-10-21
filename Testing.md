### Unit Testing

|   Terminology | Description |
| --- | ----------- |
|@SpringBootTest| Loads full application context and allows you to test the complete environment as it would run in production. It also automatically loads properties defined in application.properties|
|@Test| This JUnit annotation is used to denote a test method. It indicates that the method should be executed as a test case.|
|@WebMvcTest| Used for testing Spring MVC controllers. It only loads the web layer and can be used to test controllers without starting the entire application.|
|@DataJpaTest| This annotation is used to test JPA repositories. It configures an in-memory database and scans for JPA repositories, allowing for testing of the repository layer in isolation.|
|@Mock|  It creates mock instance of class but It does not integrate with the Spring application context.|
|@InjectMock| When you annotate a field with @InjectMocks, Mockito looks for any mocks (annotated with @Mock) in the same test class and attempts to inject them into the class under test.|
|@MockBean|This annotation is used to create a mock of a Spring bean and add it to the application context. |
|@BeforeEach| It is used to indicate that the annotated method should be executed before each test method in the test class.|
|||

### Write code to test controller
```
@WebMvcTest(UserController.class)
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    public void testGetUser() throws Exception {
        when(userService.getUser(1L)).thenReturn(new User(1L, "John"));

        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("John"));
    }
}

```
