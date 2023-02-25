# cnj-logging-backend-spring

Cloud native Spring Boot backend with support of cluster logging using an EFK stack:

* everything is logged to stdout (no file appenders)
* uses JSON logging format

## Status

![Build status](https://codebuild.eu-west-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiclY3YllNU2NWeWF3ZmQrNFVPRDc1WFpMTHh1K20vTisxVWVMajk3aUsyS1F2djd4SDhJcU9CSFNrbXk1WDdJUmhIUWROaU5sZ3hLK2dqUWlTdDBSK3BBPSIsIml2UGFyYW1ldGVyU3BlYyI6IkY5aEtiT3M1YWxPVnI3V20iLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=main)

## Release information

Check [changelog](changelog.md) for latest version and release information.

## Enable JSON logging in Spring Boot

In order to switch Spring Boot to JSON logging output format, you will have to proceed through the following steps:

### Add a dependency to the Logstash Logback Encoder

Add a dependency to the Logstash Logback Encoder to your POM:

```xml
<dependency>
    <groupId>net.logstash.logback</groupId>
    <artifactId>logstash-logback-encoder</artifactId>
    <version>${logstash.logback.encoder.version}</version>
</dependency>
```

### Add a Logback configuration file to your application

Add a Logback configuration file name `logback-spring.xml` to resource folder `/src/main/resources`.

A sample configuration file can be found [here](src/main/resources/logback-spring.xml).

The special JSON encoder will be activated when Spring profile `cloud` is activated as well.

## Temporarily switching off JSON logging

If you don't want to use the JSON logging format you simply choose any other Spring profile except profile `cloud`.

> Spring profiles are activated by adding an envvar `SPRING_PROFILES_ACTIVE` with a comma-separated list of profiles name that you wish to activate to your container configuration.
>

## Build this application 

``` 
mvn clean verify -P pre-commit-stage
```

Build results: a Docker image containing a Spring Boot application.
