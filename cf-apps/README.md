
# Business Rule Sample Applications
## Description
[Business Rules](https://cloudplatform.sap.com/capabilities/product-info.SAP-Cloud-Platform-Workflow.df696e5a-d973-4ecd-8d8d-532d60aa1921.html) allows you to automate and flexibly adapt decision logic with no application development. Users can model business rules and formulas in tabular, spreadsheet-like decision tables. A straightforward, Web-based business rules editor helps users manage business rule changes.

These *Business Rules Samples* contains a collection of business rules applications to demonstrate the consumption of Business Rules in the context of extending the standard decisions. They are intended to be used as a reference content for the development of decision-based applications.

### List of sample applications
|Application|Scenario|Scenario Description|
|---|---|---|
|Custom|[run-businessrules-sample.zip](https://github.com/SAP-samples/cloud-businessrules-samples/blob/master/cf-apps/run-businessrules-sample.zip)|helps you understand how to invoke business rules from custom application|
|Embedded|[cf_rulesmanager.zip](https://github.com/SAP-samples/cloud-businessrules-samples/blob/master/cf-apps/cf_rulesmanager.zip)|See how to embed business rules in your custom application. These custom application can be given to business users to modify rules|
|Shopping Cart Application|[cf-shoppingcart.zip](https://github.com/SAP-samples/cloud-businessrules-samples/blob/master/cf-apps/cf-shoppingcart.zip)|Use this sample shopping cart to understand how discount rules are consumed from a shopping cart application. Follow the section below to setup|
|Rule Editor (DEPRECATED)|[cf-businessruleseditor.zip](https://github.com/SAP-samples/cloud-businessrules-samples/blob/master/cf-apps/cf-businessruleseditor.zip)|This is no more to be used. It was an old way to setup business rules in Neo environment |

## Setting up Shopping Cart Sample Application
### Prerequisites
To make this sample application work, please make sure you have:

- An account on SAP Cloud Platform.
  - For Example, you may sign up for a trial account. For more information about the Sign up process, see this [blog](https://blogs.sap.com/2017/05/16/sap-cloud-platform-trial-now-includes-cloud-foundry/)
- A basic knowledge of Java/Spring
- A basic knowledge of Maven
  - Download, Install and Setup [Maven](http://maven.apache.org/download.cgi) in your system 
  - All components are built with [Apache Maven](http://maven.apache.org/)
- A basic knowledge of Node.js 
  - Install and Setup [NPM](https://www.npmjs.com/get-npm) in your system
  - For more information about working with NPM registry, see this [blog](https://blogs.sap.com/2017/05/16/sap-npm-registry-launched-making-the-lives-of-node.js-developers-easier/)

## Running the Application in Cloud Foundry Environment

### 1. Download the Shopping Cart Application
Download and extract the shopping cart application under **cf-apps** folder

### 2. Adding required security libraries

To secure the application we have to add Spring Security to the classpath. By configuring Spring Security in the application, Spring Boot automatically secures all HTTP endpoints with BASIC authentication. Since we want to use OAuth 2.0 together with [Java Web Tokens (JWT)](https://tools.ietf.org/html/rfc7519) instead, we need to add the Spring OAUTH and Spring JWT dependencies as well. To enable offline JWT validation the SAP XS Security Libraries need to be added as well. The latest version can be downloaded from the [Service Marketplace](https://launchpad.support.sap.com/#/softwarecenter/template/products/%20_APP=00200682500000001943&_EVENT=DISPHIER&HEADER=Y&FUNCTIONBAR=N&EVENT=TREE&NE=NAVIGATE&ENR=73555000100200004333&V=MAINT&TA=ACTUAL&PAGE=SEARCH/XS%20JAVA%201).

* Create **libs** folder inside the extracted **cf-shoppingcart** folder in step 1
* Unzip the file downloaded from the service marketplace to the *libs* folder
* Install SAP XS Security Libraries to your local maven repo by executing this command:

```shell
cd cf-shoppingcart/libs
mvn clean install
```
* Once the libraries are successfully installed, you will see the following dependencies are added to `pom.xml` file:

**Note:** You may need to adapt the version number in your `pom.xml` in case you are using a newer version of the SAP XS Security Libraries. You can get that version number from the downloaded libraries, and accordingly change them in `pom.xml` for all `groupIds` that starts-with `sap.com` respectively.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.security.oauth</groupId>
    <artifactId>spring-security-oauth2</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-jwt</artifactId>
</dependency>
<dependency>
    <groupId>com.sap.xs2.security</groupId>
    <artifactId>security-commons</artifactId>
    <version>0.28.6</version>
</dependency>
<dependency>
    <groupId>com.sap.xs2.security</groupId>
    <artifactId>java-container-security</artifactId>
    <version>0.28.6</version>
</dependency>
<dependency>
    <groupId>com.sap.xs2.security</groupId>
    <artifactId>java-container-security-api</artifactId>
    <version>0.28.6</version>
</dependency>
<dependency>
    <groupId>com.unboundid.components</groupId>
    <artifactId>json</artifactId>
    <version>1.0.0</version>
</dependency>
<dependency>
    <groupId>com.sap.security.nw.sso.linuxx86_64.opt</groupId>
    <artifactId>sapjwt.linuxx86_64</artifactId>
    <version>1.1.19</version>
</dependency>
<dependency>
    <groupId>com.sap.security.nw.sso.ntamd64.opt</groupId>
    <artifactId>sapjwt.ntamd64</artifactId>
    <version>1.1.19</version>
</dependency>
<dependency>
    <groupId>com.sap.security.nw.sso.linuxppc64.opt</groupId>
    <artifactId>sapjwt.linuxppc64</artifactId>
    <version>1.1.19</version>
</dependency>
<dependency>
    <groupId>com.sap.security.nw.sso.darwinintel64.opt</groupId>
    <artifactId>sapjwt.darwinintel64</artifactId>
    <version>1.1.19</version>
</dependency>
```

### 3. Configure NPM

Execute the following command:
```
npm config set @sap:registry https://npm.sap.com
```

### 4. Build the application

#### Build Java App

Execute the following command:
```
cd cf-shoppingcart/app
mvn clean install
cd ..
```

#### Build Web App
```
cd cf-shoppingcart/web
npm install
cd ..
```

### 5. Deploy application in Cloud Foundry
#### Access your cloud foundry API endpoint 
```
cf api https://api.cf.eu10.hana.ondemand.com
```

#### Login to your account
```
cf login
```

If you have access to more than 1 org or space, execute the following command:
```
cf target -o ORG -s SPACE
```

#### Update the application
URLs (or better host names) must be unique within the domain used by Cloud Foundry installation.

To prevent URL collisions with other employees who are trying the same sample application in the [trial org](http://docs.cloudfoundry.org/concepts/roles.html#orgs) of Cloud Foundry, you need to update the application [manifest-cf-factory.yml](manifest-cf-factory.yml).

For that you need to **replace** in the manifest file **all [trial user id]** occurrences with your user id. Hint: Use find/replace or sed for reliable results.

#### Create Service Instance

```
cf create-service business-rules lite java-ruleservice
cf create-service xsuaa application java-rule-sample-uaa -c ./security/xs-security.json
```

#### Push the application
Ensure that you have assembled the application with Maven as described above.

```
cd cf-shoppingcart
cf push -f manifest-cf-factory.yml
```

#### Assign Business Rules Roles

Assign the user with the following Roles

| Application Identifier         | Role Name                   | Role Template              |
| ------------- | ----------------------- | ----------------------- |
| bpmrulebroker!b\<tenant no>       | RuleRuntimeSuperUser | RuleRuntimeSuperUser |
| rule-sample-java!t\<tenant no>       | Editor | Editor |
| rule-sample-java!t\<tenant no>       | Viewer | Viewer |

Follow the [HowTo](https://jam4.sapjam.com/wiki/show/d2dgJlWR9IpwQsLOCmyJj9) JAM page for assigning the roles to a user

#### Map Routes to application

Execute the following command in order to create a tenant-specific route for the application:
* Replace the `[subdomain]` with your cloud foundry subdomain
```
cf map-route java-rule-sample-web cfapps.eu10.hana.ondemand.com -n [subdomain]-java-rule-sample-web
```

### 6. Access the application
URL: http://[subdomain]-java-rule-sample-web.cfapps.eu10.hana.ondemand.com

## Authors
Archana Shukla

## Copyright and License
Copyright (c) 2017 SAP SE. All rights reserved.
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. 
You may obtain a copy of the License at > http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an 
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

