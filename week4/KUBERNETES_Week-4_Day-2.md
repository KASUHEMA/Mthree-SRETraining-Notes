KUBERNETES 
  Kubernetes  is  an  open-source  container  orchestration  platform  that 
automates  the  deployment,  scaling,  and  management  of  containerized 
applications.  It  helps  efficiently  run  applications  across  multiple  machines, 
ensuring high availability and resource optimization. 
 
In simpler terms we can say that like managing our application without failure 
and if there is any failure maintaining auto healing so that our application does 
not fail. 
 
●  Kubernetes consists mainly of four steps. They are: 
1.  Schedule  
2.  Auto scale 
3.  Find 
4.  Self heal 
 
●  Lets understood with an example 
Imagine you have a food truck. The first step is to check where to keep it. 
The next step is maintaining two people for making our items. We are 
ensuring that if one person does not come or can't prepare items then it 
heals and is replaced with another person so that our truck runs. Next 
phase is to find the correct time to run the food truck.  
 
 
●  In terms of technical the four steps are Deploy, Expose, Manage, Secure 
 
 
●  In  the  first  stage  we  are  ensuring  that  our  containers  are  running 
successfully  and  in  this  stage  we  will  create  a  yaml  file  for  our 
application. 
●  The next stage is to expose our application, that is to ensure that our 
application needs to run on which port and Ip address. 
●  After that we need to monitor our application that is to ensure that auto 
scaling as per the requirement. If the container fails it should be restarted 
in this stage. 
●  Finally  we  need  to  secure  our  application  by  auto scaling. By using 
config maps and secrets we ensure security. 

Phases of Kubernetes 
 
1.  API Server: 
  In this phase we are planning our container where to deploy. It acts 
as the brain of kubernetes. In simpler terms, if we go to a hotel, we first 
find reception so that we can know each and every thing for ourselves. 
Like that in kubernetes this is the stage where we can know what requests 
are accepting and what are declining. 
 
2.  ETCD: 
It is the phase we are observing about pod status and configurations 
and service details. In simpler terms we can say that getting input from 
other containers also improves the present working container. 
 
3.  Scheduler: 
It is the stage where it is decided where to deploy our container. It 
also watches new pods on which nodes to be placed and it acts as a 
traffic controller where it guides the request and workload should 
run. 
 
4.  Control Manager: 
It is the final phase where we are monitoring the container and 
providing security for our container. It ensures that our container is 
matching with the expected state and doesn't fail. In simpler terms 
we can say that it is a manager who ensures that everything runs as 
expected. 
 
 
 
 
 
 
 
 
 
 
 

Terms to remember in Kubernetes: 
 
●  Kubelet : It ensures that all containers in a node are running properly or 
not.  It  is  a  supervisor  for  a  few  containers.  There  will  be  a  main 
supervisor or manager under them Kubelet is one of the supervisors. 
●  Kube  Proxy  :  Manages  the  network  flow  and  ensures  that  data  is 
reaching  the  same  container  as  expected.  It  is a traffic manager that 
mainly focuses on traffic and ensures that all the data is reaching the 
correct container. 
●  Namespace  :  It  helps  to  group  resources  and  manage  them  in  a 
multi-tenant environment, ensuring isolation between different projects or 
teams. Grouping the data into one is known as namespace. 
●  Pods : A Pod is the smallest and simplest unit in Kubernetes. It represents 
a single instance of a running process in your cluster, typically running a 
container. In simpler terms we can say that deploying actual containers. 
 
 
●  We are storing all the required details in configmap and the password is 
stored in a secret folder. 
●  Commands to remember 
1.  kubectl apply -f name 
This command tells us to create/update resources. 
2.  kubectl get pods 
This command is used when pods are running. 
3.  kubectl describe pods 
This command describes the pods in depth. 
4.  kubectl logs pod name 
Viewing logs of pods in containers. 
5.  kubectl scale deployment filename –replica=5 
Scaling the number of machines i.e, we are creating the 5 replicas. 
6.  kubectl set image deployment/path 
Updating the containers image in the pods 
 
 
 
 
 