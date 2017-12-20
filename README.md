# node-red-contrib-actionflows
Provides three nodes that allow you to create extensible, reusable,
looped, and prioritized flows. ActionFlows includes performance benchmarks with
nanosecond precision. Advanced use enables the ability to group flows into
"libraries" by using Node-RED's subflow capabilities. You can organize flows for
readability and create extendable design patterns. To understand ActionFlows,
review each section starting with Basics below and each section's examples.

## Basics
The following example of ActionFlows' `action` node does nothing! "Hello
World" is placed in the `msg.payload` and passes through the `action` node and
can be seen in the debug output; but it's use and versatility can be illustrated
with the following descriptions.

![Action Node Basics](/actionflows/demo/basic.png?raw=true "The Action Node")

ActionFlows' initial purpose was to allow for "after market" flow extendability.
Complex flows can be customized without modifying the original author's flow.
Simply include the `action` flow inline at specific points where you would like
to enable vendor customization. Like Node-RED's native subflows, a description
field allows you to create optional API (application programming interface)
documentation. The `action` node works like a subflow, allowing you to define a
reusable flow segment between the nodes `action in` and `action out`. Flow
execution resumes like Node-RED's native `links` node with "virtual wires" at
the `action in` node and returns to the calling `action` node after encountering
the `action out` node.

![Action In/Out Basics](/actionflows/demo/basic2.png?raw=true "The Action In and Action Out Nodes")

Unlike the `links` node, the `action` node invokes the `action in` node by a
prefix naming schema. An `action` node's name determines the name of the
corresponding `action in` nodes that will be activated. Use the `action` node's
name as a prefix for all subsequent `action in` nodes that you wish to be
callable by the `action` node. For instance, an `action` node named "Sample",
will activate any `action in` nodes with names like "Sample in", "Sample-in",
"Sample Exercise", or "Sample.Acme.com".

> A prefix is an existing `action` node's name followed by
> a space, hyphen, or a period.

If present, ActionFlows will invoke multiple matching prefix named nodes
sequentially.

![ActionFlow Sequence](/actionflows/demo/basic2.png?raw=true "Sequential Flow Segments")

In the example above:

1) The `action` node is encountered with `msg.payload` containing "Hello World".
2) The `action in` node (named "action in") is called, changing "World" into "World, and Solar System!".
3) The `action in` node (named "action 2") is called after the last `action out` node and "World" is replaced with "Mars".

The versatility of ActionFlows allows the adding of additional flow sequences
after the original flow has been authored. The `action in` node's flow sequences
can be created or imported dynamically (such as with the `flowman` node). Flows
can be defined on other tabs or within subflows (see the "Libraries" section
below) or restricted to the same tab or subflow where the calling `action` node
has been defined.

Flow sequence order can also be defined by the sequence author (see the
"Priorities" section).

### Benchmarks

Benchmarks in the `action` node allow you to see how long an `action in` flow
sequence takes to execute.

### Priorities

Priorities 1 to 99. The lower the number, the earlier a defined flow sequence
will execute. I.e. An `action in` node with #1 priority executes before an #2
priority flow sequence, etc. Recommend you leave the priority at 50 to allow
override by other authors (if need be).

### Nesting

## Loops
The `action` node allows execution of `action in/out` node sequences based on
a conditional loop.

### None

### Watch

### Decrement

### Increment

### Increment From Zero

## Libraries

### Private actions
Use the private checkbox in the `action` node's settings to restrict calling any
`action in/out` flow sequences to the same tab or within the given subflow.
Uncheck the checkbox to allow invoking flow sequences defined on other tabs, or
subflows.

### Private flows
Use the private flow checkbox to limit this <code>action in</code> node's
flow to `action` nodes calling from within the same tab or within the
same subflow. Uncheck to allow actions to invoke the `action in` node
from other tabs or subflows (where the `action` node's own private
checkbox is unchecked.

## Advanced
Overrides, invalidating segments at runtime, manipulating msg._af

## Installation


blah blah blah

 ,  Provides nodes to enable an extendable design pattern for flows. ActionFlows
can streamline the appearance of flows in a similar way that Node-RED's native
subflows work or the link nodes' "virtual wires"; invoking flow segments located
elsewhere. Unlike link nodes or subflows, flows that use the actionflows node do
NOT need to be aware of existing segments or have them pre-defined. Instead,
segments are invoked by a named prefix schema; allowing an arbitrary number of
flow segments to be added or imported later (such as when using flowman or flow
dispatcher) without modifying the original flow. ActionFlows' segments are
invoked sequentially with their order determined by the segment's author (see
priority description below).

## ActionFlow Segments
Action flow segments are defined by using the `action in` and `action out` nodes.
The in/out nodes should have a unique name but must start (have a prefix)
with a name of an existing action node followed by a space, hyphen, or underscore.
For instance the default name `action in` or `action_in` would be invoked when
the `action` node is encountered. The `actionflows`, `action in`, and `action out`
nodes can exist in any combination of multiple different tabs, inside or outside
of subflows.

Inspired by WordPress' core actions and filters API (but faster) that inarguably
enabled one of the world's largest and most prolific plugin communities. This
implementation leverages jump tables and indexed objects to ensure the fastest
execution of flow segments.

## Priority Description
Like WordPress' actions & filters, actionflows allow flow segments to have a
priority property with values of 1 to 100 (with a default of 50; a higher
resolution than WordPress'). The priority property determines earlier or later
execution order of a flow segment (i.e. priority 1 executes before any priority
2s, etc). These features can make flows extendable and allows flows to furnish
an expandable, "plugin-able" API.

## Examples

#### Basic Example


![ActionFlows Basic Example](/actionflows/demo/basic.jpg?raw=true "Basic use")

Description to follow...
* Place the `action` node between nodes in a given flow to make the flow extensible.
* Give the `action` node a unique and short name that describes the action.
* Use the `action in` and `action out` nodes to create a flow segment.
* Name `action in` and `action out` nodes with a prefix that matches an existing action.
* Assign a priority to the `action in` node (1 to 100).


#### Another Example
Description with flow below...

```
[
    {
    }
]
```
## Installation
Run the following command in your Node-RED user directory (typically ~/.node-red):

    npm install node-red-contrib-actionflows

The actionflows' nodes are will appear in the palette under the advanced group as
the nodes `action`, `action in`, and `action out`.
