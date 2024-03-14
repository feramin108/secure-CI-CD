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
Check the deployment status. kubectl get deployments -n *namespace* **
you can get the deployment details using the following command
**kubectl  describe deployments --namespace=namespace**

# Accessing Jenkins via Kubernetes Service
We've established a deployment, but it's not reachable from external sources. To enable access to the Jenkins deployment externally, we need to create a service and link it to the deployment.

**Step 6:** generate a *service.yml* file and insert the provided service configuration OR use modify the  exiting  one
note that we're using the NodePort type, which will make Jenkins accessible via port 32000 on all Kubernetes node IPs. 
If you have an ingress configuration, you can define an ingress rule to access Jenkins. Additionally, 
if you're running the cluster on AWS, Google Cloud, or Azure, you can expose the Jenkins service as a LoadBalancer.

Create the Jenkins service using kubectl.

**kubectl apply -f service.yml**
Now if you browse to any one of the Node IPs on port 32000, you will be able to access the Jenkins dashboard.

http://<node-ip>:32000
Jenkins will ask for the initial **Admin password** when you access the dashboard for the first time.

You can get that from the pod logs either from the kubernetes dashboard or  CLI. You can get the pod details using the following CLI command.

**kubectl get pods --namespace=namespace**
And with the pod name, you can get the logs as shown below. replace the pod name with your pod name.

**kubectl logs pods --namespace=namespace**

After entering the password, you can proceed with installing the recommended plugins and creating an admin user. These steps are straightforward and can be easily completed from the Jenkins dashboard.

# In conclusion
once you've completed these tasks, Jenkins will be ready for use, and you'll have full control over its configuration and usage.
