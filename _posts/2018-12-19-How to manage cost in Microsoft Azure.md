---
date: "2018-12-19"
title: How to manage cost in Microsoft Azure
author: Luke
categories:
  - Azure
---

Microsoft have built up the Microsoft Azure ecosystem, to offer scale and
performance as and when needed, this gives customers the ability to not only
remain competitive by lead and disrupt their industries without having to worry
about on-premises datacentre capacity, redundancy and manual processes, this
however comes at a cost, where engineers may have in the past not cared or been
responsible for cost – the Cloud has enabled us not only to consume valuable
resources, but also drive cost up which has now shifted left to System
Administrators or DevOps Engineers to keep things running and keeping cost low.

Microsoft has built (and continuously improving) some great tools to help
customers not only be aware of their cost, but make data driven decisions, this
blog post is intended to help you gain an understanding of various cost
management functions in the Microsoft Azure environment to help you drive
productivity up but keep costs low.

Microsoft Azure and other Cloud/Software as a Service products, operate in the
Opex (or Operational Expenditure) model, meaning that you are essentially paying
for subscription-based services and resources on a Monthly or as consumed basis
– verses the traditional Capex (or Capital Expenditure) model where you may pay
for something up-front whether you use it or not and usually leads to waste in
capital due to oversizing machines or purchasing more than is needed, using Opex
gives greater flexibility in terms of what you are currently (and not) consuming
and what you want to consume, one thing to remember is that if something is
scaled up, it can always be scaled down again with little (or none in some
cases) downtime or risk.

Roles & Responsibilities & Azure Governance
-------------------------------------------

