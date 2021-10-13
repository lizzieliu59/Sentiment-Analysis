# Sentiment-Analysis
Extra credit project for 14848
First, I **create a GKE cluster** using:

```
gcloud container clusters create cloud848 --zone=us-east1-d --num-nodes=1 --machine-type=custom-4-12288 
```

Then, I **build the docker images** of 3 application using the following commands  and **push them to GCR**(the similar for the rest two applications):

```
docker buildx  build -t yueliu14848/sa-logic . --platform linux/amd64
docker tag yueliu14848/sa-logig us.gcr.io/kube-328902/yueliu14848/sa-logic 
docker push us.gcr.io/kube-328902/yueliu14848/sa-logic
```

Then, I **deploy the with a deployment file**: sa-web-app-deployment.yaml using:

```
kubectl apply -f sa-web-app-deployment.yaml
```

And then **deploy the service** service-sa-web-app-lb.yaml using:

```
kubectl apply -f service-sa-web-app-lb.yaml 
```

**The same steps are applied to the the logic deployment and service**. 

After these,  I use:

```
kubectl get svc 
```

to **get the external-ip** of the sa-web-app-lb, and then **change the ip address of web app in the frontend code** to 'http://34.138.126.205:80/sentiment'.

And then do the same deployment and service for the frontend. Using:

```
kubectl apply -f sa-frontend-deployment.yaml 
kubectl create -f service-sa-frontend-lb.yaml 
```
Screenshot of frontend service external IP:
<img width="692" alt="Screen Shot 2021-10-13 at 12 04 34 AM" src="https://user-images.githubusercontent.com/53706052/137066127-c8d026ef-4281-4d97-89bd-c0c4f40bed44.png">



Screenshot of GKE cluster:

<img width="1440" alt="Screen Shot 2021-10-13 at 12 06 07 AM" src="https://user-images.githubusercontent.com/53706052/137066133-7488ea91-2e7a-46f0-83b0-08dfc9a54bd1.png">

URLs of Docker images:

Logic application: https://hub.docker.com/repository/docker/yueliu14848/sentiment-analysis-logic

Web App application: https://hub.docker.com/repository/docker/yueliu14848/sentiment-analysis-web-app

Frontend applicaiton: https://hub.docker.com/repository/docker/yueliu14848/sentiment-analysis-frontend



