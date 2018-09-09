## [Spring MVC Custom Validation](https://www.baeldung.com/spring-mvc-custom-validator)
请求参数验证是web开发中非常基础的部分，有时候业务逻辑的代码行数反而没有表单验证的代码多，另外多个接口的表单验证代码可能存在重复，在`Spring MVC`中可以使用`@NotNull` `@NotEmpty`等注解标记参数不可为Null、不可为空。

当`javax.validation.constraints`包里面内置的规则不够我们用的时候，很自然就想到了是否可以自定义注解和验证规则，答案自然是支持的。

### 参考链接
- https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-config-validation
