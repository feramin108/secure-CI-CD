# Secure-CI-CD
This project involves setting up a secure CI/CD pipeline using Jenkins, integrated with OWASP tools like Dependency-Check and ZAP. The aim is to automate security checks throughout the development and deployment process.

**Step 1:**
Create a Namespace for Jenkins. It is good to categorize all the devops tools as a separate namespace from other applications.

**Step 2:**
Create a serviceAccount.yaml file and copy the following admin service account manifest.Now create the service account using kubectl.

**kubectl apply -f serviceAccount.yml**

**Step 3:** 
Create volume.yaml and copy the following persistent volume manifest. **NB** CHANGE THE *minikube* to your  own  cluster  node  name
**kubectl create -f volume.yml**

**Step 4:**  
Create a Deployment file named deployment.yaml and copy the following deployment manifest.Create the deployment using kubectl.

**kubectl apply -f deployment.yml**

**In this deployment of Jenkins on Kubernetes, we've incorporated the following:**
. We've set up a securityContext for the Jenkins pod, enabling it to write to the local persistent volume securely.
. Implemented liveness and readiness probes to ensure the continuous health monitoring of the Jenkins pod.
. Utilized a local persistent volume, which is based on the local storage class, to store Jenkins data at the path /var/jenkins_home.

**Step 5:** 
Check the deployment status. kubectl get deployments -n *namespace*
