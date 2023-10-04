# retrosheet_2022
Extraction and transformation of Retrosheet's annual summer release June 2023
The information used here was obtained free of charge from and is copyrighted by Retrosheet. Interested parties may contact Retrosheet at "www.retrosheet.org".

## Motivation
- Extraction and transformation of the annual Retrosheet data release. The source files can be found here: https://retrosheet.org/june2023release.html
- The purpose is to compile, clean, and reorganize the data into a format appropriate for loading into a relational database with minimal redundancies.
- Errors that have been discovered have been reported to RS and, whenever possible, corrected in these files. For cases where it is not possible to correct errors, they have been left in place and should be corrected in the source files by the next summer release in 2024.

## Overview
The data is organized into the following *.csv* files:
- Personnel: Biographical data on players, managers, coaches, and umpires. 
- Parks: Data relating to the history of the ballparks used by MLB teams.
- Active teams: Teams and leagues by season.
- Teams: Basic historical info on teams.
- Rosters: Players and teams by season.
- Game info: Administrative info for games, such as teams, locations, attendance, weather conditions, etc.
- Events: Complete recounting of game events as one would see on the official score sheet, for each game in the record.
- Game log teams: Team summary statistics and related info for each game in the record.
- Game log batters: Individual batting statistics for each game in the record.
- Game log pitchers: Individual pitching statistics for each game in the record.
- Game log fielders: Individual fielding statistics for each game in the record.
- Appearances: Individual appearances by team, batting order, fielding position, and start/bench for each game in the record.
- Ejections: Summary of ejections, including personnel involved and reasons.
- Transactions: Summary of transactions such as trades, draft results, DFA, etc.

Event, appearance, and game log files are broken up into multiple *zip* files to comply with Github's file-size restrictions. The misc *zip* file contains the remaining *.csv* files:
>     retrosheets_active_teams.csv
>     retrosheets_ejections.csv
>     retrosheets_game_info.csv
>     retrosheets_game_log_teams.csv
>     retrosheets_parks.csv
>     retrosheets_personnel.csv
>     retrosheets_rosters.csv
>     retrosheets_teams.csv
>     retrosheets_transactions.csv
## Detail
**Personnel**
- *id*: Should be an 8-character alpha-numeric code. The format is the first 4 characters of the players last name followed by the first character of the players first name, followed by a three-digit numerical code. If a player's last name is less than 4 characters long, a dash "-" is used as a placeholder. Numbers starting with 001 are used for players appearing in games in or after 1983. Players completing their careers before 1983 are assigned numbers starting with 101. Umpires are assigned numbers starting with 901, coaches are assigned numbers starting with 801, and official scorers are assigned numbers starting with 701. In cases where an individual held multiple roles (manager, umpire, or coach) over the course of their careers, the player id is maintained. There are a small number of entries that do not follow this system. In these cases, the entries are left as they are in the source files and have been reported to Retrosheet for correction.
- *last_name*: individual's last name.
-  *first_name*: individual's first name.
- *use_name*: Name of individual in common use.
- *birth_date*: individual's birth date.
- *birth_city*: individual's birth city.
- *birth_state*: individual's birth state. For US states, this is given as the two-letter postal code. For international players, this is given by the full name of the administrative district for that country. The given value is contemporary to the individual's birth and may not reflect the current name due to redistricting policies. One notable example occurred in 1976 when the six Cuban provinces established by the Spanish colonial government were reorganized into fourteen provinces and one special municipality. 
- *birth_country*: individual's birth country. Whenever possible, this is given as the ISO 3166 alpha-3 country code. In several cases, this is not possible and the name of the region at the time of the player's birth is given. 
- *player_debut_date*: Date of first appearance as a player.
- *player_last_date*: Date of last appearance as a player.
- *manager_debut_date*: Date of first appearance as a manager.
- *manager_last_date*: Date of last appearance as a manager.
- *coach_debut_date*: Date of first appearance as a coach.
- *coach_last_date*: Date of last appearance as a coach.
- *umpire_debut_date*: Date of first appearance as an umpire.
- *umpire_last_date*: Date of last appearance as an umpire.
- *death_date*: Date of individual's death.
- *death_city*: City of individual's death. 
- *death_state*: State of individual's death. The same caveats regarding the birth state apply to this field.
- *death_country*: Country of individual's death. The same caveats regarding the birth country apply to this field.
- *bat_hand*: Batting hand ("l", "r", or "b").
- *throw_hand*: Throwing hand ("l", "r", or "b").
- *height*: Height in inches.
- *weight*: Weight in pounds
- *cemetery_name*: Name of cemetery where individual is buried.
- *cemetery_city*: City of cemetery where individual is buried.
- *cemetery_state*: State of cemetery where individual is buried. The same caveats regarding the birth state apply to this field.
- *cemetery_country*: Country of cemetery where individual is buried. The same caveats regarding the birth country apply to this field.
- *cemetery_note*: Additional information regarding individual's burial.
- *birth_name*: Individual's given name at birth.
- *name_change*: 
- *bat_change*:
- *hof*: Is the individual in the Baseball Hall of Fame? ("t" or "f")

