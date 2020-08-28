---
title: Email connector
---

The email connector is used to send emails using the SMTP protocol as part of a process instance. All the properties of an email can be set using values from the process, such as the recipient and sender and [Freemarker templates](https://freemarker.apache.org/docs/dgui_quickstart_basics.html){:target="_blank"} can be used to generate the email body.

The email connector is graphically represented by an envelope under the connectors menu whilst modeling a process.

The `implementation` value of the email connector in a service task would be similar to the following:

```xml
<bpmn2:serviceTask id="ServiceTask_1che7zm" implementation="emailConnector.SEND" />
```

## Actions

The email connector contains an action called `SEND` that sends an email using an external SMTP host.

### Input parameters

The following are the parameters that can be passed to the email connector as input parameters using the `SEND` action:

| Parameter | Description | Type |
| --------  | ----------- | ---- |
| `to` | *Required.* An email address or list of addresses | String |
| `from`  | *Required.* An email address | String |
| `subject` | *Optional.* A plain text subject | String |
| `html` | *Optional.* An HTML email body | String |
| `text` | *Optional.* A plain text email body | String|
| `template` | *Optional.* A [Freemarker template](https://freemarker.apache.org/docs/dgui_quickstart_basics.html){:target="_blank"} email body added to the process as a [file](../files.md) | File |
| `metadata` | *Optional.* The metadata used by the `template` | JSON |
| `attachments` | *Optional.* Any files to attach to the email | String |
| `cc` | *Optional.* An email address or list of email addresses | String |
| `bcc` | *Optional.* An email address or array of addresses | String |
| `charset` | *Optional.* Define the *charset* of the email | String |

> **Note**: If using a Freemarker template for the email body, process variables can be included in the HTML using the format `${variable-name}`.

### Output parameters

The service task execution is always successful for the email connector. Errors in the connector can be returned using an [error event](../bpmn/error.md).

## Events

The email connector contains an event called `EMAIL_RECEIVED` that can be used by a [trigger](../triggers.md) to configure an action when an email subject line meets a specific pattern.

### Inputs

| Parameter | Description | Example |
| --------  | ----------- | ------- |
| `pattern` | *Required.* A regular expression that selects which emails are published as events. Java catching group syntax can be used to create groups from the pattern as variables  | `Order Number (?<orderNumber>.+)` |
| `echo` | *Optional.* The message sent to the original sender if a message is matched | `Your reference number is ${orderNumber}` |
| `echoError` | *Optional.* The message sent to the user if an error occurs publishing the event | `There was a problem publishing that event.` |

> **Note**: Any groups created in a `pattern` can be referenced in `echo` and `echoError` using the syntax `${groupName}`.

### Outputs

| Parameter | Description | Type |
| --------  | ----------- | ---- |
| `matchGroups` | *Optional.* Any matching groups found using the regular expression in `pattern` | JSON |
| `emailSubject` | *Optional.* The subject of the matched email | String |
| `emailTo` | *Optional.* The recipient of the matched email | String |
| `emailFrom` | *Optional.* The sender of the matched email | String |
| `emailBody` | *Optional.* The message body of the matched email | String |

**Note**: Groups found in `matchGroups` can be used to map to process variables in a [trigger](../triggers.md) by referencing the variable in a JSON field, for example using `${matchGroups.orderNumber}`

## Configuration parameters

Values for configuration parameters that are specific to a connector instance can be set in the modeling application or during application deployment.

The email connector uses the `org.springframework.mail` package for managing communication to the email server. This allows `spring.mail.properties*` to be set to configure the desired email server.

The following are the configuration parameters that need to be set for the email connector:

| Parameter | Description |
| --------- | ----------- |
| `EMAIL_HOST` | The host address of the SMTP server |
| `EMAIL_PORT` | The port the SMTP server is running on |
| `EMAIL_USERNAME` | The username the connector will use to contact the SMTP server |
| `EMAIL_PASSWORD` | The password of the user the connector will use to contact the SMTP server |
| `EMAIL_SMTP_AUTH` | This is a `boolean` value that sets whether the connection to the SMTP server requires authentication |
| `EMAIL_SMTP_STARTTLS` | This is a `boolean` value that sets whether the connection uses TLS |
