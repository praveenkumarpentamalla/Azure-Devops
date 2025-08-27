# **Chapter 9: Publishing Build Artifacts**

## **9.1 The Problem: Isolated Artifacts**

The build pipeline successfully compiles the code and generates a `.war` file on the **hosted agent**. However, this agent is ephemeral—it is destroyed after the pipeline run completes. Consequently, the artifact is lost unless it is explicitly saved and published.

## **9.2 The Solution: A Two-Step Process**

To persist the build artifact and make it available for deployment, we must add two specific tasks to our YAML pipeline. These tasks will:
1.  Copy the artifact from the build directory to a staging directory on the agent.
2.  Publish the artifact from the staging directory to the Azure Pipelines service.

### **Step 1: Copy Files to the Staging Directory**

The first task copies the generated `.war` file from the source directory (`s/`) to a dedicated staging directory for artifacts.

**YAML Addition:**
```yaml
- task: CopyFiles@2
  inputs:
    Contents: '**/*.war'        # Finds all .war files in any subdirectory
    TargetFolder: '$(Build.ArtifactStagingDirectory)' # Copies them to the staging directory
```

*   **`CopyFiles@2`:** The task used to copy files between directories on the agent.
*   **`Contents: '**/*.war'`:** A pattern that recursively searches all directories (`**/`) for any file ending with `.war`.
*   **`TargetFolder: '$(Build.ArtifactStagingDirectory)'`:** A pre-defined Azure DevOps variable that provides the path to a temporary directory specifically designed for collecting artifacts before they are published.

### **Step 2: Publish the Artifact**

The second task takes the artifact from the staging directory and uploads it to Azure Pipelines, where it becomes a managed, downloadable entity.

**YAML Addition:**
```yaml
- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)' # The directory containing the files to publish
    ArtifactName: 'drop'                               # The name of the artifact container
    publishLocation: 'Container'                       # Publish to Azure Pipelines
```

*   **`PublishBuildArtifacts@1`:** The task that uploads files to Azure DevOps.
*   **`PathtoPublish`:** Points to the staging directory where we copied the `.war` file.
*   **`ArtifactName`:** The name given to this collection of artifacts. This name will appear in the pipeline run summary.
*   **`publishLocation: 'Container'`:** Specifies that the files should be published to the Azure Pipelines service (as opposed to a file share).

## **9.3 The Complete Enhanced YAML File**

The final `azure-pipelines.yml` file, incorporating both the build and publish steps, looks like this:

```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: Maven@3
  inputs:
    mavenPomFile: 'pom.xml'
    goals: 'package'

# NEW: Copy the generated .war file to the staging directory
- task: CopyFiles@2
  inputs:
    Contents: '**/*.war'
    TargetFolder: '$(Build.ArtifactStagingDirectory)'

# NEW: Publish the artifact from the staging directory to Azure Pipelines
- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'drop'
    publishLocation: 'Container'
```

## **9.4 Committing the Changes**

For the enhanced pipeline to take effect, the updated YAML file must be committed to the repository.
*   Selecting **"Save"** or **"Save and run"** commits the changes to the `main` branch of the connected GitHub repository.
*   This ensures that the next pipeline run (whether triggered manually or automatically) will execute the new, complete set of instructions.

## **9.5 Expected Outcome**

After the next successful pipeline run:
1.  The pipeline will build the project using Maven.
2.  It will copy the resulting `.war` file to the staging directory.
3.  It will publish the `.war` file as an artifact named **`drop`**.
4.  This artifact will be visible and downloadable from the pipeline run's summary page in Azure DevOps, ready for the deployment phase.

This process transforms the pipeline from a simple build tool into a robust CI system that produces ready-to-deploy artifacts.

---
### **Key Concepts**

| Concept | Description |
| :--- | :--- |
| **`CopyFiles` Task** | An Azure Pipelines task that copies files from a source to a target directory on the agent. |
| **`$(Build.ArtifactStagingDirectory)`** | A pre-defined variable that provides the path to a temporary directory used for staging artifacts before publishing. |
| **`PublishBuildArtifacts` Task** | The Azure Pipelines task that uploads files from the agent to the Azure DevOps service, making them persistent artifacts. |
| **Artifact Container** | A logical container within Azure DevOps that holds one or more published files from a build. |
| **`**/*.war`** | A file matching pattern where `**` means "any directory" and `*.war` matches all files with the `.war` extension. |