## Parks
- *id*: Unique 5-character alpha-numeric code.
- *name*: Name of park.
- *aka*: Alternate name of park.
- *city*: Name of city where park is/was located.
- *state*: State where park is located. For US states, this is given as the two-letter postal code. For international parks, this is given by the full name of the administrative district for that country.
- *start_date*: First date when the park hosted a game.
- *end_date*: Last date when the park hosted a game.
- *league_id*: League of the primary occupant of the park.
- *notes*: Additional info regarding the facility. Primarily used to identify other teams that played home games at that location.
- *country*: Country where park is located. This is given as the ISO 3166 alpha-3 country code.

## Active teams
- *season*: Year
- *id*: Unique, 3-character code for the team of record.
- *league*: League the team played in for that season. Null values indicate that the team was independent for that season.
- *division*: Division the team played in that season. Null values for season prior to introduction of division play.

## Teams
- *id* : Unique, 3-character code of the team in the time period between *est_date* and *last_date*.
- *current_id*: Unique, 3-character code of the team if the team currently plays in the MLB.
- *name1*: First identifier for the team of record; typically the city or region the team orginates from.
- *name2*: Second identifier for the team of record; typically the mascot associated with the team.
- *alt_name*: Alternate identifier for the team of record.
- *league*: League or leagues of the team in the time period between *est_date* and *last_date*.
- *division*: Division of the team in the time period between *est_date* and *last_date*.
- *city*: Home city of the team of record.
- *state*: Home state of the team of record. 
- *est_date*: Date the team was established. If the month or day is not precisely known, a default value of 4/1/xxxx is given.
- *last_date*: Date the team made its last appearance. If the month or day is not precisely known, a default value of 11/1/xxxx is given.

## Teams current names
This file is included to quickly reference older ids of current teams.
- *id*: Unique, 3-digit code of the MLB team. May be current or a previous iteration of the team.
- *current_id*: Unique, 3-digit code of the current MLB team, if applicable.	
- *league_id*: League the team played in for that season.
- *division*: Division the team played in for that season, when applicable. Null, otherwise.
- *location*: City, state, or region that the team represents.
- *name*: Common name or mascot associated with the team.	
- *alt_name*: Alternate name or mascot associated with the team.	
- *date_first*: Date of first MLB appearance with the unique combination of old_id, league, division, and name values.
- *date_last*: Date of last MLB appearance with the unique combination of old_id, league, division, and name values.
- *city*: City of the team's home park.	
- *state*: State of the team's home park as a two-character code (ON and QC for Ontario and Quebec, respectively).

## Rosters
- *player_id*: Unique 8-digit alpha-numeric code that references the personnel file.
- *team_id*: Unique 8-digit alpha-numeric code that references the teams file.
- *season*: Season for which the player appeared on the team roster.

## Game Info
- *id*: Unique 12-digit alpha-numeric code for each game in the record. of the form team_id+yyyymmdd+game_num.
- *game_date*: Date-time of the game in a 24hr format, i.e., yyyy-mm-dd hh:mm:ss.
- *game_num*: Number of the game played on game_date. Indicates a single game (0) or game (1) or game (2) of a double-header.
- *home_team*: Home team id. References team file.
- *home_league*: Home team league id as a 2 or 3-digit code:
    >     NL: National League
    >     AL: American League
    >     NNL: Negro National League
    >     NN2: Negro National League II
    >     NAL: Negro American League
    >     ECL: Eastern Colored League
    >     ANL: American Negro League
    >     EWL: East-West League
    >     NSL: Negro Southern League
    >     FL: Federal League
    >     AA: American Association
    >     PL: Players League
    >     UA: Union Association
    >     NA: National Association
