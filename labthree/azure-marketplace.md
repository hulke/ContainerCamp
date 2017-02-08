# A Shortcut - The Azure Marketplace
In this lab we are going to deploy the same resources that we deployed in Lab 1 and 2, but we are going to take advantage of the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/).  The Azure Marketplace contains pre-built and scripted solutions provided by Microsoft and partners.  Visit the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/) and take a look at some of the images that are offered.  

# Deploy a VM Running Docker and Nginx Container
For this example, we are going to go to the [Azure Portal](http://portal.azure.com).  Log into your Azure subscription and click the + sign in the upper left corner to add a new resource. In the blade that slides out you should see Marketplace, click the "see all" link.

![alt text][lab3img1]

[lab3img1]: ./Lab3-1.png " "

In the text box where it says "Search Everything," type "nginx" to see the different marketplace offerings.  One of the offers is published by Docker, select this offering.

![alt text][lab3img2]

[lab3img2]: ./Lab3-2.png " "

Once you click on the Docker Nginx image, a new blade will slide out to allow you to create the resources.  In the notes, is describes the resources that will be deployed (they should look familiar).  These resources have been highlighted in the image below.

![alt text][lab3img3]

[lab3img3]: ./Lab3-3.png " "

Click the Create button and follow the steps to deploy the image.  

This should create and deploy the Ubuntu image, install Docker, download the nginx image and start the container and setup up the port forwarding on port 80. To test, from your browser navigate to the url of your machine.

> http://DNS-LABLE-YOU-CREATED.eastus.cloudapp.azure.com

You should see the "Welcome to NGINX" default page.

## Delete the Resource Group ##
You can delete this resource group in one of two ways.  The same way we cleaned up in the previous lab:

    azure group delete {RESOURCE GROUP NAME} -q

Or, you can click on the resource group in the portal and click the Delete button there.  It will prompt you to type in the name of the resource group to validate that you are sure you want to delete all resources.

