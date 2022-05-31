# Store application data with Azure Blob storage

### Create the storage account
> az storage account create --kind StorageV2 --resource-group learn-e54db20a-2214-4281-93b3-8051a6fd4634 --location centralus --name [your-unique-storage-account-name] 

### Create an App Service app
> az appservice plan create --name blob-exercise-plan --resource-group learn-e54db20a-2214-4281-93b3-8051a6fd4634 --sku FREE --location centralus 

> az webapp create --name <your-unique-app-name> --plan blob-exercise-plan --resource-group learn-e54db20a-2214-4281-93b3-8051a6fd4634
  
### Get the storage account's connection string
  
> CONNECTIONSTRING=$(az storage account show-connection-string --name <your-unique-storage-account-name> --output tsv)
  
### Configure App Service with app settings
  
> az webapp config appsettings set --name <your-unique-app-name> --resource-group learn-e54db20a-2214-4281-93b3-8051a6fd4634 --settings AzureStorageConfig:ConnectionString=$CONNECTIONSTRING AzureStorageConfig:FileContainerName=files
  
### Publish the site to the pub folder
  
> dotnet publish -o pub
  
> cd pub
  
> zip -r ../site.zip *
  
### Deploy the zip to App Service
  
> az webapp deployment source config-zip --src ../site.zip --name <your-unique-app-name> --resource-group learn-e54db20a-2214-4281-93b3-8051a6fd4634
