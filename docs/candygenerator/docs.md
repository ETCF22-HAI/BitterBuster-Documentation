---
title: Candy Generator Documentation
---

# Candy Generator Documentation
## Overview
This document provides the details on how to set up a development environment for the BitterBuster Candy Generator.

## Setup
### Repository Link
[https://github.com/ETCF22-HAI/CandyGeneration](https://github.com/ETCF22-HAI/CandyGeneration)

### Tech Requirements
The candy generator is written in [Python 3](https://www.python.org/downloads/). Basic instructions on setting up the development environment and running the given scripts are provided in the repository's [README file](https://github.com/ETCF22-HAI/CandyGeneration/blob/master/README.md).

### Installation Steps
1. Clone the repository locally
2. Set up a Python virtual environment in the root directory

        % python -m venv venv

3. [Activate the virtual environment](https://docs.python.org/3/tutorial/venv.html#creating-virtual-environments) based on OS
4. Install all the requirements

        % pip install -r requirements.txt


## Tutorial
### Generating Candies
Assets for the candies along with a sample generation script `generate.py` are provided within the repository. This script will generate candies based on the components along with corresponding `JSON` files describing the attributes/labels of each candy. 

Some adjustable parameters are provided at the top of the `generate.py` file.

#### Example Usage
To generate all candies:
```
% python generate.py
```

To generate all candies with multiprocessing enabled:
```
% python generate.py -p
```

To generate `N` candies:
```
% python generate.py -n N
```

To generate `N` candies while feeding in a particular randomization seed `S`:
```
% python generate.py -n N -s S
```

### Categorizing Candies
A sample categorization script `categorize.py` is provided within the repository. 

To customize the parameters for determining bitterness, you can update the predicate function `is_bitter` at the top of the file. For example, to categorize Candies by warm/cold body color where cold corresponds to bitterness:

```
def is_bitter(labels):
  return labels["body"]["hue"] == "cold"
```

Categorization will then act upon the generated candies from the generation script by running:
```
% python categorize.py
```

### Candy Labels
Below is a list of all labels associated with each Candy Component that can be used for categorization:

```
{
    "left_arm": {
        "side": "left",
        "orientation": ["up", "down"]
    },
    "right_arm": {
        "side": "right",
        "orientation": ["up", "down"]
    },
    "body": {
        "hue": ["cold", "warm"],
        "shape": ["sharp", "round", "mixed"]
    },
    "eye": {
        "lash": ["lash", "nolash"],
        "distance": ["narrow", "middle", "wide"]
    },
    "leg": {
        "length": ["short", "middle", "long"],
        "orientation": ["inward", "left", "right", "outward"]
    },
    "mouth": {
        "openness": ["open", "close"]
    },
    "pattern": {
        "type": ["dots", "stripes"]
    }
}
```

## Licensing 
The 2D Candy Components were created by Constanza Tong and scripts were written by Angela Zhang. All licensing information regarding both art assets and source code can be found [here](https://github.com/ETCF22-HAI/CandyGeneration/blob/master/LICENSE.md).
