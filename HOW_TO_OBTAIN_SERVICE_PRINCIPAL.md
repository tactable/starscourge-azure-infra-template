## Context

`AZ_SERVICE_PRINCIPAL_CLIENT_ID` and `AZ_SERVICE_PRINCIPAL_CLIENT_SECRET` are github actions secrets that is part of the Service Principal in Enterprise Application ID in Azure. These are used a lot in Github Workflows to Authenticate to Azure Container Registry

## How to retrieve these values

Whenever you get a 401 when pushing images to Azure, do the following

```
az login -t <tenant>

az ad sp list --display-name GithubActions --query "[].id" -o tsv
```

Note down the id, then do

```
az ad sp credential reset --id <the-id-you-have-just-noted>
```

Then `appId` -> `AZ_SERVICE_PRINCIPAL_CLIENT_ID` and `password` -> `AZ_SERVICE_PRINCIPAL_CLIENT_SECRET`