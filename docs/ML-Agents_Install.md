# Installation : ML-Agents & Gym-Unity (part 2/2)

The second part of the installation show you how to install Git LFS, ML-Agents, Gym-Unity and Matplotlib.

Come back to [home](Home.md)

### Contents

- [Install Git LFS](#git_lfs)
- [Clone the ML-Agents Toolkit Repository](#clone)
- [Install ML-Agents Package](#ml-agents)
- [Install Gym-Unity Package](#gym)
- [Install Matplotlib](#matplotlib)
- [Next Step](#next_step)



## <a name="git_lfs">Install Git Large File Storage</a>

The first step is to install Git LFS which allows to download all the files in the Github repesitory.

```bash
brew install git-lfs
```



## <a name="clone">Clone the ML-Agents Toolkit Repository</a>

Once installed and the virtual environment launched, you will want to clone the ML-Agents Toolkit GitHub repository.

```bash
git clone https://github.com/marserret/ML-Agents.git
```

The `UnitySDK` subdirectory contains the Unity Assets to add to your projects.
It also contains many [example environments](Learning-Environment-Examples.md) to help you get started.

The `ml-agents` subdirectory contains Python packages which provide
trainers and a Python API to interface with Unity.

The `gym-unity` subdirectory contains a package to interface with OpenAI Gym.



## <a name="ml-agents">Install ML-Agents Package</a>

To install the dependencies and `mlagents` Python package, enter the
`ml-agents/` subdirectory and run from the command line:

```bash
pip install -e .
```

If you installed this correctly, you should be able to run
`mlagents-learn --help`



## <a name="gym">Install Gym-Unity Package</a>

Come back in the main folder, enter the `gym-unity` subdirectory and run from the command line:

``` bash
pip install -e .
```



## <a name="matplotlib">Install Matplotlib</a>

We advise you to install the `matplotlib` package if you want to see the agent observations and launch the notebooks:

```bash
conda install matlplotlib
```



## <a name="next_step">Next Step</a>

The next step show you how to [run an environment](Jupyter_Notebook.md) with a notebook and the main command line to interact with it

or come back to [home](Home.md)