- *home_game_num*: Number of game for the home team. Ties are counted as games and suspended games are counted from the starting rather than the ending date.
- *vis_team*: Visiting team id. References team file.
- *vis_league*: Visiting team league id as a 2 or 3-digit code. See above.
- *vis_game_num*: Number of game for the visiting team. Ties are counted as games and suspended games are counted from the starting rather than the ending date.
- *park_id*: Unique 5-digit alpha-numeric code. References parks file.
- *attendance*: Best estimate of the attendance at the game, if available.
- *completion_info*: If the game was completed later (either due to a suspension or an upheld protest) this field will include: "yyyymmdd, park, vs, hs, len" where yyyymmdd is the date the game was completed. All the rest of the information in the record refers to the entire game.
- *park*: the park ID where the game was completed.
- *vs*: the visitor score at the time of interruption.
- *hs*: the home score at the time of interruption.
- *len*: the length of the game in outs at time of interruption.
- *precip*: Precipitation reported for the game, if known. Possible values:
  >     rain
  >     drizzle
  >     showers
  >     snow
- *sky*: Sky conditions reported for the game, if known. Possible values:
  >     overcast
  >     sunny
  >     night
  >     cloudy
  >     dome
- *temperature*: Temperature in degrees F.
- *wind_dir*: Wind direction reported for the game. Possible values:
  >     to left
  >     left to right
  >     right to left
  >     from left
  >     to right
  >     to center
  >     from center
  >     from right
- *wind_speed*: Wind speed reported for the game, if known (in miles per hour).
- *day_night*: Day or night indicator ("d" or "n")
- *field_cond*: Field conditions reported for the game, if known. Possible values:
  >     wet
  >     dry
  >     soaked 
  >     damp
- *forfeit*: Forfeit information. Possible values:
    >     "V": the game was forfeited to the visiting team
    >     "H”: the game was forfeited to the home team.
    >     "T”: the game was ruled a no-decision.
- *protest_info*: Protest information. Possible values:
    >     "P”: the game was protested by an unidentified team.
    >     "V”: a disallowed protest was made by the visiting team.
    >     "H”: a disallowed protest was made by the home team.
    >     "X”: an upheld protest was made by the visiting team.
    >     "Y”: an upheld protest was made by the home team.
- *off_scorer*: 8-digit alpha-numeric code that references the personnel file.
- *htbf*:	***Drop***
- *sched_innings*: Number of scheduled innings. For NGL double-headers, this may give a value of 7. Null values indicate a regular 9-inning game.
- *season_type*: Type or "season" the game is played under. Possible values:
    >     "rs": regular season
    >     "as": all-star game
    >     "dv": post-season division series (MLB)
    >     "lc": post-season league championship series (MLB)
    >     "wc": post-season wild card game (MLB)
    >     "ws": post-season world series game (MLB)
    >     "ex": exhibition game (typically NGL or barnstorming teams)
    >     "ch": post-season championship games (NGL)
- *game_len_outs*: Length of game in outs.
- *game_len_min*: Length of game in minutes.
- *use_dh*: Use designated hitter ("t" or "f").
- *acquisition_info*: Acquisition information:
    >     "Y": the complete game is available.
    >     "N": no portion of the game is available.
    >     "D": the game was derived from box score and game story.
    >     "P": some portion of the game is available. There may be missing innings at the
    >          beginning, middle and end of the game.
- *additional_info*: Additional information. This is a mix of informational items that do not warrant a separate field. The field is alpha-numeric. Some items are represented by tokens such as "HTBF" (home team batted first). Note: if "HTBF" is specified it would be possible to see something like "01002000x" in the visitor"s line score. Changes in umpire positions during a game will also appear in this field. These will be in the form *umpchange, inning, umpPosition, umpid* with the latter three repeated for each umpire. These changes occur with umpire injuries, late arrival of umpires or changes from completion of suspended games. Details of suspended games are in completion_info.
- *ps_scorer*: Administrative info pertaining to how the game account was acquired and processed.
- *translator*: Administrative info pertaining to how the game account was acquired and processed.
- *inputter*: Administrative info pertaining to how the game account was acquired and processed.
- *input_time*: Administrative info pertaining to how the game account was acquired and processed.
- *edit_time*: Administrative info pertaining to how the game account was acquired and processed.
- *how_scored*: Administrative info pertaining to how the game account was acquired and processed.
- *pitches_entered*: Administrative info pertaining to how the game account was acquired and processed.
- *postpone_cancel_info*: Further information pertaining to why a game was postponed or canceled.

