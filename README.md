# .NET Framework Continuous Deployment Sample
A containerized (Windows) .NET Framework sample application setup with continuous deployment through **Azure DevOps** to Azure App Service. Follow the directions below to get started.

## Fork the Repository
Fork this repository or import it into your Azure DevOps repository. 

## Create Resources
Create the following resources. You will need information from each resource that will be used in the pipeline file and stored as a variable. Create your choice of registry (Azure Container Registry or Docker Hub) first since you will need information from there before you can create your App Service.

1. Azure Container Registry OR Docker Hub repository
2. App Service (Web App for Container)
3. .NET Framework application with supporting dockerfile in a GitHub repository
4. Azure SQL Database (Optional)

## Add a Service Connection
Before you create your pipeline, you should first create your Service Connection since you will be asked to choose and verify your connection when creating your template. A Service Connection will allow you to connect to your registry of choice (ACR or Docker Hub) when using the task templates. When adding a new service connection, choose the **Docker Registry** option.  The following form will ask you to choose Docker Hub or Azure Container Registry along with pertaining information.  You can create a new Service Connection following the directions [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints?view=azure-devops&tabs=yaml#create-new).  

 ## Secure Secrets with Variables
 > Variables are only accessible after your create the pipeline
 
Since we are using sensitive information that you don't want others to access, we will use variables to protect our information. Create a variable by following the directions [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch).  

To add a Variable, you click the **Variables** button next to the *Save* button in the top-right of the editing view for your pipeline.  Select the **New Variable** button and enter your information.  Add the variables below with your own secrets appropriate from each resource.

- `imageRepository`: image-name
- `containerRegistry`: - containerRegistry = 'your-registry-name.azurecr.io' OR 'your-docker-hub-registry-name'
- `applicationName`: app-name 
- `azureSQLConnectionString`: database-connection-string (Optional)
  
## Commit Changes
The `main.yaml` file is set to trigger on any pushes to master, so when you commit your changes the build will run.  View the **Actions** tab in your repository to view the build and any potential errors.
