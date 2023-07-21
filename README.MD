# terraform-by-documentation

# # Infrastructure as Code with Terraform!

Infrastructure as code (IaC) tools allow you to manage infrastructure with configuration files rather than through a graphical user interface. You can:
- Build 
- Change
- Manage

Terraform is HashiCorp's infrastructure as code tool. It lets you define resources and infrastructure in human-readable, declarative configuration files, and manages your infrastructure's lifecycle. Using Terraform has several advantages over manually managing your infrastructure:

-   Terraform can manage infrastructure on multiple cloud platforms.
-   The human-readable configuration language helps you write infrastructure code quickly.
-   Terraform's state allows you to track resource changes throughout your deployments.
-   You can commit your configurations to version control to safely collaborate on infrastructure.

## Provider
Providers define individual units of infrastructure, for example compute instances or private networks, as resources. You can compose resources from different providers into reusable Terraform configurations called modules, and manage them with a consistent language and workflow.

To deploy infrastructure with Terraform:

-   **Scope** - Identify the infrastructure for your project.
-   **Author** - Write the configuration for your infrastructure.
-   **Initialize** - Install the plugins Terraform needs to manage the infrastructure.
-   **Plan** - Preview the changes Terraform will make to match your configuration.
-   **Apply** - Make the planned changes.

# Build Infrastructure - Terraform GCP


## Prerequisites

-   **A Google Cloud Platform account.** If you do not have a GCP account, [create one now](https://console.cloud.google.com/freetrial/). This tutorial can be completed using only the services included in the GCP [free tier](https://cloud.google.com/free/).
    
-   [Terraform 0.15.3+](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) installed locally.

## Set up GCP

After creating your GCP account, create or modify the following resources to enable Terraform to provision your infrastructure:

-   **A GCP Project**: GCP organizes resources into projects. [Create one now](https://console.cloud.google.com/projectcreate) in the GCP console and make note of the project ID. You can see a list of your projects in the [cloud resource manager](https://console.cloud.google.com/cloud-resource-manager).
    
-   **Google Compute Engine**: Enable Google Compute Engine for your project [in the GCP console](https://console.developers.google.com/apis/library/compute.googleapis.com). Make sure to select the project you are using to follow this tutorial and click the "Enable" button.
    
-   **A GCP service account key**: [Create a service account key](https://console.cloud.google.com/apis/credentials/serviceaccountkey) to enable Terraform to access your GCP account. When creating the key, use the following settings:
    
    -   Select the project you created in the previous step.
    -   Click "Create Service Account".
    -   Give it any name you like and click "Create".
    -   For the Role, choose "Project -> Editor", then click "Continue".
    -   Skip granting additional users access, and click "Done".
    
    After you create your service account, download your service account key.
    
    -   Select your service account from the list.
    -   Select the "Keys" tab.
    -   In the drop down menu, select "Create new key".
    -   Leave the "Key Type" as JSON.
    -   Click "Create" to create the key and save the key file to your system.
    
    You can read more about service account keys in [Google's documentation](https://cloud.google.com/iam/docs/creating-managing-service-account-keys).
    

### Terraform Block

The `terraform {}` block contains Terraform settings, including the required providers Terraform will use to provision your infrastructure. For each provider, the `source` attribute defines an optional hostname, a namespace, and the provider type. Terraform installs providers from the [Terraform Registry](https://registry.terraform.io/) by default. In this example configuration, the `google` provider's source is defined as `hashicorp/google`, which is shorthand for `registry.terraform.io/hashicorp/google`.

You can also define a version constraint for each provider in the `required_providers` block. The `version` attribute is optional, but we recommend using it to enforce the provider version. Without it, Terraform will always use the latest version of the provider, which may introduce breaking changes.

To learn more, reference the [provider source documentation](https://developer.hashicorp.com/terraform/language/providers/requirements).## Export a file

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.

### Providers

The `provider` block configures the specified provider, in this case `google`. A provider is a plugin that Terraform uses to create and manage your resources. You can define multiple provider blocks in a Terraform configuration to manage resources from different providers.

### Resource

Use `resource` blocks to define components of your infrastructure. A resource might be a physical component such as a server, or it can be a logical resource such as a Heroku application.

Resource blocks have two strings before the block: the resource type and the resource name. In this example, the resource type is `google_compute_network` and the name is `vpc_network`. The prefix of the type maps to the name of the provider. In the example configuration, Terraform manages the `google_compute_network` resource with the `google` provider. Together, the resource type and resource name form a unique ID for the resource. For example, the ID for your network is `google_compute_network.vpc_network`.

Resource blocks contain arguments which you use to configure the resource. Arguments can include things like machine sizes, disk image names, or VPC IDs. The [Terraform Registry GCP documentation page](https://registry.terraform.io/providers/hashicorp/google/latest/docs) documents the required and optional arguments for each GCP resource. For example, you can read the [`google_compute_network`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_network.html) documentation to view the resource's supported arguments and available attributes.

The [GCP provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs) documents supported resources, including [google_compute_network](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_network.html) and its supported arguments.
