# Assignment 5 - Pushing your image to DockerHub

Now our infrastructure is ready let's go back to our application.
To use our image in our infrastructure definition the image should be available from a image registry.
We will be using DockerHub as our registry.

## Step by step instructions

## Step 1. Create a repository on DockerHub
1. Go to DockerHub and login to your account. https://hub.docker.com/

    > Create an account if you haven't already done that.

2. Create a repository for your image

    > I created a repository called gitops-workshop

## Step 2. Push our image to that repository
1. Open the terminal window in VS Code.

   > You can do this by using the hotkey ``Ctrl-` `` (Windows) or ``Shift-Ctrl-` `` (macOS).

2. Login with your docker account
```console
docker login -u YOUR-USER-NAME
```

3. Tag our image with the repository name
```console
docker tag gitops-workshop-csharp YOUR-USER-NAME/gitops-workshop
```

4. Push the image to your docker hub repository
```console
docker push YOUR-USER-NAME/gitops-workshop
```

## Next assignment

Make sure you stop all running processes and close all the terminal windows in VS Code before proceeding to the next 
assignment.

Go to [assignment 6](../Assignment06/README.md).