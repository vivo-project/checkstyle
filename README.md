# VIVO Checkstyle
Repository of VIVO checkstyle rules

The purpose of this repository is to provide resources for maintaining consistent coding style. The resources in this repository are designed as a refinement of the [DuraSpace codestyle](https://github.com/duraspace/codestyle) rules for all VIVO/Vitro projects as well as any other individuals or projects interested in maintaining a coding style consistent with well established open source projects.

[Checkstyle](#checkstyle) | [Code Style Guide](#code-style-guide) | [IDE Support](#ide-support) | [License](#license)

## Checkstyle

<p align="center">
  <a href="http://checkstyle.sourceforge.net"><img src="http://checkstyle.sourceforge.net/images/header-checkstyle-logo.png" alt="Checkstyle Logo"/></a>
</p>

[Checkstyle](https://github.com/checkstyle/checkstyle) is a development tool for Java, used to ensure that code standards are applied consistently.

Checkstyle can be enabled in Java projects with Maven using the [Maven Checkstyle Plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin). Add the following into the <build><plugins> section of your Maven POM.xml file:

```xml
<!-- Used to validate all code style rules in source code using Checkstyle -->
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-checkstyle-plugin</artifactId>
    <version>3.0.0</version>
    <executions>
        <execution>
            <id>verify-style</id>
            <!-- Bind to verify so it runs after package & unit tests, but before install -->
            <phase>verify</phase>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <configLocation>duraspace-checkstyle/checkstyle.xml</configLocation>
        <suppressionsLocation>vitro-checkstyle/checkstyle-suppressions.xml</suppressionsLocation>
        <encoding>UTF-8</encoding>
        <consoleOutput>true</consoleOutput>
        <logViolationsToConsole>true</logViolationsToConsole>
        <failOnViolation>true</failOnViolation>
        <includeTestSourceDirectory>true</includeTestSourceDirectory>
    </configuration>
    <dependencies>
        <dependency>
            <groupId>org.duraspace</groupId>
            <artifactId>codestyle</artifactId>
            <version>${duraspace-codestyle.version}</version>
        </dependency>
        <dependency>
            <groupId>org.vivoweb</groupId>
            <artifactId>checkstyle</artifactId>
            <version>${vivo-checkstyle.version}</version>
        </dependency>
        <!-- Override dependencies to use latest version of checkstyle -->
        <dependency>
            <groupId>com.puppycrawl.tools</groupId>
            <artifactId>checkstyle</artifactId>
            <version>8.18</version>
        </dependency>
    </dependencies>
</plugin>
```

Once this configuration is in place, executing a build on the project  (`mvn clean install` ) will trigger checkstyle checks which will cause the build to fail if a style violation is encountered.

## License

All resources in this repository are made available under the [Apache 2 license](https://www.apache.org/licenses/LICENSE-2.0).
