# Continuous integration of a Java API with Jenkins  
## 1 Integration of version 1.0 :   
The automatic launch of the integration process must be done after each push in the GitHub repository.       
### 1.1 The phases of the pipeline:    
#### 1.1.1 The Build phase   
This phase is made up of the following stages:   
1. Launch of the Gradle build.   
2. Generation of documentation.   
3. Archiving of the Jar file and documentation.   
4. Archiving of unit test results.  
#### 1.1.2 The Mail Notification phase   
After the build, an email notification must be sent to the member (s) of the project in both cases: success and failure of the Build phase (Use https://sendgrid.com).   
#### 1.1.3 The Code Analysis phase    
Use Jenkins SonarQube Plugin to analyze code quality and verify the state of Quality Gates. If the latter is in the Failed state, the pipeline must be finish.
#### 1.1.4 The Test reporting phase   
Use Jenkins' JaCoCo plugin to generate coverage reports for Unit tests.   
#### 1.1.5 The Deployment phase   
Launch the Gradle publish task to deploy the Jar file generated in https://mymavenrepo.com/.  
#### 1.1.6 The Slack Notification phase   
Use the Jenkins Slack Notification plugin to send a notification after deployment of the API.      
## 2 Integration of version 1.1   
The integration of version 1.1 must be done following the sending of a Pull Request (After a Fork from the main repository). The Pull Request process must not  include the Deployment and Slack Notification phases.
