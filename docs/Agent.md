# Agents

An agent is an actor that can observe its environment and decide on the best course of action using those observations. Create Agents in Unity by extending the Agent class. The most important aspects of creating agents that cansuccessfully learn are the observations the agent collects for learning.

An Agent passes its observations to its Brain. The Brain, then, makes a decision and passes the chosen action back to the agent. Your agent code must execute the action, for example, move the agent in one direction or another.

The Brain class abstracts out the decision making logic from the Agent itself so that you can use the same Brain in multiple Agents. How a Brain makes its decisions depends on the kind of Brain it is. A Player Brain allows you to directly control the agent. A Heuristic Brain allows you to create a decision script to control the agent with a set of rules. These two Brains do not involve neural networks but they can be useful for debugging. The Learning Brain allows you to train and use neural network models for your Agents.

### Contents

- [Decisions](#decisions)
  - [On Demand Decision Making](#decision_making)
- [Observations](#observations)
  - [Vector Observation Space: Feature Vectors](#observation_vector)
- [Vector Actions](#actions)
  - [Continuous Action Space](#continuous)
  - [Discrete Action Space](#discrete)
- [Agent Properties](#properties)
- [Instantiating an Agent at Runtime](#instantiate)
- [Destroying an Agent](#destroy)
- [Next Steps](#next_steps)

## <a name="decisions">Decisions</a>

The observation-decision-action-reward cycle repeats after a configurable number of simulation steps (the frequency defaults to once-per-step). You can also set up an Agent to request decisions on demand. Making decisions at regular step intervals is generally most appropriate for physics-based simulations. Making decisions on demand is generally appropriate for situations where Agents only respond to specific events or take actions of variable duration. For example, an  agent in a robotic simulator that must provide fine-control of joint torques should make its decisions every step of the simulation. On the other hand, an agent that only needs to make decisions when certain game or simulation events occur, should use on-demand decision making.  

To control the frequency of step-based decision making, set the **Decision Frequency** value for the Agent object in the Unity Inspector window. Agents using the same Brain instance can use a different frequency. During simulation steps in which no decision is requested, the Agent receives the same action chosen by the previous decision.

### <a name="decision_making">On Demand Decision Making</a>

On demand decision making allows Agents to request decisions from their Brains only when needed instead of receiving decisions at a fixed frequency. This is useful when the agents commit to an action for a variable number of steps or when the agents cannot make decisions at the same time. This typically the case for turn based games, games where agents must react to events or games where agents can take actions of variable duration.

When you turn on **On Demand Decisions** for an Agent, your agent code must call the `Agent.RequestDecision()` function. This function call starts one iteration of the observation-decision-action-reward cycle. The Brain invokes the Agent's `CollectObservations()` method, makes a decision and returns it by calling the `AgentAction()` method. The Brain waits for the Agent to request the next decision before starting another iteration.

## <a name="observations">Observations</a>

To make decisions, an agent must observe its environment in order to infer the state of the world. A state observation can take the following forms:

- **Vector Observation** — a feature vector consisting of an array of floating point numbers.
- **Visual Observations** — one or more camera images.

When you use vector observations for an Agent, implement the`Agent.CollectObservations()` method to create the feature vector. When you use **Visual Observations**, you only need to identify which Unity Camera objects will provide images and the base Agent class handles the rest. You do not need to implement the `CollectObservations()` method when your Agent uses visual observations (unless it also uses vector observations).

### <a name="observation_vector">Vector Observation Space: Feature Vectors</a>

For agents using a continuous state space, you create a feature vector to represent the agent's observation at each step of the simulation. The Brain class calls the `CollectObservations()` method of each of its Agents. Your implementation of this function must call `AddVectorObs` to add vector observations.

The observation must include all the information an agents needs to accomplish its task. Without sufficient and relevant information, an agent may learn poorly or may not learn at all. A reasonable approach for determining what information should be included is to consider what you would need to calculate an analytical solution to the problem.

```csharp
public GameObject ball;

private List<float> state = new List<float>();
public override void CollectObservations()
{
    AddVectorObs(gameObject.transform.rotation.z);
    AddVectorObs(gameObject.transform.rotation.x);
    AddVectorObs((ball.transform.position.x - gameObject.transform.position.x));
    AddVectorObs((ball.transform.position.y - gameObject.transform.position.y));
    AddVectorObs((ball.transform.position.z - gameObject.transform.position.z));
    AddVectorObs(ball.transform.GetComponent<Rigidbody>().velocity.x);
    AddVectorObs(ball.transform.GetComponent<Rigidbody>().velocity.y);
    AddVectorObs(ball.transform.GetComponent<Rigidbody>().velocity.z);
}
```

_Collect Observations example_

The feature vector must always contain the same number of elements and observations must always be in the same position within the list. If the number of observed entities in an environment can vary you can pad the feature vector with zeros for any missing entities in a specific observation or you can limit an agent's observations to a fixed subset. For example, instead of observing every enemy agent in an environment, you could only observe the closest five.

When you set up an Agent's Brain in the Unity Editor, set the following properties to use a continuous vector observation:

- **Space Size** — The state size must match the length of your feature vector.

The observation feature vector is a list of floating point numbers, which means you must convert any other data types to a float or a list of floats.

The `AddVectorObs` method provides a number of overloads for adding common types of data to your observation vector. You can add Integers and booleans directly to the observation vector, as well as some common Unity data types such as `Vector2`,`Vector3`, and `Quaternion`.

Type enumerations should be encoded in the _one-hot_ style. That is, add an element to the feature vector for each element of enumeration, setting the element representing the observed member to one and set the rest to zero. For example, if your enumeration contains \[Sword, Shield, Bow\] and the agent observes that the current item is a Bow, you would add the elements: 0, 0, 1 to the feature vector. The following code example illustrates how to add.

```csharp
enum CarriedItems { Sword, Shield, Bow, LastItem }
private List<float> state = new List<float>();
public override void CollectObservations()
{
    for (int ci = 0; ci < (int)CarriedItems.LastItem; ci++)
    {
        AddVectorObs((int)currentItem == ci ? 1.0f : 0.0f);
    }
}
```

`AddVectorObs` also provides a two-argument version as a shortcut for _one-hot_
style observations. The following example is identical to the previous one.

```csharp
enum CarriedItems { Sword, Shield, Bow, LastItem }
const int NUM_ITEM_TYPES = (int)CarriedItems.LastItem;

public override void CollectObservations()
{
    // The first argument is the selection index; the second is the
    // number of possibilities
    AddVectorObs((int)currentItem, NUM_ITEM_TYPES);
}
```



## <a name="actions">Vector Actions</a>

An action is an instruction from the Brain that the agent carries out. The action is passed to the Agent as a parameter when the Academy invokes the agent's `AgentAction()` function. When you specify that the vector action space is **Continuous**, the action parameter passed to the Agent is an array of control signals with length equal to the `Vector Action Space Size` property. When you specify a **Discrete** vector action space type, the action parameter is an array containing integers. Each integer is an index into a list or table
of commands. In the **Discrete** vector action space type, the action parameter is an array of indices. The number of indices in the array is determined by the number of branches defined in the `Branches Size` property. Each branch corresponds to an action table, you can specify the size of each table by modifying the `Branches` property. Set the `Vector Action Space Size` and `Vector Action Space Type` properties on the Brain object assigned to the Agent (using the Unity Editor Inspector window).

Neither the Brain nor the training algorithm know anything about what the action values themselves mean. The training algorithm simply tries different values for the action list and observes the affect on the accumulated rewards over time and many training episodes. Thus, the only place actions are defined for an Agent is in the `AgentAction()` function. You simply specify the type of vector action space, and, for the continuous vector action space, the number of values, and then apply the received values appropriately (and consistently) in `ActionAct()`.

For example, if you designed an agent to move in two dimensions, you could use either continuous or the discrete vector actions. In the continuous case, you would set the vector action size to two (one for each dimension), and the agent's Brain would create an action with two floating point values. In the discrete case, you would use one Branch with a size of four (one for each direction), and the Brain would create an action array containing a single element with a value ranging from zero to three. Alternatively, you could create two branches of size two (one for horizontal movement and one for vertical movement), and the Brain would create an action array containing two elements with values ranging from zero to one.

Note that when you are programming actions for an agent, it is often helpful to test your action logic using a **Player** Brain, which lets you map keyboard commands to actions.

### <a name="continuous">Continuous Action Space</a>

When an Agent uses a Brain set to the **Continuous** vector action space, the action parameter passed to the Agent's `AgentAction()` function is an array with length equal to the Brain object's `Vector Action Space Size` property value. The individual values in the array have whatever meanings that you ascribe to
them. If you assign an element in the array as the speed of an Agent, for example, the training process learns to control the speed of the Agent though this parameter.

The Reacher example defines a continuous action space with four control values.

![reacher](/Users/flowers/Documents/Unity%20ML-Agents/ml-agents-work/ml-agents/docs/ML-Agents_documentation/docs/images/reacher.png)

These control values are applied as torques to the bodies making up the arm:

```csharp
public override void AgentAction(float[] act)
{
    float torque_x = Mathf.Clamp(act[0], -1, 1) * 100f;
    float torque_z = Mathf.Clamp(act[1], -1, 1) * 100f;
    rbA.AddTorque(new Vector3(torque_x, 0f, torque_z));

    torque_x = Mathf.Clamp(act[2], -1, 1) * 100f;
    torque_z = Mathf.Clamp(act[3], -1, 1) * 100f;
    rbB.AddTorque(new Vector3(torque_x, 0f, torque_z));
}
```



### <a name="discrete">Discrete Action Space</a>

When an Agent uses a Brain set to the **Discrete** vector action space, the action parameter passed to the Agent's `AgentAction()` function is an array containing indices. With the discrete vector action space, `Branches` is an array of integers, each value corresponds to the number of possibilities for each branch.

For example, if we wanted an Agent that can move in an plane and jump, we could define two branches (one for motion and one for jumping) because we want our agent be able to move __and__ jump concurrently. We define the first branch to have 5 possible actions (don't move, go left, go right, go backward, go forward)
and the second one to have 2 possible actions (don't jump, jump). The AgentAction method would look something like:

```csharp
// Get the action index for movement
int movement = Mathf.FloorToInt(act[0]);
// Get the action index for jumping
int jump = Mathf.FloorToInt(act[1]);

// Look up the index in the movement action list:
if (movement == 1) { directionX = -1; }
if (movement == 2) { directionX = 1; }
if (movement == 3) { directionZ = -1; }
if (movement == 4) { directionZ = 1; }
// Look up the index in the jump action list:
if (jump == 1 && IsGrounded()) { directionY = 1; }

// Apply the action results to move the Agent
gameObject.GetComponent<Rigidbody>().AddForce(
    new Vector3(
        directionX * 40f, directionY * 300f, directionZ * 40f));
```



## <a name="properties">Agent Properties</a>

![Agent Inspector](/Users/flowers/Documents/Unity%20ML-Agents/ml-agents-work/ml-agents/docs/ML-Agents_documentation/docs/images/agent.png)

- `Brain` - The Brain to register this Agent to. Can be dragged into the inspector using the Editor.

- `Visual Observations` - A list of `Cameras` which will be used to generate observations.

- `Max Step` - The per-agent maximum number of steps. Once this number is reached, the Agent will be reset if `Reset On Done` is checked.

- `Reset On Done` - Whether the Agent's `AgentReset()` function should be called when the Agent reaches its `Max Step` count or is marked as done in code.

- `On Demand Decision` - Whether the Agent requests decisions at a fixed step interval or explicitly requests decisions by calling `RequestDecision()`.

  - If not checked, the Agent will request a new decision every `Decision
    Frequency` steps and perform an action every step. In the example above,
    `CollectObservations()` will be called every 5 steps and `AgentAction()`
    will be called at every step. This means that the Agent will reuse the
    decision the Brain has given it.
  - If checked, the Agent controls when to receive decisions, and take actions.
    To do so, the Agent may leverage one or two methods:
    - `RequestDecision()` Signals that the Agent is requesting a decision. This
      causes the Agent to collect its observations and ask the Brain for a
      decision at the next step of the simulation. Note that when an Agent
      requests a decision, it also request an action. This is to ensure that
      all decisions lead to an action during training.
    - `RequestAction()` Signals that the Agent is requesting an action. The
      action provided to the Agent in this case is the same action that was
      provided the last time it requested a decision.

- `Decision Interval` - The number of steps between decision requests. Not used if `On Demand Decision`, is true.

  

## <a name="instantiate">Instantiating an Agent at Runtime</a>

To add an Agent to an environment at runtime, use the Unity `GameObject.Instantiate()` function. It is typically easiest to instantiate an agent from a [Prefab](https://docs.unity3d.com/Manual/Prefabs.html) (otherwise, you have to instantiate every GameObject and Component that make up your Agent individually). In addition, you must assign a Brain instance to the new Agent and initialize it by calling its `AgentReset()` method. For example, the following function creates a new Agent given a Prefab, Brain instance, location, and orientation:

```csharp
private void CreateAgent(GameObject AgentPrefab, Brain brain, Vector3 position, Quaternion orientation)
{
    GameObject AgentObj = Instantiate(agentPrefab, position, orientation);
    Agent Agent = AgentObj.GetComponent<Agent>();
    Agent.GiveBrain(brain);
    Agent.AgentReset();
}
```

## <a name="destroy">Destroying an Agent</a>

Before destroying an Agent GameObject, you must mark it as done (and wait for the next step in the simulation) so that the Brain knows that this Agent is no longer active. Thus, the best place to destroy an Agent is in the`Agent.AgentOnDone()` function:

```csharp
public override void AgentOnDone()
{
    Destroy(gameObject);
}
```

Note that in order for `AgentOnDone()` to be called, the Agent's `ResetOnDone` property must be false. You can set `ResetOnDone` on the Agent's Inspector or in code.



## <a name="next_steps">Next Steps</a>

If you want to learn more about the key components or understand how ML-Agents work :

- [ML-Agents Overview](ML-Agents_Overview.md)
- [Brains](Brains.md)
- [Academy](Academy.md)



The Flowers team has adapted ML-Agents to fit with its work, [find out the new features](Dictionary_Informations.md)

or come back to [home](Home.md)

