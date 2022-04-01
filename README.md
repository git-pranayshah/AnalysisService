# Microsoft Azure Analysis Services with Sample Data on Azure SQL
Microsoft Analysis Services is a Platform As a Service (PaaS) service within Microsoft Azure under Business Intelligence umbrella. It brings Build rich semantic models with the capability of gaining insight at the speed of thought. It’s a proven technology on cloud with capability of provisioning and scaling with ease. There are two options to start play around with the Analysis services. 

1.  Create Sample Model directly in the Service
2.  Create Azure SQL with Sample Data and build the model from scratch with that data 

We will going to see both the options with this ARM template so that you can kickstart deploying & playing with the service with Sample (Sales Data) data.

# Azure Analysis Service with Azure SQL Landing Zone

To work with Azure SQL we need landing zone template having Azure Vnet, Private Endpoint, Azure SQL Server & Database. Combination of all the services will allow us to deploy Azure SQL with Sample Database with right network and security configuration to access the data. 

On other hand, Azure Analysis services does not need any specific network installation. It works as a standalone service in Azure with On-Premise Data gateway which needs to be configured separately on the client system where we need to develop the model before deploying it to the Azure Cloud

# Target audience

- Infrastructure Architect
- IT Professionals with the role,
    - BI Developers
    - Cloud Solution Architect
- Business Professionals with aspiring/experience of Self-service Analytics

# Pre-requisites:
-   Microsoft Azure Account to deploy services
-   Visual Studio 2019 with,
    - SSDT (SQL Server Development Tools)
    - Microsoft Analysis Services Tabular Model Plugin

# Landing Zone Architecture

The [Template.json](https://raw.githubusercontent.com/git-pranayshah/AnalysisService/master/template.json) Azure Resource Manager template will help you automatically deploy the diagram below, which includes:

- A landing zone for network with,
    Virtual Network
    Two Subnet (Default & Private-Data)
    Network Interfaces to connect to Private Network
    Private Network Links
- Azure SQL Server with,
    Sample Dataset (Please verify Pricing Tier as it contributes to cost)
    Private Network Link Connection
- Analysis Services Instance

- A Network Security Group with the necessary outbound rules for Azure Virtual Desktop Hostpools to properly activate and work.
- All services are ready to communicate with client Ip which is used to configure the service. In case of firewall error, request you to verify you client Ip under firwall section
- Cost implications are involved with Azure SQL and Analysis Services instance. Review and modify the Pricing Tier based on your needs

![alt image](https://github.com/git-pranayshah/AnalysisService/blob/master/images/Landing_Zone_Template.png)

[Template.json](https://raw.githubusercontent.com/git-pranayshah/AnalysisService/master/template.json) can be modified to match your current infrastructure needs.

## Teamplate Parameters
- ***Subscription:*** Azure Portal Subscription where you wish to deploy the template
- ***Resource Group:*** Select or create new resource group to deploy the resources
- ***Region(Default:westeruope):*** Select rigth region to deploy the resources
- ***Subscription Id:*** Select right Azure subscription id
- ***Server_owner_email:*** Email address of the server owner. 
- ***Servers_sample_db_server_mas_name(Default: samplesqldb-<Unique string based on resource group>):*** Server name for Azure SQL 
- ***Private Endpoints_private_db_name(Default: private-db):*** Private endpoint name for Azure SQL DB connection
- ***Virtual Networks_default_vnet_name(Default: defaultvnet):*** Virtual Network Name
- ***Servers_sql_db_awd_login_user(Default: sql-admin):*** SQL Admin user name for SQL Authentication
- ***Servers_sql_db_awd_login_password:*** SQL Admin user Password for SQL Authentication
- ***Storage Accounts_storagessqldb_name(Default: stgsql<Unique string based on resource group>):*** Storage Account Name for SQL Server
- ***Servers_sampledbmodel_name(Default: sampledbmodel):*** Microsoft Analysis Services Instance name
- ***Netowrk Configurations:*** (Recommend to not to change until it throws conflcits error in template execution)
    - ***Private Endpoints_data_endpoint_name(Default: data-endpoint):*** Private endpoint name for SQL Server
    - ***networkInterfaces_private_db_nic_name(Default:*** tgprivate-db.nicsql<Unique string based on resource group>): Network interface name
## One Click Deploying Teamplate
<!-- Powershell command for Translating Git URL for template.json
    $url = "https://raw.githubusercontent.com/git-pranayshah/AnalysisService/master/template.json"
    [uri]::EscapeDataString($url)
    >> uri = https%3A%2F%2Fraw.githubusercontent.com%2Fgit-pranayshah%2FAnalysisService%2Fmaster%2Ftemplate.json

Base URL: https://portal.azure.com/#create/Microsoft.Template/uri
Final URL: <Base URL>/<uri>
-->
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fgit-pranayshah%2FAnalysisService%2Fmaster%2Ftemplate.json)

## Deploying an ARM Template using the Azure portal

- Visit https://portal.azure.com

Using the search bar on top type Templates

![alt image](https://github.com/git-pranayshah/AnalysisService/blob/master/images/Search.png)

- Create a new template

![alt image](https://github.com/git-pranayshah/AnalysisService/blob/master/images/create.png)

- Give a name and a description to the template

![alt image](https://github.com/git-pranayshah/AnalysisService/blob/master/images/Name%20and%20Description.png)

- Add for modified [Template.json](https://raw.githubusercontent.com/git-pranayshah/AnalysisService/master/template.json) and save it

![alt image](https://github.com/git-pranayshah/AnalysisService/blob/master/images/add%20code.png)

- Select the newly added template and click deploy

![alt image](https://github.com/git-pranayshah/AnalysisService/blob/master/images/Select%20and%20deploy%20template.png)

- Fill out the blanks with your details and click purchase

![alt image](https://github.com/git-pranayshah/AnalysisService/blob/master/images/Fill%20out%20the%20details%20and%20purchase.png)

- Allow 20 minutes for the deployment to complete
- Peer your Hub and Spoke Virtual Networks as needed

## Azure services and related products

- Azure Networking including Vnet & network interfaces
- Security & Firewall
- Azure SQL
- Azure Analysis Services

## Related references
- https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-ver15
- https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects
- https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/
- https://docs.microsoft.com/en-us/azure/virtual-network/tutorial-connect-virtual-networks-portal#peer-virtual-networks
- https://docs.microsoft.com/en-us/azure/architecture/data-science-process/sample-data-sql-server
- https://docs.microsoft.com/en-us/azure/analysis-services/analysis-services-overview




