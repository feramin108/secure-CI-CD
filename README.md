# Secure-CI-CD
This project involves setting up a secure CI/CD pipeline using Jenkins, integrated with OWASP tools like Dependency-Check and ZAP. The aim is to automate security checks throughout the development and deployment process.

**Step 1:**
Create a Namespace for Jenkins. It is good to categorize all the devops tools as a separate namespace from other applications.

**Step 2:**
Create a serviceAccount.yaml file and copy the following admin service account manifest.Now create the service account using kubectl.

**kubectl apply -f serviceAccount.yml**

**Step 3:** 
Create volume.yaml and copy the following persistent volume manifest. **NB** CHANGE THE _ minikube _ to your  own  cluster  node  name
