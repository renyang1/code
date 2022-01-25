## SpringBoot控制配置类的加载顺序

将自己的配置类也配置在 spring.factories 中不一定能实现排序，如果你的类被自己 Spring Boot 启动类扫描到了，这个类的顺序会优先于所有通过 spring.factories 读取的配置类。所以当你的配置类对顺序有要求时就会出错。

### @AutoConfigureAfter



### @AutoConfigureBefore



### @AutoConfigureOrder