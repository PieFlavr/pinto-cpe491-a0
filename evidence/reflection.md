# Reflection

## From Python file to ROS graph

In 150–250 words, explain how the Python class and `main()` function relate to the running process, ROS node, publisher or subscriber, topic, and message visible in the ROS graph.*

The following is written with the assumption this is asking in direct relevance to the content/work covered by the assignment.

The use of a class from Python is used to extend and create subclasses of `rclpy`'s `Node`, of which instantiating it is what creates the ROS node. In that regard, `super().__init__('NODE_NAME')` inside of `__init__` registers said name within the overall ROS graph, letting it be seen in the nodes listed by `ros2 node list`.

Everything else the class sets up in its `__init__()` function such as via `self.create_publisher(...)` or `self.create_subscription(...)` and other additional logic is what wires the node to some specific topic and message type. Presumably this means a Node can have multiple Publishers and Subscribers within it.

The timer or callback defined within the class (*or some other logical condition*) is what produces and/or consumes individual messages in specified topics at runtime. 

From the functions and logic within `main()`, it seems Nodes are treated as ongoing processes whose use of `rclpy`'s functions such as `rclpy.init()`, `rclpy.spin()`, and `rclpy.shutdown()` establish communication/use with the ROS library. `init()` starts the ROS library in relation to the Node, then the rest of the code before `spin()` establish/instantiates the Node itself (*along with additional properties/aspects not already established by `__init__()`*). `rclpy.spin()` keeps the process holding the Node alive and "ticks" it, letting callbacks and similar react to the overall system. Then any code between `spin()` and `shutdown()` would likely be delegated to clean-up and similar shutdown logic, before `shitdown()` itself explicitly performs cleanup of the Node. 

In my testing without using `spin()`, the Node never meaningfully exists (*though it might momentarily*). Presumably you can manually `spin()` the Node some specific number of times? Though this is mostly conjecture as I try to keep strictly to immediately class-relevant topics. 

## Changing the message contract

Compare your status pair with your count pair. What code changed, what stayed the same, and why must the publisher and subscriber agree on both the topic name and message type?

For the most part, a majority of the changes across the two pairs are almost entirely the naming scheme of things. `CountPublisher`, `CountMonitor`, and similar replaced counterpart `StatusPublisher`, `StatusMonitor`, and etc... The only "real" changes so far that had technical consequences were with regard to the message and its data. The `timer_period` to match the requested frequency specification (*1hz --> 4hz / 1 --> 0.25*). Furthermore the imported data type for the message was also modified, from `String` to `Int32`, and subsequently the message declaration from `msg = String()` to `msg = Int32()`. The most important change was with regards to the message data itself, changing from the `System ready: %d` message to simply just `self.i` being outputted as we were no longer using a string. Consequently the use of `%s` was changed to `%d` in the logger to reflect the new data type. The topic was also changed from `/lab0/status` to `/lab0/status` in every relevant instance (*including variabel names, for clarity*). Similarly, the node names from `status_monitor` and similar to `count_monitor` and relevant.

Otherwise, literally everything else about the code stayed structurally and technically the same. No real changes were made to the overall execution flow.

Both Publisher and Subscriber must agree on both the topic name and message type because they otherwise cannot effectively communicate with one another. If the message type is different, on the receiving end data might just be completely unreadable and fail or might be read as some unexpected garbage noise value. If the topic name is different, the message is just lost entirely as neither can reasonably see one another. Its like two people where one calls the wrong phone number, or the other expects a call from the wrong phone number. ROS2's system will just not connect them if they do not agree on topic.

## A useful inspection command

Which command from this assignment would you try first on an unfamiliar ROS 2 system, and why?

If I had to pick just ONE command (*which seems to be the implication here*), I would woud run `ros2 node list` first because all the other commands rely to some degree on the information on what nodes exist or not. Though `ros2 topic list -t` is also a good contender, as commands shown so far either rely on knowledge of node names OR topic names. `ros2 node list` takes top cake though primarily because topic information can also be revealed via subsequent commands on disambiguaiting further node information/properties.

## Most useful failure

Describe one failure or wrong result, the evidence that helped you locate it, and what you changed.

Running `check_assignment.py` helped me realized the assignment was asking for `System ready`, not `Systeam Ready`. Additionally, transferring work across Windows and Linux via Git also made me realize symlinks/softlinks were going to run into a multitude of different issues, and in addition to realizing the `README.md` was different in subtle but unfrotunate ways to the assignment on WebCampus, led to me to refactor my repository structure.
