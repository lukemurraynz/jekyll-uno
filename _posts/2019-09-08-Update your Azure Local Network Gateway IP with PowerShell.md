---
date: 2019-09-08
title: Update your Azure Local Network Gateway IP with PowerShell
author: Luke
categories:
- Azure
- PowerShell
header:
  teaser: "images/powershell-blog-feature-banner.png"
---
One of the issues you face with setting up an Azure [Site to Site
VPN](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal){:target="_blank"}
is making sure that your Azure Local Network Gateway always has your
Public/On-premises IP.

This setup is fine when used in environments that have Static IPs (and yes if
setting this up for a Business or Production, it is highly recommended to have a
static IP!).

However, when used in environments like my home network or lab environments - which has a Dynamic IP that could change at any time it will cause connectivity issues if your IP changes and the Local Network Gateway is not updated.

The script below – intended to be run on as a Daily scheduled task, will find
your Public IP and connect to Azure and if needed – will update the IP of your
Local Network Gateway.

Prerequisites:

* [Az PowerShell
  Module](https://docs.microsoft.com/en-us/powershell/azure/install-az-ps?view=azps-2.6.0){:target="_blank"}
* [Azure Service
  Principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){:target="_blank"}
  (with Contributor rights to the Azure Local Network Gateway)

Once you have the Azure Service Principal and Az Module installed, you need to
edit the following variables to suit your environment:

* $ResourceGroup = 'RESOURCE GROUP OF LOCAL NETWORK GATEWAY'
* $LocalNetworkGateway = ‘NAME OF AZURE LOCAL NETWORK GATEWAY’
* $azureAplicationId =’AZURE AD APPLICATION ID’
* $azureTenantId= ‘AZURE AD TENANCY/DIRECTORY ID’
* $azureAPI = ‘AZURE AD APPLICATION API/CLIENT SECRET’

{% gist 1b73335e1d0eadcfe4064f8221077ca1 %}

_Note: Script is also hosted on my Github repository. Feel free to
clone/recommend improvements or fork._