
# **Chapter 5: Continuous Integration and Continuous Delivery (CI/CD)**

## **5.1 Defining CI/CD**

**CI/CD** is a modern software engineering practice that automates the integration, testing, and deployment of code changes. It consists of two interconnected components:

*   **Continuous Integration (CI):** The practice of automatically building and testing code every time a team member commits a change to a version control repository.
*   **Continuous Delivery/Deployment (CD):** The automated process of deploying code that has passed through the CI pipeline to various environments, such as staging or production.

## **5.2 The Continuous Integration (CI) Process**

CI focuses on the early part of the software delivery lifecycle, ensuring that new code integrates smoothly and does not break existing functionality.

### **The CI Workflow:**
1.  **Code Commit:** A developer writes code and pushes a change to a shared **Git repository** (e.g., on GitHub, Azure Repos).
2.  **Automated Trigger:** The push event automatically notifies a CI/CD tool (e.g., Azure Pipelines, Jenkins).
3.  **Build and Test:** The CI tool performs a series of automated actions:
    *   **Fetch:** Retrieves the latest code from the repository.
    *   **Build:** Compiles the code (e.g., runs `mvn clean install` for a Maven project).
    *   **Test:** Executes all unit tests and integration tests to verify the new changes do not introduce bugs.
4.  **Artifact Generation:** If all steps pass, the tool packages the application into a deployable **artifact** (e.g., a `.war` file).

> **Key Principle:** The core goal of CI is to **find issues early**. By building and testing every single commit, teams can identify and fix integration problems immediately, rather than at the end of a development cycle.

## **5.3 The Continuous Delivery (CD) Process**

CD is an extension of CI. It automates the delivery of the validated artifact to environments beyond the developer's machine.

### **The CD Workflow:**
1.  **Artifact Promotion:** The artifact that passed CI is automatically picked up for deployment.
2.  **Deploy to Test/Staging:** The CD tool deploys the artifact to a pre-production environment (e.g., a staging server that mimics production).
3.  **Automated Testing:** After deployment, a suite of **automated regression tests** is triggered to perform end-to-end validation of the application in a environment that closely resembles production.
4.  **Deploy to Production (Continuous Deployment):** If all tests pass, the artifact can be automatically deployed to the production environment. In some models, this step may require a manual approval gate.

## **5.4 The Complete CI/CD Pipeline**

A full CI/CD pipeline integrates both processes into a seamless, automated workflow. The ideal state, as used by tech giants like Amazon and Google, is one where a single code commit can trigger a fully automated path to production with no manual intervention, provided all automated checks pass.

**Visualizing the Pipeline:**
```
Developer Writes Code --> Pushes to Git --> CI Tool Triggers --> Builds Code --> Runs Unit Tests --> Creates Artifact --> CD Tool Triggers --> Deploys to Staging --> Runs Automated Tests --> (If Tests Pass) --> Deploys to Production
```

## **5.5 The Role of Azure DevOps**

**Azure Pipelines** is the tool within Azure DevOps designed specifically for building, testing, and deploying applications. It enables teams to create custom **pipelines** (defined as code in YAML or through a visual designer) that automate every step of the CI/CD process, from code commit to production deployment.

### **The Value of Automation:**
*   **Speed:** Drastically reduces the time between writing code and delivering value to users.
*   **Reliability:** Eliminates human error from manual build and deployment processes.
*   **Quality:** Ensures every change is thoroughly tested before being released.
*   **Developer Focus:** Frees developers from manual tasks, allowing them to focus on writing code.

---

### **Key Concepts**

| Concept | Definition |
| :--- | :--- |
| **Continuous Integration (CI)** | The practice of automatically building and testing code every time a change is committed to a shared repository. |
| **Continuous Delivery (CD)** | The automated process of deploying code that has passed CI to testing/staging environments and making it ready for production release. |
| **Continuous Deployment** | A further extension of CD where every change that passes all stages of the pipeline is automatically released to production. |
| **Pipeline** | An automated process that defines the steps for building, testing, and deploying an application. |
| **Automated Regression Tests** | A suite of tests that run after deployment to ensure new changes haven't broken existing functionality. |
| **Azure Pipelines** | The Azure DevOps service used to implement CI/CD workflows. |
