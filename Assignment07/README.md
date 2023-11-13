# Assignment 7 - Configure ArgoCD

Now we have everything in place to deploy our application.
Let's configure ArgoCD.

## Step by step instructions

## Step 1. Create a development namespace
1. Open the terminal window in VS Code.

   > You can do this by using the hotkey ``Ctrl-` `` (Windows) or ``Shift-Ctrl-` `` (macOS).

2. Run the following command to create a new namespace on your local kubernetes cluster
```console
kubectl create namespace dev
```

## Step 2. Create ArgoCD project
1. Create a yaml file on your machine

    > I created a file called gitops-workshop-project.yaml

2. Add the following to the file
```yaml
apiVersion: argoproj.io/v1alpha1
kind: AppProject
metadata:
  name: gitops-workshop-project
  labels:
    app: gitops-workshop
spec:
  # Project description
  description: An ArgoCD Project to run our apps locally
  # Allow manifests to deploy only from Sokube git repositories
  sourceRepos:
  - "https://github.com/<your github username>/*"
  # Only permit to deploy applications in the same cluster
  destinations:
  - namespace: dev
    server: https://kubernetes.default.svc
  # Enables namespace orphaned resource monitoring.
  orphanedResources:
    warn: false
```

3. Run the following command to create the project
```console
kubectl apply -f .\gitops-workshop-project.yaml -n argocd
```

## Step 3. Create ArgoCD application
1. Create a yaml file on your machine

    > I created a file called gitops-workshop-application.yaml

2. Add the following to the file
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  labels:
    app: gitops-workshop
  name:  gitops-workshop-application
spec:
  project: gitops-workshop-project
  source:
    repoURL: <github infra repository link>
    targetRevision: main
    path: .
    directory:
      recurse: true
  destination:
    server: https://kubernetes.default.svc
    namespace: dev
  syncPolicy:
    automated:
      prune: false
      selfHeal: true
```

3. Run the following command to create the project
```console
kubectl apply -f .\gitops-workshop-application.yaml -n argocd
```

4. Open ArgoCD in your browser and login. You will see an application in the UI and that it's synced.


5. Browse to the application in your browser to test it. http://localhost:8082/

## Next assignment

Make sure you stop all running processes and close all the terminal windows in VS Code before proceeding to the next 
assignment.

Go to [assignment 7](../Assignment07/README.md).