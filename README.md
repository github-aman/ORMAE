# ORMAE
This repo contains the test given by ORMAE

Objectives:- 


A:- Git Repo Structure for MicroServices:- 

1:- We need to create the different GIT Repo for each & every microservice with proper directory structure for concerned code files, confif files & so on..
2:- Must need to follow the branching strategy of master->release->development->feature/bug-fix/hot-fix changes, so that before merging the changes of any feature/bug-fix/hot-fix we should raise a PR to the reviewer before merging to the upper branch(development) then same must be follow for release then to master.

B:- CI Plan:- 

1:- The GIT Server must be connected to the Jenkins/Spinnaker CI for further building the artifact/docker image/package anything it can be.
2:- Jenkins must be connected with CodeQuality tool to check the quality & coverage like SonarQube, lcov & gcov(C++).
3:- Jenkins must push the artifact to the repository like Artifactory, AWS ECR for storing the package as a part of Continuous Delivery which will be further used in the deployment.

C:- CD Plan:- 

1:- Must create some pipelines which will be running the ansible playbooks for deployments on the cluster.
2:- These playbooks basically running the Kubernetes manifests which is updating the cluster.
3:- Deployment | Roll-back pipeline must be created as per requirement.
4:- Deployment will be handled by the helm(package manager for Kubernetes).
5:- Jenkins must be configured with the Slack for further deployment notification along with the updation on the Jira.

D:- Deployment Strategy:- 

1:- Deployment will be managed by the Helm, which i have already stated above in the CD Plan.
2:- Helm v3.0 now in the market without tiller component will be handling the deployment of the microservices in a complete packaged way.
3:- This helm will be working after creating Charts for each & every microservice & will be further deployed by Ansible Playbooks.

E:- Log Management:- 

A:- Datadog:- 

1:- Deploy the datadog agent in the VMs/Instances/EC2 where our cluster is running.
2:- Configure the datadog for some required values/fields of which we want to analyse the logs in the Datadog UI.

B:- Prometheus & Grafana:- 

1:- As a metrics exporter, we can deploy the Prometheus container in the Kubernetes cluster which will be capturing the logs of the Pods running in the cluster with the help of the metrics exporter.
2:- Further, we configured the Grafana(Monitoring) tool with Prometheus to analyse the logs which gives the clear & precise logs for every configured metric like (N/W)I/O, memory utilisation, DiskIO, No of requests/responses, Authentication Requests & so on..

F:- Scaling the Infrastructure for 100K users:- 

1:- There are some parameters like Auto Scaling can be done on AWS for increasing the number of instances if there is a load or the end user are increasing.
2:- Cluster can also scale in terms of (pods(containers)) using the Kubernetes manifests(Deployments).

G:- Infrastructure Provising to make the cloud agnostic using Terraform or AWS CFT(CloudFormation Templating)

1:- We must need to create the immutable infrastructure before deploying any new/updating any component.
2:- It enhances the security of the application.
3:- It prevents the entire application from being hard to maintain or fixing the issue if it occurs after any deployment or cluster upgradation.
4:- In immutable infra, it always destroys the existing infra & deploy the new one.
5:- Must be having a replica so that downtime should not occur.


Note:- Providing this info to the best of my knowledge in terms of the DevOps tools are concerned, I have not considered here the application architecture.
But if we do so, then below would be the rough diagram.


Application UI(end-user)->DNS Server(Router53-assuming)or(Public Endpoints)->LoadBalancer->API Gateway->Authenticaton API->(Services)or(Internal APIs)->Jobs/Queues->Databases+Caching(Redis)