## Events
- *game_id*: Unique 12-digit alpha-numeric code for each game in the record. Of the form team_id+yyyymmdd+game_num.
- *vis_team*:  Visiting team id. References team file.
- *inning*: Inning number.
- *batting_team*: Team at bat (0 for visiting team and 1 for home team).
- *outs*: Number of outs before the play.
- *balls*: Number of balls awarded to batter on the play of record.
- *strikes*: Number of strikes charged to the batter on the play of record.
- *pitch_sequence*: Pitch sequence for the play of record.
    >     "+": following a pickoff throw by the catcher.
    >     "*": Indicates the following pitch was blocked by the catcher
    >     ".": marker for play not involving the batter.
    >     "1": pickoff throw to first.
    >     "2": pickoff throw to second.
    >     "3": pickoff throw to third.
    >     ">": Indicates a runner going on the pitch.
    >     "A": automatic strike, usually for pitch timer violation
    >     "B": ball 
    >     "C": called strike
    >     "F": foul
    >     "H": hit batter
    >     "I": intentional ball
    >     "K": strike (unknown type)
    >     "L": foul bunt
    >     "M": missed bunt attempt
    >     "N": no pitch (on balks and interference calls)
    >     "O": foul tip on bunt
    >     "P": pitchout
    >     "Q": swinging on pitchout
    >     "R": foul ball on pitchout
    >     "S": swinging strike
    >     "T": foul tip
    >     "U": unknown or missed pitch
    >     "V": called ball because pitcher went to his mouth or automatic ball on intentional walk or
    >          pitch timer violation.
    >     "X": ball put into play by batter
    >     "Y": ball put into play on pitchout

- *vis_score*: Number of runs for the visiting team before the play of record.
- *home_score*: Number of runs for the home team before the play of record.
- *batter*: Batter id; unique 8-digit alpha-numeric code that references personnel file.
- *batter_hand*: Batter hand ("l" or "r")	
- *res_batter*: Result batter id; unique 8-digit alpha-numeric code that references personnel file. Only differs from "batter" field if the batter is replaced during the time at bat and the final event is charged to the previous batter. For example, if a pinch-hitter is inserted with two strikes and then takes strike three, the strikeout is charged to the first batter (the responsible   batter)
- *res_batter_hand*: Result batter hand ("l" or "r").	
- *pitcher*: Pitcher id; unique 8-digit alpha-numeric code that references personnel file.
- *pitcher_hand*: Pitcher hand ("l" or "r")
- *res_pitcher*: Result pitcher id; unique 8-digit alpha-numeric code that references personnel file. Only differs from the "pitcher" field when a pitcher is changed during an at-bat and the first pitcher is charged with the result.  For example, if a relief pitcher enters with a three-ball, no-strike count and throws ball four, then the walk is charged to the first pitcher.
- *res_pitcher_hand*: Result pitcher hand ("l" or "r").

Fielding positions for the play of record.
- *catcher*: Catcher id; unique 8-digit alpha-numeric code that references personnel file.
- *first_base*: First baseman id; unique 8-digit alpha-numeric code that references personnel file.
- *second_base*: Second baseman id; unique 8-digit alpha-numeric code that references personnel file.
- *third_base*: Third baseman id; unique 8-digit alpha-numeric code that references personnel file.
- *shortstop*: Shortstop id; unique 8-digit alpha-numeric code that references personnel file.
- *left_field*: Left fielder id; unique 8-digit alpha-numeric code that references personnel file.
- *center_field*: Center fielder id; unique 8-digit alpha-numeric code that references personnel file.
- *right_field*: Right fielder id; unique 8-digit alpha-numeric code that references personnel file.

Player occupying bases at the start of the play of record.
- *first_runner*: Runner on first base id; unique 8-digit alpha-numeric code that references personnel file.
- *second_runner*: Runner on second base id; unique 8-digit alpha-numeric code that references personnel file.
- *third_runner*: Runner on third base id; unique 8-digit alpha-numeric code that references personnel file.

- *event_text*: The encoded description of the play of record using the format described for the event files. Full explanation of the scoring system can be found here: https://www.retrosheet.org/eventfile.htm#:~:text=The%20event%20field%20of%20the%20play%20record
- *leadoff_flag*: Indicator if the play of record occurs for the first batter of an inning ("t" or "f").	
- *pinchhit_flag*: Indicator if the batter during the play of record is a pinch hitter.
- *defensive_position*: The defensive position currently being played by this batter. It is pinch-hitter (position 11) for pinch-hitters.
- *lineup_position*: Position in the batting order for this batter.
- *event_type*: Type of event for the play of record. There are 25 possible values that describe the type of event.
  >     "Unknown event"
  >     "No event"
  >     "Generic out"
  >     "Strikeout"
  >     "Stolen base"
  >     "Defensive indifference"
  >     "Caught stealing"
  >     "Pickoff error"
  >     "Pickoff"
  >     "Wild pitch"
  >     "Passed ball"
  >     "Balk"
  >     "Other advance"
  >     "Foul error"
  >     "Walk"
  >     "Intentional walk"
  >     "Hit by pitch"
  >     "Interference"
  >     "Error"
  >     "Fielders choice"
  >     "Single"
  >     "Double"
  >     "Triple"
  >     "Home run"
  >     "Missing play"

