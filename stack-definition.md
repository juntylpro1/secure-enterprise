---

copyright:
  years: 2022, 2024
lastupdated: "2024-03-29"

keywords: onboard, catalog management, private catalog, stack definition, software, automation, metadata

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Locally editing the stack definition
{: #stack-definition}

The stack definition file specifies the information about how the deployable architctures that are grouped together in a stack are supposed to relate to each other. For example, which inputs and outputs are used.
{: shortdesc}


## Editing your definition
{: #edit-stack-definition}

To edit your stack definition locally, you can use the following steps.

1. Create your deployable architecture stack by using the projects UI.
2. Open the `stack_definition.json` file.
2. Using the example definition as a guide, edit the input and output variables. 
3. Add the file into the root folder of your source code repository.

The next time you add a new version of your stacked deployable architecture to the catalog, your updates will be included.


## Example definition file
{: #example-definition}

The following code snippet can be used as a template.

```json
{
   "inputs": [
      {
         "name": "Stack input 1",
         "type": "string",
         "hidden": false,
         "required": true,
         "default" : "Default value"
      },
      {
         "name": "Stack input 2",
         "type": "string",
         "hidden": false,
         "required": true
      }
   ],
   "outputs": [
      {
         "name": "Output 1 name",
         "value": "The reference to this output value"
      },
      {
         "name": "Output 2 name",
         "value": "The reference to this output value"
      }
   ],
   "members": [
      {
         "Name": "Deployable architecture 1 name",
         "Version_locator": "",
         "inputs": [
            {
               "name": "Input 1 name",
               "value": "reference"
            },
            {
               "name": "Input 2 name",
               "value": "reference"
            }
         ]
      },
      {
         "Name": "Deployable architecture 2 name",
         "Version_locator": "",
         "inputs": [
            {
               "name": "Input 1 name",
               "value": "reference"
            },
            {
               "name": "Input 2 name",
               "value": "reference"
            }
         ]
      }
   ]
}
```
{: codeblock}



## Stack inputs
{: #value-stack-inputs}

The `inputs` value indicates an array of the input variables required for the stack to successfully deploy. The following values can be included at the `inputs` level.

```json
"inputs": [
   {
      "name": "Stack input 1",
      "type": "string",
      "hidden": false,
      "required": true,
      "default" : "Default value"
   },
   {
      "name": "Stack input 2",
      "type": "string",
      "hidden": false,
      "required": true
   }
]
```
{: codeblock}

name
:   The name of your input variable.

type
:   HOW TO DESCRIBE?

hidden
:   A boolean that indicates if the parameter should be hidden from users during installation.

required
:   A boolean that indicates if users are required to specify the parameter during installation.

default
:   The default value that should be set in the catalog.


## Stack outputs
{: #value-stack-inputs}

The `outputs` value indicates an array of the output variables required for the stack to successfully deploy. The following values can be included at the `outputs` level.

```json
"outputs": [
   {
      "name": "Output 1 name",
      "value": "The reference to this output value"
   },
   {
      "name": "Output 2 name",
      "value": "The reference to this output value"
   }
]
```
{: codeblock}


name
:   The name of your output variable.

value
:   The reference to where the value can be found. For more information about references, see [Referencing values](/docs/secure-enterprise?topic=secure-enterprise-config-project#reference-values).


## Member inputs
{: #value-stack-inputs}


The `members` value indicates an array of the inputs and outputs for each deployable architecture in the stack. The following values can be included at the `members` level.

```json
"members": [
   {
      "Name": "Deployable architecture 1 name",
      "Version_locator": "",
      "inputs": [
         {
            "name": "Input 1 name",
            "value": "reference"
         },
         {
            "name": "Input 2 name",
            "value": "reference"
         }
      ]
   }
]
```
{: codeblock}


`name`
:   The programatic name of the deployable architecture included in the stack.

`version_locator`
:   WHERE CAN SOMEONE FIND THIS? BRIAN / KEITH

`inputs`
:   HOW TO DESCRIBE?

   `name`:
   :   HOW TO DESCRIBE?

   `value`:
   :   HOW TO DESCRIBE?




