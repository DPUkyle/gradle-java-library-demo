# Classpath isolation demo

The 3 projects demonstrate ["implementation" vs. "api" classpath isolation](https://docs.gradle.org/current/userguide/java_library_plugin.html#sec:java_library_separation) by Gradle's "java-library" plugin. Note that this works out of the box only for Maven, not for ivy consumers.

# Updated 2021-02-16 showing failure when using unconventional Ivy setup

In this example, we have difficulty deriving `apiElements`/`runtimeElements` variants from Ivy metadata when the "primary"
artifact is not on the `compile`, `runtime` or `default` configurations.  In this example we hack the `producer` project to manipulate 
the descriptor, associating its sole artifact with the `master` configuration.

Note that when building the `ivy-consumer` jar, the parent interface cannot be found and classpath logging in the console shows
that the `apiElements` variant is correctly derived, but is missing the "primary" producer.jar artifact.

## Steps to reproduce

1. `cd producer`, then `./gradlew publishIvyPublicationToIvyRepo`. Note contents of descriptor at `less ~/local-ivy-repo/com.sample.producer/producer/1.2/ivy-1.2.xml`
2. `cd ivy-consumer`, then `./gradlew assemble`.  Note the echoed CompileJava#classpath does not contain `producer.jar`.
