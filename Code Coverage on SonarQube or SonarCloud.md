Here's your content converted to **Markdown (`.md`)** format:

---

````markdown
# Populate Code Coverage on SonarQube or SonarCloud Dashboard

To populate code coverage on the SonarQube or SonarCloud dashboard, follow these steps:

---

## 1) Update `pom.xml`

### ➤ Change 1 – Dependency for Unit Testing

```xml
<!-- #Change 1 - Changes for Unit Test Coverage Percentage Update on SonarCloud Dashboard -->
<!-- #Default Location of CodeCoverage File is 
     target/site/jacoco/jacoco.xml, 
     target/site/jacoco-it/jacoco.xml, 
     build/reports/jacoco/test/jacocoTestReport.xml -->

<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
````

### ➤ Change 2 – JaCoCo Maven Plugin for Coverage Report

```xml
<!-- #Change 2 - Changes for Unit Test Coverage Percentage Update on SonarCloud Dashboard -->
<!-- #Default Location of CodeCoverage File is 
     target/site/jacoco/jacoco.xml, 
     target/site/jacoco-it/jacoco.xml, 
     build/reports/jacoco/test/jacocoTestReport.xml -->

<build>
    <plugins>
        <plugin>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.7</version>
            <executions>
                <execution>
                    <id>prepare-agent</id>
                    <goals>
                        <goal>prepare-agent</goal>
                    </goals>
                </execution>
                <execution>
                    <id>report</id>
                    <goals>
                        <goal>report</goal>
                    </goals>
                    <configuration>
                        <formats>
                            <format>XML</format>
                        </formats>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

---

## 2) Ensure Unit Test Cases Exist

Make sure unit test cases are written and included in your source code. JaCoCo will use these tests to generate the coverage report.

---

## 3) Execute the `verify` Goal During Sonar Analysis

Use the following Maven command to run tests and send the report to SonarCloud:

```bash
mvn verify sonar:sonar
```

---

## 4) Confirm Code Coverage Report Import in Logs

During analysis, the following logs confirm that JaCoCo coverage reports are being imported by Sonar:

```text
[INFO] Sensor JaCoCo XML Report Importer [jacoco]
[INFO] 'sonar.coverage.jacoco.xmlReportPaths' is not defined. Using default locations: 
       target/site/jacoco/jacoco.xml, 
       target/site/jacoco-it/jacoco.xml, 
       build/reports/jacoco/test/jacocoTestReport.xml
[INFO] Importing 1 report(s). Turn your logs in debug mode in order to see the exhaustive list.
[INFO] Sensor JaCoCo XML Report Importer [jacoco] (done) | time=24ms
```

If you see the above logs, it confirms that code coverage is successfully being processed and will be visible in your Sonar dashboard.

---


