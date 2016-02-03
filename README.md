# sophia

- It is about how to create unit tests for ejb3 without an application server;
- No bullshit
- No tricks;
- Simple and straightforward;
- Similar as you doing with Spring Framework.

How to use:

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
        BlockServiceIn blockServiceIn = getBlockServiceIn();
		    
		    someService.setBlockServiceIn(blockServiceIn);
		    someService.run();
	}
}
```



