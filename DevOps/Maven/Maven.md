<h1 style="text-align:center;"> Maven </h1>

Maven is a widely used build automation and project management tool primarily used for Java projects. It helps to manage the build lifecycle of a software project, including tasks such as compilation, testing, packaging, and deployment. 
- Maven uses a declarative approach to project configuration.
- The project information and configuration are specified in an XML file called ``pom.xml`` (Project Object Model).
- Maven defines a standard build lifecycle with phases like **compile**, **test**, **package**, **install**, and **deploy**. 
  
### How does Maven work?
Maven works based on the concept of a Project Object Model (POM). A POM file is an XML file that contains information about the project and configuration details for building the project. Maven uses this information to manage the project's build lifecycle, dependencies, and other aspects.

### POM (Project Object Model)
The POM is an XML file that contains information about the project and configuration details, such as dependencies, plugins, goals, and other settings. It serves as the project's central configuration file.
- Maven enforces a standard project structure, making it easier for developers to understand and navigate different projects.
- Management becomes easy as the dependencies can be declared in the POM file. Maven then automatically downloads and manages the required libraries from the central repository.
- The root POM is typically located in the project's root directory and is responsible for defining configuration details.
- There can be multiple sub-modules present in the project, each sub-module (**inherit configuration details from the root POM**) will have its own POM file, but there is also a common or "root" POM that oversees the entire project.

> **Note**: The root POM aggregates information from its sub-modules. It doesn't contain actual source code or resources but serves as a coordinator for the entire project.
 
### How to run maven project?
To run a Maven, we use the Maven command-line tool to execute various build lifecycle phases, such as compiling, testing, packaging, and deploying the project. 

### ``clean package`` command
The ``clean package`` command riggers a sequence of Maven goals to clean the project, compile the source code, run tests, and package the application into a distributable format (such as a JAR, WAR, or EAR file). It is primarily used for Java projects. 

#### ``clean`` cycle
It removes the build directory and all compiled files generated in previous builds. It ensures a clean and fresh start for the build process.

#### ``package`` cycle
It performs the tasks necessary to package the compiled code and resources into a distributable format. The specific format depends on the packaging type specified in the project's POM (Project Object Model) file. Common packaging types include JAR (Java Archive), WAR (Web Archive), and EAR (Enterprise Archive).

> **Note**: This command is often used as part of a continuous integration (CI) or continuous delivery (CD) pipeline to automate the build and packaging process of a project. It helps ensure that the project is built from a clean slate and that the packaged artifact is ready for distribution or deployment.

---

### Build Source Code Polling Process
The Build Source Code is used to periodically check a version control system (such as Git, SVN, etc.) for changes in the source code of a project. If changes are detected, the CI system triggers a build process to compile, test, and package the updated source code. 

The rough process can be:
1. **Scheduled Polling:**
   - CI system periodically checks the version control system for changes.
   - Interval is defined in the CI system's configuration (e.g., every 5 minutes).

2. **Source Code Changes Detected:**
   - If changes are found in the version control system:
     - CI system initiates the build process.

3. **Build Process:**
   - Maven is invoked to execute the build lifecycle.
   - Maven performs tasks such as cleaning, compiling, testing, and packaging.

4. **Artifact Generation:**
   - Maven generates artifacts (e.g., JAR, WAR) based on the project's configuration.

5. **Test Execution:**
   - Automated tests are executed to ensure the code quality.

6. **Reports and Notifications:**
   - CI system generates reports and notifications about the build status.
   - Notifications may be sent to developers or teams.

7. **Deployment (Optional):**
   - If configured, CI system may deploy the built artifacts to a staging or production environment.

8. **Build Logs and Artifacts:**
   - Build logs and artifacts are stored for reference and analysis.

9. **Process Repeats:**
   - The process repeats at the scheduled polling interval.

### How to set the interval of the build?
Maven itself doesn't provide native scheduling capabilities for executing builds at specific times or intervals. We can use a continuous integration (CI) system to schedule a build. We can configure scheduled builds or builds triggered by specific events such as code commits or pull requests. The scheduling syntax used in many CI tools is often based on the **cron syntax**.

#### ``cron`` syntax
The cron syntax consists of five fields, often referred to as the **five stars**, representing minute, hour, day of the month, month, and day of the week. The syntax looks like this:
```
* * * * *
| | | | |
| | | | +----- Day of the week (0 - 6) (Sunday = 0 or 7)
| | | +------- Month (1 - 12)
| | +--------- Day of the month (1 - 31)
| +----------- Hour (0 - 23)
+------------- Minute (0 - 59)
```

So, if we want to schedule a job to run every day at midnight, the cron expression would be ``0 0 * * *``.