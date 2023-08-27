sample-java-app

This is a small applicaiton which contains main and test folders.  
Main contains application code.  
Test contains test cases.  
It also contains pom.xml which has all dependencies and artifact name and version


These are the steps I followed in the implementation of the entire CI/CD Pipeline.

1. Provisioned the required infrastructure like VPC, Security Group, Ansible Controller Instance, Jenkins Master and Agent Instances using Terraform.
2. Configured SSH keys for password less authentication between Ansible Controller and Agent nodes.
3. Configured the Jenkins Master and Agent nodes using Ansible. Configured Jenkins Agent as the Maven Build server.
4. Added Jenkins Agent node's credentials in Jenkins Master to establish a connection between Jenkins Master and Agent nodes.
5. Added GitHub credentials to the Jenkins Master and created Multibranch Pipeline job.
6. Configured the Multibranch Pipeline job with GitHub Webhook Trigger with the help of Multibranch Scan Webhook Trigger Plugin.
7. SonarQube:
a. Generated an access token in SonarCloud and added SonarQube server credentials in Jenkins Master.
b. Installed Sonarqube scanner plugin.
c. Added Sonarqube server to the Jenkins Master in System section.
d. Added Sonarqube scanner to the Jenkins Master in Tools section.
e. Configured an organization and project in SonarCloud and wrote a sonar-project. properties file.
f. Added sonarqube, unit tests and build stages in the Jenkinsfile.
8. Added JFrog credentials in the Jenkins Master and integrated JFrog artifactory with Jenkins by installing Artifactory plugin in Jenkins Master.
9. Created a Docker Image out of the jar file and committed that Docker Image into the Docker repository of the JFrog artifactory with the help of Docker Pipeline plugin. Added the Docker Build and Publish stage in Jenkinsfile.
10. EKS:
a. Provisioned the EKS cluster with Terraform.
b. Installed kubectl in Jenkins Slave.
c. Installed AWS CLI v2 in Jenkins Slave to connect with AWS account.
d. Downloaded Kubernetes credentials and cluster configuration from the cluster using the command i.e., aws eks update-kubeconfig --region <region_name> --name <cluster_name> 
11. Pulled the Docker Image from the JFrog artifactory using Kubernetes secret and deployed it in our EKS cluster using deployment resource and exposed it to access from outside using service resource under a particular namespace. Added the deployment stage in Jenkinsfile.
12. Added the Prometheus helm chart repository and implemented the cluster monitoring using Prometheus and Grafana. Note: Changed the default service type of Prometheus and Grafana services from ClusterIP to LoadBalancer to access them from the browser.
