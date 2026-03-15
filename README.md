Jenkins CI/CD Pipeline for Java Web Application
This project demonstrates a Jenkins Declarative Pipeline used to automate the build and deployment of a Java web application using Maven and Apache Tomcat.
The pipeline performs the following tasks:
1.	Clone source code from GitHub
2.	Build the application using Maven
3.	Deploy the generated .war file to a Tomcat server
________________________________________
Pipeline Overview
The Jenkins pipeline consists of three stages.
1️⃣ Clone Source Code (SCM)
This stage clones the application source code from the GitHub repository.
git branch: 'main', url: 'https://github.com/devopstraininghub/mindcircuit16d.git'
Purpose:
•	Fetch the latest source code from the main branch
•	Prepare the workspace for the build process
________________________________________
2️⃣ Build Artifact
This stage builds the Java project using Apache Maven.
mvn clean install
Purpose:
•	Compile the source code
•	Run tests (if configured)
•	Package the application into a .war file
Output:
target/*.war
________________________________________
3️⃣ Deploy to Tomcat
This stage deploys the generated WAR file to the Tomcat web server.
Deployment configuration:
•	Tomcat Version: Tomcat 9
•	Context Path: MC-APP
•	Server URL:
http://44.223.26.72:8090/
Deployment snippet:
deploy adapters: [tomcat9(
credentialsId: 'tomcat',
url: 'http://44.223.26.72:8090/'
)], contextPath: 'MC-APP', war: '**/*.war'
Purpose:
•	Automatically deploy the application to the Tomcat server
•	Make the application accessible via web browser
Example URL after deployment:
http://44.223.26.72:8090/MC-APP
________________________________________
Prerequisites
Before running this pipeline, ensure the following:
1️⃣ Jenkins Installed
Jenkins server should be installed and running.
2️⃣ Required Jenkins Plugins
Install the following plugins:
•	Git Plugin
•	Maven Integration Plugin
•	Deploy to Container Plugin
•	Pipeline Plugin
3️⃣ Maven Installed on Jenkins
Verify Maven installation:
mvn -version
4️⃣ Tomcat Server Running
Ensure the Tomcat server is running on:
http://44.223.26.72:8090
5️⃣ Jenkins Credentials
Add Tomcat credentials in Jenkins:
Manage Jenkins → Credentials
Credential ID used in pipeline:
tomcat
How to Run the Pipeline
1.	Create a New Pipeline Job in Jenkins
2.	Connect it to your GitHub repository
3.	Add the Jenkinsfile
4.	Click Build Now
Pipeline will automatically:
Clone Code → Build → Deploy
________________________________________
CI/CD Workflow
GitHub Repository
        │
        ▼
     Jenkins
        │
        ▼
   Maven Build
        │
        ▼
   WAR Artifact
        │
        ▼
  Deploy to Tomcat
        │
        ▼
  Application Live
