---
title: Logging Data
---

# BitterBuster Logging Data
## Overview
This document provides the details and schema for the logging data exported by the BitterBuster game. 

With each run of the game, data points are logged for each specific event that occurs within the gameplay. These are exported into a `json` file in the `Logs` directory created at the root working directory of the BitterBuster executable. The event log contains arrays of logging objects that each follow the general form:
```
{
  "eventType": string,
  "timeStamp": float,
  ...
}
```

Each different event is associated with a different set of key/value data pairs that can be parsed for data interpretation.

## Logging Event Types
### Explorer Position
Logging of Explorer position by the game every x seconds (current build sets this as 2, but this value will be adjustable in the final version)

```
{
  "eventType": "Explorer Position",
  "timeStamp": float,
  "position": Vector3 // (x, y, z) position
}
```

### Explorer Trapped
Logging of when the Explorer is trapped in the game

```
{
  "eventType": "Explorer Trapped",
  "timeStamp": float
}
```

### Enter Neighborhood
Logging of when the Explorer enters a neighborhood

```
{
  "eventType": "Enter Neighborhood",
  "timeStamp": float,
  "neighborhoodBitterProb": float // Probability of bitterness for given neighborhood
}
```

### Exit Neighborhood
Logging of when the Explorer leaves a neighborhood

```
{
  "eventType": "Exit Neighborhood",
  "timeStamp": float
}
```

### Visited House
Logging of when the Explorer visits (interacts with) a House.

```
{
  "eventType": "Visited House",
  "timeStamp": float,
  "houseBitterProb": float	// Probability of bitterness for given house
}
```

### Selector Shown Candy
Logging of when a Candy is displayed to the Selector

```
{
  "eventType": "Displayed Candy",
  "timeStamp": float,
  "selectedCandy": string // Name of the png file for the selected candy
}
```

### Selector Categorize
Logging of each decision made by the Selector with a given batch of Candies.

```
{
  "eventType": "Selector Categorize",
  "timeStamp": float,
  "selectedCandyCategory": string, 	// "Bitter" or "Sweet"
  "actualCandyCategory": string 	// "Bitter" or "Sweet"
}
```

### Selector Finish
Logging of when Selector finishes with their selection task for the current batch.

```
{
  "eventType": "Selector Finish",
  "timeStamp": float
}
```

### Marker Placed
Logging of when the Selector places a marker.

```
{
  "eventType": "Marker Placed",
  "timeStamp": float,
  "markerPos": Vector3 // (x, y, z) position of marker
}
```

### Marker Reached
Logging of when the Explorer reaches a marker.

```
{
  "eventType": "Marker Reached",
  "timeStamp": float
}
```

### Request to Leave
Logging of when either player makes a request to leave.

```
{
  "eventType": "Requested to Leave",
  "timeStamp": float,
  "playerType": string	// "Explorer" or "Selector"
}
```

### Leave Response
Logging of when either player responds to a request to leave.

```
{
  "eventType": "Leave Response",
  "timeStamp": float,
  "response": string	// "Accept" or "Deny"
}
```

### Game Summary
Logging of stats at the end of a game.

```
{
  "eventType": "Game Summary",
  "timeStamp": float,
  "numBitterCorrect": int,
  "numBitterIncorrect": int,
  "numSweetCorrect": int,
  "numSweetIncorrect": int
}
```