- *batter_event_flag*: One character indicator of whether the event terminated the batter"s appearance:
  >     "t" = yes, which is most common.
  >     "f" = no, meaning the same batter stayed at the plate, such as after a stolen base.
- *ab_flag*: A one character indication of whether batter was charged with at-bat ("t" = yes, "f" = no).
- *hit_value*: One number indicating value of hit
  >     "0" (no hit)
  >     "1" (single)
  >     "2" (double)
  >     "3" (triple)
  >     "4" (home run)
- *sh_flag*:  One character indicating sacrifice hit ("t" = yes; "f" = no).
- *sf_flag*: One character indicating sacrifice fly ("t" = yes; "f" = no).
- *outs_on_play*: Number of outs recorded on this play.  	
- *double_play_flag*: One character indicating double play ("t" = yes; "f" = no).
- *triple_play_flag*: One character indicating triple play ("t" = yes; "f" = no).	
- *rbi_on_play*: Number of runs batted in awarded to the batter on the play of record.
- *wild_pitch_flag*: One character indicating a wild pitch ("t" = yes; "f" = no).
- *passed_ball_flag*: One character indicating a passed ball ("t" = yes; "f" = no).
- *fielded_by*: Fielding position of the player who makes a play on the ball. Relevant for base hits when no formal fielding credit is given.
- *batted_ball_type*: Descriptor of batter ball type.
  >     "F" (fly ball)
  >     "L" (line drive)
  >     "P" (pop-up)
  >     "G" (ground ball)
- *bunt_flag*: One character indicating a bunt ("t" = yes; "f" = no).
- *foul_flag*: One character indicating that the play of record occurred in foul ground ("t" = yes; "f" = no).
- *hit_location*: Zone on the field where the ball was hit. A detailed description of the hit location system can be found here: https://www.retrosheet.org/location.htm
- *num_errors*: Number of errors recorded by the defense on the play of record.
- *1st_error_player*: First error player id; unique 8-digit alpha-numeric code that references personnel file.
- *1st_error_type*: One character indicating the type of error ("t" = throwing; "f" = fielding).
- *2nd_error_player*: Second error player id; unique 8-digit alpha-numeric code that references personnel file.
- *2nd_error_type*: One character indicating a bunt ("t" = throwing; "f" = fielding).
- *3rd_error_player*: Third error player id; unique 8-digit alpha-numeric code that references personnel file.
- *3rd_error_type*: One character indicating a bunt ("t" = throwing; "f" = fielding).
- *batter_dest*: The base which the batter reached at the conclusion of the play.  If the player is out, the base is 0.
- *runner_on_1st_dest*: The base which the runner on first base reached at the conclusion of the play.
  >     If there was no advance, then the base shown will be the one where the runner
  >     started.  Runner fields are not updated on plays which end an inning, even if
  >     the inning-ending play would have resulted in an advance of one or more runners
  >     had it occurred earlier in the inning.
