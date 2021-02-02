基本使用  
```java
//配置开启异步支持，检测@Async注释  
@Configuration
@EnableAsync
public class SpringAsyncConfig { ... }  

//使用@Async注释
//无返回值
@Async
public void asyncMethodWithVoidReturnType() {
     System.out.println("Execute method asynchronously. " + Thread.currentThread().getName());
}

//有返回值
@Async
public Future<String> asyncMethodWithReturnType() {
     System.out.println("Execute method asynchronously - " + Thread.currentThread().getName());
     try {
         Thread.sleep(5000);
         return new AsyncResult<String>("hello world !!!!");
     } catch (InterruptedException e) {
        //
     }
     return null;
}
```  

深入一点点  




参考博客  
1. https://blog.51cto.com/14890701/2518888  
2. https://blog.csdn.net/qq_46388795/article/details/107923432