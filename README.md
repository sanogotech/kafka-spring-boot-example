# Spring Boot Kafka Example - The Practical Developer

## Basic configuration

This sample application shows how to use basic Spring Boot configuration to set up a producer to a topic with multiple partitions and a consumer group with three different consumers.

The full explanation is on The Practical Developer website: [Spring Boot and Kafka - Practical Configuration Examples](https://thepracticaldeveloper.com/2018/11/24/spring-boot-kafka-config/).

[![Kafka Configuration Example](img/kafka-configuration-example.jpg)](https://thepracticaldeveloper.com/2018/11/24/spring-boot-kafka-config/)

## Multiple serialization / deserialization formats

To illustrate the different configuration options, this application deserializes Kafka messages in three different ways:

* As a JSON to Java object.
* As a simple String (plain JSON).
* As a byte array.

## Docker compose

This code includes a `docker-compose.yml` file so you can use Docker Compose to start up Kafka, no installation needed.

## Did I help you?

Give a star to this project and/or [buy me a coffee](https://buymeacoff.ee/ZyLJNUR) 😄

## Spring boot KAFKA Template

- https://docs.spring.io/spring-kafka/reference/html/#tips-n-tricks

##  Configuration
**server.properties**
```
auto.create.topics.enable=true
```

## logback
- https://www.baeldung.com/spring-boot-logging

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

    <property name="LOGS" value="./logs" />

    <appender name="Console"
        class="ch.qos.logback.core.ConsoleAppender">
        <layout class="ch.qos.logback.classic.PatternLayout">
            <Pattern>
                %black(%d{ISO8601}) %highlight(%-5level) [%blue(%t)] %yellow(%C{1.}): %msg%n%throwable
            </Pattern>
        </layout>
    </appender>

    <appender name="RollingFile"
        class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${LOGS}/spring-boot-logger.log</file>
        <encoder
            class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <Pattern>%d %p %C{1.} [%t] %m%n</Pattern>
        </encoder>

        <rollingPolicy
            class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- rollover daily and when the file reaches 10 MegaBytes -->
            <fileNamePattern>${LOGS}/archived/spring-boot-logger-%d{yyyy-MM-dd}.%i.log
            </fileNamePattern>
            <timeBasedFileNamingAndTriggeringPolicy
                class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <maxFileSize>10MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
    </appender>
    
    <!-- LOG everything at INFO level -->
    <root level="info">
        <appender-ref ref="RollingFile" />
        <appender-ref ref="Console" />
    </root>

    <!-- LOG "com.baeldung*" at TRACE level -->
    <logger name="com.baeldung" level="trace" additivity="false">
        <appender-ref ref="RollingFile" />
        <appender-ref ref="Console" />
    </logger>

</configuration>


```