- *runner_on_2nd_dest*: The base which the batter reached at the conclusion of the play.
- *runner_on_3rd_dest*: The base which the batter reached at the conclusion of the play.
- *play_on_batter*: Encoded description of the play on the batter. For example, "53" would indicate a batted ball fielded by the third baseman and thrown to the first baseman.
- *play_on_runner_on_1st*: Encoded description of the play on the runner on first.
- *play_on_runner_on_2nd*: Encoded description of the play on the runner on second.
- *play_on_runner_on_3rd*: Encoded description of the play on the runner on third.
- *sb_for_runner_on_1st_flag*: One character indicating a stolen base for the runner on first ("t" = yes; "f" = no).
- *sb_for_runner_on_2nd_flag*: One character indicating a stolen base for the runner on second ("t" = yes; "f" = no).	
- *sb_for_runner_on_3rd_flag*: One character indicating a stolen base for the runner on third ("t" = yes; "f" = no).
- *cs_for_runner_on_1st_flag*: One character indicating the runner on first was caught stealing ("t" = yes; "f" = no).
- *cs_for_runner_on_2nd_flag*: One character indicating the runner on second was caught stealing ("t" = yes; "f" = no).	
- *cs_for_runner_on_3rd_flag*: One character indicating the runner on third was caught stealing ("t" = yes; "f" = no).
- *po_for_runner_on_1st_flag*: One character indicating the runner on first was picked off ("t" = yes; "f" = no).
- *po_for_runner_on_2nd_flag*: One character indicating the runner on second was picked off ("t" = yes; "f" = no).	
- *po_for_runner_on_3rd_flag*: One character indicating the runner on third was picked off ("t" = yes; "f" = no).
- *responsible_pitcher_for_runner_on_1st*: ID of the pitcher responsible for the runner on first base; unique 8-digit alpha-numeric code that references personnel file.
- *responsible_pitcher_for_runner_on_2nd*: ID of the pitcher responsible for the runner on second base; unique 8-digit alpha-numeric code that references personnel file.
- *responsible_pitcher_for_runner_on_3rd*: ID of the pitcher responsible for the runner on third base; unique 8-digit alpha-numeric code that references personnel file.
- *new_game_flag*: One character indicating the start of a new game ("t" = yes; "f" = no).
- *end_game_flag*: One character indicating the end of a game ("t" = yes; "f" = no).
- *pinch_runner_on_1st*: One character indicating a pinch runner on first base ("t" = yes; "f" = no).
- *pinch_runner_on_2nd*: One character indicating a pinch runner on second base ("t" = yes; "f" = no).
- *pinch_runner_on_3rd*: One character indicating a pinch runner on third base ("t" = yes; "f" = no).
- *runner_removed_for_pinch_runner_on_1st*: ID of the runner removed (for pinch runner) from first base; unique 8-character alpha-numeric code that references personnel file.
- *runner_removed_for_pinch_runner_on_2nd*: ID of the runner removed (for pinch runner) from second base; unique 8-character alpha-numeric code that references personnel file.	
- *runner_removed_for_pinch_runner_on_3rd*: ID of the runner removed (for pinch runner) from third base; unique 8-character alpha-numeric code that references personnel file.	
- *batter_removed_for_pinch_hitter*:  ID of the batter removed for a pinch hitter; unique 8-character alpha-numeric code that references personnel file.	
- *position_of_batter_removed_for_pinch_hitter*: Fielding position of the removed batter removed for a pinch hitter. If there is no pinch hitter, this value is 0.
- *fielder_with_first_putout*: Fielding position of the fielder with the first putout.
- *fielder_with_second_putout*: Fielding position of the fielder with the second putout.
- *fielder_with_third_putout*: Fielding position of the fielder with the third putout.
- *fielder_with_first_assist*: Fielding position of the fielder with the first assist.
- *fielder_with_second_assist*: Fielding position of the fielder with the second assist.
- *fielder_with_third_assist*: Fielding position of the fielder with the third assist.
- *fielder_with_fourth_assist*: Fielding position of the fielder with the fourth assist.
- *fielder_with_fifth_assist*: Fielding position of the fielder with the fifth assist.
- *event_num*: Numerical sequence indicating the order of the plays.

## Game log teams
- *game_id*: Unique 12-character alpha-numeric code for each game in the record. Of the form team_id+yyyymmdd+game_num.
- *team_id*: Unique 8-character alpha-numeric code that references the teams file.
- *score*: Runs scored by the team.
- *win_loss*: One character indicating a win or loss ("w" = win; "l" = loss).
- *pitcher_of_record*: ID of the pitcher of record (winner or loser); unique 8-character alpha-numeric code that references personnel file.

Offensive team statistics
- *pa*: Number of plate appearances
- *ab*: Number of at bats
- *h*: Number of hits
- *2b*: Number of doubles
- *3b*: Number of triples
- *hr*: Number of home runs
- *rbi*: Number of RBIs
- *sach*: Number of sacrifice hits. This may include sacrifice flies for years prior to 1954 when sacrifice flies were allowed.
- *sacf*: Number of sacrifice flies (1954 to present)
- *hbp*: Number of hit by pitches.
- *bb*: Number of walks
- *ibb*: Number of intention walks
- *k*: Number of strikeouts
- *sb*: Number of stolen bases
- *cs*: Number of caught stealing.
- *gidp*: Number of grounded into double plays.
- *ci*: Number of catcher interference
- *lob*: Number of runners left on base.
- *bat_noout_pa*: Number of no-out plate appearances
- *bat_outsplayed*: Number of outs played by the offense.

Pitching statistics
- *pitchers_used*: Number of pitchers used.
- *ind_er*: Number of individual earned runs.
- *team_er*: Number of team earned runs
- *wp*: Number of wild pitches
- *balk*: Number of balks

Fielding stats
- *po*: Number of putouts
- *assist*: Number of assists.
- *err*: Number of errors.
- *pb*: Number of passed balls.
- *dp*: Number of double plays
- *tp*: Number of triple plays

