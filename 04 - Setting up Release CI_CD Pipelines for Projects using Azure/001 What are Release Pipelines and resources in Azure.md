# **Chapter 11: Introduction to Release Pipelines and Azure Cloud**

## **11.1 From Build to Release**

The **build pipeline** successfully automates the creation of a deployable artifact. The next phase is **release**, which involves deploying this artifact to a target environment (e.g., testing, staging, production). This is managed by a **release pipeline** in Azure DevOps.

## **11.2 Understanding Release Pipelines**

A release pipeline automates the deployment and testing of built artifacts across different environments. Its primary functions are:
*   **Deployment:** Taking the artifact (e.g., the `.war` file) and deploying it to a hosting server.
*   **Environment Management:** Managing promotions through different stages (e.g., Dev -> Test -> Prod), often with approval gates.
*   **Integration:** Running post-deployment tests and checks.

## **11.3 Deployment Targets: Self-Hosted vs. Cloud**

You can deploy your application to two primary types of infrastructure:

### **1. Self-Hosted Servers (Your Own Agents)**
*   **Definition:** Physical or virtual machines (on-premises or in a cloud VPS) that you manage yourself.
*   **Process:** You install and configure an **Azure Pipelines agent** on these machines. The release pipeline then uses this agent to deploy code to the server.
*   **Use Case:** Organizations with existing infrastructure or specific security requirements.

### **2. Azure App Service (Cloud Hosting)**
*   **Definition:** A **Platform-as-a-Service (PaaS)** offering from Microsoft Azure. It provides managed hosting environments for web applications, eliminating the need to manage underlying VMs or operating systems.
*   **Benefits:**
    *   **Managed Infrastructure:** Azure handles server maintenance, patching, and scaling.
    *   **Integration:** Native, seamless integration with Azure DevOps for deployment.
    *   **Scalability:** Easy to scale resources up or down based on application load.
*   **Use Case:** The modern, cloud-native approach demonstrated in this course.

## **11.4 Prerequisites for Azure Cloud Deployment**

To deploy to **Azure App Service**, you must first set up an Azure account and create the necessary cloud resources.

1.  **Azure Subscription:** An active Azure subscription is required. New users can typically access a **free trial** with credit for 30 days.
2.  **Azure Portal:** Cloud resources are created and managed via the **Azure Portal** (`portal.azure.com`).
3.  **Authentication:** Azure DevOps authenticates with the Azure Portal using the same Microsoft account credentials, enabling a seamless connection between the two services.

## **11.5 The Deployment Goal**

The objective is to configure a release pipeline that will:
1.  Automatically pick up the artifact produced by the build pipeline.
2.  Deploy it to a **Linux-based Azure App Service**.
3.  Make the application accessible over the internet via a URL provided by Azure.

This approach demonstrates a complete **CI/CD** workflow, from code commit to cloud deployment, using fully managed Azure services.

## **11.6 Key Terminology**

| Term | Description |
| :--- | :--- |
| **Release Pipeline** | An Azure DevOps pipeline that automates the deployment of artifacts to target environments. |
| **Azure App Service** | A PaaS offering from Microsoft for hosting web apps, APIs, and mobile backends. |
| **Azure Portal** | The web-based management interface for Azure resources (`portal.azure.com`). |
| **Azure Subscription** | A logical container used to provision and manage Azure resources. It is linked to a payment method. |
| **PaaS (Platform-as-a-Service)** | A cloud computing model where a provider delivers hardware and software tools, usually for application development, to users over the internet. |

The subsequent chapter will provide a practical guide to creating an Azure App Service resource in the Azure portal, which will serve as the deployment target for our release pipeline.