Before I start through some of the Products that can help you on your manging
cost journey – I need to cover off the People aspect first, what I mean by this
is Roles & Responsibilities, you need to have some clear clarity in your
organisations around who is responsible for what costs are not only created but
anything running, whether you have a Product Owner approving and manging the
financials or entire Agile Squads dedicated to keeping their resources lean and
responsibly for any costs incurred you need to be transparent around
Responsibility and Accountability of your costs to help manage (and pay for) the
costs and avoid waste. Microsoft Azure has a ‘[Billing
Administrator](https://docs.microsoft.com/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles){:target="_blank"}’
role which may be helpful to give someone visibility of costs in Microsoft
Azure, also be aware of what roles users have and what they can do with it, you
don’t want to give someone Contributor rights over a subscription and have them
create a ton of resources when all they needed was Reader rights to view someone
else work or skip internal processes for deploying resources.

If you haven’t already – I highly recommend getting an [Azure
Scaffold](https://docs.microsoft.com/en-us/azure/architecture/cloud-adoption/appendix/azure-scaffold){:target="_blank"}
or Governance model in place to help determine how you not only use Azure, but
how you manage the costs – whether it’s per subscription based or Resource
Groups, the use of Tags to tag Azure resources based on cost centre or
department etc is invaluable.

Pricing Calculator
------------------

The first place to start in the journey of managing technical costs in Azure, is
the Pricing Calculator

<https://azure.microsoft.com/en-us/pricing/calculator/>{:target="_blank"}

The Pricing Calculator allows you select various Azure services (Virtual
Machines, App Services Plans, IoT Hubs) and work out estimated pricing vs
criteria which may be service specific such as runtime, geo-redundancy, the
amount of storage required etc. You need to be aware of whether a service is
costing money if it is running, how many read/writes is allowed etc. I recommend
spending some time to look through the Pricing Calculator and various services
that Microsoft Azure offers to get a feel of cost – if you are in NZ (make sure
to select ‘New Zealand Dollar’), the default is US.

Cost Visibility across Subscriptions & Resource Groups
------------------------------------------------------

The Microsoft Azure Portal offers a lot of visibility into the cost of running
resources in Azure, whether you want to look at the costs per subscription or in
this example the Resource Group.

You can find the cost information under the ‘Resource Costs’ blade in the
Resource Group or ‘Cost Analysis’ at a Resource Group level.

![Azure Resource Group Costs](/images/posts/appservice_resourcecosts.png)

Using the built in Azure Portal tools you filter costs based on Time/Date and
Tags.

On the Overview Blade of an Azure Subscription you can see the highest costs by
Resource type and estimated forecast of cost based on current consumption.

![Azure Subscription Forecast](/images/posts/subscription_costs_forecast.png.png)

Invoices & Consumption Insights
-------------------------------

For those of you who pay by Credit Card or want to know the Pre-tax costs of
your Azure resources, you can go to your subscription and click on the Invoices
blade to review current and previous invoices, if not setup already I recommend
you configure the Email Invoice to automatically send the invoice to your
Billing Administrator.

If you are on an Enterprise Agreement, you can setup [Microsoft Azure
Consumption
Insights](https://docs.microsoft.com/en-us/power-bi/desktop-connect-azure-consumption-insights){:target="_blank"}
PowerBI pack to help give visibility of Azure costs through the use of the API
key from your enrolment portal.

Azure Policies
--------------

Along with your Cloud Scaffold or Governance framework, you need to be able to
force or guide your environment, [Azure
Policies](https://docs.microsoft.com/en-us/azure/governance/policy/overview) can
be used to not only keep your Azure ecosystem in alignment but stop creation of
unapproved resources, high costing Virtual Machines, or resources in specific
regions, you can use Azure Policies to Audit resources or completely prevent
them from being created. Azure Policy samples can be at the
[azure-policy](https://github.com/Azure/azure-policy/tree/master/samples){:target="_blank"}
git repository.

Hybrid Use Benefit 
-------------------

If you already own on-premises Windows Server/SQL server licenses – you may be
eligible for [HUB (Hybrid Use
Benefit)](https://azure.microsoft.com/en-us/pricing/hybrid-benefit/)
{:target="_blank"} which allows you to run certain machines, based on licensed
cores in Azure under the same Windows Server licensing for no additional cost,
this can be enabled in the Azure Portal on a Virtual Machine with no downtime.

Azure Advisor & Reserved Instances
----------------------------------

Microsoft has built an Advisor into Azure, this Advisor not only gives Security
& Performance recommendations, it also includes Cost Recommendations

![Azure Advisor](/images/posts/azureadvisorbutton.png)

![Azure Reserved Instance](/images/posts/azurerihub.png)

These Cost recommendations, are based on CPU usage of workloads (and can be
adjusted) – such as workloads that have been running at 5% CPU utilisation for
the past 14 days and recommends Cost Savings by resizing down the Virtual
Machine.

The Azure Advisor also recommends [Reserved
Instances](https://azure.microsoft.com/en-us/pricing/reserved-vm-instances/){:target="_blank"},
instead of ‘Pay As You Go’ or ‘Pay As You Consume’ Opex model, you pay for the
Virtual Machines up-front (think capital expenditure) for 1 or 3 year terms, in
some cases you can get 72% savings and if you have machines you know will be on
24/7 and won’t need resizing – think Infrastructure servers, such as Domain
Controllers then Reserved Instances are a good idea.

Last Considerations
-------------------

You need to be aware that pricing in the Azure Portal or Pricing Calculator, may
not show all costs. These price indications are only based on the service or
size of a resource, they do not take into consideration Network dependencies
such as data egress (data leaving Azure), storage replication etc – the reality
is, is sometimes the only way to know how much something will cost is to
provision it, use it and monitor the costs.

A side bit of information also is that although a service might cost x in
AustraliaEast it may be a lot cheaper to run it in the US for example so if you
need to quickly spin something up or test it and not concerned about latency or
data sovereignty then check out [Azure
Price](https://azureprice.net/?currency=NZD){:target="_blank"}, this website
lists the cost of the Virtual Machines, their costs and recommended regions to
get in some cases 30-40% cost savings.