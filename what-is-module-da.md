---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-15"

keywords: deployable architecture, deployment architecture, da, module, infrastructure as code, what is, stack, variation, projects

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# What are modules and deployable architectures?
{: #understand-module-da}

Creating secure, compliant, and scalable application infrastructure can be difficult to set up and costly to maintain. Instead of figuring out how to assemble a compliant infrastructure architecture on your own, you can take advantage of modules and deployable architectures. Modules and deployable architectures can help you to create a framework around how resources are deployed in your organization's accounts. By working with these reusable configurations, you can define the standard for deployment once and ensure that it is easily repeatable for each member of your organization.

For example, think about an architect who is building an apartment complex. These designs are typically executed in a modular way. There are patterns for standard one-bedroom, two, or three bedroom apartments. The builder can combine the standard apartments, each functional in their own way, into a larger, more complex, but functional living arrangement. IBM applied this same analogy to deploying solutions on the cloud. Rather than your organization spending months figuring out how to get services and software to work together, you can use IBM Cloud's well-architected patterns. Each pattern is packaged as composable, automated building bocks known as modules and deployable architectures. 


## What is a module?
{: #what-is-module}

A module is a stand-alone unit of automation code that can be reused by developers and shared as part of a larger system. Similar to Node.js or Python packages, modules are a convenience to developers who are managing related resources. While it is possible to use modules alone, they're more powerful when you combine them to build a deployable architecture. Modules that are created by IBM Cloud are made available in the IBM Cloud Terraform modules public GitHub repository. For example, the Red Hat OpenShift VPC cluster on IBM Cloud module installs and configures a Red Hat OpenShift cluster on IBM Cloud.


## What is a deployable architecture?
{: #what-is-da}

A deployable architecture is a cloud automation for deploying a common architectural pattern that combines one or more cloud resources. It is designed to provide simplified deployment by users, scalability, and modularity. Typically a deployable architecture incorporates one or more modules, but you can choose to build one entirely from scratch as well. Deployable architectures are coded in Terraform, which you configure with input variables to achieve the behavior that you want. 

For example, the VPC landing zone is a deployable architecture that provisions several virtual private clouds in a hub-and-spoke networking pattern that is connected by a transit gateway. It includes a number of supporting services that are used for the monitoring and security of the workloads that run on the VPCs. 

Deployable architectures that are built and maintained by experts at IBM Cloud are made available to you in the IBM Cloud catalog. If you choose to create your own version of those deployable architectures, or build one from scratch, you can onboard your deployable architecture to a private catalog and share your ready-to-deploy solution with your organization through the catalog.

A deployable architecture might include variations, have dependencies, be compatible with other architectures, or be stacked together to create more complex solutions. 

Variations
:  A variation is a type of deployable architecture that applies differing capabilities or complexity to an existing deployable architecture. For example, there might be a *Quick start* variation to your deployable architecture that has basic capabilities for simple, low-cost deployment to test internally. And, you might have a *Standard* variation that is a bit more complex that is ready for use in production.

Dependencies and compatibility
:   A deployable architecture is considered dependent upon another architecture when it has inputs that require the outputs from the other architecture to properly deploy. Similarly, compatible architectures are defined by the input and output variables. For example, if you want to use a deployable architecture that is compatible with a database that you've deployed, you can reference the deployed database from the deployable architecture.

[Experimental]{: tag-purple} Stacks 
:   A deployable architecture stack links together multiple architectures to create an end-to-end solution. This linking is achieved by specifying references in the configuration of each architectures inputs. You do not need to be an expert in Terraform, or have any Terraform coding skills, to create and deploy a stack. Deployable architecture stacks are created with IBM Cloud Projects and then can be shared with others through a private catalog. A stacked deployable architecture has independent configuration states for each of the architectures in the stack. This allows each component deployable architecture to be individually deployed, updated, or undeployed independently. The deployable architecture stack derives much of its cost, compliance, support, and quality assurances from its included deployable architectures. However, each stack is uniquely versioned and has its own descriptions and reference architecture. For example, the watsonx deployable architecture is assembled from three separate deployable architectures, including the Red Hat OpenShift secure landing zone. For more information, see [stacking deployable architectures](/docs/secure-enterprise?topic=secure-enterprise-config-stack&interface=cli).


## What are projects and how do they work with deployable architectures?
{: #what-are-projects}

An IBM Cloud project is a management tool that is designed to organize and provide visibility into a real-world project that exists in your organization. A project manages all of the configured instances of a deployable architecture and the resources that are related to the real-world reason that they are deployed. Projects store versioned deployable architecture instances and organize the instances and resources in to environments to help improve visibility into the development lifecycle. An environment is a group of related deployable architecture instances that share values for easier deployments. For example, development, test, or prod. 

Projects are responsible for ensuring that only approved deployable architectures can be deployed. Additionally, they can help to ensure that the architectures and the resources that they created are up-to-date, compliant, and that drift does not occur over time. For example, you might have an account management application project. This project is designed to manage all of the resources that the accounts management application needs to deploy into a development, test, or production environment. Each environment has the same variables, such as a region or prefix, but has different values. When a deployable architecture is assigned to an environment through a project, their input values can automatically reference any of the environment's properties that have the same name. While IBM Cloud projects are easy to create and update, they are not templatized or optimized for replication or sharing.

## How do I know which component to create?
{: #which-component}

| Purpose | Recommended component | Why? |
|:--------|:----------------------|:-----|
| Creating a library of sharable automation components | Module | Modules provide reusable, curated automation to speed up the process for those who are creating and configuring deployable architectures. |
| Ensuring that your organization's cloud environment is secure and compliant | Deployable architecture | Deployable architectures are packaged in a way that you can define a secure and compliant deployment once and ensure that all members of your organization are repeating the deployment in the same way. |
| Architecting your own solutions | Deployable architecture stack | By combining architectures, you can create a more complex end-to-end solution for your organization. |
{: caption="Table 1. Understanding for automated deployments use-cases" caption-side="top"}

