# ARMLinked
Testing Linked Templates
- ARM Linked Templates
  - Linked Templates are a continuance of the main ARM Template

## collapsible markdown?

<details><summary>Summary</summary>
<br>Hello World!</br>
</details>

<details><summary>CLICK ME</summary>
<p>

#### yes, even hidden code blocks!

```python
print("hello world!")
```

</p>
</details>

```JSON
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "VNetName": {
            "type": "string",
            *"defaultValue": "VNetName",*
            "metadata": {
                "description": "VNet Name"
            }
        },
        "SubnetName": {
            "type": "string",
            "defaultValue": "SubnetName",
            "metadata": {
                "description": "description"
            }
        }
    },
    "functions": [],
    "variables": {},
    "resources": [
        {
            "name": "[parameters('VNetName')]" ,
            "type": "Microsoft.Network/virtualNetworks",
            "apiVersion": "2020-11-01",
            "location": "[resourceGroup().location]",
            "tags": {
                "displayName": "[parameters('VNetName')]"
            },
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "10.0.0.0/16"
                    ]
                },
                "subnets": [
                    {
                        "name": "[parameters('SubnetName')]",
                        "properties": {
                            "addressPrefix": "10.0.0.0/24"
                        }
                    }
                ]
            },
            "dependsOn": [
                "[resourceId('Microsoft.Resources/deployments', 'linkedDeployment1')]"
            ]
        },
        {
            "name": "linkedDeployment1",
            "type": "Microsoft.Resources/deployments",
            "apiVersion": "2021-04-01",
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "https://raw.githubusercontent.com/Matthew5689/ARMLinked/master/childTemplate.json",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {}
            }
        }
    ],
    "outputs": {}
}
```
