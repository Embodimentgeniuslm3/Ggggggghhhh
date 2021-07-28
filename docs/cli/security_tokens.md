﻿---
title: CLI Security tokens for permissions management
titleSuffix: Azure DevOps 
description: Use Azure DevOps CLI to manage security tokens for permissions management
ms.topic: reference 
ms.prod: devops 
ms.technology: devops-ref
ms.manager: mijacobs 
ms.author: geverghe
author: KathrynEE
monikerRange: 'azure-devops'
ms.date: 06/18/2019
---

# Security tokens for permissions management

[!INCLUDE [temp](../includes/version-vsts-only.md)] 

Tokens are arbitrary strings representing resources in Azure DevOps. Token format differs per resource type, however hierarchy and separator characters are common between all tokens.

## Hierarchy

A security namespace can be either hierarchical or flat.
Tokens in a hierarchical namespace exist in a hierarchy with effective permissions being inherited from parent tokens to child tokens.
Tokens in a flat namespace have no concept of a parent-child relationship between any two tokens.

## Separator character

Tokens in a hierarchical namespace either have a fixed length for each path part, or variable length.
If the tokens have variable-length path parts, then a separator character is used to distinguish where one path part ends and another begins.

## Token examples for different namespaces

### Namespace name: Project

   Namespace ID:52d39943-cb85-4d7f-8fa8-c6baac873819

   Basically tokens in this namespace are of the following format.
   Root token : '$PROJECT'

   Token to secure permissions for each project in your organization
   '$PROJECT:vstfs:///Classification/TeamProject/PROJECT_ID'

   So, let's assume you have a project named 'Test Project 1'.
   You can get the project ID for this project by referring project show command
   `az devops project show --project "Test Project 1"`

   Above command would return a project-id (say xxxxxxxx-a1de-4bc8-b751-188eea17c3ba)

   Thus, the token to secure project related permissions for 'Test Project 1' would be
   '$PROJECT:vstfs:///Classification/TeamProject/xxxxxxxx-a1de-4bc8-b751-188eea17c3ba'

### Namespace name : Tagging

   Namespace ID : bb50f182-8e5e-40b8-bc21-e8752a1e7ae2

   Token format for project level permissions : '/PROJECT_ID'

   Example : '/xxxxxxxx-a1de-4bc8-b751-188eea17c3ba'

### Namespace name : AnalyticsViews

   Namespace ID : d34d3680-dfe5-4cc6-a949-7d9c68f73cba

   Token format for project level permissions : '$/Shared/PROJECT_ID'

   Example : '$/Shared/xxxxxxxx-a1de-4bc8-b751-188eea17c3ba'

### Namespace name : Analytics

   Namespace ID : 58450c49-b02d-465a-ab12-59ae512d6531

   Token format for project level permissions : '$/PROJECT_ID'

   Example : '$/xxxxxxxx-a1de-4bc8-b751-188eea17c3ba'

### Namespace name: Iteration

   Namespace ID : bf7bfa03-b2b7-47db-8113-fa2e002cc5b1

   Token format: 'vstfs:///Classification/Node/Iteration_Identifier/'

   Suppose, you have following iterations configured for your team.
   
   - ProjectIteration1
   1. TeamIteration1
        - TeamIteration1ChildIteration1
        - TeamIteration1ChildIteration2
        - TeamIteration1ChildIteration3
   2. TeamIteration2
        - TeamIteration2ChildIteration1
        - TeamIteration2ChildIteration2

   If you need to update permissions for ProjectIteration1\TeamIteration1\TeamIteration1ChildIteration1, security token would look like this:

   'vstfs:///Classification/Node/ProjectIteration1_Identifier:vstfs:///Classification/Node/TeamIteration1_Identifier:vstfs:///Classification/Node/TeamIteration1ChildIteration1_Identifier'

### Namespace name :  BuildAdministration

   Namespace ID : 302acaca-b667-436d-a946-87133492041c

   Token format: 'BuildPrivileges'

### Namespace name :  Build

   Namespace ID : 33344d9c-fc72-4d6f-aba5-fa317101a7e9

   Token format for project level build permissions : 'PROJECT_ID'

   If you need to update permissions for a particular build definition ID [Let's say 12], security token for that build definition would look like this

   Token format for project level build permissions : 'PROJECT_ID/12'

   Example : 'xxxxxxxx-a1de-4bc8-b751-188eea17c3ba/12'

### Namespace name :  Identity

   Namespace ID : 5a27515b-ccd7-42c9-84f1-54c998f03866

   Token format for project level permissions : 'PROJECT_ID'

   Example : 'xxxxxxxx-a1de-4bc8-b751-188eea17c3ba'

   To modify group level permissions for Group Origin ID [2b087996-2e64-4cc1-a1dc-1ccd5e7eb95b]

   Token : 'xxxxxxxx-a1de-4bc8-b751-188eea17c3ba\2b087996-2e64-4cc1-a1dc-1ccd5e7eb95b'

### Namespace name :  ReleaseManagement

   Namespace ID : c788c23e-1b46-4162-8f5e-d7585343b5de

   Token format for project level permissions : 'PROJECT_ID'

   Example : 'xxxxxxxx-a1de-4bc8-b751-188eea17c3ba'

   If you need to update permissions for a particular release definition ID [Let's say 12], security token for that release definition would look like this

   Token format for project level build permissions : 'PROJECT_ID/12'
   
   Example : 'xxxxxxxx-a1de-4bc8-b751-188eea17c3ba/12'
   
   If the release definition ID lives in a folder, then the security token would look like this
   
   Token format: 'PROJECT_ID/{folderName}/12'
   
   For stages, tokens look like: 'PROJECT_ID/{folderName}/{DefinitionId}/Environment/{EnvironmentId}'

### Namespace name :  Git Repositories

   Namespace ID : 2e9eb7ed-3c0a-47d4-87c1-0ffdd275fd87

   Token format for project level permissions : 'repoV2/PROJECT_ID'

   You need to append RepositoryID to update repo level permissions

   Token format for repository level permissions : 'repoV2/PROJECT_ID/REPO_ID'

   For more information on this namespace and its tokens refer this [blog](https://devblogs.microsoft.com/devops/git-repo-tokens-for-the-security-service/)

### Namespace name : AuditLog
   
   Namespace ID : a6cc6381-a1ca-4b36-b3c1-4e65211e82b6
   
   Token format : '/AllPermissions'
 
### Namespace name : UtilizationPermissions
   
   Namespace ID : 83abde3a-4593-424e-b45f-9898af99034d
   
   Token format : '/'
   
   This namespace controls the ability to query usage summaries for users. 
   
### Namespace name : WorkItemTrackingProvision 

   Namespace ID : 5a6cd233-6615-414d-9393-48dbb252bd23
   
   Root token format : '/$'
   
   Token format for a specific project: '$/PROJECT_ID'
   
   This is an older security namespace that is mostly used for Azure DevOps Server and older Azure DevOps Services projects. It has been largely replaced by the "Process" namespace. 
   
### Namespace name : Workspaces 
   
   Namespace ID : 93bafc04-9075-403a-9367-b7164eac6b5c
   
   Root token format: '/'
   
   Token format for a specific workspace: '/{workspace_name};{owner_id}' 
   
   This security namespace is used only with TFVC. The user ID in the token is the TeamFoundationID of the Workspace's owner/creator.
