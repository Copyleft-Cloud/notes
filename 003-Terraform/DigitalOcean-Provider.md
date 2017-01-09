# Terraform + DigitalOcean Provider


## Overview
We've decided to use DigitalOcean to host our Hubot! To get started, we're going to provision our new host using Terraform.


### STEP 1: Review the DigitalOcean Provider Docs
- https://www.terraform.io/docs/providers/do/index.html

The DigitalOcean (DO) provider is used to interact with the resources supported by DigitalOcean. The provider needs to be configured with the proper credentials before it can be used.

#### EXAMPLE
```
# Set the variable value in *.tfvars file
# or using -var="do_token=..." CLI option
variable "do_token" {}

# Configure the DigitalOcean Provider
provider "digitalocean" {
    token = "${var.do_token}"
}

# Create a web server
resource "digitalocean_droplet" "web" {
    ...
}
```


### STEP 2:  DigitalOcean API Token
Let's quickly confirm that we have saved our DigitalOcean API token in /global/secret.tfvars

```
# DIGITAL OCEAN (DO)
do_api_token = "<DigitalOcean API Token>"
```

### STEP 3: Create Environment Directory
We're going to use DigitalOcean to host several DevOps services. Let's create a directory where we can manage the state of this service environment.  

```
cd /Users/<username>/Github/copyleft-cloud/terraform/provider-do
mkdir env-svc
```
