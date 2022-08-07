# BDTagCreatorProject 

## Introduction and Demo
BDTagCreatorProject solution was developed to make easier organizing and identifying resources groups among Microsoft Azure subscription by tagging newly created resource group with creator's user name. Azure Event Grid, Azure Functions and PowerShell script enable to automate this task - see [How does it work?](how-does-it-work?) section for detailed solution architecture.
This project was made mostly for cloud solutions training purposes so any feedback is more than welcome!
<img src="https://github.com/Talamakk/BDTagCreatorProject/blob/main/Images/CreatingRG.jpg" width="500">  

## Solution concept 
Microsoft Azure has plenty of different tools we can use to automate tasks. This project was built using [Azure Event Grid](https://azure.microsoft.com/pl-pl/services/event-grid/) and [Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview).
### Azure Event Grid
This tool is designed for enabling creation of event-based solutions. It's main function is to monitor particular event sources and trigger the proper event handler if the event occurs. 
### Azure Functions
Azure Functions is the solution enabling serverless code execution and running apps in Azure cloud environment. 
### How does it work?
Every time a new resource is created among the subscription, information about this event reaches the Azure Event Grid endpoint. After filtering events only related to creation of resource group, Event Grid routes these events directly to the proper event handler - function app. All event data and metadata are received by the function inside of the function app and are used to get necessary information: resource group URI and it's creator. Subsequently, the function updates newly created resource group with creator's user name using the `Update-AzTag` cmdlet.  
![Screen2](https://github.com/Talamakk/BDTagCreatorProject/blob/main/Images/DIAGRAM1.jpg)

## Implementation step by step
1. Create separate resource group in order to have all resources related to this solution in one place
2. Create new Function App within created resource group and uncomment "Az" line in requirements in order to enable using Az Powershell module
![Screen3](https://github.com/Talamakk/BDTagCreatorProject/blob/main/Images/SBS1.jpg)
3. Enable the access to tags for Function App by configuring system assigned managed identity for it and assign it a proper role, eg. Tag Contributor
![Screen4](https://github.com/Talamakk/BDTagCreatorProject/blob/main/Images/SBS2.jpg)
4. Create a new function triggered by Azure Event Grid within your Function App and paste code from *BDTagCreatorFunction.ps1* file
5. Create a new event subsciption within you resource group and select event types to filter (*Resource Write Success* only) and endpoint type - previously created function 
![Screen5](https://github.com/Talamakk/BDTagCreatorProject/blob/main/Images/SBS3.jpg)


Thanks to JSON 


