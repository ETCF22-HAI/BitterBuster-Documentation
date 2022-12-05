---
title: Development Documentation
---

# BitterBuster Development Documentation
## Overview
This document provides the details on how to set up a development environment for BitterBuster.

## BitterBuster Game
### Repository Link
(TO BE PROVIDED)

### Game Development
The majority of the BitterBuster code is developed in C# within the [Unity](https://unity.com/download) game engine version 2021.3.9f1. 

Unity provides download instructions for Unity Hub and the Editor itself; the specific version used by Team HAI can be found [here](https://unity.com/releases/editor/archive).

### Multiplayer
#### PUN
Multiplayer is implemented using [Photon PUN](https://www.photonengine.com/en-US/Photon). Currently, this project is being developed using the [free tier](https://www.photonengine.com/en-US/PUN/Pricing) offered by Photon, which allows for 20 CCU. Should the project be expanded in the future, higher tiers may need to be purchased to account for a larger user base.

Photon provides extensive [documentation](https://doc.photonengine.com/en-us/pun/current/getting-started/pun-intro/) on its many features. The package needed to integrate PUN with Unity has already been installed but is currently being used with a development PUN ID belonging to the HAI team; a new ID and account should be made to set up the game for the research team. You can follow the setup tutorial provided [here](https://doc.photonengine.com/en-us/pun/current/demos-and-tutorials/pun-basics-tutorial/intro).

#### ParrelSync
To test multiplayer development within the Unity editor, we use the [ParrelSync](https://github.com/VeriorPies/ParrelSync) plugin. This has already been installed via the package manager.

## BitterBuster Candy Generator
### Repository Link
[https://github.com/ETCF22-HAI/CandyGeneration](https://github.com/ETCF22-HAI/CandyGeneration)

### Setup Requirements
The candy generator is written in [Python 3](https://www.python.org/downloads/). Instructions on setting up the development environment and running the given scripts are provided in the repository's [README file](https://github.com/ETCF22-HAI/CandyGeneration/blob/master/README.md).
