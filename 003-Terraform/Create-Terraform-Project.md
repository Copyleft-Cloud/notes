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


### STEP 6: Review Our Directory Structure
Per our good practices, we are wanting to manage configuration and state separately for each environment.  As we will be using both DigitalOcean and AWS as providers for environments, we'll set up our directory accordingly to separate contexts...

Thus, if we need to manage additional providers and subsequent environments, we have a neat and organized project.  Managing state (.tfstate) separately for each environment removes a substantial amount of risk and limits the blast radius of our infrastructure changes.  

Overview...
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
      operations.tf       # Operations Environment Terraform Plan
      operations.tfvars   # Operations Environment Variables
      secret.tfvars       # Symlinked from Global
      global.tfvars       # Symlinked from Global

  /provider-do            # DigitalOcean Provider
    /env-svc              # Service (SVC) Environment
      service.tf          # Service Environment Terraform Plan
      service.tfvars      # Service Environment Variables
      secret.tfvars       # Symlinked from Global
      global.tfvars       # Symlinked from Global

```

## Summary
