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

### STEP 4: Create an Environment Terraform File (service.tf)
Let's create a terraform file for this environment which configures the provider.

```
# DEFINE THE VARIABLE FOR THE DIGITAL OCEAN API TOKEN
# SET THE VALUE IN /global/secret.tfvars
variable "do_api_token" {}


# CONFIGURE THE DIGITAL OCEAN PROVIDER
provider "digitalocean" {
    token = "${var.do_api_token}"
}
```

### STEP 5: Create a Device Terraform File (device-hubot.tf)
Let's create a device-hubot.tf Terraform file that we'll use to provision a new droplet in DigitalOcean to host our Hubot Instance.  

Using the device-&lt;role&gt;.tf naming convention is very declarative and makes it easy to identify and manage the roles within your platform infrastructure.

#### TIP
It is a good practice as a team to follow a consistent infrastructure naming scheme.  

```
hubot.svc.copyleft.io
<hostname>.<environment>.<domain>
```

Here is the resource we've defined...
```
# CREATE A NEW DROPLET

resource "digitalocean_droplet" "hubot" {
    image = "ubuntu-16-04-x64"
    name = "hubot.svc.copyleft.io"
    region = "nyc3"
    size = "1gb"
}
```

### STEP 6: Symlink secret.tfvars to our Environment Directory
```
cd /Users/<username>/Github/copyleft-cloud/terraform/provider-do/env-svc
ln -s ../../global/secret.tfvars secret.tfvars

ls -lart
total 24
drwxr-xr-x  3 brian.hooper  1446486574  102 Jan  9 08:09 ..
-rw-r--r--  1 brian.hooper  1446486574  225 Jan  9 13:44 service.tf
-rw-r--r--  1 brian.hooper  1446486574  175 Jan  9 13:49 device-hubot.tf
lrwxr-xr-x  1 brian.hooper  1446486574   26 Jan  9 13:59 secret.tfvars -> ../../global/secret.tfvars
drwxr-xr-x  5 brian.hooper  1446486574  170 Jan  9 13:59 .
```

### STEP 7: Update .gitignore
We do not want to push any of our symlinked secret.tfvars files to our repo.

```
# DO NOT PUSH SYMLINKED secret.tfvars
# Includes Account IDs, Private Keys, and API Tokens
**/secret.tfvars
```

### STEP 8: Terraform Plan
Now that we have all of our configuration in place, let's run terraform plan to verify the changes that will be implemented.
```
terraform plan -var-file="secret.tfvars"

Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but
will not be persisted to local or remote state storage.

The Terraform execution plan has been generated and is shown below.
Resources are shown in alphabetical order for quick scanning. Green resources
will be created (or destroyed and then created if an existing resource
exists), yellow resources are being changed in-place, and red resources
will be destroyed. Cyan entries are data sources to be read.

Note: You didn't specify an "-out" parameter to save this plan, so when
"apply" is called, Terraform can't guarantee this is what will execute.

+ digitalocean_droplet.hubot
    disk:                 "<computed>"
    image:                "ubuntu-16-04-x64"
    ipv4_address:         "<computed>"
    ipv4_address_private: "<computed>"
    ipv6_address:         "<computed>"
    ipv6_address_private: "<computed>"
    locked:               "<computed>"
    name:                 "hubot.svc.nyc.copyleft.io"
    region:               "nyc3"
    resize_disk:          "true"
    size:                 "1gb"
    status:               "<computed>"
    vcpus:                "<computed>"


Plan: 1 to add, 0 to change, 0 to destroy.
```

As you can see via the output above, a new droplet will be created.


### STEP 9: Terraform Apply
Let's apply our terraform plan and create our new instance.

```
terraform apply -var-file="secret.tfvars"

digitalocean_droplet.hubot: Creating...
  disk:                 "" => "<computed>"
  image:                "" => "ubuntu-16-04-x64"
  ipv4_address:         "" => "<computed>"
  ipv4_address_private: "" => "<computed>"
  ipv6_address:         "" => "<computed>"
  ipv6_address_private: "" => "<computed>"
  locked:               "" => "<computed>"
  name:                 "" => "hubot.svc.nyc.copyleft.io"
  region:               "" => "nyc3"
  resize_disk:          "" => "true"
  size:                 "" => "1gb"
  status:               "" => "<computed>"
  vcpus:                "" => "<computed>"
digitalocean_droplet.hubot: Still creating... (10s elapsed)
digitalocean_droplet.hubot: Still creating... (20s elapsed)
digitalocean_droplet.hubot: Creation complete

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

The state of your infrastructure has been saved to the path
below. This state is required to modify and destroy your
infrastructure, so keep it safe. To inspect the complete state
use the `terraform show` command.

State path: terraform.tfstate
```

