---
title: Future Development
---

# BitterBuster Future Development

## Overview
This document provides a list of current limitations and potential steps for future development.

## Future Development
### AI Communication
We were able to explore different methods of communication with Python-based agents, but were not able to fully implement the communication framework. 

Our idea for the game flow was that an Explorer/Selector would be able to join the room, then toggle themselves for being a human or AI agent; if an AI agent was selected, then once the game starts, it would periodically output observations and wait to receive actions from the agent. So, the agent would be running locally on the player machine that joins the room.

As a summary of our progress:

- [x] Create a serialization function for all main objects in the game in the `Controller` classes, along with a global function in `GameManager` demonstrating how to compile all the data together and export into a `json` file
- [x] Create a function to capture screenshots in `CameraController` and export them into `png`
- [ ] Create a function that exports an array of actions that can be taken by the Explorer/Selector
    - A sample of one potential way this can be done for the Explorer is found [here](https://github.com/ETCF22-HAI/BitterBuster/blob/7e95a29af2c6dcc33e4ddb6b47001786dcfa9ef4/Multiplayer%20Test%20v2/Assets/Scripts/Controllers/ExplorerController.cs#L343)
- [ ] Connect Unity with Python 
- [ ] Send observation data in an efficient way that does not lag the game
- [ ] Receive action input from Python
- [ ] Apply the action input to the Explorer/Selector controllers in the game
- [ ] Create a button on the pre-game screen that allows a player to toggle between being human/AI

In our most-completed demo (conducted on [this branch](https://github.com/ETCF22-HAI/BitterBuster/tree/angelaz1/networking-test/Multiplayer%20Test%20v2/Assets/Scripts)), we had successfully connected Unity to a Python server via C#-based TCP socket communication. We wrote a very simple Python script to take (and scrap) the observational input and return a random action based on the action array received. However, native C# solutions seemed to have conflicts with Unity and caused the game to lag (and eventually crash).

One of the paths that seemed promising was using an external library that would handle the communication, such as [this one](https://github.com/off99555/Unity3D-Python-Communication).

### Additional Game Features
Some of the final changes we were not able to complete within the project semester:

- When a house is visited, adjusting the mailbox mesh to be flag-down along with the current color change
- A game over screen to be displayed to the host with a quick "replay" button that would bring everyone back to the pre-game screen with the same gameplay settings
- A full-on Input Manager that would allow for remapping of keys; currently, J & K work for Selectors, but we did not add in support for left-handedness
- Different houses being enabled/disabled on each gameplay session for having candies
- Updates to the tutorial screen:
    - Currently missing the information that different neighborhoods and houses may have different probability distributions
    - Also did not include the J/K for Selector and arrow keys as an option for movement
