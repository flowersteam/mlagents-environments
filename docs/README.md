# Flowers environment Documentation

This documentation is an extension of the original ml-agents documentation (also available in [this subfolder](ML-Agents_documentation)). To meet the needs of exploration experimentation, a few changes were brought to the original ml-agent implementation. This documentation should give you the most important pieces to use the environments and eventually modify them. If you intend to do more, you can proceed with the original documentation.

## Detailed installation

Before attempting anything, make sure that you completed the installation of the repository by following this procedure:

```bash
$ git clone https://github.com/flowersteam/mlagents-environments.git
$ cd mlagents-environments
$ wget https://flowers.inria.fr/archives/mlagents-environments.tar.xz
$ tar -zxvf mlagents-environments.tar.xz
```

Then the preferred way to use the environments is to create a specific `conda` or `virtualenv` environment, and install the python packages:

```bash
$ conda create --name ml-agents python=3.6
$ conda activate ml-agents
(ml-agents) $ pip install -e gym-unity
(ml-agents) $ pip install -e ml-agents
```

A few extra packages may be needed.

Fore more thourough installation tutorials, check:

   * [Anaconda](Anaconda_Install.md)
   * [ML-Agents & Gym-Unity](ML-Agents_Install.md)

## Using the environments with gym

In the `environments` folder, you will find the compiled binaries of every environments. Binaries are available for `linux` and `osx` binaries are available. 

We also provide a jupyter notebook, to help you discover the features of every environments, and easily start your experiments.

For more detailed explanations, check:

   * [Jupyter Notebook](Jupyter_Notebook.md)

   * [Gym-Unity's main commands](Gym-Unity_Commands.md)


## Modifying the environments

You can modify the environments to suit the needs of your experiments. The following tutorials should give you a good basis to begin with. If you lack some informations, refer to the [original documentation](ML-Agents_documentation).


1. Unity Installation

   * [Unity 2018.4.2f1](Unity_Installation.md)

   * [Unity SDK and project organization](Unity_project.m)

2. ML-Agents Assets

   * [ML-Agents Overview](ML-Agents_Overview.md)

   * [Agent](Agent.md)

   * [Brains](Brains.md)

   * [Academy](Academy.md)

3. Other features

   * [Add informations in the dictionary](Dictionary_Informations.md)
   
   * [Add reset parameters](Reset_parameters.md)
   
   * [Change an environment during a simulation](Environment_modification.md)
   
   * [Frequent mistakes](Frequent_mistakes.md)


If you want learn more about ML-Agents v0.7, read the [documentation](ML-Agents_documentation/README.md) (warning : the documentation available on the ML-Agents GitHub repository is the documentation for ML-Agents v0.8)

