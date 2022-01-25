## SpringBoot常见注解

### 1、@EnableConfigurationProperties、@ConfigurationProperties

@ConfigurationProperties是为了使使用了@ConfigurationProperties注解的xxx.java类中的属性能和yml中的配置进行绑定,并将xxx.java类被当作一个Bean注册到容器中,为了达到以上目的,有下面两种方式.

1、使用@Component将xxx.java类声明为一个Bean,此时能将xxx.java类注册到容器中,并完成和配置文件中属性的绑定

```java
@Data
@ConfigurationProperties(prefix = "ry")
@Component
public class User {
    private String name;
    private int age;
    private Cat cat;
}
```

2、在配置类(有@Configuration注解的类)上使用@EnableConfigurationProperties(xxx.class)进行声明,同样也能完成和配置文件中属性的绑定并将xxx.java做为Bean注册到容器中.

如果@ConfigurationProperties是在第三方包中，那么@component是不能注入到容器的。只有@EnableConfigurationProperties才可以注入到容器。

```java
@Data
@ConfigurationProperties(prefix = "ry")
//@Component
public class User {
    private String name;
    private int age;
    private Cat cat;
}

Configuration(proxyBeanMethods = false)
@EnableConfigurationProperties(User.class)
public class TestConfig {

}
```

### 2、@Conditional

作用:必须是@conditional注解指定的条件成立,才会将组件真的添加到容器中,里面配置的内容才会生效.

| @Conditional扩展注解作用        | 判断是否满足当前指定条件                                     |
| ------------------------------- | ------------------------------------------------------------ |
| @ConditionalOnJava              | 系统的java版本是否符合要求                                   |
| @ConditionalOnBean              | 容器中存在指定Bean                                           |
| @ConditionalOnMissingBean       | 容器中不存在指定Bean                                         |
| @ConditionalOnExpression        | 满足SpEL表达式指定                                           |
| @ConditionalOnClass             | 系统中有指定的类                                             |
| @ConditionalOnMissingClass      | 系统中没有指定的类                                           |
| @ConditionalOnSingleCandidate   | 容器中只有一个指定的Bean，或者这个Bean是首选Bean             |
| @ConditionalOnProperty          | 系统中指定的属性是否有指定的值                               |
| @ConditionalOnResource          | 类路径下是否存在指定资源文件@ConditionalOnWebApplication 当前是web环境 |
| @ConditionalOnNotWebApplication | 当前不是web环境                                              |
| @ConditionalOnJndi              | JNDI存在指定项                                               |

