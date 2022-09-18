# REPO for Maven, Docker and etc.

## Gradle (Maven)

Set in $HOME/.gradle/gradle.properties gpr.user to GitHub Username and gpr.key to Personal Access Token.

### Publish

```kotlin
plugins {
    `maven-publish`
}


publishing {
    repositories {
        maven {
            name = "repo"
            url = uri("https://maven.pkg.github.com/Layercraft/repo")
            credentials {
                username = project.findProperty("gpr.user") as String? ?: System.getenv("USERNAME")
                password = project.findProperty("gpr.key") as String? ?: System.getenv("TOKEN")
            }
        }
    }
    publications {
        register<MavenPublication>("gpr") {
            from(components["java"])
        }
    }
}
```

### Pull
```kotlin
repositories {
    maven { 
        url = uri("https://maven.pkg.github.com/Layercraft/repo")
        credentials {
            username = project.findProperty("gpr.user") as String? ?: System.getenv("USERNAME")
            password = project.findProperty("gpr.key") as String? ?: System.getenv("TOKEN")
        }
    }
}

dependencies {
    implementation("io.layercraft.translator:translator-api:0.0.1")
}
```


