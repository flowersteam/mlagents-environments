# Use an environment : Jupyter Notebook (part 1/2)

The first part explain you how to launch an environment through a Jupyter Notebook and Gym commands

Come back to [home](Home.md)

### Contents

- [The environments](#environments)

- [Jupyter Notebook](#notebook)

- [Next Step](#next_step)

  

## <a name="environments">The environments</a>

Go in the main folder and enter the `environments` subdirectory. You will find 6 folders that correspond to the new environments. In each folder, you will find 6 files or folders :

* `.app` (Mac) and `x86_64` (Linux) files: these are the environments launched by the notebook. They contain an agent, a brain and an academy.
* `playable`: this folder contain the environment where the user can control the agent actions with the keyboard. It allow the user to test the environment.
* `description.md`: a description of the environment. The user will find a presentation of the environment but also the actions of the agent and the parameters editable before a reset.
* `.ipynb` file: the notebook that show you how to launch and interact with an Unity environment.



## <a name="notebook">Jupyter Notebook</a>

Until the en of this part, we will work with the environment `PushBlocks`. Enter in the `PushBlocks ` subdirectory and run from the command line: (don't forgive to activate the virtual environment [create before](Anaconda_Install.md))

```bash
jupyter notebook
```

This command open a webpage. In this page, you will find the currently folder.

<img src="images/JupyterFolder.png" align="middle" width="100%"/>

Open the notebook `notebook_push_blocks.ipynb`. You must have the window below: 

<img src="images/PushBlocksNotebook.png" align="middle" width=100%/>



This page explain you how to launch the environment, reset it, control the agent and change the parameters before a reset. Don't forget to change the `environment_filename` in according to your operating system.



## <a name="next_step">Next Step</a>

The next step is the explanation of [Gym-Unity's main commands](Gym-Unity_Commands.md) allowing to use the environment.

or come back to [home](Home.md)

