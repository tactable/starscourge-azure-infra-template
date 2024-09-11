# Starscourge Pod - Azure Template

This will serve as a template for init an Azure project. This contains:

1. DevContainer setup with `az cli` and `bicep`. Feel free to add more
2. PR template
3. CI/CD bare minimum

# Getting started

1. Create repo from this template. See [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)
2. Change [name](./.devcontainer/devcontainer.json#L2) to your project name
3. Add your language to [features](./.devcontainer/devcontainer.json#L4) section. See [available features](https://containers.dev/features)

To enable CI/CD, create an Environment in Github. You can do that under Settings. At the moment of writing this, this workflow only supports deploy to dev environment on push to `main`. It is recommended to do a manual release `workflow_dispatch` for `staging` and `prod`. In the environment, configure the following

1. Create a Github Enterprise App in Entra ID. Follow [this guide](https://learn.microsoft.com/en-us/azure/app-service/deploy-github-actions?tabs=userlevel%2Caspnetcore)
2. In your terminal, generate azure service principal by following [this guide](./HOW_TO_OBTAIN_SERVICE_PRINCIPAL.md). Note down your `client secret` and `client id`. 
3. `AZURE_CREDENTIALS`: should be in the format of

```
{
    "clientSecret":  "******",
    "subscriptionId":  "******",
    "tenantId":  "******",
    "clientId":  "******"
}
```

4. `AZ_SERVICE_PRINCIPAL_CLIENT_ID`: the previously generate client id.
5. `AZ_SERVICE_PRINCIPAL_CLIENT_SECRET`: the previously generate client secret.

Configure the following vars:

1. `AZ_CONTAINER_REGISTRY_LOGIN_SERVER`: in the format of {registry-name}.azurecr.io
2. `IMAGE_NAME`: container image name
3. `AZ_BICEP_STACK_NAME`: the stack you want to deploy
4. `AZ_RESOUCE_GROUP`: The Azure resource group


