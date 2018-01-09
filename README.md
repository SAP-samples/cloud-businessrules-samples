# SAP Cloud Platform Business Rules Sample Projects and Applications
SAP Cloud Platform Business Rules enables line of business users, application developers to automate decisions in simple human friendly rule language and integrate these decisions via APIs with their cloud applications. 
You can use these sample applications and rule projects as reference content to learn more about how-to build and consume business rules.

## Solution Diagram
This diagram shows how you can consume business rules service from workflow, cloud integration and other SAP Cloud solutions. 
![Solution Diagram](https://github.com/SAP/cloud-businessrules-samples/blob/master/images/BusinessRules_SolutionDiagram.png)

Beside these, there are many other services which can consume SAP Cloud Platform Business Rules. Below diagram shows a rich list of various consumption models:
![Consumption Models](https://github.com/SAP/cloud-businessrules-samples/blob/master/images/BusinessRules_ConsumptionPatterns.png)

## Prerequisites
You need to have the following:
1.  SAP Cloud Platform (Neo) account with an active subscription to Business Rules service.Refer [here](https://blogs.sap.com/2017/04/26/sap-cloud-platform-business-rules-try-it-yourself/) for information on getting a free trial account of SAP Cloud Platform and how to enable SAP Cloud Platform Business Rules Service.
2.  **RuleSuperUser** role for Runtime and Repository operations.
3.  **Developer** role to create and deploy SAPUI5 applications in SAP Cloud Platform.
4.  SAP WebIDE Full-Stack service enabled in SAP Cloud Platform.

## Repository Overview
The available samples are of 2 types depending upon the folder containing them. There would be different setup process for each type:
1. **apps** - It contains SAPUI5 applications that need to imported from WebIDE and deployed. **shoppingcart** application shows how to consume rule service in custom HTML5 application and **rulesmanager** application shows how to embed SAPUI5 Rules Builder control in your custom application. 
2. **rulesprojects** - It contains business rules projects that need to imported from business rules editor

## Getting Started
1. Download the content from the git: https://github.com/SAP/cloud-businessrules-samples
2. Extract the content into local file system

- From content in **apps** folder:
  - Open SAP Web IDE Full-Stack and import the project zip using File --> Import --> From File System option.

- From content in **rulesproject** folder:
  - Open Business Rules Editor and import the project using the Import button on the Manage Projects screen

## Authors
Archana Shukla

## Copyright and License
Copyright (c) 2017 SAP SE. All rights reserved.
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. 
You may obtain a copy of the License at > http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an 
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
