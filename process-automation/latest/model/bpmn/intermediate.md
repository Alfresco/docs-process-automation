## Message intermediate catch events

Message intermediate catching events cause the process flow to wait until the message named in the `messageRef` property is received before it proceeds.

When used in the Modeling Application, a previously created `Message` can be selected from the dropdown in its properties, or a new one created using the `+` symbol.

Message intermediate catching events are graphically represented by two thin concentric circles with a hollow envelope icon inside.

The XML representation of message intermediate catching events is:

```xml
<bpmn2:intermediateCatchEvent id="IntermediateCatchEvent2">
	<bpmn2:incoming>SequenceFlow_5</bpmn2:incoming>
	<bpmn2:outgoing>SequenceFlow_6</bpmn2:outgoing>
    <bpmn2:messageEventDefinition messageRef="Message_6" />
</bpmn2:intermediateCatchEvent>
```

## Message intermediate throw events

Message intermediate throw events send the message event named in the `messageRef` property when the process flow reaches them.

When used in the Modeling Application, a previously created `Message` can be selected from the dropdown in its properties, or a new one created using the `+` symbol

Message intermediate throwing events are graphically represented by two thin concentric circles with a solid envelope icon inside.

The XML representation of message intermediate throwing events is:

```xml
<bpmn2:intermediateThrowEvent id="IntermediateThrowEvent1">
	<bpmn2:incoming>SequenceFlow_5</bpmn2:incoming>
	<bpmn2:outgoing>SequenceFlow_6</bpmn2:outgoing>
    <bpmn2:messageEventDefinition messageRef="Message_6" />
</bpmn2:intermediateThrowEvent>
```







## Signal intermediate catch events

Signal intermediate catching events cause the process flow to wait until the signal named in the `signalRef` property is received before it proceeds.

When used in the Modeling Application, a previously used `Signal` can be selected from the dropdown in its properties, or a new one created using the `+` symbol. Signals can be restricted to the process instance they are thrown in, or be global in scope. The scope of a global signal is restricted to the application they are used in.

Signal intermediate catching events are graphically represented by two thin concentric circles with a hollow triangle icon inside.

The XML representation of signal intermediate catching events is:
	
```xml
<bpmn2:intermediateCatchEvent id="IntermediateCatchEvent2">
	<bpmn2:incoming>SequenceFlow_5</bpmn2:incoming>
	<bpmn2:outgoing>SequenceFlow_6</bpmn2:outgoing>
    <bpmn2:signalEventDefinition signalRef="Signal_0hnsd2r" />
</bpmn2:intermediateCatchEvent>
```


## Signal intermediate throw events

Signal intermediate throwing events are events that emit a signal when they are reached in the process flow. The signal that is emitted is then caught by any catching signal events with a name matching the signal that was thrown.

When used in the Modeling Application, a previously used `Signal` can be selected from the dropdown in its properties, or a new one created using the `+` symbol. Signals can be restricted to the process instance they are thrown in, or be global in scope. The scope of a global signal is restricted to the application they are used in.

Signal intermediate throwing events are graphically represented by two thin concentric circles with a solid triangle icon inside.

The XML representation of signal intermediate throwing events is:

```xml
<bpmn2:intermediateThrowEvent id="IntermediateThrowEvent1">
	<bpmn2:incoming>SequenceFlow_3</bpmn2:incoming>
	<bpmn2:outgoing>SequenceFlow_4</bpmn2:outgoing>
   <bpmn2:signalEventDefinition signalRef="Signal_1jiw9tp" />
</bpmn2:intermediateThrowEvent>
```


## Timer intermediate catch events

Timer intermediate catching events cause the process flow to wait until a specific time or interval is reached. The time to wait is defined in the `timerEventDefinition` property.

Timer intermediate catching events are graphically represented by two thin concentric circles with a clock icon inside.

The XML representation of timer intermediate catching events is:

```xml
<bpmn2:intermediateCatchEvent id="IntermediateCatchEvent5">
	<bpmn2:incoming>SequenceFlow_3</bpmn2:incoming>
	<bpmn2:outgoing>SequenceFlow_4</bpmn2:outgoing>
	<bpmn2:timerEventDefinition>
  		<bpmn2:timeDuration xsi:type="bpmn2:tFormalExpression">P5D</bpmn2:timeDuration>
	</bpmn2:timerEventDefinition>
</bpmn2:intermediateCatchEvent>
```

> **Note**: This will wait five days before continuing the process.