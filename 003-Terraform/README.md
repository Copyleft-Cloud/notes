# Terraform
What is Terraform? https://www.terraform.io/

## Overview
Terraform is a tool for building, changing, and versioning infrastructure. We're going to use Terraform to integrate with service providers such as DigitalOcean and AWS to provision and manage our infrastructure as code.  

When thinking about Infrastructure as a Service (IaaS) and using Infrastructure as Code to achieve that objective we are concerned with thinking about the "Configuration" and "State" of the things we manage... how we use patterns... and the separation of roles (e.g. single role per node). And while we will often reuse patterns and roles to manage the “Configuration" in a consistent manner, we don't dare intermingle the "State" between devices.

So, when thinking about "Platform as a Service" (PaaS) and how best to implement we should approach it with a similar mindset as IaaS considering Configuration, State, and the Separation of Responsibility.

```
Configuration (noun)
an arrangement of elements in a particular form, figure, or combination.

State (noun)
the particular condition that someone or something is in at a specifc time.
```

## Goal
The goal with using Infrastructure as Code to implement IaaS and more broadly PaaS capabilities is to be objectively simple. As a team we'll want to avoid creating unnecessary and unintentional complexity by specifically focusing on how we use Patterns and Roles to manage Configuration and State in a variety of contexts.


#### What will make your day better?

- An objectively simple design that allows you to reason about the system and its moving parts.
- An implementation that provides you with flexibility while limiting risk from changes.
- A solution that delivers value today and continues to build momentum over the long haul.


### Some Good Practices
Here is a quick summary of some of the good practices we'll be following...

- (1) Managing "State" separately for every Environment
- (2) Implementing Modules for consistent "Configuration"
- (3) Keeping it real simple with "Patterns".


### Here is the short, short version of how it works in a nutshell...
- Configuration (.tf) files describe to Terraform the components needed to run a single application or your entire datacenter.
- Terraform generates an execution plan (terraform plan) describing what it will do to reach the desired state
- Terraform then executes the plan (terraform apply) to build the described infrastructure.
- As the configuration changes, Terraform is able to determine what has changed and create incremental execution plans which can then be applied.
