### boxfuse
---
https://github.com/boxfuse/cloudwatchlogs-java-appender

https://boxfuse.com/

```java
// cloudwatchlogs-java-appender/src/test/jav/com/boxfuse/cloudwatchlogs/log4j2/Log4J2SmallTest.java

public class Log4J2SmallTest {
  @Test
  public void log() throws Exception {
    ThreadContext.put("my-custom-key", "my-custom-value");
    ThreadContext.put("my-invalid-key", "my-invalid-value");
    checkLog("OK", null, "OK");
    checkLog("ABC", new IllegalArgumentException("XYZ"), "ABC\\njava.lang.IllegalArgumntException: XYZ");
  }
  
  private void checkLog(String inMsg, Throwable inEx, String outMsg) throws Exception {
    PrintStream original = System.out;
    ByteArrayOutStream baos = new ByteArrayOutputStream();
    System.setOut(new PrintStream(baos));
    
    Logger logger = LogManager.getLogger("log4j2_test");
    logger.info(inMsg, inEx);
    Thread.sleep(1000);
    
    String stdOut = baos.toString("UTF-8");
    assertThat(stdOut, containsString(outMsg));
    assertThat(stdOut, containsString("my-custom-value"));
    assertThat(stdOut, not(containsString("my-invalid-value")));
    
    System.setOut(original);
  }
}


```

```
```

```
```


