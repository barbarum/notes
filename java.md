# Java

## Spring Boot

### Unit Testing

#### Gradle for spring boot unit testing

```bash
dependencies {
    testImplementation('org.springframework.boot:spring-boot-starter-test') {
        exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
    }
}
```

#### Mockito

##### Gradle for mock test

```bash
dependencies {
    testImplementation "org.mockito:mockito-core:2.28.2"
}
```
## Command Line

```bash
jar tf jarfile # View all files from a jarfile.
```
