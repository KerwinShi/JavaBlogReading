源码或者很多配置类上面都会出现@Import注解
功能:@Import注解是用来导入配置类或者一些需要前置加载的类，和Spring XML配置类似.  

基本使用  
1. 直接填class数组方式
2. ImportSelector方式【重点】
3. ImportBeanDefinitionRegistrar方式  

```java  
@Import({ 类名.class , 类名.class... })
public class TestDemo {

}

public class Myclass implements ImportSelector {
//既然是接口肯定要实现这个接口的方法
    @Override
    public String[] selectImports(AnnotationMetadata annotationMetadata) {
        return new String[0];
    }
}

public class Myclass2 implements ImportBeanDefinitionRegistrar {
    @Override
    public void registerBeanDefinitions(AnnotationMetadata annotationMetadata, BeanDefinitionRegistry beanDefinitionRegistry) {
        //指定bean定义信息（包括bean的类型、作用域...）
        RootBeanDefinition rootBeanDefinition = new RootBeanDefinition(TestDemo4.class);
        //注册一个bean指定bean名字（id）
        beanDefinitionRegistry.registerBeanDefinition("TestDemo4444",rootBeanDefinition);
    }
}
```  


深入一点点  
