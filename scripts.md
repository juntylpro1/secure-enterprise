---

copyright:
  years: 2024
lastupdated: "2024-05-16"

keywords:

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Creating scripts for deployable architectures
{: #understand-scripts}

You can have scripts that are run for your deployable architectures before or after validating, deploying, and undeploying. Scripts are configured to a specific version of your deployable architecture, and must be run and validated through projects. For more information about projects, see [Creating a project](/docs/secure-enterprise?topic=secure-enterprise-setup-project&interface=ui).
{: shortdesc}

There are several benefits and use cases for using scripts for your deployable architectures:

* Performing custom validation, for example, if you want to ensure that the `tag` parameter is always a valid cost center ID. The pre-validation script might call out to a service to check that the cost center ID was valid.
* Tracking deployments and adding resources, for example, adding to an inventory system by providing a post-deployment script that can call out to a service to track which resources were deployed.
* Completing data migration. A pre-deployment script can back up data. Then, after the deployable architecture deletes the old data store and creates the new one, the post-deployement script can restore it to the new data store.
* Installing or configuring software
* Completing day two maintenance tasks such as manual backup, restore, or key rotations.

## Adding pre- and post-scripts
{: #creating-scripts}

Scripts are optional for an offering, but if they are used they are required to be in the source repository in a directory named `scripts`. The script files themselves must conform to the following naming convention `<action>-<stage>-ansible-playbook.yaml`. Options for `action` include `deploy`, `validate`, and `undeploy`. Options for `stage` include `pre` and `post`.

Only ansible scripts in the playbook format are currently supported.
{: important}

You must also reference your scripts in the `ibm_catalog.json` manifest file in your source repo. Provide the required information for your scripts per variation of your deployable architecture in the `scripts` array:

```json
"scripts": [
   {
      "type": "ansible",
      "short_description": "Short description of what your script is intended to do.",
      "path": "Path to script location.",
      "stage": "The stage. For example, pre.",
      "action": "The action. For example, validate."
   }
],
```
{: codeblock}

You can add this information to your catalog manifest file in the source repo before you onboard to {{site.data.keyword.cloud_notm}}, or you can manually add the scripts during the onboarding workflow in the console. If you manually add the scripts during onboarding, [download your manifest file](/docs/secure-enterprise?topic=secure-enterprise-onboard-da#download-manifest) and add it to your source repo to keep the information in sync for future versions.
{: tip}

All scripts must be able to run more than once without failing. For example, a pre-deployment or post-deployment script must operate correctly, even if it is run several times. Post-deployment scripts might add resources to a catalog management database and must be sure not to add duplicate resources if run more than once.

## Pre- and post-script examples
{: #script-examples}

The following is an example of a pre-script that is used to display a message after the deployable architecture is validated. Pre-scripts get passed to all of the inputs from the deployable architecture, including the credentials used to authorize deployment.

```python
- name: Validate pre playbook
  hosts: localhost
  vars:
    ibmcloud_api_key: "{{ lookup(`ansible.builtin.env`, `ibmcloud_api_key`)}}"
    cos_instance_name: "{{ lookup(`ansible.builtin.env`, `cos_instance_name`)}}"
    workspace_id: "{{ lookup(`ansible.builtin.env`, `workspace_id`)}}"
  tasks:
  - name: Print message
    ansible.builtin.debug:
      msg: "The workspace id is {{ workspace_id }}"
    when: workspace_id is defined and workspace_id != ""
  - name: Print message
    ansible.builtin.debug:
      msg: "The cos instance name is {{ cos_instance_name }}"
    when: cos_instance_name is defined
  - name: Print result
    ansible.builtin.debug:
      msg: "Received api key"
    when: ibmcloud_api_key is defined
```
{: codeblock}

The following is an example of a post-script. Post-scripts get passed to the outputs of the deployable architecture.

```python
- name: Deploy post playbook
  hosts: localhost
  vars:
    ibmcloud_api_key: "{{ lookup(`ansible.builtin.env`, `ibmcloud_api_key`)}}"
    git_repo_url: "{{ lookup(`ansible.builtin.env`, `git_repo_url`)}}"
  tasks:
   - name: Print result
     ansible.builtin.debug:
       msg: "Received api key"
     when: ibmcloud_api_key is defined
   - name: Print result
     ansible.builtin.debug:
       msg: "The result is: {{ git_repo_url }}"
     when: git_repo_url is defined and git_repo_url != ""
```
{: codeblock}
