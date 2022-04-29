---
page_type: sample
languages:
  - n/a
products:
  - azure
  - azure-video-analyzer
description: "Samples to show how to use Postman to call the Azure Video Analyzer management API."  
---

# Deprecated - Azure Video Analyzer REST API Postman samples

We’re retiring the Azure Video Analyzer preview service, you're advised to transition your applications off of Video Analyzer by 01 December 2022. This repo is no longer being maintained.

## Introduction

[Postman](https://www.postman.com) is an API platform for building and using APIs. Using the Postman application is great way to try out and familiarize yourself with the [Video Analyzer management REST APIs](https://docs.microsoft.com/rest/api/videoanalyzer/) without writing code using one of the SDKs, such as .NET or Python.

This repository contains a Postman collection file that can be imported and allows a selection of the Video Analyzer management REST APIs to be called.

## Contents

| File/folder       | Description                                |
|----------------------|--------------------------------------------|
| AzureVideoAnalyzer_2021-11-01-preview.postman_collection.json | Exported Postman collection with sample API calls - API version '2021-11-01-preview'. |
| `README.md` | This README file. |
| `LICENSE.md` | The license for this sample. |
| `CONTRIBUTING.md` | Contribution guidelines |

## Prerequisites

The following prerequisites are required in order to setup and use this sample:

- An active Azure subscription.
- An active Video Analyzer account.
- The [Azure CLI](https://docs.microsoft.com/cli/azure/) is installed. This will be used to create a service principal, which is needed to access the Video Analyzer API.
- The [Postman](https://www.postman.com) application installed with basic familiarity of the application required.

## Setup

1. Create an Azure service principal from which tokens are obtained to authenticate with the Video Analyzer account REST APIs. The tokens will allow 'Contributor' access to a specified Video Analyzer account. The Azure documentation has a [complete description](https://docs.microsoft.com/rest/api/azure/) of how to call Azure REST APIs, including from Postman.
    1. Use the Azure CLI to login:
        ```azurecli
        az login
        ```

    1. Select the Azure subscription to use:
        ```azurecli
        az account set --subscription <name of your subscription>
        ```

    1. Use the following CLI command to create the service principal that will be used to access to Video Analyzer account. You will need the subscription ID, resource group, and name used to create the Video Analyzer account. Make note of the output from the CLI command and keep the output safe.
        ```azurecli
        az ad sp create-for-rbac -n "AvaPostmanSample" --role Contributor --scopes /subscriptions/<Subscription ID>/resourceGroups/<Resource Group>/providers/Microsoft.media/videoAnalyzers/<VideoAnalyzerAccountName>
        ```

1. Create a local copy of the '.postman_collection.json' export file by downloading or copying the file.
1. Import the collection file in Postman using the 'Import' option.
1. Postman collection variables need to be configured:
    1. Select the imported collection.
    1. Select the 'Variables' section.
    1. Enter 'CURRENT VALUE' cell values for variables 'SubscriptionId', 'ResourceGroupName', and 'VideoAnalyzerAccountName'. These values are the same ones used with the Azure CLI to create the service principal.
    1. Using the Azure CLI output when the service principal was created, enter 'CURRENT VALUE' cell values for variables 'appId', 'password', 'tenant'. Do not enter values for 'bearerTokenExpiresOn' and 'bearerToken' - these variables are set by the pre-request script.
    1. Save the collection, otherwise the newly entered variable values may not be used when requests are sent and an error will be displayed.

## Running API requests

- The sample requests are grouped by operations.
- The 'List' requests require no further information to be configured.
    - For example, select the 'Video Analyzers - List' request and select 'Send', no further configuration is required and details for the configured Video Analyzer account will be returned.
- The 'Create' requests can have a both a 'Params' variable and 'Body' json that need to be entered. The json format for the the 'Body' being specified in the [REST API reference](https://docs.microsoft.com/rest/api/videoanalyzer/).
    - For example, select the 'PipelineJobs - Create' request - the 'Params' section needs to be selected so the value for 'pipelineJobName' can be specified, then the 'Body' section needs to be selected so that the associated topology name for the pipeline job can be specified.
- The 'Get' and 'Delete' requests have a variable value to be entered to identify the item, such as an edge module name. The variable values are entered in the 'Params' section.
    - For example, for the 'Edge Modules - Get' request, the 'EdgeModuleName' needs to be specified in the 'Params' section.

## Resources

- [Video Analyzer documentation](https://docs.microsoft.com/azure/azure-video-analyzer/video-analyzer-docs)
- [Video Analyzer REST API](https://docs.microsoft.com/rest/api/videoanalyzer/)
