<h1 style="text-align:center;"> CI/CD Pipeline </h1>

### What is CI/CD pipeline?
A CI/CD (Continuous Integration and Continuous Delivery) pipeline is a series of automated steps that take code from development to deployment. It helps to ensure that code is always in a deployable state and that changes are made quickly and safely.
- It involves continuous integration of code changes, automated testing, and automated deployment.

### How the development was taking place before the CI/CD pipeline
Before CI/CD pipelines, development was a manual process. Developers would write code, test it locally, and then manually deploy it to production. This process was slow and error-prone. The process can be simplified into the steps:
1. **Manual Integration**: Developers work on their features or bug fixes independently.
2. **Infrequent Integration**: Changes are integrated periodically, leading to longer periods between code integration.
3. **Manual Testing:** After integration, testing is performed manually, often leading to inconsistencies and delays.
4. **Deployment Challenges**: Deployments are infrequent, complex, and error-prone due to manual processes.

### Issues with traditional development workflow
1. **Integration Challenges**: Delayed integration can lead to conflicts and integration issues.
2. **Bugs and Inconsistencies**: Manual testing is prone to errors, and inconsistencies may arise due to differences in testing environments.
3. **Deployment Challenges**: Manual deployment processes are slow, error-prone, and hinder frequent releases.
4. **Reduced Productivity**: Developers spend more time resolving integration and deployment issues rather than focusing on coding.

#### Diagram of development without CI/CD pipeline
```
Developer writes code -> Developer tests code locally -> Developer deploys code to production
--------------------------------------------
Developer 1      Developer 2     Developer 3
    |                |               |
    |                |               |
    |                |               |
    v                v               v
(Feature 1)      (Feature 2)    (Feature 3)
      \              |              /
       \             |             /
        \            |            /
         \           v           /
            Manual Integration
           \         |        /
            \        |       /
             \       v      /
              Manual Testing
                \    |    /
                 \   |   /
                  \  |  /
                   \ v /
                (Production)
```

### How CI/CD pipeline is better (how it solves the problem we were facing earlier)
CI/CD pipelines solve the problems of manual development by automating the process. This makes development faster, more reliable, and less error-prone.

#### Diagram of development with CI/CD pipeline
```
Developer writes code -> CI/CD pipeline tests code -> CI/CD pipeline deploys code to production
```
![Alt text](image.png)

### Benefits of using CI/CD pipeline
1. **Frequent Integration**: Developers integrate code changes regularly, reducing conflicts and integration challenges.
2. **Automated Testing**: Continuous automated testing ensures early detection of bugs and inconsistencies.
3. **Continuous Deployment**: Automated deployment enables frequent and reliable releases to production.
4. **Increased Collaboration**: Team members collaborate more effectively due to a shared and automated development pipeline.
5. **Efficiency and Productivity**: Reduced manual tasks and faster feedback loops enhance overall efficiency and productivity.

---
<h1 style="text-align:center;"> Jenkins </h1>
### What is Jenkins?
Jenkins is an open-source automation server that facilitates building, testing, and deploying code. It plays a crucial role in CI/CD pipelines by automating various stages of the software development lifecycle. 
- It is a popular choice for many teams because it is free, open source, and easy to use.
- It was developed by Sun Microsystem in 2004 under the name Hudson. Later, Jenkins was forked from it in 2011. Hudson is now provided as paid enterprise edition by Oracle.

### What problem it solves?
Jenkins solves the problem of managing and automating the CI/CD pipeline. It provides a central platform for managing all of the steps in the pipeline, from building the code to testing it to deploying it to production.

![Alt text](image-1.png)

Jenkins automates the building, testing, and deployment processes, reducing manual intervention and minimizing errors. It integrates with version control systems, allowing for continuous integration of code changes. 

Jenkins is scalable, supporting the automation of projects of different sizes and complexities. A wide range of plugins are also available that enhances Jenkins' functionality, enabling integration with various tools and technologies.

### How Jenkins is Used
Jenkins monitors version control repositories for changes and triggers builds when new code is committed. Jenkins can execute automated tests as part of the build process, providing quick feedback on code quality. Jenkins automates the deployment process, ensuring that applications are delivered to production efficiently and reliably. Jenkins allows the scheduling of jobs at specific times, ensuring routine tasks are performed automatically.

### Impact of Jenkins on CI/CD
Jenkins accelerates the development lifecycle, reducing the time from code creation to deployment. Automated processes in Jenkins result in consistent and reliable builds, tests, and deployments. Quick feedback on code changes through automated testing improves overall code quality. Automation reduces the chances of errors introduced by manual processes.

----

### Build Source Code Polling
It is used to periodically check a version control system (such as Git, SVN, etc.) for changes in the source code of a project. If changes are detected, the CI system triggers a build process to compile, test, and package the updated source code. This helps automate the build process and ensures that the latest version of the software is continuously integrated and tested.

> **Note**: We can even set the build to be done at a specific period.

