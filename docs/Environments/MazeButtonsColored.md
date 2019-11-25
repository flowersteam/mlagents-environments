# MazeButtons (Colored)

Come back to [home](../Home.md)

### Contents

- [Description](#description)

- [Agent's Actions](#actions)

- [Brain](#brain)

- [Observations](#observations)

- [Reset](#Reset)

- [Reset's Parameters](#parameters)

- [Distraction](#distraction)

- [Next Steps](#next_steps)

  

## <a name="class">Information</a>



<p align="center">
  <img src="../images/Environments/MazeButtonsColored.png"
       alt="using "
       width="70%" border="10" />
</p>



|            <a name="description">Description</a>             | <br />This environment is the same as `Maze Buttons (Textured)`.The agent goes from room to room when he pushes buttons. Each room has a specific color and each kind of buttons teleports instantaneously the agent in the same room. The agent can explore 10 rooms.<br /> |
| :----------------------------------------------------------: | :----------------------------------------------------------- |
|            <a name="actions">Agent's Actions</a>             | The agent has 5 actions : nothing (0) / go forward (1) / go backward (2) / turn left (3) / turn right (4) |
|                  <a name="brain">Brain</a>                   | The brain has only one branch : `observation, reward, done, info = env.step(0)` |
|       <a name="observations">Agent's Observations</a>        | The agent sends its observations (image 84x84) at each step  |
| <a name="informations">Informations stored in a dictionary</a> | The agent stores its **position** and its **current room number** at each step |
|                  <a name="Reset">Reset</a>                   | <br />If the user wants to reset the environment. He can change the parameters. He can choose to **start in any room** at the beginning of the simulation.<br /> |
|         <a name="parameters">Reset's Parameters</a>          | **loadLevel [0, 9]** : load the room choosen                 |
|            <a name="distraction">Distraction</a>             | None                                                         |

## <a name="next_steps">Next Steps</a>

Other environments : 

1. [PushBlocks](PushBlocks.md)
2. [Television](Television.md)
3. [MazeButtons (colored)](MazeButtonsColored.md)
4. [MazeButtons (textured)](MazeButtonsTextured.md)
5. [Drawing](Drawing.md)
6. [VideoGame](VideoGame)

or come back to [home](../Home.md)