# **Chapter 2: Getting Started with Azure DevOps**

## **2.1 Accessing the Azure DevOps Portal**

Azure DevOps is a cloud-based service accessible via a web browser.
*   Navigate to the official Azure DevOps website by searching for "Azure DevOps" or by visiting the direct URL.
*   As a Microsoft product, the service is hosted on the `microsoft.com` domain.
*   A **Microsoft account** or a **GitHub account** is required to sign in and create projects.

## **2.2 Creating Your First Project**

The primary organizational unit within Azure DevOps is a **Project**. A project consolidates all repositories, pipelines, work items, and dashboards for a specific application or initiative.

**Steps to Create a Project:**
1.  After signing in, you will be prompted to create a new project.
2.  Provide a **Project name** (e.g., "Azure-Demo-Project").
3.  Configure the project **Visibility**:
    *   **Public:** Visible and accessible to anyone on the internet.
    *   **Private:** Accessible only to users you explicitly grant permissions to.
4.  Click **Create project** to initialize the project environment.

## **2.3 Overview of the Project Dashboard**

Once a project is created, you gain access to the integrated Azure DevOps dashboard. The portal is organized into several key sections, each representing a core DevOps functionality:

*   **Boards:** For Agile planning, work item tracking, and sprint management (e.g., user stories, tasks, bugs).
*   **Repos:** For version control using Git repositories (e.g., code, commits, branches, pull requests).
*   **Pipelines:** For building **Continuous Integration/Continuous Deployment (CI/CD)** automation.
*   **Test Plans:** For manual and exploratory test case management.
*   **Artifacts:** For package management (e.g., NuGet, npm packages).

## **2.4 Introduction to Azure Pipelines**

**Azure Pipelines** is a primary component and a major reason for the platform's popularity. It automates the process of building, testing, and deploying code to any target environment.

### **Core Purpose of Pipelines**
*   **Automate Builds:** Compile source code, run tests, and produce deployable packages known as **artifacts**.
*   **Automate Deployments:** Release built artifacts to various environments (e.g., development, staging, production).
*   **Enable CI/CD:** Facilitate the practices of **Continuous Integration** (automatically building and testing every code change) and **Continuous Delivery/Deployment** (automatically deploying every change that passes tests).

### **The Integrated Advantage**
While other tools like Jenkins can automate CI/CD, Azure Pipelines offers a significant advantage: **deep integration** with all other ALM tools (Boards, Repos, Test Plans) within a single, unified portal.

## **2.5 Learning Path: Deployment Basics First**

To fully understand and appreciate the power of Azure Pipelines, one must first grasp fundamental deployment concepts. The subsequent chapter will cover these prerequisites before diving into practical pipeline creation.

**Key topics to be covered next:**
*   Application servers and deployment environments (e.g., staging vs. production).
*   The meaning of "building" a project and generating "artifacts".
*   A concrete demonstration of a CI/CD pipeline goal.
*   Detailed definitions of Continuous Integration and Continuous Delivery.

This foundational knowledge will provide the necessary context to effectively build and configure pipelines from scratch.

---

### **Key Concepts**

| Concept | Definition |
| :--- | :--- |
| **Project** | The top-level container in Azure DevOps that organizes all work, code, and pipelines for a specific initiative. |
| **Azure Pipelines** | The Azure DevOps service for automating builds, tests, and deployments (CI/CD). |
| **Artifact** | A deployable package (e.g., a .zip file, container image) produced by a build pipeline. |
| **CI/CD** | **Continuous Integration** and **Continuous Delivery/Deployment**; practices for automating the software release process. |
| **Build** | The process of compiling source code and running tests to create a verifiable artifact. |
