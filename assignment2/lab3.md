#  Creating a Google Kubernetes Engine cluster containing several containers

1. Sign in to the Google Cloud Platform (GCP) Console
2. Confirm that needed APIs are enabled
    - In the GCP Console, on the Navigation menu (Navigation menu), click `APIs & Services`.
    - Scroll down in the list of enabled APIs, and confirm that both of these APIs are enabled:
        a. *Kubernetes Engine API*
        b. *Container Registry API*
    - If either API is missing, click `Enable APIs and Services` at the top. Search for the above APIs by name    and enable each for your current project

## Start a Kubernetes Engine cluster

1. In GCP console, on the top right toolbar, click the `Open Cloud Shell` button and click `continue`
2. For convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. At the Cloud Shell prompt, type this partial command: eg `export MY_ZONE=us-central1-a`
3. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster `webfrontend` and configure it to run 2 nodes:
4. After the cluster is created, check your installed version of Kubernetes using the `kubectl version` command:
The `gcloud container clusters create` command automatically authenticated kubectl for you.

## Run and deploy a container

1. From your `Cloud Shell` prompt, launch a single instance of the nginx container. 
`kubectl create deploy nginx --image=nginx:1.17.10`
In Kubernetes, all containers run in pods. This use of the kubectl create command caused Kubernetes to create a deployment consisting of a single pod containing the nginx container. A Kubernetes deployment keeps a given number of pods up and running even in the event of failures among the nodes on which they run. In this command, you launched the default number of pods, which is 1.

2. View the pod running the nginx container: `kubectl get pods`
3. Expose the nginx container to the Internet: `kubectl expose deployment nginx --port 80 --type LoadBalancer`
Kubernetes created a service and an external load balancer with a public IP address attached to it. The IP address remains the same for the life of the service. Any network traffic to that public IP address is routed to pods behind the service: in this case, the nginx pod.
4. View the new service `kubectl get services`
5. Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.
6. Scale up the number of pods running on your service: `kubectl scale deployment nginx --replicas 3`
Scaling up a deployment is useful when you want to increase available resources for an application that is becoming more popular.
7. Confirm that Kubernetes has updated the number of pods:
`kubectl get pods`
8. Confirm that your external IP address has not changed: `kubectl get services`
9. Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.




