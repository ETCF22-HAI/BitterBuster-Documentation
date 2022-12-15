---
title: Configuration Data
---

# BitterBuster Configuration Data
## Overview
This document provides the details and schema for the configuration file that can be used to configure the BitterBuster game. 

## Configuration File Details
A `JSON` file can be used to configure various parts of the game - i.e. the bitterness distribution of each neighborhood, game round time, etc. This should make it easier to upload settings for the game rather than having to fill out a settings page or rebuild the game.

Below is a sample configuration file and the default values of each.
```
{
  "showVisualMemory": false,          // Toggle for visual memory on the selector
  "sourBitterProb": -1.0f,            // Bitterness probability for the sour neighborhood
  "dessertBitterProb": -1.0f,         // Bitterness probability for the dessert neighborhood
  "giftBitterProb": -1.0f,            // Bitterness probability for the gift neighborhood
  "partyBitterProb": -1.0f,           // Bitterness probability for the party neighborhood
  "explorerPosPingInterval": 2.0f,    // Interval in seconds at which the explorer's position will be logged
}
```

### Parameter Notes
For each of the neighborhood bitterness probability, a value between [0, 1] is expected. If a value outside of this range is provided, then the bitterness probability for this neighborhood will be randomly generated.

Game time is pulled out to its own input box in the settings configuration page as it's most likely to be changed more frequently.
