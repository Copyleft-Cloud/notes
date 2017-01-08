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

### STEP 2: Generate an API Access Token at DigitalOcean
Per the Terraform Documentation, we need a DigitalOcean API Token in order to provision resources such as new Droplets (aka Virtual Servers)

- Login to DigitalOcean using your Individual Account
- Navigate to API
- Click Generate New Token
- Name: (e.g. john.doe.do.api.token)

We're going to save our new API token in our /global/secret.tfvars
