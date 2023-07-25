---

copyright:
  years:  2023
lastupdated: "2023-07-25"

keywords: change log for Projects, updates to Projects

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Projects API change log
{: #projects-api-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the [Projects API](/apidocs/projects). The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

<!-- Always include a link to the task-based docs that guide users through making updates to their code for the related changes.
For instructions on how to update to the latest version of this API, see [Updating to the latest version of the _service_ API](/docs/url).

<!-- If you have SDKs, mention that their change logs are in a separate location and provide links
For information about the latest changes to the `<service name>` SDKs, see the change logs in the SDK repositories:
- [Java SDK change log](https://github.com/IBM/<service-java-sdk>/blob/main/CHANGELOG.md)
- [Node SDK change log](https://github.com/IBM/<service-node-sdk>/blob/main/CHANGELOG.md)
- [Python SDK change log](https://github.com/IBM/<service-python-sdk>/blob/main/CHANGELOG.md)
- [Go SDK change log](https://github.com/IBM/<service-go-sdk>/blob/main/CHANGELOG.md)
-->
<!--
## API versioning
{: #projects-api-versioning}

<!-- Include information about how your API is versioned, with version numbers or date-based versions. The following example uses date-based versioning. -->
<!--API requests require a version parameter that takes the date in the format `version=YYYY-MM-DD`. Send the version parameter with every API request.

When the API is changed in a way that is not compatible with previous versions, a new minor version is released. To take advantage of the changes in a new version, change the value of the version parameter to the new date. If you're not ready to update to that version, don't change your version date. -->

<!-- If your API has multiple active versions, include a table that lists the versions along with information about what changes are included with each version. -->
<!--### Active version dates
{: #active-version-dates}

The following table shows the service behavior changes for each version date. Switching to a later version date will activate all changes introduced in earlier versions.

| Version date | Summary of changes |
|---|---|
|`2021-07-04`| New English entities model with improved accuracy and confidence scores.|
|`2021-02-14`| Version 2 Italian entity type system. |
|`2020-12-25`| Version 2 French and German entity type system. |
|`2020-10-31`| Base version.|

<!-- Organize the content of the change log in a list of H2 (##) headings, titled with the date of the changes in the format DD Month YYYY -->

## 06 July 2023
{: #06-jul-2023}

The response models for all methods now enforce a lower snake case format in `state` values. This format is to be expected in the response when you are calling the project and configuration endpoints. This update is a breaking change.
{: important}

Project `state` values can now be `ready`, `deleting`, and `deleting_failed`. For an example, see [the response schema for the `update-project` method](/apidocs/projects#update-project).

Configuration `state` values can now be `deleted`, `deleting`, `deleting_failed`, `installed`, `installed_failed`, `installing`, `not_installed`, `uninstalling`, `uninstalling_failed`, and `active`. For an example, see [the response schema for the `get-config` method](/apidocs/projects#get-config).
