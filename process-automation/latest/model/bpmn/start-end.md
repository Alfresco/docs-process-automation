---
title: Start and end events
---



End events indicate where the current process flow ends, therefore there can be no outgoing [sequence flow](LINK) from an end event. Different types of end event can have have actions other than just ending the process flow execution path.

## Start events

Start events are where the trigger is unspecified for starting a process. The trigger can be using a form, manually through the Digital Workspace, using the REST API or from a [trigger](LINK).

Start events are graphically represented by a single thin circle without an icon inside.

### Start event basic properties

The basic properties for a start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the start event does. |

### Start event form name

An optional [form]({% link process-automation/latest/model/form.md %}) can be used to begin a process. The form must exist within the same project as the process definition to be selected. Select a form from the dropdown, else create a new form using the **+** symbol.

Once a form has been selected, it can be edited using the **Open Form** symbol.

### Start event mapping type

The mapping type sets how data is passed between the start event and the process. There are [five options](%{ link process-automation/latest/model/processes.md %}#process-variable-mapping) for how to send this data. The default value is **Send no variables**.

### Start event XML

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

## Error start events

Error start events can only be used in [event sub-processes](LINK). They begin an event sub-processes when a named error is received.

Error start events are graphically represented by a single thin circle with a hollow lightning bolt icon inside.

### Error start event basic properties

The basic properties for an error start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the error start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the error start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the error start event does. |

### Error start event form name

An optional [form]({% link process-automation/latest/model/form.md %}) can be used to begin a process. The form must exist within the same project as the process definition to be selected. Select a form from the dropdown, else create a new form using the **+** symbol.

Once a form has been selected, it can be edited using the **Open Form** symbol.

### Error start event mapping type

The mapping type sets how data is passed between the error start event and the process. There are [five options](%{ link process-automation/latest/model/processes.md %}#process-variable-mapping) for how to send this data. The default value is **Send no variables**.

### Error start event errors

An error needs to be defined for the error start event to catch. A previously created **Error** can be selected from the dropdown in its properties, or a new one created using the **+** symbol. An **Error name** and **Error code** can then be set.

See [error events](LINK) for more information regarding error events and how they can be caught.

### Error start event XML

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

## Message start events

Message start events begin a process instance when a named message is received.

Message start events are graphically represented by a single thin circle with a hollow envelope icon inside.

### Message start event basic properties

The basic properties for a message start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the message start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the message start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the message start event does. |

### Message start event form name

An optional [form]({% link process-automation/latest/model/form.md %}) can be used to begin a process. The form must exist within the same project as the process definition to be selected. Select a form from the dropdown, else create a new form using the **+** symbol.

Once a form has been selected, it can be edited using the **Open Form** symbol.

### Message start event mapping type

The mapping type sets how data is passed between the message start event and the process. There are [five options](%{ link process-automation/latest/model/processes.md %}#process-variable-mapping) for how to send this data. The default value is **Send no variables**.

### Message start event messages

A message needs to be defined for the message start event to pick up when it is thrown. A previously created **Message** can be selected from the dropdown in its properties, or a new one created using the **+** symbol. A **Message name** and payload can then be set.

See [message events](LINK) for more information regarding messages and how they can be generated.

### Message start event XML

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

## Signal start events

Signal start events begin a process instance using a caught, named signal.

Signal start events are graphically represented by a single thin circle with a hollow triangle icon inside.

### Signal start event basic properties

The basic properties for a signal start event are:

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the signal start event. This is system generated and cannot be altered, for example `StartEvent_1w29b3h`. |
| Name | *Optional.* The name of the signal start event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the signal start event does. |

### Signal start event signals

A signal needs to be defined for the signal start event to catch. A previously used **Signal** can be selected from the dropdown in its properties, or a new one created using the **+** symbol. A **Signal name** can then be set.

Signals can be restricted to the process instance they are thrown in, or be global in scope. The scope of a global signal is restricted to the project they are used in.

See [signal events](LINK) for more information regarding signals and how they can be thrown.

### Signal start event XML

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

## End events

End events complete the process flow with no additional behavior.

End events are graphically represented by a single thick circle without an icon inside.

### End event basic properties

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the end event. This is system generated and cannot be altered, for example `EndEvent_00ln22h`. |
| Name | *Optional.* The name of the end event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the end event does. |

### End event XML

An example of the XML of an end event is:

```xml
<bpmn2:endEvent id="EndEvent_1">
    <bpmn2:incoming>SequenceFlow_1</bpmn2:incoming>
</bpmn2:endEvent>
```

## Error end events

Error end events throw an error when the process flow reaches them.

Error end events are graphically represented by a single thick circle with a solid lightning bolt icon inside.

### Error end event basic properties

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the error end event. This is system generated and cannot be altered, for example `EndEvent_00ln22h`. |
| Name | *Optional.* The name of the error end event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the error end event does. |

### Error end event errors

An error needs to be defined for the error end event to throw. A previously created **Error** can be selected from the dropdown in its properties, or a new one created using the **+** symbol. An **Error name** and **Error code** can then be set.

See [error events](LINK) for more information regarding error events and how they can be thrown.

### Error end event XML

An example of the XML of an error end event is:

```xml
<bpmn2:endEvent id="EndEvent_1">
    <bpmn2:incoming>SequenceFlow_8</bpmn2:incoming>
    <bpmn2:errorEventDefinition errorRef="Error_3vbkafg" />
</bpmn2:endEvent>
```

An example of the XML of an error is:

```xml
<bpmn2:error id="Error_3vbkafg" name="payment-failed-error" errorCode="404" />
```

## Message end events

Message end events complete the process flow and send a message event.

Message end events are graphically represented by a single thick circle with a solid envelope icon inside.

### Message end event basic properties

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the message end event. This is system generated and cannot be altered, for example `EndEvent_00ln22h`. |
| Name | *Optional.* The name of the message end event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the message end event does. |

### Message end event messages

A message needs to be defined for the message end event to send. A previously created **Message** can be selected from the dropdown in its properties, or a new one created using the **+** symbol. A **Message name** and payload can then be set.

See [message events](LINK) for more information regarding messages and how they can be generated.

### Message end event XML

An example of the XML of a message end event is:

```xml
<bpmn2:endEvent id="EndEvent_1">
	<bpmn2:incoming>SequenceFlow_1</bpmn2:incoming>
	<bpmn2:messageEventDefinition messageRef="Message_45sdihj" />
</bpmn2:endEvent>
```

## Terminate end events

Terminate end events cause the current process scope to be immediately ended, including any parallel process flows. The scope is determined by the location of the terminate end event. If the terminate end event is in a [sub-process](LINK) or [call activity](LINK), only the sub-process or call activity instance will be ended, not the parent or originating process instance. In the case of a multi-instance sub-process or call activity only a single instance will be ended.

Terminate end events are graphically represented by a single thick circle with a solid circle inside.

### Terminate end event basic properties

| Property | Description |
| -------- | ----------- |
| ID | *Required.* The unique identifier for the terminate end event. This is system generated and cannot be altered, for example `EndEvent_00ln22h`. |
| Name | *Optional.* The name of the terminate end event. This will be displayed on the canvas. |
| Documentation | *Optional.* A free text description of what the terminate end event does. |

### Terminate end event XML

An example of the XML of a terminate end event is:

```xml
<bpmn2:endEvent id="EndEvent_1">
	<bpmn2:incoming>SequenceFlow_1</bpmn2:incoming>
	<bpmn2:terminateEventDefinition id="TerminateEventDefinition_0j911ut"/>
</bpmn2:endEvent>
```
