---
tags:
  - java
  - spring
---

# Maven

Maven is a **build automation and dependency management tool** for Java projects.

> It helps developers manage project builds, dependencies, and packaging.

Maven automatically:
- **Finds and downloads dependencies** (and their transitive dependencies).
- **Builds, tests, and packages** your application.
- Can also install the built artifact into a local or remote repository for reuse.

## CLI-Based Tool

Maven is primarily a **command-line tool**, but most IDEs (like IntelliJ, Eclipse, VS Code) support it with graphical interfaces.

---

# Maven Basics

## Command Structure

	`mvnw [options] [<goals>] [<phases>]`

- `mvn` — main Maven command (or `./mvnw` if using the Maven Wrapper).
- **Goals** — specific tasks to run (e.g., `compile`, `test`, `package`).
- **Phases** — part of the build lifecycle (e.g., `validate`, `install`, `deploy`).

> You usually run phases, and Maven figures out what goals to run under the hood.

---

# Maven Lifecycles

Maven has **three built-in lifecycles**, each with specific purposes.

> Think of a **lifecycle** as a sequence of phases that define the *order of build steps*. (order of things you are looking to achieve)

---

## 1. `clean` Lifecycle

**Cleans the project** by removing previously generated files (like `/target` folder).


### Common Phases:
- `pre-clean` : Hook for before cleaning
- `clean` : Does actual cleaning
- `post-clean` : Hook for after cleaning

##### The `target/` Directory
- This is where **Maven stores all build output**.
- Created automatically when you run `mvn compile`, `mvn package`, etc.
- Contains:
  - Compiled `.class` files
  - Generated `.jar` or `.war` files
  - Temporary files, logs, and reports (e.g., test results)
- Safe to delete — Maven will recreate it as needed.

> `mvn clean` deletes this directory.

---

## 2. `default` (aka `build`) Lifecycle

**The main lifecycle** that handles compiling, testing, packaging, and installing.

### Common Phases:

| Phase      | Description                                                                     |
| ---------- | ------------------------------------------------------------------------------- |
| `validate` | Checks if the project is correct and all required info is available.            |
| `compile`  | Compiles the source code into bytecode.                                         |
| `test`     | Runs unit tests using a suitable test framework (e.g., JUnit).                  |
| `package`  | Bundles the compiled code into a JAR, WAR, etc.                                 |
| `verify`   | Runs additional checks to verify the package is valid.                          |
| `install`  | Installs the package into the **local Maven repository** (`~/.m2/repository`).  |
| `deploy`   | Uploads the final package to a **remote repository** (used in CI/CD pipelines). |

> The important thing here is order.

They are in ascending order. So compile will always happen before test and so on.

Each phase depends on the previous one.  

 For example:
- Running `test` will **automatically trigger** `compile` and any earlier phases.
- You don’t need to manually run each phase in sequence — Maven handles it.

> So `compile` always runs **before** `test`, and `package` always comes **after** both.


> Running the Packaged Application

After running:
	`mvn package`

Maven generates a `.jar` or `.war` file inside the `target/` directory.

To Run a JAR File Manually:

You can execute the generated JAR using:
	`java -jar target/drive-track-0.0.1-SNAPSHOT.jar`
This will launch your Spring Boot (or Java) application.

> This only works if the project is packaged as an **executable JAR** with a proper `main()` method and `MANIFEST.MF`.


---

## 3. `site` Lifecycle

Generates **documentation** for the project (project reports, site structure, java-doc).

### Common Phases:
| Phase         | Description |
|---------------|-------------|
| `pre-site`    | Runs tasks before generating the site. Useful for setup/preparation. |
| `site`        | **Generates the actual site** (HTML pages, Javadocs, reports). |
| `post-site`   | Runs tasks after site generation is done (e.g., cleanup or formatting). |
| `site-deploy` | **Uploads/publishes the site** to a remote server or hosting location. |


---

## Goals vs Phases

- A **goal** is a single task (e.g., `compiler:compile`, `surefire:test`).
- A **phase** is a step in the lifecycle — running it may invoke **multiple goals**.

> Example:
`mvn clean install`

---

##  Standard Directory Layout

| `src/main/java`      | Application/Library sources                                                |
| -------------------- | -------------------------------------------------------------------------- |
| `src/main/resources` | Application/Library resources                                              |
| `src/main/filters`   | Resource filter files                                                      |
| `src/main/webapp`    | Web application sources                                                    |
| `src/test/java`      | Test sources                                                               |
| `src/test/resources` | Test resources                                                             |
| `src/test/filters`   | Test resource filter files                                                 |
| `src/it`             | Integration Tests (primarily for plugins)                                  |
| `src/assembly`       | Assembly descriptors                                                       |
| `src/site`           | Site                                                                       |
| `LICENSE.txt`        | Project's license                                                          |
| `NOTICE.txt`         | Notices and attributions required by libraries that the project depends on |
| `README.txt`         | Project's readme                                                           |