## Game log batters
- *id*: Unique 8-character alpha-numeric code that references the personnel file.
- *game_id*: Unique 12-character alpha-numeric code for each game in the record. of the form team_id+yyyymmdd+game_num.
- *pa*: Number of plate appearances
- *ab*: Number of at bats
- *1b*: Number of singles
- *2b*: Number of doubles
- *3b*: Number of triples
- *hr*: Number of home runs
- *rbi*: Number of RBI
- *sach*: Number of sacrifice hits. This may include sacrifice flies for years prior to 1954 when sacrifice flies were allowed.
- *sacf*: Number of sacrifice flies (1954 to present)
- *bb*: Number of walks
- *ibb*: Number of intention walks
- *hbp*: Number of hit by pitches.
- *k*: Number of strikeouts
- *int*: Number of interference
- *gidp*: Number of grounded into double plays.
- *gitp*: Number of grounded into triple plays.
- *ci*: Number of catchers interference
- *gwrbi*: Game winning RBI (0=false, 1=true)
- *runs*: Number of runs
- *sb*: Number of stolen bases
- *cs*: Number of caught stealing.
- *pickoff*: Number of times picked-off.
- *games*: Number of games (=1)

## Game log pitchers
- *id*: Unique 8-character alpha-numeric code that references the personnel file.
- *game_id*: Unique 12-character alpha-numeric code for each game in the record. of the form team_id+yyyymmdd+game_num.
- *pa*: Number of plate appearances
- *ab*: Number of at bats
- *1b*: Number of singles
- *2b*: Number of doubles
- *3b*: Number of triples
- *hr*: Number of home runs
- *rbi*: Number of RBI
- *sach*: Number of sacrifice hits. This may include sacrifice flies for years prior to 1954 when sacrifice flies were allowed.
- *sacf*: Number of sacrifice flies (1954 to present)
- *bb*: Number of walks
- *ibb*: Number of intention walks
- *hbp*: Number of hit by pitches.
- *k*: Number of strikeouts
- *int*: Number of interference
- *gidp*: Number of grounded into double plays.
- *gitp*: Number of grounded into triple plays.
- *outs_played*: Number of outs pitched (alternate to innings pitched)
- *pickoff*: Number of pickoffs
- *balk*: Number of balks
- *sb*: Number of stolen bases
- *cs*: Number of caught stealing.
- *r*: Number of runs
- *er*: Number of earned runs.
- *gs*: Number of game starts
- *win*: Recorded a win (0=false, 1=true)
- *loss*: Recorded a loss (0=false, 1=true)
- *save*: Recorded a save (0=false, 1=true)
- *cg*: Recorded a complete game (0=false, 1=true)
- *sho*: Recorded a shutout (0=false, 1=true)
- *games*: Number of games (=1)

## Game log fielders
- *id*: Unique 8-character alpha-numeric code that references the personnel file.	
- *game_id*: Unique 12-character alpha-numeric code for each game in the record. of the form team_id+yyyymmdd+game_num.
- *field_pos*: Numerical code representing the fielding position of the player of record.
- *outs_played*: Number of outs played by the player of record at a fielding position.
- *putout*: Number of putouts
- *assist*: Number of assists.
- *error*: Number of errors
- *pb*: Number of passed balls.
- *int*: Number of interference calls

## Appearances
- *game_id*: Unique 12-character alpha-numeric code for each game in the record of the form team_id+yyyymmdd+game_num.
- *id*: Unique 8-character alpha-numeric code that references the personnel file.
- *team_id*: Unique 3-character alpha-numeric code that references the teams file.
- *field_pos*: Numerical code representing the fielding position of the player of record.
- *batt_ord*: Batting order of the player of record.
- *start*: Indicator if the player started the game ("t"=true, "f"=false)

## Ejections
- *game_id*: Unique 12-character alpha-numeric code for each game in the record of the form team_id+yyyymmdd+game_num.
- *game_date*: Date-time of the game of record.
- *ejectee_id*: Unique 8-character alpha-numeric code that references the personnel file.
- *ejectee_team_id*: Unique 3-character alpha-numeric code that references the teams file.
- *ejectee_role*:
  >     "P" for player,
  >     "M" for manager,
  >     "C" for coach
- *ump_id*: Unique 8-character alpha-numeric code that references the personnel file.
- *inning*: Inning when the ejection occurred.
- *reason*: Explanation of the reason for the ejections, if known.

