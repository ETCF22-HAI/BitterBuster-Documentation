---
title: AI Support [WIP]
---

# BitterBuster AI Support
## Overview
This document provides the details and schema for the various data elements that will be exported/expected as input for AI agent support by the BitterBuster game.

## Game State Data [WIP]
The game state data is created through compiling all of serializable data from the different objects in the game. Each of these objects have a `Serialize` function that converts their fields into a JSON format, then all of the serialized data is compiled by the `GameManager`.

The rough schema of what would be outputted is as follows:
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
Screenshots can be captured for the game (which uses a 16:9 ratio). The size of the screenshot can be adjusted within Unity via the `CameraController` class.
