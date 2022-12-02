---
layout: page
title: Data
permalink: /data/
---

<nav class="toc-fixed" markdown="1">
* TOC
{:toc}
</nav>

# BitterBuster Data Documentation
## Overview
This document provides the details and schema for the various data elements exported by the BitterBuster game. 

## Logging
With each run of the game, data points are logged for each specific event that occurs within the gameplay. These are exported into a `json` file in the `Logs` directory created at the root working directory of the BitterBuster executable. The event log is an array of logging objects that each follow the general form:
```
{
  eventType: string,
  timeStamp: float,
  data: [
    {
      key: string,
      value: string
    },
    ...
  ]
}
```

Each different event is associated with a different set of key/value data pairs that can be parsed for data interpretation.

*Note:* Logging was written very early in development and hasn't been updated. The data array was used to bypass an earlier problem with logging, but each of them will be compressed to just be within the log event object itself as such:
```
{
  eventType: string,
  timeStamp: float,
  key: value,
  ...
}
```

Some of the below events are still WIP and some need to be updated based on the new gameplay. 

### Event Types
#### Explorer Position
Logging of Explorer position by the game every x seconds (current build sets this as 2, but this value will be adjustable in the final version)

```
{
  eventType: "Explorer Position",
  timeStamp: float,
  position: Vector3 // (x, y, z) position
}
```

#### Enter Neighborhood
Logging of when the Explorer enters a neighborhood

```
{
  eventType: "Enter Neighborhood",
  timeStamp: float
}
```

#### Exit Neighborhood
Logging of when the Explorer leaves a neighborhood

```
{
  eventType: "Exit Neighborhood",
  timeStamp: float
}
```

#### Visited House
Logging of when the Explorer visits (interacts with) a House.

```
{
  eventType: "Visited House",
  timeStamp: float,
  houseBitterProb: float	// Probability of bitterness for given house
}
```

#### Selector Shown Candy [WIP]
Logging of when a Candy is displayed to the Selector

```
{
  eventType: "Displayed Candy",
  timeStamp: float,
  selectedCandy: string // Name of the png file for the selected candy
}
```

#### Selector Categorize
Logging of each decision made by the Selector with a given batch of Candies.

```
{
  eventType: "Selector Categorize",
  timeStamp: float,
  selectedCandyCategory: string, 	// "Bitter" or "Sweet"
  actualCandyCategory: string 	// "Bitter" or "Sweet"
}
```

#### Selector Finish [WIP]
Logging of when Selector finishes with their selection task for the current batch.

```
{
  eventType: "Selector Finish",
  timeStamp: float
}
```

#### Marker Placed
Logging of when the Selector places a marker.

```
{
  eventType: "Marker Placed",
  timeStamp: float,
  markerPos: Vector3 // (x, y, z) position of marker
}
```

#### Marker Reached
Logging of when the Explorer reaches a marker.

```
{
  eventType: "Marker Reached",
  timeStamp: float
}
```

#### Request to Leave [WIP]
Logging of when either player makes a request to leave.

```
{
  eventType: "Requested to Leave",
  timeStamp: float,
  playerType: string	// "Explorer" or "Selector"
}
```

#### Leave Response [WIP]
Logging of when either player responds to a request to leave.

```
{
  eventType: "Leave Response",
  timeStamp: float,
  response: string	// "Accept" or "Deny"
}
```

#### Game Summary [WIP]
Logging of stats at the end of a game.

```
{
  eventType: "Game Summary",
  timeStamp: float,
  numBitterCorrect: int,
  numBitterIncorrect: int,
  numSweetCorrect: int,
  numSweetIncorrect: int
}
```

## AI Input
Currently, the plan is to communicate with Python over local TCP sockets (i.e. localhost:12345). The game will intermittedly send over game state data (and potentially screenshot data) to the Python program over the socket, and will request for input back into the game.

### Game State Data [WIP]
The current structure of data is as follows:
```
{
  observation: {
    explorer: {
      position: Vector3,
      scale: Vector3,
      rotation: Vector4, // Quaternion
      allowPlayerInput: bool, // NOT NEEDED: express through actions array
      canInteract: bool // NOT NEEDED: express through actions array
    },
    selector: {
      position: Vector3,
      allowPlayerInput: bool, // NOT NEEDED: express through actions array
      
      // TODO: when selector is in selection mode
      candyImg: byte[]
    },
    neighborhoodData: [
      {
        houseData: [
          {
            position: Vector3,
            scale: Vector3,
            rotation: Vector4, // Quaternion
            visited: bool,
            mailboxColor: Vector4
          },
          ...
        ],
        numBitterCorrect: int,
        numBitterIncorrect: int
      },
      ...
    ],
    barrierData: [
      {
        position: Vector3,
        scale: Vector3,
        rotation: Vector4, // Quaternion
      },
      ...
    ],
    trapData: [
      {
        position: Vector3,
        scale: Vector3,
        rotation: Vector4, // Quaternion
      },
      ...
    ],
    timeLeft: float,
    scoring: {
      numBitterCorrect: int,
      numBitterIncorrect: int,
      numSweetCorrect: int,
      numSweetIncorrect: int
    }
  },
  actions: int[] // Array of possible actions that can be taken
}
```
Many parts of the above are static (barrier, house, and trap positions). These can be exported once at the beginning, then not needed again. For houses, we can export positions once, associate them with IDs, then only need to continuously output the ID and whether or not a house has been visited.

### Screenshot
Screenshots can be captured for the game (which uses a 16:9 ratio). The size of the screenshot can be adjusted within Unity.

## Game Config [TODO]
A json file will be usable to configure various parts of the game - i.e. the bitterness distribution of each neighborhood, game round time, etc. This should make it easier to just upload settings for the game rather than having to fill out a settings page. Will update this as implementation progresses.
