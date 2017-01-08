# Create Terraform Project

### STEP 1: Check Out The Documentation
Terraform has great documentation.  Do yourself a solid and read through their docs.

- Intro ( https://www.terraform.io/intro/index.html )
- Docs ( https://www.terraform.io/docs/index.html )

### STEP 2: Download Terraform
- Go To https://www.terraform.io/downloads.html
- Select the correct download for your OS
- Terraform is a binary file
- After you download it
  - Place the terraform binary in a directory of your choice
  - `(e.g. /Users/<username>/.terraform/terraform)`
  - Add it to your PATH environment variable

### STEP 3: Confirm Terraform is Installed
Open a terminal and check the version...
```
terraform --version
Terraform v0.8.2
```

Sweet!  Terraform is installed.  When need to upgrade to the newest version, simply download the latest binary and swap it out with the current binary.


## Next Steps
- We're going to setup our Terraform Project Directory.
- We're going to discuss some best practices and get hands-on.


### STEP 4: Create New Github Repository
Let's go ahead create our Git Repository on GitHub
- Repository Name: terraform
- Public: Yes
- Initialize README (YES)
- Add Write Permissions to for our Engineers


### STEP 5: Clone New Git Repo
Let's clone the new repo to our local workstation
```
cd /Users/<username>/Github/copyleft-cloud
git clone git@github.com:Copyleft-Cloud/terraform.git
```

### STEP 6: Overview Our Project Directory

The Big Picture...
```
/
  /global
    secret.tfvars         # Keys, Credentials, etc
    global.tfvars         # Global Variables

  /modules                # Modules Directory
    /aws                  # AWS Modules
    /do                   # DigitalOcean Modules

  /provider-aws           # AWS Provider
    /env-ops              # Operations (OPS) Environment
      device-<role1>.tf   # Device (e.g. EC2 Instance)
      device-<role2>.tf   # Device (e.g. EC2 Instance)
      device-<role3>.tf   # Device (e.g. EC2 Instance)
      network.tf          # Network (e.g. VPC, Subnets, Gateways, Routes)
      security.tf         # Security (e.g. Security Groups)
      operations.tfvars   # Operations Environment Variables
      secret.tfvars       # Symlinked from Global
      global.tfvars       # Symlinked from Global

  /provider-do            # DigitalOcean Provider
    /env-svc              # Service (SVC) Environment
      device-<role1>.tf   # Device (e.g. Droplet Instance)
      device-<role2>.tf   # Device (e.g. Droplet Instance)
      device-<role3>.tf   # Device (e.g. Droplet Instance)    
      network.tf          # Network (e.g. Private Network, DNS, IPs)
      service.tfvars      # Service Environment Variables
      secret.tfvars       # Symlinked from Global
      global.tfvars       # Symlinked from Global

```

Per our good practices, we are wanting to manage configuration and state separately for each environment as well as provider.  As we will be using both DigitalOcean and AWS as Cloud Hosting providers for our operations and execution environments, we'll set up our directory accordingly to separate these contexts.

Thus, if we need to manage additional providers and subsequent environments, we have a neat and organized project directory where we can manage those artifacts.  Here are a few good tips that we've implemented based on our experience...

#### TIP 1: Limit the Blast Radius
Managing state (.tfstate) separately for each environment removes a substantial amount of risk and limits the blast radius of our infrastructure changes.  As you can see above we are doing this by provider (AWS, DO) and by environment.

#### TIP 2: Separate your Concerns
Note that within each environment we are separating our concerns (e.g. Devices, Network, Security, etc) so that it is more straightforward to develop and maintain our code base.

When implementing infrastructure as code... code commits and pull requests will most likely become real changes to your platform.  Make it as simple as possible for yourself and your team to reason about your platform, identify and manage the risk of  those changes.

#### TIP 3: Symlink Global Files
Note that we've symlinked a few files (.tfvars) from a global directory down into our specific provider environments... this allows us to use global variables in addition to the local variable files (.tfvars) per environment.  This helps to keep our terraform project DRY (don't repeat yourself) and can help with reusability and consistency across contexts.

#### TIP 4: Modules for Consistency across Environments
Note that we've got a modules directory. This is where we will create some reusable modules that we can leverage for consistency across environments for a provider. This helps to keep our terraform project DRY (don't repeat yourself) and can help with reusability and consistency across environments.


### STEP 7: Create New Github Repository
Let's go ahead create our Git Repository on GitHub
- Repository Name: terraform
- Public: Yes
- Initialize README: Yes
- Add Write Permissions to for our Engineers

### STEP 8: Clone New Git Repo
Let's clone the new repo to our local workstation
```
cd /Users/<username>/Github/copyleft-cloud
git clone git@github.com:Copyleft-Cloud/terraform.git

```

### STEP 9: Initial Project Directory

Create our Base Folder Structure to start...
```
cd /Users/<username>/Github/copyleft-cloud/terraform
mkdir global modules provider-aws provider-do
```

Create our .gitignore File
```
# SECRET VARS (do not push to git)
# Includes Credentials, Private Keys
global/secret.tfvars

# Do not Push .terraform modules
*/.terraform

```

Create /terraform/global/secret.tfvars
```
# SECRET VARIABLES (do not push to git)
# ADD TO .gitignore

# AMAZON WEB SERVICES (AWS)
aws_account_id = "<AWS Account ID>"
aws_access_key = "<AWS Access Key>"
aws_secret_key = "<AWS Secret Key>"

# DIGITAL OCEAN (DO)
do_api_token = "<DigitalOcean API Token>"
```

### STEP 10: Push an Initial Commit to Github
Following our successful test, let's push our initial commit to our Git Repository on Github.  

Friendly reminder, be sure that you have your .gitignore file in place and saved.  Double check the git status to ensure that you are not committing and pushing your secret.tfvars (with your private keys) up to Github.

```
git status
git add .
git commit -m "Initial Commit"
git push -u origin master
git status

```


## Summary
Ok, we're ready to start working with Terraform. As we roll up our sleeves and get to work, we'll be covering more topics in depth as we go with each provider and solution we develop.  At this point we have accomplished the following...

- We've installed the terraform binary
- We've reviewed our project directory
- We've reviewed a few good practices
- We've setup our initial project directory and a few files

The next step is to start working with a provider such as AWS and DigitalOcean to provision our infrastructure!