### STEP 10: Review the Terraform State File (.tfstate)
Following the Apply, you'll see that a Terraform State File (terraform.tfstate) was created within the scope of our env-svc environment.


### STEP 11: Verify the New Droplet via DigitalOcean Console
- Go to https://cloud.digitalocean.com and Login to your acccount.
- You should now see the droplet.


### STEP 12: Email Verification...
You should receive an email notification with Root Credentials to access your new droplet. (See Below)

This is pretty messy, and would be much more secure using SSH Keys Associated with our DigitalOcean Account.  Let's do this again and this time create a new droplet using an SSH Key for our Authentication.

```
Your new Droplet is all set to go! You can access it using the following credentials:

Droplet Name: hubot.svc.nyc.copyleft.io
IP Address: <public_ip_address>
Username: root
Password: <random_password>
```

### STEP 13: Get List of SSH KEYS
Let's use our API Token and the DigitalOcean API to retrieve the list of SSH Keys for our Account.

See: https://developers.digitalocean.com/documentation/v2/#ssh-keys

```
# EXAMPLE CURL REQUEST
 curl -X $HTTP_METHOD -u "$TOKEN:" "https://api.digitalocean.com/v2/$OBJECT"

# EXAMPLE CURL REQUEST TO LIST SSH KEYS FOR OUR ACCOUNT
 $ curl -X GET -u "<YOUR API TOKEN>" "https://api.digitalocean.com/v2/account/keys"
Enter host password for user '<YOUR API TOKEN>': <YOUR PASSWORD>

# RESPONSE
{"ssh_keys":[{"id":<SSH_KEY_ID>,"fingerprint":"<FINGER_PRINT>","public_key":"<SSH RSA PUBLIC KEY>","name":"<KEY NAME>"}],"links":{},"meta":{"total":1}}[14:26:35 ]
```

From the above response we're able to get the SSH_KEY_ID

Now we can use that SSH_KEY_ID during provisioning with Terraform, and the list of ssh key(s) we pass in will be automatically installed and configured at the time of droplet creation.  

Let's update our ./global/secret.tfvars file and add the ssh_key_id we want to use during provisioning of new droplets.  For now, let's just use the main ssh key we created for our team. (e.g. id_cloud_copyleft_io)

./global/secret.tfvars
```
# DIGITAL OCEAN (DO)
do_api_token = "<api_token>"
do_ssh_key_id = "<ssh_key_id>"
```

Let's update our service.tf file and define the variable in our Terraform plan for our Service Environment.
```
# DEFINE THE VARIABLE FOR THE SSH KEY TO USE DURING PROVISIONING
# SET THE VALUE IN /global/secret.tfvars
variable "do_ssh_key_id" {}
```


### STEP 14: Delete the old Droplet
Let's Comment out the resource and re-run Terraform Plan and Terraform Apply to delete the droplet... so we can reprovision a new instance using our SSH Key(s)

Comment out the resource in device-hubot.tf
```
#resource "digitalocean_droplet" "hubot" {
#    image = "ubuntu-16-04-x64"
#    name = "hubot.svc.nyc.copyleft.io"
#    region = "nyc3"
#    size = "1gb"
#}
```

Review the proposed changes (i.e. destroy) via Terraform Plan
```
terraform plan -var-file="secret.tfvars"
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but
will not be persisted to local or remote state storage.

digitalocean_droplet.hubot: Refreshing state... (ID: 36774324)

The Terraform execution plan has been generated and is shown below.
Resources are shown in alphabetical order for quick scanning. Green resources
will be created (or destroyed and then created if an existing resource
exists), yellow resources are being changed in-place, and red resources
will be destroyed. Cyan entries are data sources to be read.

Note: You didn't specify an "-out" parameter to save this plan, so when
"apply" is called, Terraform can't guarantee this is what will execute.

- digitalocean_droplet.hubot


Plan: 0 to add, 0 to change, 1 to destroy.
```


