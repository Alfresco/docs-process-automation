---
title: BPMN
---








## Start events

A process must always contain at least one start event as they define how a process begins.

### Start event

Start events are where the trigger is unspecified for starting a process. The trigger can be using a form, manually through the Digital Workspace, using the REST API or from a [trigger](LINK).

{% capture start-prop %}

#### Basic properties

The basic properties for a start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the start event does. |

#### Form name

An optional [form]({% link process-automation/latest/model/form.md %}) can be used to begin a process. The form must exist within the same project as the process definition to be selected. Select a form from the dropdown, else create a new form using the **+** symbol.

Once a form has been selected, it can be edited using the **Open Form** symbol.

#### Mapping type

The mapping type sets how data is passed between the start event and the process. There are [five options](%{ link process-automation/latest/model/processes.md %}#process-variable-mapping) for how to send this data. The default value is **Send no variables**.

{% endcapture %}
{% capture start-img %}

Start events are graphically represented by a single thin circle without an icon inside.

{% endcapture %}
{% capture start-xml %}

An example of the XML of a start event without a form defined is:

```xml
<bpmn2:startEvent id="StartProcess_1" name="FormStart_4">
	<bpmn2:outgoing>SequenceFlow_1</bpmn2:outgoing>
</bpmn2:startEvent>
```

An example of the XML of a start event with a form defined is:

```xml
<bpmn2:startEvent id="StartProcess_1" name="FormStart_4" activiti:formKey="form-4ccd023b-d607-4cab-8623-da4c87dd9611">
	<bpmn2:outgoing>SequenceFlow_1</bpmn2:outgoing>
</bpmn2:startEvent>
```

> **Note**: The `activiti:formKey` is the `id` of the form used to start the process.

{% endcapture %}

{% include tabs.html tableid="start" opt1="Properties" content1=start-prop opt2="Appearance" content2=start-img opt3="XML" content3=start-xml %}

### Error start events

Error start events can only be used in [event sub-processes](LINK). They begin an event sub-processes when a named error is received.

{% capture error-start %}

#### Basic properties

The basic properties for an error start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the error start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the error start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the error start event does. |

#### Form name

An optional [form]({% link process-automation/latest/model/form.md %}) can be used to begin a process. The form must exist within the same project as the process definition to be selected. Select a form from the dropdown, else create a new form using the **+** symbol.

Once a form has been selected, it can be edited using the **Open Form** symbol.

#### Mapping type

The mapping type sets how data is passed between the error start event and the process. There are [five options](%{ link process-automation/latest/model/processes.md %}#process-variable-mapping) for how to send this data. The default value is **Send no variables**.

#### Error

An error needs to be defined for the error start event to catch. A previously created **Error** can be selected from the dropdown in its properties, or a new one created using the **+** symbol. An **Error name** and **Error code** can then be set.

{% endcapture %}
{% capture error %}

Error events are used to model an exception in a business process. Errors are thrown by error end events and caught by error start events and error boundary events.

The `errorRef` property in the `errorEventDefinition` of an error event element will match against the `id` of an error when viewing the **XML Editor**.

Error events are graphically represented by a lightning bolt icon inside different shapes that differentiate between the event types. A solid lightning bolt represents a throwing event, whilst a hollow lightning bolt represents a catching event.

To create a new error use the **+** symbol against an error event such as a start error event, or make sure no BPMN element is selected by clicking on a blank section of the process canvas and the **Edit Errors** button will be visible in the right-hand properties panel.

{% endcapture %}
{% capture error-start-img %}

Error start events are graphically represented by a single thin circle with a hollow lightning bolt icon inside.

{% endcapture %}
{%capture error-start-xml %}

An example of the XML of an error start event is:

```xml
<bpmn2:startEvent id="StartEvent3">
	<bpmn2:errorEventDefinition errorRef="Error_0vbkbeb" />
</bpmn2:startEvent>
```

An example of the XML of an error is:

```xml
<bpmn2:error id="Error_0vbkbeb" name="payment-failed-error" errorCode="404" />
```

{% endcapture %}

{% include tabs.html tableid="error-start" opt1="Properties" content1=error-start-prop opt2="Error" content2=error opt3="Appearance" content3=error-start-img opt4="XML" content4=error-start-xml %}

### Message start events

Message start events begin a process instance when a named message is received.

{% capture message-start-prop %}

#### Basic properties

The basic properties for a message start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the message start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the message start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the message start event does. |

#### Form name

An optional [form]({% link process-automation/latest/model/form.md %}) can be used to begin a process. The form must exist within the same project as the process definition to be selected. Select a form from the dropdown, else create a new form using the **+** symbol.

Once a form has been selected, it can be edited using the **Open Form** symbol.

#### Mapping type

The mapping type sets how data is passed between the message start event and the process. There are [five options](%{ link process-automation/latest/model/processes.md %}#process-variable-mapping) for how to send this data. The default value is **Send no variables**.

#### Message

A message needs to be defined for the message start event to pick up when it is thrown. A previously created **Message** can be selected from the dropdown in its properties, or a new one created using the **+** symbol. A **Message name** and payload can then be set.

{% endcapture %}
{% capture message %}

#### Message

Messages have a name and contain a payload. They are sent by message throwing events and received by message catching events in a 1:1 relationship between throw events and catch events. Messages contain a payload known as a message payload and can be passed between scopes, for example between two different [pools](LINK).

The message `id` property of a message is matched against the `messageRef` property in the corresponding throw and catch message elements when viewing the **XML Editor**.

To create a new message use the **+** symbol against a message event such as a message boundary event, or make sure no BPMN element is selected by clicking on a blank section of the process canvas and the **Edit Messages** button will be visible in the right-hand properties panel.

Message events are graphically represented by an envelope icon inside different shapes that differentiate between the event types. A solid envelope represents a throwing event, whilst a hollow envelope represents a catching event.

#### Message payloads

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

#### Correlation keys

Message events can optionally contain a correlation key. If a correlation key is present then when a message is thrown it uses the `activiti:correlationKey` value and the `messageRef` of the throwing event to match against the same two properties in a catching event. If only one property is matched then the message will not be caught.

Using a [process variable]({% link process-automation/latest/model/processes.md %}#process-variables) for the correlation key in a throwing event and a static value for its corresponding catching event allows for the message to only be caught in specific circumstances.

> **Note**: Message start events cannot contain a correlation key unless they are used in a [sub process](LINK).

#### Message flows

When messages are used between two different [pools](LINK) the sequence flow that connects them is a dotted line called a message flow. The message flow is part of the `collaboration` element in the XML created by introducing a pool. Message flows reference the throwing message event as the `sourceRef` and the catching message event as the `targetRef`.

{% endcapture %}
{% capture message-start-img %}

Message start events are graphically represented by a single thin circle with a hollow envelope icon inside.

{% endcapture %}
{% capture message-start-xml %}

An example of the XML of a message start event is:

```xml
<bpmn2:startEvent id="StartEvent2">
	<bpmn2:outgoing>SequenceFlow_1</bpmn2:outgoing>
	<bpmn2:messageEventDefinition messageRef="Message_15xakkk" />
</bpmn2:startEvent>
```

An example of the XML of a message is:

```xml
<bpmn2:message id="Message_15xakkk" name="Message_15xakkk" />
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

{% endcapture %}

{% include tabs.html tableid="message-start" opt1="Properties" content1=message-start-prop opt2="Message" content2=message opt3="Appearance" content3=message-start-img opt4="XML" content4=message-start-xml %}

### Signal start events

Signal start events begin a process instance using a caught, named signal.

{% capture signal-start-prop %}

#### Basic properties

The basic properties for a signal start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the signal start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the signal start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the signal start event does. |

#### Signal

A signal needs to be defined for the signal start event to catch. A previously used **Signal** can be selected from the dropdown in its properties, or a new one created using the **+** symbol. A **Signal name** can then be set.

Signals can be restricted to the process instance they are thrown in, or be global in scope. The scope of a global signal is restricted to the project they are used in.

{% endcapture %}
{% capture signal %}

Signal events can be either catching or throwing. A throwing signal event will emit a signal when it is reached in a process instance that will be picked up by any catching signal event with a matching signal name. Signals can be restricted to the process instance they are thrown in, or be global in scope. The scope of a global signal is restricted to the project they are used in.

The `id` of a signal will match against the `signalRef` of a catching or throwing event.

Signal events are graphically represented by a triangle icon inside different shapes that differentiate between the event types. A solid triangle represents a throwing event, whilst a hollow triangle represents a catching event.

{% endcapture}
{% capture signal-start-img %}

Signal start events are graphically represented by a single thin circle with a hollow triangle icon inside.

{% endcapture %}
{% capture signal-start-xml %}

An example of the XML of a signal start event is:

```xml
<bpmn2:startEvent id="StartEvent1">
	<bpmn2:outgoing>SequenceFlow_1</bpmn2:outgoing>
 	<bpmn2:signalEventDefinition signalRef="Signal_0hnsd2r" />
</bpmn2:startEvent>
```

An example of the XML of a signal with a global scope is:

```xml
<bpmn2:signal id="Signal_0hnsd2r" name="Signal_0hnsd2r" />
```

An example of the XML of a signal with a process instance scope is:

```xml
<bpmn2:signal id="Signal_0hnsd2r" name="Signal_0hnsd2r" activiti:scope="processInstance" />
```

{% endcapture}

{% include tabs.html tableid="signal-start" opt1="Properties" content1=signal-start-prop opt2="Message" content2=signal opt3="Appearance" content3=signal-start-img opt4="XML" content4=signal-start-xml %}





## Timer start events

Timer start events begin a process at a specific time once or repeatedly at intervals.

Timer start events are graphically represented by a single thin circle with a clock icon inside.

### Timer start event basic properties

The basic properties for a timer start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the timer start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the timer start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the timer start event does. |

### Timer start event form name

An optional [form]({% link process-automation/latest/model/form.md %}) can be used to begin a process. The form must exist within the same project as the process definition to be selected. Select a form from the dropdown, else create a new form using the **+** symbol.

Once a form has been selected, it can be edited using the **Open Form** symbol.

### Timer start event mapping type

The mapping type sets how data is passed between the timer start event and the process. There are [five options](%{ link process-automation/latest/model/processes.md %}#process-variable-mapping) for how to send this data. The default value is **Send no variables**.

### Timer start event timers

A choice of timer must be set for timer start events. See [timer events](timer.md) for more information regarding the different timers and their properties.

### Timer start event XML

An example of the XML of a timer start event is:

```xml
<bpmn2:startEvent id="StartEvent3">
    <bpmn2:outgoing>SequenceFlow_1</bpmn2:outgoing>
    <timerEventDefinition>
        <timeCycle xsi:type="bpmn2:tFormalExpression">R10/2020-12-10T13:00/PT12H</timeCycle>
    </timerEventDefinition>
</bpmn2:startEvent>
```

> **Note**: This will start the process 10 times, at 12 hour intervals starting on the 10th December 2020.
