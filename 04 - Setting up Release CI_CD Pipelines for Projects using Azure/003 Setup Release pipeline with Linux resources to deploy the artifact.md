# **Chapter 13: Configuring the Release Pipeline**

## **13.1 Connecting the Release Pipeline to Azure**

The release pipeline automates deployment to the Azure App Service created in the previous chapter. The first step is to establish a connection between Azure DevOps and your Azure subscription.

1.  **Authorize Connection:** Within the release pipeline task, you must authorize Azure DevOps to access your Azure subscription. This is a one-time setup that grants the necessary permissions.
2.  **Select Subscription and App Service:** After authorization, you can select:
    *   Your **Azure Subscription** from the dropdown list.
    *   The specific **App Service name** (e.g., `rahul-academy-demo`) you created in the Azure portal. This tells the pipeline exactly where to deploy the application.

## **13.2 Specifying the Package for Deployment**

The pipeline needs to know which file to deploy. The artifact (`.war` file) published by the build pipeline is stored in a default working directory within Azure DevOps.

*   **Package or Folder Path:** You must provide the path to the deployable file.
*   **Using Wildcards:** The path `**/*.war` is used to dynamically locate the `.war` file. This pattern instructs the pipeline to:
    1.  Recursively search all directories (`**/`) within the default working directory.
    2.  Find any file with the `.war` extension.
*   **Why This Works:** This approach is effective because of the previous `PublishBuildArtifacts` task in the build pipeline, which ensured the `.war` file was copied to this known location.

## **13.3 Linking the Artifact**

A release pipeline must be explicitly connected to the build artifact it will deploy.

1.  **Add an Artifact:** In the release pipeline definition, you add an artifact source.
2.  **Select Source:** Choose the build pipeline that produces the artifact (e.g., the `java-maven-build` pipeline created earlier).
3.  **Automatic Linking:** Once linked, the release pipeline will automatically have access to the latest artifact published by that build pipeline. This creates a clear, traceable connection between the build and release processes.

## **13.4 Pipeline Visualization**

After configuration, the pipeline interface visually represents the workflow:
*   The **build pipeline** is shown as the source of the artifact.
*   The **release pipeline** (with its stage, e.g., "Deploy to QA") is shown as the consumer of that artifact.
*   This visualization provides a clear overview of the end-to-end CI/CD process, from code commit to deployment.

## **13.5 Summary of Configuration**

The release pipeline is now configured to:
1.  **Listen** for new artifacts from the specified build pipeline.
2.  **Authenticate** with the correct Azure subscription.
3.  **Target** the correct Azure App Service resource.
4.  **Deploy** the found `.war` file to the Tomcat server running on that App Service.

The final step is to create a release, which will execute this pipeline and deploy the application to the cloud.

---
### **Key Concepts**

| Concept | Description |
| :--- | :--- |
| **Service Connection** | A secured connection in Azure DevOps that allows pipelines to authenticate with external services like Azure. |
| **Wildcard Pattern (`**/*.war`)** | A file matching pattern where `**` means "any directory" and `*.war` matches all files with the `.war` extension. |
| **Artifact Source** | The definition within a release pipeline that specifies which build pipeline provides the artifact to be deployed. |
| **Default Working Directory** | The standard directory on the agent where Azure DevOps places artifacts before task execution. |
