# Terraform Apply for Azure Action

This Action allows you to apply Terraform manifests to Azure. It expects an Azure blob storage (to be specified in your manifests like the below) to store the shared state.

```terraform
terraform {
  backend "azurerm" {
    storage_account_name = "storage_account_name"
    container_name       = "storage_container_name"
  }
}
```

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `arm_client_id` | `string` | | Azure Service Principal client_id |
| `arm_client_secret` | `string` | | Azure Service Principal client_secret |
| `arm_subscription_id` | `string` | | Azure subscription |
| `arm_tenant_id` | `string` | | Azure Tenant id |
| `arm_access_key` | `string` | | Azure Storage access key |
| `variables` | `string` | `""` | Comma-separated string of Terraform variables |
| `path` | `string` | `.` | Path to Terraform directory, defaults to the working directory |
| `varfile` | `string` | `.` | Name of tfvars file, defaults to variables.tfvars |

## Usage

```yaml
jobs:
  provisioning:
    runs-on: ubuntu-latest
    steps:
    - uses: nil0blue/terraform-azure-pipeline@v1
      with:
        arm_client_id: ${{ secrets.ARM_CLIENT_ID }}
        arm_client_secret: ${{ secrets.ARM_CLIENT_SECRET }}
        arm_subscription_id: ${{ secrets.ARM_SUBSCRIPTION_ID }}
        arm_tenant_id: ${{ secrets.ARM_TENANT_ID }}
        variables: var=${{ rg_name=aks }}
        path: terraform/dev
        varfile: variables.tfvars
```

## License

The MIT License (MIT)
