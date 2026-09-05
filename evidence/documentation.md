# Documentation trail

Use the two official ROS 2 Jazzy source files linked in Part 3. Quote only the short line or fragment needed to identify each element.

NOTE: I was unsure if this was inteded to be pertaining to a particular file, or was generic, so treat any FULLY CAPTITALIZED word or set of words as generic "variable" names to substitute for the appropriate purpose/application (*"quote" as specific examples vs. documentation as generic/reproducable*). There are further disambiguated in the `[brief note]` sections provided. For the most part, these are solely used in the situation of multiple specific lines fulfilling the same purpose/"element" (*simplest example is `super().__init__('NODE_NAME')` to illustrate*).

NOTE #2: Additional to the above, in-code comments will be used as substitute for "specific" documentation, as to avoid the issue of multiple individual independently updatable code bits.

NOTE #3: ADDITIONAL to the above, for multi-line fragments, I will be using `\n` to denote NEW LINES. This is to accomodate the table format which... does not support in-cell new lines.

NOTE #4: As it is not specified, the following are additionally based on the unmodified imported source files mentioned in Part 3.

| Code element | File and line or short fragment | What this element does |
|---|---|---|
| Import the message type | `from std_msgs.msg import String` | This specifically pertains to a `String`, however more generally data types from `std_msgs`. Theoretically, so long as the exact class/interface imported is derivative of the message generic/abstract, it should also work. Either way, this lets us use the `String` message type |
| Assign the node name | `super().__init__('NODE_NAME')` | `NODE_NAME` here could be any string or name. In particular, `__init__` actually initializes the `Node` object, and `super()` lets us inherit from/extend the parent `Node` class.  |
| Create the publisher | `self.PUBLISHER = self.create_publisher(MESSAGE_CLASS, 'TOPIC', QUEUE_SIZE)` | `PUBLISHER` hereis any arbitrary name for the field letting us access the Pubslisher. `MESSAGE_CLASS` is any Message class like `String` that will be used to publish to the Topic. `TOPIC` lets us specify the existing Topic to publish to. `QUEUE_SIZE` determines the number of Messages sent to receive before dropping via FIFO order. |
| Create the subscription | `self.SUBSCRIPTION = self.create_subscription(MESSAGE_CLASS, 'TOPIC', self.CALLBACK_FUNCTION, QUEUE_SIZE)` | This particular example works exactly like the above, with the additional argument of a `CALLBACK_FUNCTION` from the `self` object being pased to be controlled/called later by some condition. `SUBSCRIPTION` has the same effective function as `PUBLISHER` as an accessible field name. `MESSAGE_CLASS` specifies Message Class to listen to instead of sending. `QUEUE_SIZE` is identical but received. |
| Assign the topic name | `self.INTERFACE = self.create_INTERFACE(MESSAGE_CLASS, 'TOPIC', ...)`| Creates a topic and assigns the name TOPIC to it. Additionally, INTERFACE is any generic interface constructor such as a publisher or subscriber or otherwise, thereby in use being `create_publisher()` or `create_subscription()` or similar. |
| Control when a callback occurs | `self.timer = self.create_timer(timer_period, self.timer_callback)` | While this is a specific example of a `callback` being attatched to a timer via the `create_timer()` function, more generally so long as the `callback` is attached to a condition via some function as an anonymous function argument, its occurence is controllable.  |
| Initialize, run, and shut down ROS | `rclpy.init(args=args) \n rclpy.spin(INTERFACE) \n rclpy.shutdown()` | `init()` initializes ROS to let us talk to the rest of the network. `spin()` lets us block the thread so the target node name `INTERFACE` can react to events . `shutdown()` cleans up and safely shuts down the ROS resources being used for the current Python process. |

**One place where the documentation helped me correct or avoid a mistake:**  
This act of filling in this documentation format has helped as an example of bad documentaiton to avoid in the future for works of any kind. In specific regards to the assignment, I suppose this helped me disambiguate the structural difference in the passed argument types between Publishers and Subscribers.

**PERSONAL REMARK**: As of writing this, I realize I am torn and caught in the torrent of the two interpretations of the purpose of this documentation. The first being "documentation for replicability/actual documentation" and the other being "documentation for the assignment/performative documentation". The former is heavily explicitly stated by the class, the latter is heavily implied by the assignment structure, wording, and the context. The question of "Is this for my/others use? Or is this solely for the assignment?" has come across my mind more times than I believe it was expected to do so.

My personal gripes on this are, well, personal, but for future reference and for those like me, it would be appreciated that a lane be picked, stayed on, and also specified in writing. I've spent quite a lot of time trying to figure how to best interpret the assignment, and the bounds of acceptable error only ever implied within it.

The simplest thing to specify that would help greatly, is that the room of interpretability OF the room of interpretability with this assignment's wording/documentation so far as of writing this should be specified. A statement like "if its not specified, then do what you want" or even a "strictly do not modify documentation templates", or even a simple specified range of acceptable deviation. Examples of "correctness" would be highly illustrative as well, as opposed to leaving the range of expectations largely unbounded and decided by words outside of the class. If documentation should be an explicit focus of the class, then such ambiguity would best be left resolved in writing as opposed to oration.

Kill us with openness, or kill us with specificity. It doesn't matter which, just please pick one, and please write it down.
