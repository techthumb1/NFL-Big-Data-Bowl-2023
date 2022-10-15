# File Descriptions

The 2023 Big Data Bowl allows participants to use supplemental NFL data as long as it is free and publicly available to all participants. Examples of sources that could be used include nflverse and Pro Football Reference. Please note that the gameId and playId of the Big Data Bowl data merge with the old_game_id and play_id of nflverse's play-by-play data.

Game data: The `games.csv` file contains the teams playing in each game. The _key_ variable `**gameId**` uniquely identifies the game.

Play data: The `plays.csv` file contains all plays in each game along with detailed information on each play. This file also contains play-level information from each game. The _key_ variables that uniquely identifies each play are the `**gameId**` and the `**playId**`.

Player data: The `players.csv` file contains player-level information from players that participated in any of the tracking data files. The _key_ variable to uniquely identify each player is the `**nflId**` variable.

Tracking data: Files `week[week].csv` contain player tracking data from season [week]. The _key_ variables are `**gameId**`, `**playId**`, and `**nflId**`.


## Game Data

- gameID: Game identifier, unique for each game (numeric)
- season: Season of the game 
- week: Week number of the week that the game was played (updated from data reviews)
- gameDate: Game date in mm/dd/yyyy format
- gameTimeEastern: Game start time in Eastern Time in hh:mm:ss format
- homeTeamAbbr: 3-letter abbreviation for visiting team
- visitorTeamAbbr: 3-letter abbreviation for home team awayTeamAbbr

## Play Data

- gameId: Game identifier, unique for each game (numeric)
- playId: Play identifier, not necessarily unique across games; might need to concatenate `gameId` and playId to make a unique play identifier (numeric)
- playDescription: Description of the play from the play-by-play data (string)
- quarter: Quarter of the game (1-5, 5 meaning overtime) (numeric)
- down: Down of the quarter (1 for first down, 2 for second down, etc.) (numeric)
- yardsToGo: Yards needed for a new set of downs (10 yard line, 15 yard line, etc.) (numeric)
- possessionTeam: Abbreviation of the team with the ball (string)
- playType: Type of Play (Pass, Run, Kickoff, Punt, Field_Goal, Extra_Point) (string)
- yardlineSide: Yardline on the given side of the field as labeled by the referee (e.g. 10 yards to go for team A means A has a 80 yard line) (string)
- yardlineNumber: Yardline as labeled by referee (numeric)
- offenseFormation: Formation of offensive players (Shotgun, Shotgun Empty, Shotgun 3 Back, etc.) (string)
- personnelOffense: Player formation of offensive team, space delimited (2 RB, 2 WR, 1 TE, etc.) (string)
- defendersInTheBox: Number of defensive players within 10 yards of the line of scrimmage noted by the referee (updated from data reviews) (numeric)
- numberOfPassRushers: Number of defensive linemen near the line of scrimmage that are right outside of the quarterback (updated from data reviews) (numeric)
- gameClock: Amount of time left in the quarter, does not include overtime periods (mm:ss format) (string)
- preSnapHomeScore: Home score prior to the snap of ball  (numeric)
- preSnapVisitorScore: Visitor score prior to the snap of ball (numeric)
- passResult: Dropback outcome of the play (`C` = Completion, `I` = Incomplete Pass, `S`: Quarterback sack, `IN` = Intercepted by defensive player, `R`: Scramble) (string)
- penaltyYards: yards gained by offense by penalty
- prePenaltyYards: Net yards gained prior to penalties (numeric)
- playResult: Net yards gained by the offense during the play. i ranges between 1 and 3 (numeric)
- absoluteYardlineNumber: Field location of the ball in terms of absolute yards from the opponent's end zone on the play's ground (numeric)
- offenseFormation: Formation used by possession team (string)
- personnelO: Personnel used by possession team (string)
- dropbackType: Dropback category of the quarterback (string)
- pff_playAction: indicator for whether or not play was classified by pff metrics as "play action"
- pff_passCoverage: Coverage scheme of defense. Variable provided by PFF metrics. (string)  
    - Possible values:
        - `Man_coverage`: Coverage type is single coverage. Data will not include "zone" coverage or blended types. (string)
        - `Zone_coverage`: Coverage type is any zone, Cover 4, Cover 3, Cover 1 or Cover 2. (string)
        - `Cover-0`: A Man-to-Man coverage across the board, with no safeties or deep defenders. Typically accompanied by a blitz of some sort. (string)
        - `Cover-1`: When a defense plays Cover 1, only one defender is responsible for covering the entire deep left side of the field. On the deep right side, five defenders are responsible for 20 yards, on the deep middle three are responsible for 10 yards, and one defender covers 20 yards in the opposite flat. All other defense players are responsible for the remaining 30 yards near the line of scrimmage. (string)
        - `Cover-2`: When a defense plays Cover 2, two defenders are responsible for the deep left side, six defenders are responsible for the second level including the deep right, three are responsible for the middle and two defenders split the deep middle, one defender is responsible for the opposite flat, two linebackers split the remaining two zones, and one defender is responsible for covering short/medium passing routes within 3 yards of the line of scrimmage. (string)
        - `Cover-3`: When a defense plays Cover 3, three defenders are responsible for deep left, seven defenders are responsible for the second level, three defenders are responsible for the deep middle, two defenders split the deep right, one defender covers the opposite flat, two players split the other two zones, and one player is responsible for covering short/medium passing routes near the line of scrimmage. (string)
        - `Quarters`: A Quarters Concept on both halves of the field. In general it will be a 4 Deep, 3 Under concept where the corners are on #1, safeties on #2, and backside safety rotation dependent on formation. (string)
        - `Cover-6`: A Quarters Concept on half the field and a 2 Deep on the other half. It contains a fairly common pattern for zone defenses. (string)
        - `Bracket`: Recorded in the field and up to the 12 yard line in the red zone – when two offensive players      have an in and out bracket by two defenders
        - `Goal Line`: Calls where a Goal Line defense is used.
        - `Red Zone`:  Calls that are typically specific to the Red Zone and do not occur in the field often
        - `Prevent`: Special end of half or end of game situations where a Prevent defense is utilized
        - `Miscellaneous`: Coverage concepts that we feel do not comfortably fit into any of our coverage categories
        - `pff_passCoverageType`: Whether defense's coverage type was man, zone or other. Variable provided by PFF      (text)


