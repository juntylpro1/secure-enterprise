---

copyright:
  years: 2023
lastupdated: "2023-04-18"

subcollection: secure-enterprise

keywords: project json, project metadata, JSON config, project config, export JSON

---

{{site.data.keyword.attribute-definition-list}}


# Project JSON
{: #json-project}

Each configuration in a project is stored as JSON in a file called `project.json`. Projects require governance over configuration changes that are stored in `project.json`, for example, requiring approvals and ensuring that automated checks pass before changes are saved.

You can export and edit a project JSON to a public or private Git repository of your choice and push direct edits to the code. For more information, see [Exporting a JSON](/docs/secure-enterprise?topic=secure-enterprise-setup-project#json-export).

## What's in my Project.json file?
{: #project-json}

The `project.json` file has several parts:

* The project ID and description, which are user-defined values.
* The project metadata, which includes project CRN, location, resource group, and state.
* An array of configuratons that contains a reference to the deployable architecture and all of the input values.

It's recommended to create your initial `project.json` from the [Projects page](/projects) in the console. This provides an initial `project.json` file that can be edited. When you create a project in the console, the `project.json` is automatically created for you.

### Project metadata
{: #project-metadata}

Project metadata might contain `cumulative_needs_attention_view`, if there are events that have happened related to the project that the user must now take action on. `event_notifications_crn` is also an optional value, if the project is configured as a source for {{site.data.keyword.en_short}}. For more information, see [Enabling event notifications for projects](/docs/secure-enterprise?topic=secure-enterprise-event-notifications-events&interface=ui).

```json
  ...
  "id": "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
  "name": "CRA Test",
  "description": "",
  "metadata": {
    "crn": "crn:v1:staging:public:project:us-south:a/<account_id>:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "location": "us-south",
    "resource_group": "Default",
    "state": "READY",
    "cumulative_needs_attention_view": [
      {
        "event": "config.defn.update"
      },
      {
        "event_id": "489f0090-6d7c-4af5-8f20-9106543e4974"
      },
      {
        "config_id": "069ab83e-5016-4bf2-bd50-cc95cf678293"
      },
      {
        "config_version": 1
      }
    ],
    "event_notifications_crn": "crn:v1:staging:public:event-notifications:us-south:a/<account_id>:instance-id::"
  }
  ...
```

A project's ID and CRN can't be editied and are stored by {{site.data.keyword.cloud_notm}}. Also, tags on the project instance itself are stored in global search and tagging.

### Configurations
{: #project-config-json}

Each validated and approved configuration in a project has an object in the configs array. Each configuration object has a name, an array of inputs, and a type. If the type is an IaC template, then a catalog `locator_id` is included.

```json
...
"configs": [
    {
      "id": "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "name": "my-deployment",
      "description": "A microservice to deploy on top of ACME infrastructure.",
      "locator_id": "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
      "type": "terraform_template",
      "input": [
        {
          "name": "cos_bucket_name",
          "type": "string",
          "required": true,
          "default": "sample-cos-bucket",
          "value": ""
        },
        {
          "name": "ibmcloud_api_key",
          "type": "password",
          "required": true,
          "default": "__NOT_SET__",
          "value": ""
        },
      ],
      "output": [
        {
          "name": "resource_group_id"
        },
        {
          "name": "logdna_id"
        }
      ]
   ]
...
```
