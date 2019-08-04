# Classpath isolation demo

The 3 projects demonstrate "implementation" vs. "api" classpath isolation by Gradle "java-library" plugin. Note that this works out of the box only for Maven, not for ivy consumers.

## Use case

- "producer" project is a java library that has "implementation" dependency on guava
- "consumer" projects attempt to compile against "guava" without explicit "guava" compile dependency
- building producer (needed to reproduce):

```
cd producer
./gradlew publishToMavenLocal publishIvyPublicationToIvyRepo
```

### Maven

Maven consumer correctly fails compilation. Reproduce:

```
cd maven-consumer
./gradlew build
```

### Ivy

Ivy consumer does not fail compilation by default. Reproduce:

```
cd ivy-consumer
./gradlew build
```
