# **Chapter 10: Continuous Integration in Action**

## **10.1 Verifying the Published Artifact**

The enhanced build pipeline, now including the `CopyFiles` and `PublishBuildArtifacts` tasks, successfully executes. The outcome is a published artifact available within the Azure DevOps portal.

*   **Location:** Upon a successful pipeline run, the **Artifacts** section of the run summary will display the published artifact (e.g., named `drop`).
*   **Content:** This artifact contains the generated `.war` file, which is now persistantly stored and readily available for download or use in subsequent deployment pipelines.

## **10.2 Automated Continuous Integration (CI)**

A core feature of the configured pipeline is its ability to perform **Continuous Integration** automatically.

### **The CI Trigger Mechanism**
The trigger is defined in the YAML file:
```yaml
trigger:
- main
```
This configuration instructs Azure Pipelines to **automatically start a new build** whenever a code change is pushed to the `main` branch of the connected repository.

### **Demonstrating CI**
1.  **Action:** A developer makes a change (e.g., adds a comment) to a file in the `main` branch and pushes the commit to GitHub.
2.  **Result:** Within seconds, Azure DevOps detects the push event.
3.  **Automation:** A new pipeline run is **automatically queued and executed** without any manual intervention.
4.  **Output:** A new, updated artifact is generated based on the latest code commit.

This process ensures that the artifact stored in Azure DevOps is always up-to-date with the latest successful build from the `main` branch.

## **10.3 The Value of CI**

*   **Immediate Feedback:** Developers receive immediate feedback on their changes. If a commit introduces a compilation error or causes tests to fail, the build pipeline will break, alerting the team to fix the issue promptly.
*   **Always-Ready Artifacts:** The latest valid artifact is always available for testing, staging, or production deployment, streamlining the release process.
*   **Quality Assurance:** Automated testing integrated into the build process ensures that only code that passes all checks is promoted.

## **10.4 Key YAML Configuration**

The power of automation is contained within the `azure-pipelines.yml` file. The key elements are:

```yaml
trigger:
- main  # Enables CI by triggering on pushes to the main branch

pool:
  vmImage: 'ubuntu-latest' # Defines the build environment

steps:
- task: Maven@3           # Step 1: Build the project and run tests
  inputs:
    mavenPomFile: 'pom.xml'
    goals: 'package'

- task: CopyFiles@2       # Step 2: Prepare the artifact for publishing
  inputs:
    Contents: '**/*.war'
    TargetFolder: '$(Build.ArtifactStagingDirectory)'

- task: PublishBuildArtifacts@1 # Step 3: Save the artifact to Azure DevOps
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'drop'
    publishLocation: 'Container'
```

## **10.5 Summary**

The build pipeline is now fully functional and automated. It demonstrates a complete **Continuous Integration** process:
1.  **Code Change:** A developer pushes code to the `main` branch.
2.  **Automated Build:** The pipeline is automatically triggered.
3.  **Test & Package:** The code is compiled, tested, and packaged into an artifact.
4.  **Publish:** The artifact is saved to Azure DevOps.

This creates a reliable, automated foundation for the next phase: **Continuous Delivery**, where these artifacts will be automatically deployed to various environments.

---
### **Key Concepts**

| Concept | Description |
| :--- | :--- |
| **CI Trigger** | The `trigger:` keyword in the YAML file that defines which branch events will automatically start a pipeline. |
| **Automated Build** | A pipeline run that starts without manual intervention due to a configured trigger. |
| **Build Validation** | The process of compiling and testing code immediately after a change is committed, providing rapid feedback. |
| **Artifact Repository** | Azure DevOps serves as a repository for versioned build artifacts, ready for deployment. |