## Player data

- `nflId`: Player identification number, unique across players (numeric)
- `height`: Player height (text)
- `weight`: Player weight (numeric)
- `birthDate`: Date of birth (YYYY-MM-DD)
- `collegeName`: Player college (text)
- `officialPosition`: Official player position (text)
- `displayName`: Player name (text)


## PFF Scouting data

- `gameId`: Game identifier, unique (numeric)
- `playId`: Play identifier, not unique across games (numeric)
- `nflId`: Player identification number, unique across players (numeric)
- `pff_role`: The player's role on this play (text)
    - Possible values:
        - Coverage: Defensive player. Player whose initial goal is to play man or zone coverage
        - Pass: Offensive player. Player identified as the passer
        - Pass block: Offensive player. Anyone fully blocking a defender from the QB, or anyone in a clear pass block stance
        - Pass route: Offensive player. Any player not identified as a Pass Blocker or Passer
        - Pass rush: Defensive player. Any player whose initial intent is to rush the passer
- `pff_positionLinedUp`: Position that the player was aligned at the snap of the ball on this play (text)
- `pff_hit`: If player is a defensive player, indicator for whether they are credited with recording a hit on this play (binary)
- `pff_hurry`: If player is a defensive player, indicator for whether they are credited with recording a hurry on this play (binary)
- `pff_sack`: If player is a defensive player, indicator for whether they are credited with recording a sack on this play (binary)
- `pff_beatenByDefender`: If player is a blocking offensive player, indicator for whether they are by a defender but was not charged for yielding a hit, hurry or sack (binary)
- `pff_hitAllowed`: If player is a blocking offensive player, indicator for whether they are responsible for a hit on the QB (binary)
- `pff_hurryAllowed`: If player is a blocking offensive player, indicator for whether they are responsible for a hurry on the QB (binary)
- `pff_sackAllowed`: If player is a blocking offensive player, indicator for whether they are responsible for a sack on the QB (binary)
- `pff_nflIdBlockedPlayer`: If player is a blocking offensive player, the nflId of the first defender the offensive player blocked (numeric)
- `pff_blockType`: If player is a blocking offensive player, the type of block that the offensive player is executing on the defender (text)

    - Possible values:
        - BH: Backfield Help - A block from a player aligned in the backfield on which the blocker merely helps on a block rather than fully engaging his assignment. Usually seen when a blocker is clearing up a block or picking up a defender when he has broken through or been missed by another blocker
    CH: Chip Block - This is only to be used for players who chip a pass rusher when they release for their route
    CL: Second Level – A block made at the second level, this must be at least two yards across the line of scrimmage
    NB: No Block - If a blocker executes no block on a play but simply runs his path or takes his pass set then we will note him with one all blocking line with this block type
    PA: Play Action Pass Protection - A blocker pass protecting inline on a play action pass selling the play action by stepping in to show a run block before converting to pass protect
    PP: Pass Protection - A standard pass protection block from an inline blocker
    PR: Pocket Roll Block - This block type will be used any time the offense is executing a “rolling pocket” by which the entire offensive line moves with the QB’s rollout to stay in front of him but without ever taking a “conventional” pass set. There will be flexibility here to record the PR – Pocket Roll Block type in the same way as PA & RP block types in that individual matchups & responsibilities won’t always be obvious or necessary, so PR block types can be recorded by multiple blockers on an individual defender on the same play
    T: Post Block - A post block by an offensive player in pass protection to control a defender for another blocker while clearly demonstrating that he is not, at least initially, trying to fully engage with the block
    PU: Backfield Pickup - A pass protection pick-up by a player aligned in the backfield
    SR: Set & Release - A blocker who sets to pass protect a defender before releasing. This block will cover both players releasing from a set to block for a screen as well as “hold ups” by tight ends before they leak into the flat
    SW: Switch Block - A blocker who passes off (or attempts to pass off) a defender. Most often used on stunts but can also be used for pass offs when pass rushers are slanting across the pocket or interior defenders are working to the edge to replace a dropping edge rusher, with an interior offensive lineman passing them out rather than staying with them
    UP: Pull Pass Protection - A blocker pulling in pass protection from an inline alignment to block a defender in pass protection
