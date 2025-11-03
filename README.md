# java-ci-sample

This repository now contains a minimal Maven Java project and a sample Jenkins pipeline (`Jenkinsfile`) that demonstrates a CI pipeline.

What was added:
- `pom.xml` — minimal configuration using Java 17 and JUnit 5
- `src/main/java/com/example/App.java` — simple main and greet method
- `src/test/java/com/example/AppTest.java` — unit test for the greet method
- `Jenkinsfile` — declarative pipeline using the official Maven Docker image to run the build and publish JUnit reports

How to run the tests locally (requires Docker):

```bash
# from the repo root
docker run --rm -v "$PWD":/workspace -w /workspace maven:3.8.8-openjdk-17 mvn -B -DskipTests=false clean test
```

Jenkins pipeline notes:
- Create a Pipeline job named `Java-CI-Pipeline` and choose "Pipeline script from SCM" pointing to this repository.
- If you prefer Jenkins to use an installed Maven tool instead of Docker, replace the `agent` block in the `Jenkinsfile` with a node agent and set the `tools { maven 'M3' }` entry (configure `M3` in Global Tool Configuration).
