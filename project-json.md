---

copyright:
  years: 2023
lastupdated: "2023-03-23"

subcollection: secure-enterprise

keywords: project json, project metadata, JSON config, project config, export JSON

---

{{site.data.keyword.attribute-definition-list}}


# Project JSON
{: #json-project}

Each configuration in a project is stored as a JSON file called the project.json. This allows for governance over configuration changes, for example, requiring approvals and ensuring that automated checks pass before changes are saved.

You can export and edit a project JSON to a public or private Git repository of your choice and push direct edits to the code. For more information, see [Exporting a JSON](/docs/secure-enterprise?topic=secure-enterprise-setup-project#json-export).

## Project.json
{: #project-json}

The project.json file has several parts:

* The project metadata which includes the name and description.
* An array of deployments that contains a reference to the deployable architecture and all of the input values.
* A dashboard configuration that contains metadata to configure the widgets on the project dashboard.

It's recommended to create your initial project.json from the [projects page](/projects) in the console. This provides an initial project.json file that can be edited. When you create a project in the console, the project.json is automatically created for you.

### Project metadata
{: #project-metadata}

Project's have user-defined name and descriptions that are stored in the project.json.

```json
  ...
  "name": "CRA Test",
  "description": "",
  ...
```

A project's ID (and CRN) are not stored in the project.json as they can't be edited by users. Instead, these are stored by {{site.data.keyword.cloud_notm}}. Also, tags on the project instance itself are stored in ghost. User-controlled tags that a project wants to apply to deployed resources are stored in the project metadata.

### Configurations
{: #project-config-json}

Each configuration in a project has an object in the configs array. Each deployment object has a name, an array of inputs, a type, and if the type is an IaC template, then a template object with a catalog "locator_id".

```json
...
"configs": [
    {
      "name": "my-deployment",
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
      "type": "terraform_template",
      "template": {
        "locator_id": "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.feb66dbc-9af3-4dc6-a8a1-3d617e863194-global"
      }
   ]
...
```

### Dashboard
{: #project-dash}

The project.json also includes a dashboard section. The dashboard section will be used in the future to allow the project dashboard to be configured, but is currently ignored.

```json
  ...
  "dashboard": {
    "description": "",
    "widgets": []
  }
  ...
```
