# ejbunit

- It's about how to create junit test class for ejb3 without an application server;
- Simple; 
- Straightforward.

How to install:

1. download target/ejbunit-0.0.1-SNAPSHOT.jar

2. add local repo

mvn install:install-file -Dfile=<path-to-file>/ejbunit-0.0.1-SNAPSHOT.jar -DgroupId=com.github.andersonfonseka \
    -DartifactId=ejbunit -Dversion=0.0.1-SNAPSHOT -Dpackaging=jar

reference: https://maven.apache.org/guides/mini/guide-3rd-party-jars-local.html

3. add dependency in your pom.xml:

```xml
		<dependency>
			<groupId>com.github.andersonfonseka</groupId>
		    <artifactId>ejbunit</artifactId>
		    <version>0.0.1-SNAPSHOT</version>		
		</dependency>
```

How to use:

DAO Stateless SessionBean

```java

@Stateless
public class SomeDAO {

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
		 EJBUnit ejbUnit = new EJBUnit();
		              someService = (SomeService) ejbUnit.getBean(SomeService.class);	
	}

  	@Test
	public void testRules() {
		someService.execute();
	}
}
```



