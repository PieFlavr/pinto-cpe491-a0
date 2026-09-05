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

![alt text](images/part_1.png)

## Part 2: Standard demo

### Running nodes

NOTE: I am interpreting "record short, relevant excerpts" as NOT the entire terminal, but the specific exact output of each command, cutting out and/or compressing details not discussed in the Interpretation section.

NOTE #2: Additionally, I'm going to interpret each topic section following thereafter to roughly match multiple commands as per the implication of the assignment.

NOTE #3: I also converted the `text` format to `bash` for commands, so it looks nice :D

NOTE #4: I am also assuming the intention is for a hands-on experience, and presumably this means some implicit degree of not looking stuff up, which I will do my best NOT to. 
**Commands:**
NOTE: this was modified to include both "node" commands intentionally.

```bash
ros2 node list
ros2 node info /talker
```

```text
halifulis@Parcae:~$ ros2 node list
/listener
/talker

halifulis@Parcae:~$ ros2 node info/talker
Subscribers:

Publishers:
/chatter: std_msgs/msg/String
... 2 more lines ...
Service Servers:
/talker/describe_parameters: rcl_interfaces/srv/DescribeParameters
... 6 more lines ...

Service Clients:

Action Servers:

Action Clients:

```

**Interpretation:** [What does this tell you?]
`ros2 node list` appears to list all nodes that exist in the environment. The implication of the use of `\` implies that nodes can be nested within one another. Though this is largely unconfirmed by the output given the current "flat" environment.

`ros2 node info /talker` appears to output the interfaces of a node grouped by their type. This is largely implied by the constant reappearance of `rcl_interfaces` across almost all of the information that exists there in similar form as by the `/talker/describe_parameters` listed above.

Additionally, `/chatter` in the `Publishers` section seems to be the Topic that Talker is publishing too. This is corroborated by the fact `/chatter` appears in the Subscriber interfaces of Listener in a separate command not listed above. Similarly, the other lines like `/parameter_events` and `/rosout` also appear to be Topics themselves for the same reasoning.

The interfaces `/parameter_events` and `/rosout` seem to exist in the Publisher section of both Talker and Listener. Their names and shared existence implies this is something that exists in all nodes that can be subscribed to, though the only thing that can be definitively concluded is that they exist in both.

Furthermore, `/talker/describe_parameters` along with a similar copy in Listeners with the appropriate `/listener` prefix to `/describe_parameters` exists. Similar parameters with the `rcl_interfaces` across the `:`, which might mean its being published to some common standard internal output? Considering `/rosout` exists across all nodes as a Publisher, this implies that this is the Topic its being outputted to by standard of some rudimentary operation and/or function in ROS2 (rcl = ros command log?).

Finally, there also exists empty Service Clients, Action Servers, and Action Clients sections. Subscribers is also empty in Talker specifically, though this might just mean Talker is not listening/subscribing to any particular Topic. Regardless, the three totally empty sections could just imply that neither Talker nor Listener are themselves a Service that provides anything to a client but use a Service themselves from some other part of the overall architecture given the non-emptiness of Service Servers. Additionally, no "Actions" are being performed or received either as denoted by its appropriately empty sections.

### Connections and message type

**Commands:**

```bash
ros2 topic list -t
ros2 topic info /chatter
ros2 interface show std_msgs/msg/String
```

```text
halifulis@Parcae:~$ ros2 topic list -t
/chatter [std_msgs/msg/String]
/parameter_events [rcl_interfaces/msg/ParameterEvent]
/rosout [rcl_interfaces/msg/Log]

halifulis@Parcae:~$ ros2 topic info /chatter
Type: std_msgs/msg/String
Publisher count: 1
Subscription count: 1

halifulis@Parcae:~$ ros2 interface show std_msgs/msg/String
# This was originally provided as an example message.
# It is deprecated as of Foxy
# It is recommended to create your own semantically meaningful message.
# However if you would like to continue using this please use the equivalent in example_msgs.

string data
```

**Interpretation:** [Identify the publisher, subscriber, topic, and message structure.]
Assuming the above is asking to identify the SPECIFIC relevant Publisher, Subscriber, and Topics pertaining to the output and the specific environment produced by the assignment so far... AND assuming "Publisher" and "Subscriber" refer to the nodes containing them...

There are Three topics: Chatter, Parameter_Events, and Rosout. All nodes so far are appear to be Publishers (or contain them?) to Parameter_Events and Rosout. Talker specifically appears to be a Publisher to Chatter, while Listener appears to be a Subscriber to Chatter. Additionally, it seems messages can be structured rather freely considering the variety across the three topics (String, ParameterEvent, Lod). With that in mind and given the application of ROS2 (sending rich data for robots to use), `string data` seems to correspond to `data_type name`, and messages are structured therefore as a collection of accessible fields (though this might be a stretch). In this particular case, the messages being sent across the current existing nodes (Talker and Listener) are probably just straight Strings.

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
zz
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
