# Cloudify Automation Toolset

## Cloudify AIO
The blueprint provisions a Virtual Machine on the desired Cloud environment.  
Supported cloud providers are: AWS, Azure, and GCP.  

### Requirements
In order to run the blueprint successfully you need to provide secrets with credentials and install plugins relevant for the cloud provider.  

### Secrets
Before deploying the blueprint on any Cloud Provider, create a license secret:

| Name                  | Description                             |
| --------------------- | --------------------------------------- |
| license               | Cloudify Manager license in yaml format |

In order to deploy to AWS, you need to create the following secrets beforehand:

| Name                  | Description           |
| --------------------- | --------------------- |
| aws_access_key_id     | AWS Access Key ID     |
| aws_aceess_secret_key | AWS Access Secret Key |

For Azure:

| Name                  | Description            |
| --------------------- | ---------------------- |
| azure_tenant_id       | Azure tenant ID        |
| azure_subscription_id | Azure subcription ID   |
| azure_client_id       | Azure client ID        |
| azure_client_secret   | Azure client secret    |

For GCP:

| Name                  | Description                       |
| --------------------- | --------------------------------- |
| gcp_credentials       | GCP credentials json file content |


### Plugins

Blueprints use the following [plugins](https://cloudify.co/plugins/):
- [Cloudify Fabric Plugin](https://github.com/cloudify-cosmo/cloudify-fabric-plugin)
- [Cloudify Utilities Plugin](https://github.com/cloudify-incubator/cloudify-utilities-plugin)
- [Cloudify AWS Plugin](https://github.com/cloudify-cosmo/cloudify-aws-plugin) (for AWS deployment)
- [Cloudify Azure Plugin](https://github.com/cloudify-cosmo/cloudify-azure-plugin) (for Azure deployment)
- [Cloudify GCP Plugin](https://github.com/cloudify-cosmo/cloudify-gcp-plugin) (for GCP deployment)

### Inputs

| Display Label                           | Name                            | Type   | Description                                               | Default      |
| --------------------------------------- | ------------------------------- | ------ | --------------------------------------------------------- | ------------ |
| Provider name                           | provider_name                   | string | Provider name chosen from: AWS, Azure, GCP.               | aws          |
| Cloudify Manager Version                | cloudify_manager_version        | string | Version of the Cloudify Manager to install.               | 6.4.1        |
| Resources Prefix                        | resource_prefix                 | string | Control parameters for names in resources.                | dev          |
| Cloudify Manager Admin Password         | cloudify_manager_admin_password | string | Password for Admin user on the Cloudify Manager instance. | admin        |
| Region name                             | region_name                     | string | Select region name.                                       | us-east-1    |
| VPC CIDR                                | vpc_cidr                        | string | CIDR of the new VPC.                                      | 10.10.0.0/16 |
| Subnet CIDR                             | subnet_cidr                     | string | CIDR of the new Subnet.                                   | 10.10.0.0/24 |
| Availability Zone                       | availability_zone               | string | Select Availability Zone in VPC.                          | a            |
| VM size                                 | instance_type                   | string | VM size.                                                  | t2.medium    |
| Agent Username                          | agent_user                      | string | The username of the agent on the VM.                      | centos       |
| Secret name for Agent Private Key       | agent_key_name                  | string | Secret name for Agent Private Key.                        | agent_key    |
| Subnet CIDR                             | subnet_cidr                     | string | CIDR of the new Subnet.                                   | 10.10.0.0/24 |
| URL for secrets vallidation zip archive | secrets_validation_archive      | string | URL for secrets vallidation zip archive                   | N/A          |
| Secrets to validate                     | secrets_to_validate             | dict   | Provider secrets to check existence & values              | N/A          |

### Capabilities

| Name              | Description                         |
| ----------------- | ----------------------------------- |
| endpoint          | The external endpoint of the VM.    |
| user              | User ID.                            |
| key_content       | Private agent key.                  |
| vpc_id            | VPC resource ID.                    |
| vm_id             | VM resource ID.                     |

### Estimated Install & Uninstall times

The times may be longer for the first deployment as the relevant plugin installs.  

| Cloud   | Estimated Install Time   |
| ------- | ------------------------ |
| AWS     | ~ 10 min                 |
| Azure   | ~ 14 min                 |
| GCP     | ~  9 min                 |

| Cloud   | Estimated Uninstall Time |
| ------- | ------------------------ |
| AWS     | ~  3 min                 |
| Azure   | ~  4 min                 |
| GCP     | ~  4 min                 |
