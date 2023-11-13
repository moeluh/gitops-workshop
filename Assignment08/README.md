# Assignment 8 - Change infrastructure

Now that ArgoCD is syncing let's change the infrastructure a bit.

## Step by step instructions

## Step 1. Change amount of replicas
1. Open you deployment yaml from your infrastructure repository

2. Change the ammount of replicas from 1 to 2

3. Commit and push the change

4. Open ArgoCD and see if the changes are applied automatically

2. Run the following command to create a new namespace on your local kubernetes cluster
```console
kubectl create namespace dev
```