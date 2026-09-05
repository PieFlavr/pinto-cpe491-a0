# Inspection record

Replace every bracketed prompt with your own observation. Keep output excerpts short.

## Part 1: First observation

**What appears to be happening?**  
`ros2 run demo_nodes_py talker` seems to output a "Hello World" every second, with the count of how many messages it has sent so far being put next to it.

`ros2 run demo_nodes_py listener` seems to listen and copies, and outputs the message the Talker is publishing.

Notably, it seems the actual Message the Talker is publishing is specifically the Hello World message (*see the observation for more detail*). This is because the overlapping message aside from the informational block is simply the "Hello World: X" message for both Listener and Talker.

**What did you observe that supports this?**  
On the Talker terminal, it outputs `Publishing: "Hello World: X"`, where X is an always ascending number corresponding to the number of messages so far (i.e. the count published messages so far).

On the Listener terminal, it outputs `I heard: [Hello World: X]`, wherein the latest message with X corresponds to the latest Talker's X.

On both terminals, it also outputs a preceding informational message to the above formatted as `[INFO] [NNNNNNNNNN.MMMMMMMMM] [type]`, wherein the sequence of Ns is the same for both, the sequence of Ms is roughly close but always different, and `type` being replaced by `talker` and `listener` respectively.

See the following image for better clarification.

![alt text](evidence/part_1.png)

## Part 2: Standard demo

### Running nodes

**Command:** `[command]`

```text
[relevant output]
```

**Interpretation:** [What does this tell you?]

### Connections and message type

**Commands:**

```text
[commands]
```

```text
[relevant output]
```

**Interpretation:** [Identify the publisher, subscriber, topic, and message structure.]

### Message and rate

**Commands:**

```text
[commands]
```

```text
[relevant output]
```

**Interpretation:** [Describe one message and the approximate rate.]

## Part 4: Your status system

### Nodes and topic

**Commands and relevant output:**

```text
[commands and output]
```

**Interpretation:** [Explain how this supports the required node names, topic, type, publisher, and subscriber.]

### Message and rate

**Commands and relevant output:**

```text
[commands and output]
```

**Interpretation:** [Explain how this supports the required message content and 4 Hz rate.]

## Part 6: Your count system

**Commands and relevant output:**

```text
[commands and output]
```

**Interpretation:** [Explain how this supports the node names, /lab0/count topic, Int32 type, publisher/subscriber connection, increasing values, and 1 Hz rate.]

## CPE 691 extension

Delete this section if you are enrolled in CPE 491.

```text
[output of ros2 topic info /lab0/status --verbose]
```

```text
[output of ros2 topic info /lab0/count --verbose]
```
