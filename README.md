Environment Setup (Prerequisites)
Java Development Kit (JDK 17):
Download the Windows MSI installer from Adoptium (Eclipse Temurin).
Install it and ensure JAVA_HOME is set in your Windows Environment Variables

Git:
Download and install Git for Windows. Keep the default installation settings.
Apache Maven:

Download the binary zip archive from the Maven website.
Extract it to a permanent location (e.g., C:\maven).
Add C:\maven\bin to your Windows Path environment variable.

Phase 2: Create the Java Web Project & GitHub Repo
Open your terminal (PowerShell or Command Prompt) and create a new directory for your project:
mkdir local-cicd-demo
cd local-cicd-demo

Create the pom.xml
In the root of local-cicd-demo, create a file named pom.xml and add this code:

Create the Java Application Code
Create the necessary folder structure for your Java packages:
mkdir src\main\java\com\example\cicddemo
Create Application.java inside src\main\java\com\example\cicddemo:

Push to GitHub
git init
git add .
git commit -m "Initial Java project commit"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/local-cicd-demo.git
git push -u origin main

Phase 3: Install & Configure Jenkins Locally
Download the jenkins.war file from the Jenkins Generic Java package page.
https://www.jenkins.io/download/
Open a new terminal window, navigate to where you downloaded the file, and start Jenkins:
java -jar jenkins.war --httpPort=9090
Check port: 9090 should be free.

Keep this terminal window open. Jenkins is now running locally.
Open your browser and navigate to http://localhost:9090

You will be prompted for an Administrator Password. Look at your Jenkins terminal window; you will see a 32-character alphanumeric password printed there. Copy and paste it into the browser.
Click Install suggested plugins and wait for them to download.
Create your First Admin User when prompted and finish the setup.

Phase 4: Create the Pipeline (Jenkinsfile)

1. Add the Jenkinsfile
In your project directory (local-cicd-demo), create a file named exactly Jenkinsfile

or You can add pipeline in Jenkins also.

git add Jenkinsfile
git commit -m "Add Jenkins CI/CD pipeline"
git push

Phase 5: Execute the CI/CD Pipeline
Now we connect Jenkins to your GitHub repository to execute the instructions in the Jenkinsfile.
Go to your Jenkins dashboard (http://localhost:9090).
Click New Item on the left menu.
Enter a name for your job (e.g., Java-Web-Pipeline), select Pipeline, and click OK.
Scroll down to the Pipeline section.
Change the Definition dropdown to Pipeline script from SCM.
Change SCM to Git.
In the Repository URL field, paste your GitHub repo URL (e.g., [https://github.com/YOUR_GITHUB_USERNAME/local-cicd-demo.git](https://github.com/YOUR_GITHUB_USERNAME/local-cicd-demo.git)).
Ensure the Branch Specifier is set to */main (or whichever your default branch is).
Click Save.

On the project page, click Build Now on the left menu.

You should see the pipeline execute through the Checkout, Build, Test, and Deploy stages. Once it turns green, open a new browser tab and navigate to http://localhost:9090. You will see your application running: "CI/CD Pipeline is successfully running!"

Step 2: Configure Jenkins

Open your Jenkins Dashboard (http://localhost:9090).

On the left menu, click Manage Jenkins.

Under the System Configuration section, click Tools.

Scroll down to the JDK section:

Click the Add JDK button.

Uncheck the "Install automatically" checkbox.

In the Name field, type exactly: Default

In the JAVA_HOME field, paste the full path to your JDK folder.

Scroll down to the Maven section:

Click the Add Maven button.

Uncheck the "Install automatically" checkbox.

In the Name field, type exactly: Default

In the MAVEN_HOME field, paste the full path to your Maven folder (e.g., C:\maven).

Click Save at the bottom of the page.

Go back to your Java-Web-Pipeline job and click Build Now. The pipeline will now successfully find the tools and proceed to the Build stage!

Run The app: http://localhost:8080/
