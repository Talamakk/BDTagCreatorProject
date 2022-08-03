# BDTagCreatorProject 

## Introduction and Demo
BDTagCreatorProject solution was developed to make easier organizing and identifying resources groups among Microsoft Azure subscription by tagging newly created resource group with creator's user name. Using different Azure tools (Azure Event Grid, Azure Functions) and PowerShell script enables to automate this task - [see All together - how does it work? section](all-together---how-does-it-work?) for detailed solution architecture.
This project was made mostly for cloud solutions training purposes so any feedback is more than welcome!

![Screen1](https://github.com/Talamakk/BDTagCreatorProject/blob/main/Images/CreatingRG.jpg)
## Solution concept 
Microsoft Azure has plenty of different tools we can use to automate tasks. This project was built using [Azure Event Grid](https://azure.microsoft.com/pl-pl/services/event-grid/) and [Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview).
### Azure Event Grid
This tool is designed for enabling creation of event-based solutions. It's main function is to monitor particular event sources and trigger the proper event handler if the event occurs. 
### Azure Functions
Azure Functions is the solution enabling serverless code execution and running apps in Azure cloud environment. 
### All together - how does it work?
Every time a new resource is created among the subscription, information about this event reaches the Azure Event Grid endpoint. After filtering events only related to creation of resource group, Event Grid routes these events directly to the proper event handler - function app. All event data and metadata are received by function inside of function app and are used to get necessary information: resource group URI and it's creator. Subsequently, the function updates newly created resource group with creator's user name. 
