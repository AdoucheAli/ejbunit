# sophia

- It is about how to create junit test class for ejb3 without an application server;
- No tricks;
- Simple and straightforward;
- Similar as you doing with Spring Framework.

How to install:

Coming soon...

How to use:

DAO Stateless SessionBean

```java

@Stateless
public class SomeDAO<T> {

	@PersistenceContext(name="ProjectPU", unitName="ProjectPU")
	private EntityManager entityManagerCreator;

```

Service Stateless SessionBean

```java

@Stateless
public class SomeService {

	@EJB
	private SomeDAO someDAO;

```

Persistence.xml

```xml

	<persistence-unit name="ProjectPUTest" transaction-type="RESOURCE_LOCAL"> 
		<provider>org.eclipse.persistence.jpa.PersistenceProvider</provider> 
		
		<class>package.entity.SomeBean</class>

		<properties> 
			<property name="javax.persistence.jdbc.driver" value="oracle.jdbc.OracleDriver" /> 
			<property name="javax.persistence.jdbc.url" value="jdbc:oracle:thin:@xx.xx.xxx.x:1521:db"/> 
			<property name="javax.persistence.jdbc.user" value="user"/> 
			<property name="javax.persistence.jdbc.password" value="pwd"/> 
		</properties>
		 
	</persistence-unit>

```

Test Class:

```java
public class SomeRuleTest {
  private static SomeService someService;
	
	@Before
	public void setUp() throws Exception {
		 EJBTestUtil testUtil = new EJBTestUtil();
		              someService = (SomeService) testUtil.getBean(SomeService.class);	
	}

  	@Test
	public void testRules() {
		someService.execute();
	}
}
```



