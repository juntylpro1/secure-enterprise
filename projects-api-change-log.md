---

copyright:
  years:  2023
lastupdated: "2023-11-06"

keywords: change log for Projects API, updates to Projects API, Projects API

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Projects API change log
{: #projects-api-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the [Projects API](/apidocs/projects). The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## 06 November 2023
{: #06-nov-2023}

The latest updates include the following breaking changes:
* The `pipeline_state` is now retired from the `configurations` `response` model. All status information of a `configuration` is available in the augmented `state` property in the canonical schema of a `configuration`.

### Projects and configurations changes
{: #projects-and-configs}

`create-project: POST /v1/projects`
* The `resource_group` and `location` are now to be embedded in the `request` payload. They are no longer supported as query parameters.

`delete-config: PATCH /v1/projects/{project_id}/configs/{id}`
* The `draft_only` query parameter is deprecated.
* The API now supports delete of `configuration` of a specified project ID and `version`.
    * See [projects#delete-config-version](/apidocs/projects#delete-config-version).

### Renamed configuration endpoints
{: #renamed-config-endpoints}

* `POST /v1/projects/{project_id}/configs/{id}/check` -> `POST /v1/projects/{project_id}/configs/{id}/validate`.
* `POST /v1/projects/{project_id}/configs/{id}/install` -> `POST /v1/projects/{project_id}/configs/{id}/deploy`.
* `POST /v1/projects/{project_id}/configs/{id}/uninstall` -> `POST /v1/projects/{project_id}/configs/{id}/undeploy`.

### Replaced configuration endpoints
{: #replaced-config-endpoints}

* The `drafts` methods were replaced by the `versions` operations.
    * `GET /v1/projects/{project_id}/configs/{config_id}/drafts` -> `GET /v1/projects/{project_id}/configs/{id}/versions`.
    * `GET /v1/projects/{project_id}/configs/{config_id}/drafts/{version}` -> `GET /v1/projects/{project_id}/configs/{id}/versions/{version}`

### Configuration states
{: #config-states}

* The state model for `configurations` has been flattened.
* Effectively the `pipeline_state` is no longer available and the one `state` property is now augmented to capture all possible status of a `configuration`.
* The new `state` values are `approved`, `deleted`, `deleting`, `deleting_failed`, `discarded`, `deployed`, `deploying_failed`, `deploying`, `superceded`, `undeploying`, `undeploying_failed`, `validated`, `validating`, `validating_failed`
* All `configuration` endpoints include this `state` property in the `response` model. For an example, see [projects#get-config-version-response](/apidocs/projects#get-config-version-response).

### Configuration new metadata
{: #config-new-metadata}

The `response` model of `configurations` operations now defines new metadata in the root.

If an `approve` job was run on a `configuration`, an `approved_version` property is included in the `response` payload.

Similarly, if a `deploy` job was run on a `configuration`, a `deployed_version` and `last_deployed` metadata are available in the `response` body.

Running a `validation` job yields the metadata `last_validated`, while running an `undeploy` job yields the metadata `last_undeployed` in the `response`.

## 26 October 2023
{: #26-oct-2023}

In `projects` and `configurations` operations, such as `create` and `update`, definition properties such as `name` and `description` must now be provided in a `definition` wrapper. Similarly, these properties are now only available inside a `definition` block in the `response` payload of `create`, `update`, `get`, and `list` operations. This is a breaking change that was originally released on 06 July 2023. The following sections provide more information about the methods that are affected by this update. 

### Projects
{: #projects}

`create-project: POST /v1/projects`
* For both the `request` & `response`, the `name`, `description`, and `destroy_on_delete` are now wrapped inside a `definition` object.
* Callers of this endpoint are now expected to supply the definition properties inside this wrapper, for example: 
    * `definition: {“name”: “test”, “description”: “This is a test project”, “destroy_on_delete”: false}`.
        * If `destroy_on_delete` is not provided, a default value of `true` is assigned on a project create operation.
    * See [projects#create-project-request](/apidocs/projects#create-project-request).
* Similarly, in the `response` body, the previously mentioned properties are now available in a `definition` block.
    * See [projects#create-project-response](/apidocs/projects#create-project-response).

`update-project: PATCH /v1/projects/{id}`
* For both the `request` & `response`, the `name`, `description`, and `destroy_on_delete` are now wrapped inside a `definition` object.
* Callers of this endpoint are now expected to supply the definition properties inside this wrapper, for example: 
    * `definition: {“name”: “test_update”, “description”: “This is an updated test project“}`.
    * See [projects#update-project-request](/apidocs/projects#update-project-request).
* Similarly, in the `response` body, the previously mentioned properties are now available in a `definition` block.
    * See [projects#update-project-response](/apidocs/projects#update-project-response).

`get-projects: GET /v1/projects/{id}`
* In the `response` of this operation, the `name`, `description`, and `destroy_on_delete` are now wrapped inside a `definition` block.
    * See [projects#get-project-response](/apidocs/projects#get-project-response).

`list-project: GET /v1/projects`
* Each project that is returned in the `response` array wraps the `name`, `description`, and `destroy_on_delete` properties in a `definition` block.
    * See [projects#list-projects-response](/apidocs/projects#list-projects-response).

### Configurations
{: #configurations}

`create-config: POST /v1/projects/{project_id}/configs`
* For both `request` & `response`, the `locator_id`, `name`, `labels`, `authorizations`, `compliance_profile`, `input`, `setting`, `description` are now wrapped inside a `definition` object.
* Callers of this endpoint are now expected to supply the definition properties inside this wrapper, for example: 
    * `definition: {“name”: “test”, “description”: “This is a test config”, “locator_id”: “1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.cd596f95-95a2-4f21-9b84-477f21fd1e95-global”}`.
    * See [projects#create-config-request](/apidocs/projects#create-config-request).
* Similarly, in the `response` body, the previously mentioned properties are now available in a `definition` block.
    * A `setting` property is also included in the `definition` block.
    * See [projects#create-config-response](/apidocs/projects#create-config-response).

`update-config: PATCH /v1/projects/{project_id}/configs/{id}`
* For both `request` & `response`, the `locator_id`, `name`, `labels`, `authorizations`, `compliance_profile`, `input`, `setting`, `description` are now wrapped inside a `definition` object.
* Callers of this endpoint are now expected to supply the definition properties inside this wrapper, for example: 
    * `definition: {“name”: “test”, “description”: “This is a test config”, “locator_id”: “1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.cd596f95-95a2-4f21-9b84-477f21fd1e95-global”}`.
    * See [projects#update-config-request](/apidocs/projects#update-config-request).
* Similarly, in the `response` body the previously mentioned properties are moved into a `definition` block.
    * See [projects#update-config-response](/apidocs/projects#update-config-response).

`get-config: GET /v1/projects/{id}`
* In the `response` of this operation, the `locator_id`, `name`, `labels`, `authorizations`, `compliance_profile`, `input`, `setting`, `description`, and `setting` are now wrapped inside a `definition` object.
    * See [projects#get-config-response](/apidocs/projects#get-config-response).

`list-configs: GET /v1/projects/{project_id}/configs`
* In the `response` of this operation, the `name` and `description` are now wrapped inside a `definition` object.
    * See [projects#list-configs-response](/apidocs/projects#list-configs-response).

## 06 July 2023
{: #06-jul-2023}

The response models for all methods now enforce a lower snake case format in `state` values. This format is to be expected in the response when you are calling the project and configuration endpoints. This update is a breaking change.
{: important}

Project `state` values can now be `ready`, `deleting`, and `deleting_failed`. For an example, see [the response schema for the `update-project` method](/apidocs/projects#update-project).

Configuration `state` values can now be `deleted`, `deleting`, `deleting_failed`, `installed`, `installed_failed`, `installing`, `not_installed`, `uninstalling`, `uninstalling_failed`, and `active`. For an example, see [the response schema for the `get-config` method](/apidocs/projects#get-config).
