# Assignment 6 - Creating our infrastructure repository

Now we have our infrastructure ready to run our application.
- [x] Kubernetes is running.
- [x] ArgoCD is running.
- [x] Image available from registry
Now we need to bring everything together by defining how our application needs to run on our infrastrucure in our infrastructure repository

## Step by step instructions

## Step 1. Creating our repository on github
1. Go to GitHub and login to your account. https://github.com/

    > Create an account if you haven't already done that.

2. Create a repository for our infrastructure definition

    > I created a repository called gitops-workshop-infra

3. Clone the repository to your local environment
```console
git clone LINK-TO-YOUR-GITHUB-REPOSITORY
```

## Step 2. Defining our infrastructure
1. Now that we have our repository ready we need to define our infrastructure for our application

2. Create a yaml file within your infrastructure repository

    > I created a file called gitops-workshop-deployment.yaml

3. Add the following to the file and change the `<add your image from you docker hub>` part to your image from docker hub.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: gitops-workshop-deployment
  labels:
    app: gitops-workshop
spec:
  replicas: 1
  selector:
    matchLabels:
      app: gitops-workshop
  template:
    metadata:
      labels:
        app: gitops-workshop
    spec:
      containers:
      - name: gitops-workshop-website
        image: <add your image from you docker hub>
        ports:
        - containerPort: 80
```

4. Create another yaml file within your infrastructure repository

    > I created a file called gitops-workshop-service.yaml

5. Add the following to the file
```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: gitops-workshop
  name: gitops-workshop-service
spec:
  type: ClusterIP
  selector:
    app: gitops-workshop
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: 80
```

6. Create another yaml file within your infrastructure repository

    > I created a file called gitops-workshop-ingress.yaml

7. Add the following to the file
```yaml
apiVersion: v1
kind: Ingress
metadata:
  labels:
    app: gitops-workshop
  name: gitops-workshop-ingress
  annotations:
    ingress.kubernetes.io/ssl-redirect: "false"
    traefik.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /app
        backend:
          serviceName: gitops-workshop-service
          servicePort: 80
```

8. Push the files to the repository

## Next assignment

Make sure you stop all running processes and close all the terminal windows in VS Code before proceeding to the next 
assignment.

Go to [assignment 7](../Assignment07/README.md).