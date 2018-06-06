# Run Mautic on Kubernetes

The goal of this project is to be able to run Mautic on Kubernetes in a way that is easy to configure and manage.

## Step 0: Set up Kubernetes

The obvious requisite step here is to set up Kubernetes. This can vary depending on your infrastructure. I have tested this both locally (using Docker for Mac), along with GKE (Googke Kubernetes Engine) and evertyhing works well.

If you are having platform specific issues, feel free to create an issue and I'll try to troubleshoot.

## Step 1: Get Volumes

## Step 2: Set up MySQL

First, you want to create a [secret](https://kubernetes.io/docs/concepts/configuration/secret/) for the MySQL password:
`kubectl create secret generic mysql --from-literal=password=YOUR_PASSWORD`

Then you'll want to use the `mysql.yaml` file to deploy the manifest:
`kubectl apply -f mysql.yaml`

After that, use the `mysql-service.yaml` file to expose the service:
`kubectl apply -f mysql-service.yaml`

## Step 3: Set up Mautic

First use the `mautic.yaml` file to deploy the manifest:
`kubectl apply -f mautic.yaml`

Then, expose the service on Port 80:
`kubectl apply -f mautic-service.yaml`

## Step 4: View your site!

After waiting a few minutes to create the containers and set up the IP forwarding rules, run `kubectl get service` to get the public IP of the Mautuic pod.

Go to that IP and you will see the installation screen.
