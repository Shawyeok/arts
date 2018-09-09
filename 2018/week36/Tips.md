## Dockerfile集成工程构建环境
项目源代码通过`编译-打包-发布`到各个环境这个过程叫做部署，部署中有非常关键的一部分就是`构建`，构建就需要一个`构建环境`，要求这个环境`稳定`、`无差别`、`易于维护`。

容器化应用的构建过程可以集成到`Dockerfile`中的一个`stage`中，例如下面这个Dockerfile，描述了一个基于`gradle`的`spring boot`应用的构建过程：
```
FROM gradle:jdk8 AS build

ARG DEPLOY_ENV=default

WORKDIR /home/gradle/project

EXPOSE 8080

USER root

ENV GRADLE_USER_HOME /home/gradle/project

COPY . /home/gradle/project

RUN gradle build -x test


FROM java:8 AS runtime

LABEL maintainer "Jon Snow <maintainer@example.com>"

ARG DEPLOY_ENV

WORKDIR /home/gradle/project

EXPOSE 8080

ENV TZ="Asia/Shanghai"

ENV JAVA_OPTS="-Xmn512m -Xms2048m -Xmx2048m -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintGCTimeStamps -XX:+PrintTenuringDistribution -Xloggc:/home/gradle/project/gc.log"

ENV SPRING_PROFILES_ACTIVE ${DEPLOY_ENV}

COPY --from=build /home/gradle/project/build/libs/generic-exam-java-backend.jar .

ENTRYPOINT java ${JAVA_OPTS} -jar generic-exam-java-backend.jar
```

基于`Dockerfile`描述构建环境，主要有以下几点好处：
- 对开发人员透明，一般部署的任务由团队的运维人员负责，部署对于开发人员来说就是一个黑盒，并不知道里面做了什么，而`Dockerfile`可以由开发自已去定义描述项目的构建环境和运行环境
- 构建环境易于复制，通过Dockerfile生成的构建环境具有一致性，不会出现构建环境存在差异的情况
- 环境隔离，工程专属的构建环境，不会和其他项目的构建环境产生干扰
- 易于修改，随着应用的变化，构建环境可能同时随之变化，这时候只需要开发人员修改Dockerfile即可，不用再去和运维沟通自己的环境需要作何种改变

### 参考链接
- https://docs.docker.com/engine/reference/builder/#from
