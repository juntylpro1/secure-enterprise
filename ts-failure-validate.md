---

copyright:
  years: 2023
lastupdated: "2023-04-17"

keywords: troubleshoot projects, validate config, unable to validate your configuration, needs attention failure, validation failure, needs attention, failure, validation

subcollection: secure-enterprise

content-type: troubleshoot
---

{{site.data.keyword.attribute-definition-list}}

# Why can't I validate my configuration?
{: #ts-cant-validate}
{: troubleshoot}

You tried to validate changes to a configuration in a project, but an error prevented the validation from completing.
{: shortdesc}

You tried to validate changes to a configuration in a project, but the following error displays:
{: tsSymptoms}

> Unable to validate your configuration.

An availability issue occurred, which prevented validation.
{: tsCauses}

A service might have been down during the validation. Check the [Status page](/status){: external} for the service, and try to validate your configuration again when the service is back up.
{: tsResolve}

A timeout might have occurred during the validation, which caused a failure. Try validating your configuration again.

If the error message provides information about a `bad request` or `parameters`, you might need to edit your input values, then validate your configuration again.
