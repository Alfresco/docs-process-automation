---
Title: Project deployment
--- 

# Project deployment

The **DevOps** section of the Admin Application is used to deploy projects and manage and upgrade applications.

## Project releases

The **Project Releases** section displays a list of all [released projects](../model/projects.md#release-a-project) created in the Modeling Application.

**Note**: If you can't find your project in the list, make sure it has been released. To release a project:

1. Sign into the Modeling Application.
2. Find or search for your project in the list of projects.
3. Select the **Release** action from the **Options** column for the project.

### Properties

The properties for a released project are:

| Property | Description |
| -------- | ----------- |
| Project Name | The name of the project as it appears in the Modeling Application. |
| Version | The latest version number of the released project. |
| Created By | The user that created the project. |
| Created | The time since the project `version` was released. |

### Deployment

After choosing to **Deploy** a released project, there are a number of configuration settings required depending on the contents of the project.

**Note**: When a project is deployed, a [deployment descriptor](#deployment-descriptors) is created. Deployment descriptors can be exported from one environment and imported into another, for example between test and production. See the [deployment service architecture](architecture.md#deployment-service) for further details on the deployment process.

#### Application name

All projects require an application name for when they are deployed.

**Reminder**: Projects are referred to as applications when they are deployed.

1. Provide an **Application Name** for the project. The name must be unique and must be in lowercase and between 1 and 26 characters in length. Alphanumeric characters and hyphens are allowed, however the name must begin with a letter and end alphanumerically, for example: `finance-application`.

2. Select which released version of the project to deploy.

#### Admin access

All applications require at least one administrator to manage the application. Administrators have access to the [Process Admin](monitor.md) actions for an application.

Select a user or group to administer the application. The user or group must exist and cannot be set as static values.

#### User access

The users selected for an application are those able to start process instances and tasks for it.

**Note**: Any users or groups that were assigned to [user tasks](../model/processes/bpmn.md#user-task) using the **Identity** method will already be entered in this field.

Select the users and groups that can access the application. The users and groups must exist and cannot be set as a static values.

#### Connectors

**Note**: This tab will not appear if there are no [connectors](../model/connectors/README.md) in the project being deployed.

Applications that contain connectors need to have their [configuration parameters](../model/connectors/README.md#configuration-parameters) set.

All parameters will appear as key value pairs and additional pairs can be added by clicking **Add config variable**.

Any default values, or values entered whilst modeling the project will be pre-filled but can still be updated.

#### Storage

The storage options are used to set the default location for where data related to a process is stored. This data includes content uploaded from [attach file fields](../model/forms.md#attach-file-fields) in forms, [generated documents](../model/connectors/generate.md), [signed documents](../model/connectors/docusign.md) and content edited using the [content connector](../model/connectors/content.md).

**Note**: The default location set for the application storage will be used to store the content from the above actions if none of the target locations are set in their configuration. For example, if `targetFile`, `targetFolder`, `targetFolderId` and `targetFolderPath` are not set for the DocuSign connector, the signed document will be stored in the default storage location.

The options for the storage location are:

* **Store content in the following ACS site** can use an existing site in the repository to store the data or create a new one as part of the deployment process.

* **Store content in the folder with the following relative path** can store the application data in a specific folder rather than a site.

**Important**: Connectors can read and write from files and folders outside of the default storage location, however the service accounts must be given explicit [permission](../model/connectors/README.md#permissions) to read and write to those files and folders.

**Important**: Users filling in forms with an [attach file field](../model/forms.md#attach-file-fields) must be given explicit permission to the upload directory if it is outside of the default storage location for the application.

After clicking **Create** the deployment descriptor will be created and the application deployed, if **Deploy** was selected.

## Deployment descriptors

The **Deployment Descriptors** section displays a list of all deployment descriptors in the environment. These are created by the [deployment service](architecture.md#deployment-service) whenever a project is deployed.

Deployment descriptors are fully configured projects that can be exported and imported between environments, for example between test and production.

### Properties

The properties for deployment descriptors are:

| Property | Description |
| -------- | ----------- |
| Name | The name of the descriptor and the name that will be used for the application. |
| Status | The status of the descriptor. Once it has been created it will display as `DescriptorCreated`. |
| Created | The date and time the descriptor was created. |
| Modified | The date and time since the descriptor was last modified. |

### Export and import

Deployment descriptors can be exported as `.zip` files using the **Export Deployment Descriptor** option against a specific descriptor.

A previously exported deployment descriptor can be imported using the **Import** button in the **Deployment Descriptors** page.

**Note**: A deployment descriptor cannot be imported if it uses the same name as a deployment descriptor that already exists.

## Application instances

The **Application Instances** section displays a list of all deployed applications, and applications currently in the process of being deployed. Applications can have their permissions updated

**Reminder**: Projects are referred to as applications when they are deployed.

### Properties

The properties for application instances are:

| Property | Description |
| -------- | ----------- |
| Name | The name of the application. |
| Version | The version of the application. **Note**: This is the application version related to [upgrading](#upgrade) an application and not the project version. |
| Created | The time since the application was deployed. |
| Status | The status of the application. Once fully deployed it will display as `Running`. |
| Content App | A link to the [user interface](../model/interfaces.md) for the application. |

### Upgrade

Upgrading an application allows for a new version of a released project to be deployed to an existing application. Tasks and process instances that are in progress and based on a previous application version can still be completed, however any new ones started will use the new model definitions.

**Note**: An application can be upgraded to a released project version that is lower than the one currently deployed, however the application version will still increment.

The version of an application is incremental and independent of the released project version, for example:

| Released project version | Application version |
| ------------------------ | ------------------- |
| 1 | 1 |
| 2 | 2 |
| 4 | 3 |
| 5 | 4 |
| 3 | 5 |
| 10 | 6 |

The upgrade process displays the same configuration as [deploying](#deployment) an application. The only field that cannot be changed when upgrading is the application name.

### Manage permissions

The **Manage Permissions** option allows for additional users to be granted user or administrator access to an application without having to upgrade it.

### Undeploy

The **Undeploy** action removes a deployed application.

**Important**: Undeploying an application will remove all data related to the application including processes and tasks. It is not possible to retrieve this data once an application has been undeployed.
