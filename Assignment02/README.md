# Assignment 2 - Containerize the application

In this assignment, you'll create a docker file and build a docker image for the application.
We will also run the image in a container locally.
This is to prepare the application for running in a kubernetes cluster

## Step by step instructions

## Step 1. Create a dockerfile
1. Open the source code folder in your IDE (Ex: Visual Studio Code)

2. Create a new file called `dockerfile` in the root of the repository

3. Add the following lines to the dockerfile
```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Website/Website.csproj", "."]
RUN dotnet restore "Website.csproj"
COPY . .
RUN dotnet build "Website/Website.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Website/Website.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Website.dll"]
```

## Step 2 Build the image
1. Open the terminal window in VS Code.

   > You can do this by using the hotkey ``Ctrl-` `` (Windows) or ``Shift-Ctrl-` `` (macOS).

2. Build an image from the application using docker by running the follwing command.
```console
docker build -t gitops-workshop-csharp .
```

## Step 3 Run the image in a container
1. When the build is done we can run the image in a container

2. Run the image in a container using docker by running the follwing command.
```console
docker run -p 8080:80 gitops-workshop-csharp
```

3. Open your browser and verify if you can access the application by browsing to the following [link](http://localhost:8080/)


## Next assignment

Make sure you stop all running processes and close all the terminal windows in VS Code before proceeding to the next 
assignment.

Go to [assignment 3](../Assignment03/README.md).