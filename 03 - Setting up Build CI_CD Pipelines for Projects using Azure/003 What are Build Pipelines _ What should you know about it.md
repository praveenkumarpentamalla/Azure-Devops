# **Chapter 7: Creating a Build Pipeline with Azure Pipelines**

## **7.1 Introduction to Build Pipelines**

A **build pipeline** automates the process of compiling source code, running tests, and producing deployable artifacts. In Azure DevOps, this is configured using a **YAML** file that defines the steps, tools, and environment required for the build process.

## **7.2 Pipeline Creation Steps**

### **1. Connect to a Source Code Repository**
The first step in creating a pipeline is to tell Azure DevOps where your code is located.
*   Azure Pipelines supports various repositories:
    *   **Azure Repos Git** (the built-in option)
    *   **GitHub** (as demonstrated)
    *   **Bitbucket**
    *   **Other Git repositories**
*   The system authenticates with the chosen repository provider to grant access.

### **2. Select a Repository**
After connecting, you must select the specific repository and branch (e.g., `main` or `master`) that contains the code you want to build.

### **3. Configure the Pipeline with a YAML Template**
Instead of writing a YAML file from scratch, Azure DevOps provides pre-configured templates for common project types. For a Java Maven project, selecting the **Maven** template auto-generates a starter YAML file.

## **7.3 Anatomy of the Auto-Generated Maven YAML File**

The generated YAML file contains the essential instructions to build a Maven project.

```yaml
# File: azure-pipelines.yml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: Maven@3
  inputs:
    mavenPomFile: 'pom.xml'
    goals: 'package'
```

### **Key YAML Components Explained:**

*   **`trigger:`**
    *   Defines which branch events should start a new build. `- main` means any push to the `main` branch will trigger the pipeline.

*   **`pool:`**
    *   Specifies the **hosted agent** (a virtual machine) where the build will run.
    *   **`vmImage: 'ubuntu-latest'`** tells Azure to use the latest Ubuntu Linux image. You could change this to `windows-latest` or another image.

*   **`steps:`**
    *   A sequence of tasks to execute. The template provides one core task.
    *   **`- task: Maven@3`**: This instructs the agent to use version 3 of the Maven task.
    *   **`inputs:`**: The parameters for the Maven task.
        *   **`mavenPomFile: 'pom.xml'`**: Tells Maven where to find the project configuration file.
        *   **`goals: 'package'`**: The Maven goal to execute. The `package` goal compiles code, runs tests, and packages the result into a JAR/WAR file.

> **Note:** The `package` goal is equivalent to the `mvn clean install` command used in the manual demo, as it also runs the test phase.

## **7.4 How the Pipeline Executes**

1.  **Event:** A developer pushes code to the `main` branch of the connected GitHub repository.
2.  **Trigger:** Azure DevOps detects the push event.
3.  **Agent Provisioning:** Azure spins up a fresh Ubuntu virtual machine (the **hosted agent**).
4.  **Code Checkout:** The agent clones the repository onto itself.
5.  **Task Execution:** The agent reads the YAML file and executes the `Maven@3` task with the `package` goal.
6.  **Output:** If the build and tests pass, a deployable artifact (e.g., a `.war` file) is created in the agent's workspace.

## **7.5 Preparing for Practice**

To follow along, you need a GitHub repository containing a Maven project. You can:
1.  **Use the Instructor's Repository:** The transcript provides a GitHub URL. You can **import** this repository into your own GitHub account to create a personal copy for practice.
2.  **Create Your Own:** Push any existing Maven project to a new GitHub repository.

This setup provides the foundation. The next chapter will cover saving, running the pipeline, and publishing the generated artifact so it can be used in a release pipeline.

---

### **Key Concepts**

| Concept | Description |
| :--- | :--- |
| **Build Pipeline** | An automated workflow that compiles source code and produces artifacts. |
| **YAML** | A human-readable data-serialization language used to configure Azure Pipelines. |
| **Hosted Agent** | A pre-configured virtual machine provided by Microsoft Azure to run pipeline jobs. |
| **Trigger** | An event (e.g., a code push) that automatically starts a pipeline run. |
| **Maven Goal** | A specific task defined in Maven (e.g., `compile`, `test`, `package`). |
