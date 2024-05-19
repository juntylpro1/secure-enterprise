---

copyright:
   years: 2024
lastupdated: "2024-05-17"

keywords:

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# How do I decide what kind of component to create?
{: #choose-plan-process}

How do you decide whether you should be creating a module, a deployable architecture, or a deployable architecture stack? Let's compare the differences and evaluate the use cases in the following sections to help you decide.
{: shortdesc}


## Comparing deployable architectures and modules
{: #compare-options}

The following table provides a comparison and quick summary of the key differences between modules and types of deployable architectures.

|    | Scope | Coupling | Deployable | Author |
|----|-------|----------|------------|--------|
| Module | Narrow | Tight | No | Developer |
| Deployable architecture | Medium to broad | Tight | Yes | Developer |
| Deployable architecture stack | Broad | Loose | Yes | Anyone |
{: row-headers}
{: caption="Table 1. Comparison of concepts" caption-side="bottom"}


The following table can help you decide whether to use a module, a deployable architecture, or a deployable architecture stack depending on your use case.

| Purpose | Recommended component | Notes |
|----|-------|----------|
| Accelerate coding automation | Modules | Modules provide reusable, curated automation to get developers of deployable architectures coding faster. Modules are for developers, not consumers. |
| Ensure that the cloud is secure and compliant | Deployable architecture | Deployable architectures enforce security and compliance for an architecture. If a deployable architecture is too small in scope, it cannot enforce compliance. For example, a deployable architecture that deploys only a virtual server instance can't ensure network security. |
| Give users a choice with guardrails | Stacked deployable architecture | With stacked deployable architectures, you can swap deployable architectures or add on deployable architectures and give users more choices. Since deployable architectures enforce security and compliance, stacking helps ensure the overall solution remains compliant. Stacked deployable architectures are excellent for things like selecting which database to use. |
| User-created solutions or architectures | Stacked deployable architectures | Stacked deployable architectures allow users to create and publish their own repeatable patterns that are still safe, as they are composed of secure and compliant deployable architectures. |
| Decoupled architecture components | Stacked deployable architectures | Deployable architectures can be independently developed and versioned, but then combined into a stacked deployable architecture for deployment. |
| Simplified user experience | Deployable architecture | Deployable architectures can provide a small or simple list of inputs to the user even for large or complex architectures. Deployable architectures are simple to understand and deploy. In comparison, stacking deployable architectures is a little more complex as the deployable architectures are exposed. |
{: caption="Table 2. Help me choose the component to use" caption-side="bottom"}

[{{site.data.keyword.cloud_notm}} projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects) ensure that resources are deployed through deployable architectures from the catalog and operate within the security and compliance guardrails of the organization. They also ensure that these resources are kept up to date and do not drift.

## Terraform versus Ansible
{: #terraform-ansible}

In {{site.data.keyword.cloud_notm}}, a deployable architecture must use Terraform to declare the inputs and outputs of the deployable architecture (the interface) as Ansible does not have a machine-readable interface definition. Otherwise, the author of a deployable architecture might use any combination of Ansible pre- or post-scripts and Terraform to run the work of the deployable architecture. So, how does a developer decide which technology to use and for what?

|    | Terraform | Ansible |
|----|-------|----------|
| Language | Declarative | Procedural |
| Syntax | HCL (similar to JSON) | YAML (and callouts to other scripts) |
| Default approach | Mutable infrastructure | Immutable infrastructure |
| Focus | Infrastructure | Configuration |
| Drift | Comparison with wanted state | Idempotent tasks |
{: row-headers}
{: caption="Table 3. Comparison of configuration languages" caption-side="bottom"}
{: summary="The first column are categories used to compare Terraform and Ansible. The second column provides information about how Terraform relates to the set category in column one and the third column provides information about how Ansible relates to the set category in column one."}

Terraform is excellent at creating and managing infrastructure, whereas Ansible is excellent at configuring the software and operating systems that are running on that infrastructure. Because Ansible is procedural, you can also script one-time operations. Maintenance tasks, like restoring from backup, are easy in Ansible.

| Purpose| Recommended configuration language | Notes |
|----|-------|----------|
| Deploy cloud infrastructure or services | Terraform | Terraform targets this use case and is better at handling changing infrastructure. {{site.data.keyword.cloud_notm}} provides Terraform modules and supported deployable architectures to accelerate secure and compliant infrastructure patterns. The Terraform state model allows developers to preview the changes. Those changes can be scanned for compliance. |
| Install or configure software | Ansible | If a pre-built container or virtual machine image is not suitable for the use case, Ansible is better at handling the software installation and configuration. Ansible has extensive support for automated operations such as configuration edits, package management, and process restarts. A large library of Ansible modules and playbooks are available to ease the configuration of thousands of commonly used software packages. |
| CCDB integration | Ansible | Making a dynamic call to an on-premises service like a CCDB can be done in Terraform or Ansible but is easier to accomplish in a procedural or scripting language. |
| Input validation | Terraform or Ansible | Terraform has limited ability to do input validation, but it is declarative and can be used by user interfaces. Ansible adds the ability to do dynamic input validation where inputs to a deployable architecture are checked against a remote service. |
| Day 2 maintenance actions | Ansible | Day 2 maintenance is generally procedural in nature and best completed in Ansible. Examples include manual backup, restore, or key rotations. |
| Drift management | * Terraform \n * Ansible | * Terraform can be used to determine whether drift occurred and what that drift is, which can help you decide how to manage the drift. The drift information is powerful because it might indicate that you can add a change to automation. \n * Ansible can't detect drift. But by regularly reapplying an idempotent ansible script, you can prevent drift. |
{: caption="Table 4. Help me choose the configuration language to use" caption-side="bottom"}

For more information about including pre- or post-scripts with your deployable architectures, see [Creating scripts for deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-understand-scripts).


## Next steps: Deciding where to publish
{: #decide-next-steps}

After you've planned out your architecture and decided what type of component to create, you should [consider where you plan to share or publish](/docs/secure-enterprise?topic=secure-enterprise-publish-da-options&interface=ui) your solution, so that other users can take advantage of the solution that you create. Depending on where you plan to share or publish, you might have different levels of requirements or approvals to complete.
