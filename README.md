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

