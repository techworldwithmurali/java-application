<b>Manually - Build and Push to Jfrog Artifactory</b>

<h2>Prerequisites:</h2>
  <b>Git is installed<b>
  <b>maven is installed<b>
  <b>Jfrog Artifactory is installed<b>

Step 1: Clone the repository
github url: https://github.com/techworldwithmurali/nodejs-application.git
          branch name:

Step 2: Update the jfrog Artifactory details in pom.xml
Step 3: Update the jfrog credentials in settings.xml
Step 4: Run the below command to push the artifacts to Jfrog Artifactory.
mvn deploy
Step 5: Verify whether artifact(war) is published or not in Jfrog Artifactory

Congratulations. You have successfully Published the artifact(war) file in Jfrog repository
