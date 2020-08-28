---
title: Connectors overview
---

Connectors are used to handle interactions between external systems and a process. Values are sent from a process to a connector as input parameters and send back as output parameters after the connector logic has executed.

Examples of what connectors can be used for include:

* Sending an email using values from a process to populate the fields
* Interacting with an installation of Slack to post messages
* Calling a custom REST API and passing the response back to a process

Connectors are modeled as [service tasks](../bpmn/service.md) within a process definition.

## Connectors setup

Connectors are created with two separate elements:

* A [connector definition](#connector-definitions) that can contain actions and events.
* A [connector image](#connector-images) that is deployed with an application and contains the logic of the connector.

### Connector definitions

Connector definitions are the templates for modeling a connector. The definitions are where the input and output parameters are set for the connector to send and receive variables from an external source or system.

Connector definitions are stored as JSON files in the format `<connector-name>.json` and can be modeled in the GUI or the **JSON Editor**.

The basic properties for connector definitions are:

| Property | Description | Example |
| -------- | ----------- | ------- |
| `ID` | *Required.* The unique identifier for a connector. This is system generated and cannot be altered. | `connector-50991833-6231-4052-9d1b-170117f90165` |
| `Name` | *Required.* The name of the connector. Connector names must be in lowercase and between 1 and 26 characters in length. Alphanumeric characters and hyphens are allowed, however the name must begin with a letter and end alphanumerically. | `email-connector-1` |
| `Description` | *Optional.* A free text description of what the connector does | `A connector to send emails as part of a process.` |

Connector definitions can contain [actions](#actions), [events](#events) and [configuration parameters](#configuration-parameters).

#### Actions

Actions are the operations a connector can take. Connector definitions can have multiple actions, however only one action can be executed by each [service task](../bpmn/service.md). Connector actions are attached to service tasks using the `implementation` attribute with a value in the format `<connector-name>.<action-name>`, for example:

```xml
<bpmn2:serviceTask id="ServiceTask_3xcd7zp" implementation="slackConnector.SEND_MESSAGE" />
```

The basic properties for actions are:

| Property | Description | Example |
| -------- | ----------- | ------- |
| `ID` | *Required.* The unique identifier for an action. This is system generated and cannot be altered. | `647e0849-4937-4189-9650-eff4aa081979` |
| `Name` | *Required.* The name of the action | `SEND_MESSAGE` |
| `Description` | *Optional.* A free text description of what the action does | `Sends a message to a Slack channel.` |

Each action has a set of input parameters and output parameters. Input parameters are the values sent from a process to the connector and output parameters are the ones returned to the process after the connector has executed its logic. Values are defined in a service task using [process variables](../processes/variables.md), values or an expression.

The properties for input and output parameters are:

| Property | Description | Example |
| -------- | ----------- | ------- |
| `Name` | *Required.* The name of the parameter | `userId` |
| `Description` | *Optional.* A free text description of the parameter | `The ID of a Slack user` |
| `Type` | *Required.* The data type of the parameter | `String` |
| `Required` | *Optional.* Set whether the parameter requires a value when being used | `true` |

Actions are stored in the `actions` section of the connector JSON, for example in an excerpt of the [Slack connector](slack.md) `SEND_MESSAGE` event:

```json
    "actions": {
        "88296a50-f6cf-496e-b433-5d794788fc8f": {
            "id": "88296a50-f6cf-496e-b433-5d794788fc8f",
            "name": "SEND_MESSAGE",
            "description": "Sends a standalone message to a Slack conversation. Conversations can be public or private channels, or direct messages.",
            "inputs": [
                {
                    "id": "f7435a5c-20bd-46e4-9d26-901a9dabb87c",
                    "name": "userId",
                    "description": "Internal Slack user id. If present, the message will be sent as a direct message.",
                    "type": "string"
                },
...
            ],
            "outputs": [
                {
                    "id": "c9daca61-6ecd-4dd2-b8b0-f1f99589cd52",
                    "name": "slackError",
                    "description": "If present, it describes the error occurred trying to send the message.",
                    "type": "string"
                },
...
            ]
        },
```


#### Events

Events are used by [triggers](../triggers.md) to configure a connector event that can be listened for and published by a trigger.

The basic properties for events are:

| Property | Description | Example |
| -------- | ----------- | ------- |
| `ID` | *Required.* The unique identifier for an event. This is system generated and cannot be altered. | `62bfa43e-a495-4786-9495-1e24eedf1a1f` |
| `Name` | *Required.* The name of the event | `EMAIL_RECEIVED` |
| `Description` | *Optional.* A free text description of what the event does | `An event that is dispatched when an email is received.` |

Events contain input and output parameters that define the properties used by a trigger. Input parameters are used to set the criteria for event publishing and any notification of matches. Output parameters are variables that can be used in the payload of [trigger actions](../triggers.md#actions).  

The properties for input and output parameters are:

| Property | Description | Example |
| -------- | ----------- | ------- |
| `Name` | *Required.* The name of the parameter | `pattern` |
| `Description` | *Optional.* A free text description of the parameter | `A regular expression to match against incoming messages` |
| `Type` | *Required.* The data type of the parameter | `String` |
| `Required` | *Optional.* Set whether the parameter requires a value when being used | `true` |

Events are stored in the `events` section of the connector JSON, for example in an excerpt of the [email connector](email.md) `EMAIL_RECEIVED` event:

```json
"events": {
        "62bfa43e-a495-4786-9495-1e24eedf1a1f": {
            "id": "62bfa43e-a495-4786-9495-1e24eedf1a1f",
            "name": "EMAIL_RECEIVED",
            "description": "Event that is dispatched when an email is received",
            "inputs": [
                {
                    "id": "3dbe2c22-dfc2-41c6-a576-7797f9fbeb62",
                    "name": "pattern",
                    "description": "Regular expression that any incoming message shall match in order to be published as events. Regular expressions can contain matching groups delimited by '(' and ')'. Matching groups can be used in variables and the echo message.",
                    "type": "string"
                },
...
            ],
            "outputs": [
                {
                    "id": "fa6b0f2a-ca79-476b-ba4e-f0f082eff47c",
                    "name": "matchGroups",
                    "description": "Matching groups between pattern and message. They can be used in variables and the echo messages.",
                    "type": "json"
                },
...
            ]
        }
    },
```

#### Configuration parameters

Configuration parameters are the environment variables specific to each connector instance that are set at deployment time. They set values such as the SMTP host and port each instance of the [email connector](email.md) will use.

> **Note**: Additional configuration parameters can be specified at deployment time and existing parameters set during the modeling experience can be overridden.

The basic properties for configuration parameters are:

| Property | Description | Example |
| -------- | ----------- | ------- |
| `Name` | The name of the parameter | `SLACK_XOXB` |
| `Description` | A free text description of what the parameter is for | The Slack bot user token. |
| `Value` | An optional default value for the parameter. This can be overridden at deployment time. | `xoxb-` |
| `Required` | Set whether the parameter requires a value when being used | `true` |

Configuration parameters are stored in the `config` section of the connector JSON, for example in an excerpt of the [Slack connector](slack.md):

```json
    "config": [
        {
            "name": "SLACK_XOXB",
            "description": "Slack bot user token",
            "value": "",
            "required": true

        },
        {
            "name": "SLACK_XOXP",
            "description": "Slack admin user token",
            "value": "",
            "required": true
        }
    ],
```

### Connector images

Connectors are deployed as separate Docker images with an application. Connectors execute their logic outside of the application runtime bundle, with communication between the connector and the application runtime bundle using the message broker, by default Rabbit MQ.

## Modeling connectors

Available connectors can be selected directly from the palette when modeling a process.

1. Select the connector from the connector palette.

2. Choose whether to create a new instance of the connector or use an existing one.

    > **Note**: Multiple actions linked to different [service tasks](../bpmn/service.md) can use the same instance of a connector image. Different instances of a connector are only required if you need to use different [connector variables](#connector-variables).

3. Choose the `Action` your connector will use for that service task.

    > **Note**: Details of the actions are described for each connector in their respective pages.

4. Assign the input and output parameters for the connector using [process variables](../processes/variables.md), static values or an expression.

5. Name the service task and complete your process definition model.

6. Save the process definition.