pff_backFieldBlock:If player is a blocking offensive player, indicator for whether block occured in offensive backfield.

## Tracking data

Files week[week].csv contains player tracking data from week [week].

- **`gameId1`**: Game identifier, unique (numeric)
- **`playId`**: Play identifier, not unique across games (numeric)
- **`nflId`**: Player identification number, unique across players. When value is NA, row corresponds to ball. (numeric)
`frameId`: Frame identifier for each play, starting at 1 (numeric)
`time`: Time stamp of play (time, yyyy-mm-dd, hh:mm:ss)
`jerseyNumber`: Jersey number of player (numeric)
`club`: Team abbrevation of corresponding player (text)
`playDirection`: Direction that the offense is moving (left or right)
`x`: Player position along the long axis of the field, 0 - 120 yards. See Figure 1 below. (numeric)
`y`: Player position along the short axis of the field, 0 - 53.3 yards. See Figure 1 below. (numeric)
`s`: Speed in yards/second (numeric)
`a`: Acceleration in yards/second^2 (numeric)
`dis`: Distance traveled from prior time point, in yards (numeric)
`o`: Player orientation (deg), 0 - 360 degrees (numeric)
`dir`: Angle of player motion (deg), 0 - 360 degrees (numeric)
`event`: Tagged play details, including moment of ball snap, pass release, pass catch, tackle, etc (text)
