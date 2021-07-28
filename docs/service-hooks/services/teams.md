---
ms.technology: devops-collab
ms.topic: conceptual
monikerRange: '>= tfs-2017'
title: Create a service hook Microsoft Teams
titleSuffix: Azure DevOps Server
description: Use Microsoft Teams with your Azure DevOps organization
ms.date: 03/16/2020
---

# Create a service hook for Team Foundation Server (TFS) with Microsoft Teams

>[!NOTE]
>If you use Azure DevOps Services, we recommend you use the following suite of apps which offer rich features, to integrate with Microsoft Teams.

### Azure Boards app for Teams
[Azure Boards app for Teams](https://aka.ms/AzureBoardsTeamsIntegration) helps to easily create and monitor work items from your Teams channels.Users can create work items using a command, or use message actions to convert conversations in the channel into work items. Users can also set up and manage subscriptions to get notifications in their channel whenever work items are created or updated. 
### Azure Pipelines app for Teams
[Azure Pipelines app for Teams](https://aka.ms/AzurePipelinesTeamsIntegration) helps to easily monitor the events in your pipelines. Users can set up and manage subscriptions for completed builds, releases, pending approvals and more from the app and get notifications for these events in their channels. Users can also approve release deployments from their channels. 
### Azure Repos app for Teams
[Azure Repos app for Teams](https://aka.ms/AzureReposTeamsIntegration) helps to easily monitor the events in your repositories. Users can set up and manage subscriptions for code commits, PR creation and PR updates and more from the app and get notifications for these events in their channels. 

 
See activity about your Team Foundation Server (2017.2 and later) projects directly in your Microsoft Teams channel, for example:
* Work item updates
* Pull requests
* Code commits
* Builds
* Release deployments and approvals

## Configuring a new connector for TFS

Configuring integration between Team Foundation Server and Teams is a two-step process. First set up a connector in Teams, then set up one or more service hook subscriptions in your Team Foundation Server project.

>[!NOTE]  
>Project administrator permissions are required to create service hook subscriptions. 
>Events for YAML pipelines are not supported. 


### From Teams

1. To bring events from TFS into Microsoft Teams, click the ellipsis or '...' at the top nav of your team channel, and select Connectors. 

   <img alt="Adding a new Connector to Teams" src="./media/teams/Teams Connector config 1.png" style="width:80%;" />

1. Select **Team Foundation Server** from the list.

   <img alt="Connectors list" src="./media/teams/Teams Connector config tfs 1.png" style="width:80%;" />

1. Choose a name for the Connector, for example "My project notifications", and click Create. Note: this name is only used for managing the Connector.
<br/>
<img alt="Connectors list" src="./media/teams/Teams Connector config tfs 2.png" style="width:80%;" />

1. Copy the generated web hook URL. Provide this URL when you're setting up service hook subscriptions in your TFS project.

### From Team Foundation Server

1. From your TFS team project page (```https://mycompany/tfs/[collection]/[project]```), navigate to **Service Hooks** in the settings:

   <img alt="Azure DevOps Services, Service Hook Settings" src="./media/slack/vsts-service-hooks.png" style="width:70%; height:auto;" />

1. Click **Create subscription** and select the "Teams" service.

1. Choose the type of activity you want to appear in your Teams channel.
   > You can filter each of the triggers in specific ways.
   > For example, the *pull request created* trigger can be filtered on the repository in which the pull request occurs,
   > the target branch it applies to, and the team members that are required or invited to review the request.

1. Paste the web hook URL from the Teams connector configuration step and click Finish.

Activity from your TFS project will start appearing in your Teams channel.


## Configuring Azure DevOps Services Tabs in Microsoft Teams

1. To bring your Kanban board or Dashboard into Microsoft Teams, click the '+' ('add new tab') button on the top nav of your team channel. Find the Website icon and add the link to your Azure DevOps board or dashboard. 

   <img alt="Add a new tab to Teams channel" src="./media/teams/teams-as-website.png" style="width:80%;" />

2. Once you've authenticated you will see your Kanban board or Dashboard.
   

## Frequently asked questions (FAQs)

<!-- BEGINSECTION class="m-qanda" -->

### Q: How can I get multiple events from my TFS project to show up in my Teams channel?

A: Create a new subscription for each type of event you want.
For example, if you want to see build failures and new work items in your Teams channel,
create two additional subscriptions.

### Q: Why don't I see my organization when trying to connect Microsoft Teams?

A: Only organizations in the same Azure Active Directory tenant as your Microsoft Teams account can be connected. Even if your email address is the same for Azure DevOps Services and Microsoft Teams, they may be backed by different tenants, so they can't be linked.

Create a new Team in the same Azure Active Directory (Azure AD) as Azure DevOps Services, or move your Azure DevOps Services to the same Azure AD as Teams, see [Q: Why is my organization already connected to a directory? Can I change that directory?](../../organizations/accounts/faq-azure-access.md#q-why-is-my-organization-already-connected-to-a-directory-can-i-change-that-directory).

<!-- ENDSECTION -->
