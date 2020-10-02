---
title:  Errors, messages, signals and timers
---

Errors, messages, signals and timers are the four main ways of changing the behavior of standard BPMN elements.

* Errors are used to model business exceptions in a process.
* Messages are used to send a payload between throwing and catching message events.
* Signals are thrown and caught by different elements within a process instance or a project.
* Timers are used to begin or interrupt events at specific times or intervals.

## Errors

Error events are used to model an exception in a business process. Errors are thrown by error end events and caught by error start events and error boundary events.

The `errorRef` property in the `errorEventDefinition` of an error event element will match against the `id` of an error when viewing the **XML Editor**.

Error events are graphically represented by a lightning bolt icon inside different shapes that differentiate between the event types. A solid lightning bolt represents a throwing event, whilst a hollow lightning bolt represents a catching event.

To create a new error use the **+** symbol against an error event such as a start error event, or make sure no BPMN element is selected by clicking on a blank section of the process canvas and the **Edit Errors** button will be visible in the right-hand properties panel.

### Types of error events

The types of error events are:

* [Error start events]({% link process-automation/latest/model/bpmn/start-end.md %}#error-start-events)
* [Error end events]({% link process-automation/latest/model/bpmn/start-end.md %}#error-end-events)
* [Error boundary events](LINK)

### Error XML

An example of the XML of an error is:

```xml
<bpmn2:error id="Error_04mep1k" name="payment-error" errorCode="404" />
```

## Messages

Messages have a name and contain a payload. They are sent by message throwing events and received by message catching events in a 1:1 relationship between throw events and catch events. Messages contain a payload known as a [message payload](#message-payloads) and can be passed between scopes, for example between two different [pools](LINK).

The message `id` property of a message is matched against the `messageRef` property in the corresponding throw and catch message elements when viewing the **XML Editor**.

To create a new message use the **+** symbol against a message event such as a message boundary event, or make sure no BPMN element is selected by clicking on a blank section of the process canvas and the **Edit Messages** button will be visible in the right-hand properties panel.

Message events are graphically represented by an envelope icon inside different shapes that differentiate between the event types. A solid envelope represents a throwing event, whilst a hollow envelope represents a catching event.

### Message payloads

Message payloads contain a set of values that are sent from a throwing event and received by a catching event.

Message payloads are created on a message throw event and contain one or more properties that have a `name`, `type` and `value`. The property types for payloads are:

| Type | Description |
| ---- | ----------- |
| String | A sequence of characters, for example `#Mint-Ice-Cream-4!` |
| Integer | A positive whole number, for example `642` |
| Boolean | A value of either `true` or `false` |
| Date | A specific date in the format `YYYY-MM-DD`, for example `2020-04-22` |
| Variable | A value passed from a [process variable]({% link process-automation/latest/model/processes.md %}#process-variables). |

The receiving message catch event is then used to map the received values in the payload to process variables in its own scope.

Message payload mappings can be viewed in the **Extensions Editor** of a process diagram. Throwing events are mapped as `inputs` and catching events are mapped as `outputs` from an event.

### Correlation keys

Message events can optionally contain a correlation key. If a correlation key is present then when a message is thrown it uses the `activiti:correlationKey` value and the `messageRef` of the throwing event to match against the same two properties in a catching event. If only one property is matched then the message will not be caught.

Using a [process variable]({% link process-automation/latest/model/processes.md %}#process-variables) for the correlation key in a throwing event and a static value for its corresponding catching event allows for the message to only be caught in specific circumstances.

> **Note**: Message start events cannot contain a correlation key unless they are used in a [sub process](LINK).

### Message flows

When messages are used between two different [pools](LINK) the sequence flow that connects them is a dotted line called a message flow. The message flow is part of the `collaboration` element in the XML created by introducing a pool. Message flows reference the throwing message event as the `sourceRef` and the catching message event as the `targetRef`.

### Types of message events

The types of message events are:

* [Message end events]({% link process-automation/latest/model/bpmn/start-end.md %}#message-end-events)
* [Message intermediate catch events](LINK)
* [Message intermediate throw events](LINK)
* [Message start events]({% link process-automation/latest/model/bpmn/start-end.md %}#message-start-events)
* [Message boundary events](LINK)

### Message XML

An example of the XML of a message is:

```xml
<bpmn2:message id="Message_0k9hibo" name="payment-message" />
```

An example of the XML of a message payload is:

```json
    "mappings": {
        "EndEvent_0ss2fp3": {
            "inputs": {
                "name": {
                    "type": "variable",
                    "value": "username"
                },
                "order-number": {
                    "type": "value",
                    "value": 1459283
                }
            }
        }
    },
```

An example of the XML of a message with a correlation key is:

```xml
<bpmn2:endEvent id="EndEvent_1">
	<bpmn2:incoming>SequenceFlow_8</bpmn2:incoming>
	<bpmn2:messageEventDefinition messageRef="Message_1hxecs2" activiti:correlationKey="${userId}" />
```

In this example the message will only be caught if a catching event has a `messageRef` of `Message_1hxecs2` and an `activiti:correlationKey` that matches the value of `userId`.

An example of the XML of a message flow is:

```xml
<bpmn2:collaboration id="Collaboration_0kgbwi1">
	<bpmn2:participant id="Participant_1i6u1my" processRef="Process_1d9yxsm" />
	<bpmn2:participant id="Participant_10umhbc" processRef="Process_1piiyp4" />
	<bpmn2:messageFlow id="MessageFlow_0vh4zdb" sourceRef="Event_00acemq" targetRef="Event_13u5jtf" />
</bpmn2:collaboration>
```

## Signals











Signal events can be either catching or throwing. A throwing signal event will emit a signal when it is reached in a process instance that will be picked up by any catching signal event with a matching signal name. Signals can be restricted to the process instance they are thrown in, or be global in scope. The scope of a global signal is restricted to the project they are used in.

The `id` of a signal will match against the `signalRef` of a catching or throwing event.

Signal events are graphically represented by a triangle icon inside different shapes that differentiate between the event types. A solid triangle represents a throwing event, whilst a hollow triangle represents a catching event.

The XML representation of a signal is the following:

```xml
<bpmn2:signal id="Signal_10meg5t" name="notification" />
```

The following are signal events:

* [Signal intermediate throw events](LINK)
* [Signal intermediate catch events](LINK)
* [Signal start events](LINK)
* [Signal boundary events](LINK)


The XML representation of a signal with a global scope is:

```xml
<bpmn2:signal id="Signal_0hnsd2r" name="Signal_0hnsd2r" />
```

The XML representation of a signal with a process instance scope is:

```xml
<bpmn2:signal id="Signal_0hnsd2r" name="Signal_0hnsd2r" activiti:scope="processInstance" />
```






Timer events are used to influence events at specific times, after a set amount of time has passed or at intervals. All timer events use the international standard [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601){:target="_blank"} for specifying time formats.

Timer events are graphically represented by a clock icon inside different shapes that differentiate between the event types.

The following are timer events:

* [Timer start events](start-end.md#timer-start-events)
* [Timer boundary events](boundary.md#timer-boundary-events)
* [Timer intermediate catch events](#timer-intermediate-catch-events)

All timer events require either a [`timeDate`](#timedate), [`timeDuration`](#timeduration) or [`timeCycle`](#timecycle) property included within the `timerEventDefinition` to define the timer trigger behavior.

## timeDate

The `timeDate` property for timer events defines a specific date and time in ISO 8601 format for when the trigger will be fired and can include a specified time zone.

The following is an example of the `timerEventDefinition` using a `timeDate`:

* `2017-05-17` represents the 17th May 2017 in *YYYY-MM-DD* format
* `T12:42:23` represents the time of 12:42:23 in *hh:mm:ss* format
* `Z` represents that the time format is in UTC (Coordinated Universal Time). The time can also contain UTC offsets such as `+01` for an hour ahead of UTC. When an offset is defined the `Z` is not required, for example: `T12:42:23+01`

```xml
<bpmn2:timerEventDefinition> 
  <bpmn2:timeDate xsi:type="bpmn2:tFormalExpression">2017-05-17T12:42:23Z</bpmn2:timeDate>
</bpmn2:timerEventDefinition>
```

## timeDuration

The `timeDuration` property for timer events defines how long a timer should wait in ISO 8601 format before the trigger is fired.

The following are the letters used to refer to duration:

| Letter | Description | Example | 
| ------ | ----------- | ------- |
| `P` | Designates that the following letters and numbers represent a duration. Must always be present | |
| `Y` | Represents a year and follows the number of years | `P2Y` for 2 years |
| `M` | Represents a month and follows the number of months when preceded by a `P` | `P3Y4M` for 2 years and 4 months |
| `W` | Represents a week and follows the number of weeks | `P10W` for 10 weeks |
| `D` | Represents a day and follows the number of days | `P1Y1M1D` for 1 year, 1 month and 1 day |
| `T` | Designates that the following letters represent a duration of hours to seconds. Must always be present to refer to hours, minutes and seconds | 
| `H` | Represents an hour and follows the number of hours | `P1DT0.5H` for 1 day and half an hour |
| `M` | Represents a minute and follows the number of minutes when preceded by a `T` | `PT1M` for 1 minute |
| `S` | Represents a second and follows the number of seconds | `P2Y3M4DT5H6M7S` for 2 years, 3 months, 4 days, 5 hours, 6 minutes and 7 seconds |

The following is an example of the `timerEventDefinition` using a `timeDuration` to represent a duration of 5 days: 

```xml
<bpmn2:timerEventDefinition>
  <bpmn2:timeDuration xsi:type="bpmn2:tFormalExpression">P5D</bpmn2:timeDuration>
</bpmn2:timerEventDefinition>
```

## timeCycle

The `timeCycle` property for timer events defines intervals for the trigger to fire at. Intervals can be defined using the [time intervals](#time-intervals) that adhere to the ISO 8601 standard or by using [cron expressions](#cron-expression-intervals).

### Time intervals

Time intervals use the syntax `R/` to set a number of repetitions, for example `R5/` would repeat five times. 

Following the repetition, a duration can be set for when the repetition occurs, for example `R5/PT10H` would repeat every 10 hours, five times. 

> **Note** The duration uses the same format as for [`timeDuration`](#timeduration).

An optional end date can also be set after the duration and separated by a `/`.

> **Note**: The end date uses the same format as for [`timeDate`](#timedate).

The following is an example of the `timerEventDefinition` using time interval syntax for `timeCycle` to represent three repetitions every 30 minutes:

``` xml
<bpmn2:timerEventDefinition>
  <bpmn2:timeCycle xsi:type="bpmn2:tFormalExpression">R3/PT30M</bpmn2:timeCycle>
</bpmn2:timerEventDefinition> 
```

### Cron expression intervals

[Cron expressions](https://en.wikipedia.org/wiki/Cron#CRON_expression){:target="_blank"} can be used to define repeating triggers for timer events.  

The following is an example of the `timerEventDefinition` using a cron expression for `timeCycle` to represent a trigger firing every 5 minutes beginning at the top of the hour:

```xml
<bpmn2:timerEventDefinition>
  <bpmn2:timeCycle>0 0/5 * * * ?</bpmn2:timeCycle>
</bpmn2:timerEventDefinition>
```

## Timer expressions

All properties within `timerEventDefinition` can accept process variables as their values as long as they are in ISO 8601 or cron expression format.

The following is an example of the process variable `{$duration}` being used:

```xml
<bpmn2:timerEventDefinition>
	<bpmn2:timeDuration xsi:type="bpmn2:tFormalExpression">${duration}</bpmn2:timeDuration>
</bpmn2:timerEventDefinition>
```




