# **Chapter 4: Practical Deployment with Apache Tomcat**

## **4.1 Objective**

This chapter provides a practical demonstration of deploying a Java web application. The goal is to build a project into a deployable **artifact** (a `.war` file) and place it into an **Apache Tomcat** application server to make the application accessible via a web browser.

## **4.2 Prerequisites and Tools**

*   **Apache Tomcat:** An open-source Java application server.
*   **Maven:** A build automation tool used primarily for Java projects.
*   **A Java Web Application Project:** The source code to be deployed.

## **4.3 Step-by-Step Deployment Process**

### **1. Download and Install Apache Tomcat**
1.  Navigate to the official Apache Tomcat website.
2.  Download the appropriate distribution for your operating system (e.g., the 64-bit Windows ZIP for Windows systems).
3.  Extract the downloaded ZIP file to a location on your machine. The extracted directory contains the Tomcat file structure (e.g., `bin`, `conf`, `webapps`).

### **2. Build the Project to Generate an Artifact**
For a Maven-based Java project, the build process compiles code, runs tests, and packages the application.
1.  Navigate to the root directory of your project using a command prompt or terminal.
2.  Execute the Maven command:
    ```bash
    mvn clean install
    ```
    *   **`clean`:** Removes previous build files.
    *   **`install`:** Compiles the code, runs unit tests, and packages the project into a `.war` (Web Application Resource) file.
3.  Upon successful completion, the build **artifact** (e.g., `myapp.war`) is generated in the project's `target/` directory.

> **Key Term:** The **`target/` directory** is a standard Maven output folder where compiled code, reports, and the final build artifact are placed after a successful build.

### **3. Start the Tomcat Server**
1.  Navigate to the Tomcat `bin/` directory.
2.  Execute the startup script:
    *   **On Windows:** Run `startup.bat`
    *   **On Linux/macOS:** Run `startup.sh`
3.  **Troubleshooting Port Conflicts:** If port `8080` is already in use, you must identify and terminate the process using it.
    *   Find the Process ID (PID) using the port: `netstat -ano | findstr :8080`
    *   Terminate the process: `taskkill /PID <PID> /F`

### **4. Deploy the Artifact**
1.  Copy the generated `.war` file from your project's `target/` directory.
2.  Paste the file into the Tomcat `webapps/` directory.
3.  Tomcat will automatically detect, unpack, and deploy the new application.

### **5. Access the Deployed Application**
1.  Open a web browser.
2.  Construct the URL using the following pattern:
    ```
    http://localhost:8080/<name-of-war-file>/
    ```
    *   **`localhost`:** Refers to your local machine's IP address (`127.0.0.1`).
    *   **`8080`:** The default port the Tomcat server listens on.
    *   **`<name-of-war-file>`:** The name of your deployed `.war` file (without the `.war` extension).
3.  The application will load in the browser, confirming a successful deployment.

## **4.4 From Localhost to Production**

This demo uses `localhost` for simplicity. To make an application publicly accessible on the internet, the process is similar but requires:
1.  A **host server** (e.g., a cloud VM) with a public IP address.
2.  Installing Tomcat on that server.
3.  Deploying the `.war` file to the remote Tomcat's `webapps/` directory.
4.  Configuring network security groups/firewalls to allow traffic on port `8080`.
5.  Accessing the application via the server's public IP address (e.g., `http://<PUBLIC_IP>:8080/myapp/`).
6.  (Optional) Mapping a custom **domain name** to the public IP address using DNS.

## **4.5 Key Takeaways**

*   Deployment involves moving a **built artifact** to an **application server**.
*   The build process (e.g., `mvn clean install`) is crucial for creating a clean, tested, and packaged artifact.
*   Apache Tomcat is a popular, lightweight server for hosting Java web applications.
*   The `webapps/` directory is the standard deployment location for Tomcat.
*   Understanding this manual process is foundational for automating deployments with CI/CD tools like **Azure Pipelines**.

---

### **Key Concepts**

| Concept | Description |
| :--- | :--- |
| **`mvn clean install`** | A Maven command that cleans the project, compiles code, runs tests, and packages it into a deployable artifact. |
| **`.war` file** | A Web Application Resource file; a packaged Java web application archive used for deployment. |
| **`target/` directory** | The default Maven output directory where build artifacts and reports are generated. |
| **`webapps/` directory** | The default directory in Apache Tomcat where applications are deployed. |
| **`localhost:8080`** | The default address and port used to access a Tomcat server running on the local machine. |
