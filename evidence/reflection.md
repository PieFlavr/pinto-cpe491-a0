# Reflection

## From Python file to ROS graph

In 150–250 words, explain how the Python class and `main()` function relate to the running process, ROS node, publisher or subscriber, topic, and message visible in the ROS graph.

[Your response]

## Changing the message contract

Compare your status pair with your count pair. What code changed, what stayed the same, and why must the publisher and subscriber agree on both the topic name and message type?

[Your response]

## A useful inspection command

Which command from this assignment would you try first on an unfamiliar ROS 2 system, and why?

If I had to pick just ONE command (*which seems to be the implication here*), I would woud run `ros2 node list` first because all the other commands rely to some degree on the information on what nodes exist or not. Though `ros2 topic list -t` is also a good contender, as commands shown so far either rely on knowledge of node names OR topic names. `ros2 node list` takes top cake though primarily because topic information can also be revealed via subsequent commands on disambiguaiting further node information/properties.

## Most useful failure

Describe one failure or wrong result, the evidence that helped you locate it, and what you changed.

Running `check_assignment.py` helped me realized the assignment was asking for `System ready`, not `Systeam Ready`. Additionally, transferring work across Windows and Linux via Git also made me realize symlinks/softlinks were going to run into a multitude of different issues, and in addition to realizing the `README.md` was different in subtle but unfrotunate ways to the assignment on WebCampus, led to me to refactor my repository structure.
