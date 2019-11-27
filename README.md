

<p align="center">
  <img src="docs/images/Logo-Inria.png" align="middle" width=30% style="margin-right:20%;"/>
  <img src="docs/images/unity-wide.png" align="middle" width=30%/>
</p>


<img src="docs/images/AllEnvironments.png" align="middle" width=100%/>



# Unity ML-Agents Environments for Curiosity Learning

This repository contains a set of [unity ml-agent](https://github.com/Unity-Technologies/ml-agents) environments meant to be used in curiosity-based exploration algorithms, e.g. exploration without extrinsic reward.

## Flower's environments

1. [PushBlocks](docs/Environments/PushBlocks.md)
2. [Television](docs/Environments/Television.md)
3. [MazeButtons (colored)](docs/Environments/MazeButtonsColored.md)
4. [MazeButtons (textured)](docs/Environments/MazeButtonsTextured.md)
5. [Drawing](docs/Environments/Drawing.md)
6. [VideoGame](docs/Environments/VideoGame.md)
  

## Documentation

* For more information, in addition to installation and usage instructions, see
  our [documentation home](docs/Home.md).
  
* If you only want to use the new environments with Gym, see the first part of the documentation

* If you want to change the new or the old environments with Unity (add elements or informations, set up the reset, test manually, etc.) see the second part of the documentation
  
* If you want to learn more about ML-Agents, see the last part of the documentation


## Features

* New environments designed with Unity 2018.4.2f1 version
* ML-Agents 0.7 version
* Python 3.6
* Linux & Mac only

## Installation

This repository does not contain all the binaries and unity assets. To completely install the repository please follow this procedure :

```bash
$ git clone https://github.com/flowersteam/mlagents-environments.git
$ cd mlagents-environments
$ wget https://flowers.inria.fr/archives/mlagents-environment.tar.xz
$ tar -zxvf mlagents-environment.tar.xz
```

## Contact

We used the open-source project ML-Agents and designed our environments with the software Unity. If you have questions about how work these toolkits you can read the [ML-Agents documentation](docs/ML-Agents_documentation/README.md).

If you want to learn more about the Flowers Team of Inria Bordeaux Sud-Ouest, go on our [web site](https://flowers.inria.fr/).
