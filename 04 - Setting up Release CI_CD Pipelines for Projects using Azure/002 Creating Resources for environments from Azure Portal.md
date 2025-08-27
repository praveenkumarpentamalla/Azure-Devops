# **Chapter 12: Creating an Azure App Service for Deployment**

## **12.1 Choosing a Deployment Target**

When deploying a web application, you have two primary options for your hosting infrastructure in Azure:

### **Option 1: Virtual Machines (IaaS - Infrastructure-as-a-Service)**
*   **What it is:** Azure provides a dedicated Windows or Linux virtual machine (VM).
*   **Responsibility:** **You are responsible** for all management:
    *   Installing the application server (e.g., Tomcat, Apache).
    *   Installing the runtime (e.g., Java JDK).
    *   Configuring security, networking, and patches.
    *   Manually deploying the application artifact to the server.
*   **Use Case:** Best for applications requiring full control over the OS and custom configurations.

### **Option 2: Azure App Service (PaaS - Platform-as-a-Service)**
*   **What it is:** A fully managed platform for hosting web applications.
*   **Responsibility:** **Azure manages** the underlying infrastructure (VMs, OS, runtime, web server). You only need to provide your application code.
*   **Use Case:** The recommended approach for most web applications, as it simplifies deployment and management. This is the option demonstrated in this course.

## **12.2 Creating an Azure App Service Resource**

The Azure App Service handles the installation and configuration of the application server (e.g., Tomcat) and runtime (e.g., Java), allowing you to focus solely on deploying your application.

### **Step-by-Step Creation Process:**

1.  **Navigate to the Azure Portal:** Go to `portal.azure.com`.
2.  **Create a Resource:** Click on "Create a resource".
3.  **Select Web App:** Choose "Web App" from the marketplace.
4.  **Configure Basics:**
    *   **Subscription:** Select your active Azure subscription (e.g., a Free Trial subscription).
    *   **Resource Group:** Create a new one or use an existing one. A resource group is a logical container for related Azure resources.
    *   **Name:** Provide a unique name for your web app (e.g., `rahul-academy-demo`). This will form part of the default URL: `https://<your-app-name>.azurewebsites.net`.
    *   **Publish:** Select "Code" (as opposed to a Docker container).
    *   **Runtime Stack:** Select the application's runtime environment.
        *   For a Java app: Choose **Java** version (e.g., Java 8, Java 11).
    *   **Java Web Server Stack:** Select the application server (e.g., **Apache Tomcat** and a specific version like 9.0).
    *   **Operating System:** Select **Linux**.
5.  **App Service Plan:** This defines the compute resources (CPU, memory) and cost for your app. A basic, low-cost plan (e.g., B1) is sufficient for development and testing.
6.  **Review + Create:** Validate your settings and click "Create".

Azure will now provision and configure a new Linux server with Tomcat and the specified Java version pre-installed. This process typically takes a few minutes.

## **12.3 Outcome and Next Steps**

Once deployment is complete:
*   You have a fully managed **hosting environment** ready for your application.
*   The application will be accessible at `https://<your-app-name>.azurewebsites.net` (it will display a default page until you deploy your code).
*   This Azure App Service resource is now a valid **deployment target** that can be selected within an Azure DevOps release pipeline.

The creation of this resource is a prerequisite for automating deployments. The next chapter will cover configuring the release pipeline in Azure DevOps to deploy the built artifact directly to this Azure App Service.

---
### **Key Concepts**

| Concept | Description |
| :--- | :--- |
| **Azure App Service** | A PaaS offering in Azure that provides a managed environment for hosting web applications. |
| **IaaS (Infrastructure-as-a-Service)** | A cloud computing model where the provider supplies virtualized computing resources over the internet. The user manages the OS and software. |
| **PaaS (Platform-as-a-Service)** | A cloud computing model where the provider delivers hardware and software tools for application development. The user manages the application and data. |
| **Runtime Stack** | The combination of programming language and framework version (e.g., Java 11, Tomcat 9.0) required to run an application. |
| **Resource Group** | A logical container in Azure that holds related resources for an application or solution, making management and cleanup easier. |
| **App Service Plan** | Defines the set of compute resources (CPU, memory, storage) for your web app to run. It also determines the cost. |
