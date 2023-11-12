# Assignment 4 - Installing ArgoCD on our cluster

We have our kubernetes cluster up and running locally
Now it's time to install our orchestrator ArgoCD

## Step by step instructions

## Step 1. Installing ArgoCD
1. Open the terminal window in VS Code.

   > You can do this by using the hotkey ``Ctrl-` `` (Windows) or ``Shift-Ctrl-` `` (macOS).

2. Create the argocd namespace by running the following command:
```console
kubectl create namespace argocd
```

3. Install ArgoCD on your local cluster by running the following command:
```console
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

4. Now ArgoCD is installed. Let's try to navigate to the UI. Run the following command to make ArgoCD available on port 8081
```console
kubectl port-forward svc/argocd-server -n argocd 8081:443
```

5. Open your browser and navigate to https://localhost:8081/ you will see the ArgoCD UI

6. To login we need to retrieve our password. Open up a new termininal. We can get the admin password as base64 by running the following command:
```console
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"
```

7. You will see a base64 string. After decoding the string you can login with `admin` as udername and the password you just decoded

8. You now have ArgoCD up and running on your local environment

## Next assignment

Make sure you stop all running processes and close all the terminal windows in VS Code before proceeding to the next 
assignment.

Go to [assignment 5](../Assignment05/README.md).