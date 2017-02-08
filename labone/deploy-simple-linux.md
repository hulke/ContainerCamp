# A Very Simple Deployment of a Linux VM #
Let's set the stage, we want to deploy a VM into Azure. This VM will be a basic install of Ubuntu 14.04 with docker. 

1. Browse the [Azure Quick Start Template Repo](https://github.com/Azure/azure-quickstart-templates)
	1. Yea there is a lot there...
2. Have a look at the [docker-simple-on-ubuntu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu) folder.
	1. There is a azuredeploy.json file. It descibes the resources we want to create. It also has parameters for things like username and password.
	2. There is a azuredeploy.parameters.json file that contains the parameters to pass to the template. Customers use multiple param files to create different environments like dev, test, prod. **We will not use this for the lab.**

In this template there is a resource called a VM extension. This extends our ability to deploy software or run scripts on the VM after it's created in Azure. There are many different VM extensions, but will be using the Docker VM Extension. The docker extension installs docker on the VM for us.

    {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "[concat(variables('vmName'),'/', variables('extensionName'))]",
      "apiVersion": "2015-05-01-preview",
      "location": "[resourceGroup().location]",
      "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
      ],
      "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.0",
    "autoUpgradeMinorVersion": true,
    "settings": { }
      }
    }

> This extensions supports docker-compose... we'll check that out later.

## Create Resource Group ##
A resource group is a grouping of Azure resouces that can be managed and secured as a single unit. Read "I can delete every resource in a resource group by deleting the resource group"... kind of scary.

**Create a resource group from the Azure-CLI:**

Note: The Azure CLI commands should be run from a **Command Prompt**

    azure group create {RESOURCE GROUP NAME} eastus

> Replace {RESOURCE GROUP NAME} with whatever you like. The "eastus" at the end is the data center location. There something like 22+ DCs now...

## Deploy the VM ##
Now it's time to create a VM... 

**Deploy an ARM Template using the Azure-CLI:**

    azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json

> Replace {RESOURCE GROUP NAME} with the resource group name you just created.

> Replace {DEPLOYMENT NAME} with whatever you like.

This command creates a deployment with the resource manager and passes the URI of the Linux template we just reviewed. It will also prompt you for the following parameters:

1. Username (don't use "admin")
2. Password (needs to be more than 8 chars and be complex)
3. DNS Label (this will be the dns prefix used to connect to the box)
4. Storage Account Name (blob storage for VM Disks)

## SSH to your new Linux Box ##
From the command line we'll ssh to the server, feel free to poke around once connected.

    ssh username@DNS-LABLE-YOU-CREATED.eastus.cloudapp.azure.com

> On Windows and need SSH? [Download Putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).
