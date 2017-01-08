# Terraform + DigitalOcean Provider


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


### STEP 2:  Save our API Token in /global/secret.tfvars
We're going to save our new API token in our /global/secret.tfvars
