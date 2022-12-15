---
title: AI Support
---

# BitterBuster AI Support
## Overview
This document provides the details and schema for the various data elements that will be exported/expected as input for AI agent support by the BitterBuster game. 

Currently, the plan is to communicate with Python over local TCP sockets (i.e. localhost:12345). The game will intermittedly send over game state data (and potentially screenshot data) to the Python program over the socket, and will request for input back into the game.

## Game State Data [WIP]
The current structure of data is as follows:
```
{
  "observation": {
    "explorer": {
      "position": Vector3,
      "scale": Vector3,
      "rotation": Vector4, // Quaternion
      "allowPlayerInput": bool, // NOT NEEDED: express through actions array
      "canInteract": bool // NOT NEEDED: express through actions array
    },
    "selector": {
      "position": Vector3,
      "allowPlayerInput": bool, // NOT NEEDED: express through actions array
      
      // TODO: when selector is in selection mode
      "candyImg": byte[]
    },
    "neighborhoodData": [
      {
        "houseData": [
          {
            "position": Vector3,
            "scale": Vector3,
            "rotation": Vector4, // Quaternion
            "visited": bool,
            "mailboxColor": Vector4
          },
          ...
        ],
        "numBitterCorrect": int,
        "numBitterIncorrect": int
      },
      ...
    ],
    "barrierData": [
      {
        "position": Vector3,
        "scale": Vector3,
        "rotation": Vector4, // Quaternion
      },
      ...
    ],
    "trapData": [
      {
        "position": Vector3,
        "scale": Vector3,
        "rotation": Vector4, // Quaternion
      },
      ...
    ],
    "timeLeft": float,
    "scoring": {
      "numBitterCorrect": int,
      "numBitterIncorrect": int,
      "numSweetCorrect": int,
      "numSweetIncorrect": int
    }
  },
  "actions": int[] // Array of possible actions that can be taken
}
```
Many parts of the above are static (barrier, house, and trap positions). These can be exported once at the beginning, then not needed again. For houses, we can export positions once, associate them with IDs, then only need to continuously output the ID and whether or not a house has been visited.

## Screenshot
Screenshots can be captured for the game (which uses a 16:9 ratio). The size of the screenshot can be adjusted within Unity.
