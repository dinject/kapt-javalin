# kapt-javlin
Maven tile for Kotlin compile, kapt annotation processors for DI and Javlin controllers + java compile

## Add this tile via

```xml

  <build>
    <plugins>

      <plugin>
        <groupId>io.repaint.maven</groupId>
        <artifactId>tiles-maven-plugin</artifactId>
        <version>2.12</version>
        <extensions>true</extensions>
        <configuration>
          <tiles>
            <tile>io.dinject.kapt:javlin:0.1-SNAPSHOT</tile>
          </tiles>
        </configuration>
      </plugin>

    </plugins>
  </build>

```



## This tile brings in


```xml

  <properties>
    <java.version>1.8</java.version>
    <kotlin.version>1.2.71</kotlin.version>
    <kotlin.apiVersion>1.2</kotlin.apiVersion>
    <kotlin.jvmTarget>1.8</kotlin.jvmTarget>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <build>
    <sourceDirectory>src/main/kotlin</sourceDirectory>
    <testSourceDirectory>src/test/kotlin</testSourceDirectory>

    <plugins>

      <plugin>
        <groupId>org.jetbrains.kotlin</groupId>
        <artifactId>kotlin-maven-plugin</artifactId>
        <version>${kotlin.version}</version>
        <configuration>
          <apiVersion>${kotlin.apiVersion}</apiVersion>
          <jvmTarget>${kotlin.jvmTarget}</jvmTarget>
        </configuration>

        <executions>
          <execution>
            <id>kapt</id>
            <goals>
              <goal>kapt</goal>
            </goals>
            <configuration>
              <sourceDirs>
                <sourceDir>src/main/kotlin</sourceDir>
              </sourceDirs>
              <annotationProcessorPaths>
                <annotationProcessorPath>
                  <!-- DInject DI -->
                  <groupId>io.dinject</groupId>
                  <artifactId>dinject-generator</artifactId>
                  <version>0.8</version>
                </annotationProcessorPath>
                <annotationProcessorPath>
                  <!-- Generate web route adapters for Javlin Controllers -->
                  <groupId>io.dinject</groupId>
                  <artifactId>javlin-generator</artifactId>
                  <version>0.3</version>
                </annotationProcessorPath>
              </annotationProcessorPaths>
            </configuration>
          </execution>

          <execution>
            <id>compile</id>
            <phase>compile</phase>
            <goals>
              <goal>compile</goal>
            </goals>
          </execution>
          <execution>
            <id>test-compile</id>
            <phase>test-compile</phase>
            <goals>
              <goal>test-compile</goal>
            </goals>
          </execution>
        </executions>
      </plugin>

      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.0</version>
        <configuration>
          <source>${java.version}</source>
          <target>${java.version}</target>
        </configuration>
        <executions>
          <!-- Replacing default-compile as it is treated specially by maven -->
          <execution>
            <id>default-compile</id>
            <phase>none</phase>
          </execution>
          <!-- Replacing default-testCompile as it is treated specially by maven -->
          <execution>
            <id>default-testCompile</id>
            <phase>none</phase>
          </execution>
          <execution>
            <id>java-compile</id>
            <phase>compile</phase>
            <goals>
              <goal>compile</goal>
            </goals>
          </execution>
          <execution>
            <id>java-test-compile</id>
            <phase>test-compile</phase>
            <goals>
              <goal>testCompile</goal>
            </goals>
          </execution>
        </executions>
      </plugin>

    </plugins>

  </build>
```