## Transactions
- *pri_date*: Date when the transaction occurred. If only the year is known, then the primary date will be 1-1-xxxx. If the month and year are known, then the primary date is given as the first day of that month.
- *pri_date_approx*: Indicator if the primary date is an approximate value ("t"=true, "f"=false), i.e., the primary date given is a guess.
- *sec_date*: At present this is used for "Da" types to indicate the player's signing date (the primary-date field for these transactions contains the date of the start of the draft).
- *sec_date_approx*: Indicator if the primary date is an approximate value ("t"=true, "f"=false), i.e., the secondary date given is a guess.
- *player_id*: Can be a null value, a unique 8-character alpha-numeric code (RS player code), or the full name of the player if that player has not reached the major leagues.
- *trans_type*: Code that describes the type of transaction. Possible values:
  >     "A": assigned from one team to another without compensation
  >     "C": conditional deal
  >     "Cr": returned to original team after conditional deal.
  >     "D": rule 5 draft pick
  >     "Da": amateur draft pick
  >     "Df": first year draft pick
  >     "Dm": minor league draft pick
  >     "Dn": selected in amateur draft but did not sign.
  >     "Dr": returned to original team after draft selection.
  >     "Ds": special draft pick
  >     "Dv": amateur draft pick voided.
  >     "F": free agent signing
  >     "Fa": amateur free agent signing
  >     "Fb": amateur free agent "bonus baby" signing under the 1953-57 rule requiring player to stay on ML roster
  >     "Fc": free agent compensation pick
  >     "Fg": free agent granted.
  >     "Fo": free agent signing with first ML team.
  >     "Fv": free agent signing voided.
  >     "Hb": went on the bereavement list.
  >     "Hbr": came off the bereavement list.
  >     "Hd": declared ineligible.
  >     "Hdr": reinstated from the ineligible list.
  >     "Hf": demoted to the minor league.
  >     "Hfr": promoted from the minor league.
  >     "Hh": held out.
  >     "Hhr": ended hold out.
  >     "Hi": went on the disabled list
  >     "Hir": came off the disabled list.
  >     "Hm": went into military service.
  >     "Hmr": returned from military service.
  >     "Hs": suspended.
  >     "Hsr": reinstated after a suspension.
  >     "Hu": unavailable but not on DL
  >     "Hur": returned from being unavailable.
  >     "Hv": voluntarily retired
  >     "Hvr": unretired
  >     "J": jumped teams
  >     "Jr": returned to original team after jumping.
  >     "L": loaned to another team
  >     "Lr": returned to original team after loan.
  >     "M": obtained rights when entering into working agreement with minor league team
  >     "Mr": rights returned when working agreement with minor league team ended.
  >     "P": purchase
  >     "Pr": returned to original team after purchase.
  >     "Pv": purchase voided.
  >     "R": release
  >     "T": trade
  >     "Tn": traded but refused to report.
  >     "Tp": added to trade (usually because one of the original players refused to report or retired)
  >     "Tr": returned to original team after trade.
  >     "Tv": trade voided.
  >     "U": unknown (could have been two separate transactions)
  >     "Vg": player assigned to league control
  >     "V": player purchased or assigned to team from league
  >     "W": waiver pick
  >     "Wf": first year waiver pick
  >     "Wr": returned to original team after waiver pick.
  >     "Wv": waiver pick voided.
  >     "X": expansion draft
  >     "Xe": premium phase of expansion draft
  >     "Xm": either the 1960 AL minor league expansion draft or the premium phase of the 1961 NL draft
  >     "Xp": added as expansion pick later.
  >     "Xr": returned to original team after expansion draft.
  >     "Z": voluntarily retired
  >     "Zr": returned from voluntarily retired list.

- *team_from*: Either a three-character major league team abbreviation or the name of an independent minor league team indicating where the player came from.  Some transactions (for example, "Da" will not have a from-team (or league).
- *league_from*: either a two-character major league abbreviation or the name of a minor league in parenthesis.
- *team_to*: Either a three-character major league team abbreviation or the name of an independent minor league team indicating where the player went to.  Some transactions (for example, "Fg" will not have a to-team (or league).
- *league_to*: Either a two-character major league abbreviation or the name of a minor league in parenthesis.
- *draft_type*: The type of amateur draft (Da, Dn and Dv types only). The default is the regular draft.
  >     "S": secondary phase (or secondary phase delayed)
  >     "A": secondary phase active
  >     "L": American Legion
  >     "D": Dominican draft

- *draft_round*: The round of the amateur draft that the player was selected in (Da, Dn and Dv types only).
 - *pick_num*: For expansion drafts, this contains the number of the pick. For amateur drafts, this will contain the number of the selection for first round picks.
- *info*: This contains information associated with the transaction. For trades, this field could contain money sent in addition to players.  For player sales, this could contain the sale amount.

If a "F" transaction has both a from and a to team, there will be no corresponding "Fg" transactions.  These two-team "F" transactions are used in eras where players were not reserved and so were free to sign with whoever at the end of each contract.



