---
title:  "PowWow: A Dataset and Study on Collaborative Communication in Pommerman"
layout: project
permalink: /pow-wow/
---
<div markdown="block">
Takuma Yoneda<sup>🤖</sup>, &nbsp;Matthew R. Walter<sup>🤖</sup>, &nbsp;Jason Naradowsky<sup>🦄</sup>  
🤖: Toyota Technological Institute at Chicago &nbsp;&nbsp;🦄: Preferred Networks, Inc.  
[[PDF][paper]]  [[Dataset][dataset]]  [[Data collection tools (Github)][data-collection-tools]]
</div>
{: class="centering"}

<!-- ### Abstract -->
<!-- <h3 class="centering margin-above">Abstract</h3> -->
### Abstract
{: class="centering margin-above"}
<div markdown="block">
In multi-agent learning, agents must coordinate with each other in order to succeed.
For humans, this coordination is typically accomplished through the use of language.
In this work we perform a controlled study of human language use in a competitive team-based game, and search for useful lessons for structuring communication protocol between autonomous agents.

We construct Pow-Wow, a new dataset for studying situated goal-directed human communication.
Using the Pommerman game environment, we enlisted teams of humans to play against teams of AI agents, recording their observations, actions, and communications. We analyze the types of communications which result in effective game strategies, annotate them accordingly, and present corpus-level statistical analysis of how trends in communications affect game outcomes.
Based on this analysis, we design a communication policy for learning agents, and show that agents which utilize communication achieve higher win-rates against baseline systems than those which do not.
</div>

# Dataset
You can **download the dataset from [HERE][dataset]**.  
The dataset includes game logs and annotations.

<!-- The data is hosted on Google Drive. If you want to download it with `wget`, please use the following command:   -->
<!-- `wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1x-GHvVTaZ_X2BFlNM1duxA7ZS_iUQAga' -O pow-wow.tar.gz` -->
<!-- Note that it takes ~1 minute to get a response from Google Drive (presumably because it runs virus scan before response). -->
<!-- [the collected game logs](http://example.com) and [annotations of dialogue](http:/example.com). -->


## Brief Statistics

| # Games | # Messages | # Participants |
|---------|------------|----------------|
| 80      | 2,513      | 59             |

## Game logs
Game logs are stored in `valid_games_anonymized/` as json files. The directory structure is the following:
```
valid_games_anonymized/
├── pomlog_20191104-150039
│   ├── 000.json
│   ├── 001.json
│   ├── ...
│   ├── 078.json
│   ├── game_result.txt
│   └── envinfo.json
~
└── pomlog_20191203-214947
    ├── 000.json
    ├── 001.json
    ├── ...
    ├── 095.json
    ├── game_result.txt
    └── envinfo.json
```
A directory `pomlog_20xxxxxx-xxxxxx` contains the information in a game, and `XXX.json` in each directory contains recorded dialogues and game states up to the timestep `XXX`. The result of the game and meta-information of the game environment are stored in `game_result.txt` and `envinfo.json`.

Each json file has the following key & value pairs:
* agents: location and ability of each agent
* board: 11 x 11 matrix that describes what object occupies each cell
* board_size
* bombs: location and state of each bomb
* flames: location and state of each flame
* messages:
	* current_timestep
	* *an integer that corresponds to a timestep*: list of messages sent by both human players at the timestep.
	
For some other details, it can be helpful to visit [the official document of Pommerman](https://docs.pommerman.com/environment/)

## Annotations
Annotations are stored in `annotations_anonymized.csv`.


[data-collection-tools]: https://github.com/takuma-ynd/pow-wow-data-collection
[dataset]: https://github.com/takuma-ynd/pow-wow-data-collection/raw/master/dataset/pow-wow.tar.gz
[paper]: https://larel-ws.github.io/
