# mini-project
Deploying the image on kubernetes cluster using CD pipeline

1.We used Dockerfile to build nginx image and then we pushed it to docker hub registry.
2.Jenkinsfile consists of declarative jenkins pipeline
3.deploy.yml consists of deployment and service information of the kubernetes cluster.
4.We used minikube to create  a cluster and deployed the image on that kubernetes cluster.
5.We did the whole process locally using jenkins at localhost:8080 and so we can access the image which is deployed on the cluster locally using localhost:80.
