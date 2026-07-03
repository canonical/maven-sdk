# Maven SDK for Workshop

A development environment for Maven projects. It provides versioned releases
of the Apache Maven build tool and persists packages to speed up builds across
workshop updates.

---

## Reference workshop

A minimal workshop:

```yaml
# workshop.yaml
name: maven-app
base: ubuntu@24.04
sdks:
  - name: openjdk
    channel: 21/stable
  - name: gradle
    channel: 9/stable

actions:
  verify: mvn verify
  launch: java -jar target/your-app-name-1.0-SNAPSHOT.jar
```

This demonstrates a basic Maven build workflow.

> Note: The Maven Workshop SDK requires a [Java Development Kit](https://jdk.java.net/) (JDK) installation with a suitable version to run.

---

## Using the SDK

### Prerequisites, project layout

1. The `openjdk` SDK (or other JDK installation) is required.
2. Your Maven project should be in your project directory.
3. On launch, the SDK confugures `PATH`. No dependencies are pre-installed; Packages are downloaded during the first `gradle build` or `gradle run`.

### Verify the project

Once the workshop is ready:

```bash
workshop shell
mvn verify
```

The first verify downloads packages in `~/.m2/repository`, which is mapped to your host via the `maven-cache` mount plug. Subsequent builds reuse cached packages.

To see where the Maven cache is stored on the host:

```bash
workshop info
```

### Run the project

From within the workshop shell:

```bash
workshop shell
mvn package
java -jar target/your-app-name-1.0-SNAPSHOT.jar
```

Use standard `mvn` commands; the toolchain behaves exactly as it would in a regular Maven installation.

---

## Plugs (resources this SDK consumes)

### `maven-cache`

- Interface: `mount`
- Workshop target: `/home/workshop/.m2/repository`
- Purpose: Persists package downloads between workshop updates.

## Slots (resources this SDK provides)

This SDK doesn't define any slots.

---

## Documentation and guidance

- [Maven official documentation](https://maven.apache.org/index.html)
- [OpenJDK workshop SDK reference](https://github.com/canonical/openjdk-sdk)
- [Workshop documentation](https://ubuntu.com/workshop/docs/)

---

## Community and support

- Maven community: [Maven Community Docs](https://maven.apache.org/community.html)
- Workshop forum: [Discourse](https://discourse.ubuntu.com/)
- Please review our [Code of Conduct](https://ubuntu.com/community/ethos/code-of-conduct)
  before participating.

---

## Contributions

All contributions, including code, documentation updates, and issue reports,
are welcome!

- See [CONTRIBUTING]([public-github-url]) for guidelines.
- Open issues or pull requests on the [official repository]([repo-url]).

---

## License and copyright

Copyright 2026 Canonical Ltd.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License version 2.1 (LGPLv2.1) as published by the Free Software Foundation.

Maven is licensed under [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