Delete the Droplet via Terraform Apply
```
terraform apply -var-file="secret.tfvars"
digitalocean_droplet.hubot: Refreshing state... (ID: 36774324)
digitalocean_droplet.hubot: Destroying...
digitalocean_droplet.hubot: Still destroying... (10s elapsed)
digitalocean_droplet.hubot: Destruction complete

Apply complete! Resources: 0 added, 0 changed, 1 destroyed.
```




### STEP 14: Create a New Droplet with SSH Keys Installed
Let's recreate the droplet for our hubot instance, this time configuring our SSH Key(s) to be installed at the time of droplet creation...

```
# CREATE A NEW DROPLET

resource "digitalocean_droplet" "hubot" {
    image = "ubuntu-16-04-x64"
    name = "hubot.svc.nyc.copyleft.io"
    region = "nyc3"
    size = "1gb"
    ssh_keys = ["${var.do_ssh_key_id}"]
}
```

Review the proposed changes (i.e. add) via Terraform Plan
```
$ terraform plan -var-file="secret.tfvars"
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but
will not be persisted to local or remote state storage.


The Terraform execution plan has been generated and is shown below.
Resources are shown in alphabetical order for quick scanning. Green resources
will be created (or destroyed and then created if an existing resource
exists), yellow resources are being changed in-place, and red resources
will be destroyed. Cyan entries are data sources to be read.

Note: You didn't specify an "-out" parameter to save this plan, so when
"apply" is called, Terraform can't guarantee this is what will execute.

+ digitalocean_droplet.hubot
    disk:                 "<computed>"
    image:                "ubuntu-16-04-x64"
    ipv4_address:         "<computed>"
    ipv4_address_private: "<computed>"
    ipv6_address:         "<computed>"
    ipv6_address_private: "<computed>"
    locked:               "<computed>"
    name:                 "hubot.svc.nyc.copyleft.io"
    region:               "nyc3"
    resize_disk:          "true"
    size:                 "1gb"
    ssh_keys.#:           "1"
    ssh_keys.0:           "<ssh_key_id>"
    status:               "<computed>"
    vcpus:                "<computed>"


Plan: 1 to add, 0 to change, 0 to destroy.
```

Create the Droplet via Terraform Apply
```
$ terraform apply -var-file="secret.tfvars"
digitalocean_droplet.hubot: Creating...
  disk:                 "" => "<computed>"
  image:                "" => "ubuntu-16-04-x64"
  ipv4_address:         "" => "<computed>"
  ipv4_address_private: "" => "<computed>"
  ipv6_address:         "" => "<computed>"
  ipv6_address_private: "" => "<computed>"
  locked:               "" => "<computed>"
  name:                 "" => "hubot.svc.nyc.copyleft.io"
  region:               "" => "nyc3"
  resize_disk:          "" => "true"
  size:                 "" => "1gb"
  ssh_keys.#:           "" => "1"
  ssh_keys.0:           "" => "<ssh_key_id>"
  status:               "" => "<computed>"
  vcpus:                "" => "<computed>"
digitalocean_droplet.hubot: Still creating... (10s elapsed)
digitalocean_droplet.hubot: Still creating... (20s elapsed)
digitalocean_droplet.hubot: Creation complete

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

The state of your infrastructure has been saved to the path
below. This state is required to modify and destroy your
infrastructure, so keep it safe. To inspect the complete state
use the `terraform show` command.

State path: terraform.tfstate
```

### STEP 15: SSH into the new Droplet
Let's use our ssh private key to ssh into our new droplet...

```
ssh root@<public_ip_address> -i <ssh_private_key>
The authenticity of host '<public_ip_address> (<public_ip_address>)' can't be established.
ECDSA key fingerprint is SHA256:<finger_print>.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '<public_ip_address>' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-57-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

root@hubot:~#
```

## SUCCESS!
As you can see, we can now access our new Digital Ocean instances using our SSH Key.  

Hopefully this gives you a great primer into the power of using Terraform to define, configure, and provision cloud hosted infrastructure.  

## Summary
Ok, we've accomplished quite a bit here... There is quite a bit more customized provisioning that we can do using Terraform which we will cover in more detail as we go.

Here is what we've knocked out... 
- Defined a New Environment in our Terraform Project (env-svc)
- Created and Deleted a Droplet using Terraform
- Used our API Token and the DigitalOcean API to retrieve our SSH Keys
- Created a New Droplet and Provisioned our SSH Key
- Verified SSH Authentication
