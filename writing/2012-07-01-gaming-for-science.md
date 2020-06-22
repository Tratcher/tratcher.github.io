---
layout: page
title: Gaming, for Science!
---

###### 2012 July 1<br>
Science, for gaming?  Yes, I have strange hobbies.  One of these involves playing lots of Dungeon Keeper 2, an absolutely fantastic game.  Replaying it for dozenth time I realized that I had never reached the top of the high score chart. This is where the science begins.

Just how does one get a very high score in DK2?  How is the score even computed?  At a glance possible scores range from 1,000 to 1,000,000, but I was consistently falling into the 100,000-500,000 range without any obvious correlation to how well I’d done on a given level.

Conveniently the score screen at the end of each level has a long list of statistics about your accomplishments.  However there is no obvious relationship drawn between these fields and your score beyond the high-level observation that higher numbers tend to give you a higher score.  A much more careful analysis was going to be needed.

Here are the score screen fields:
| Field                  | Description                                                                   | Sample range                  |
|------------------------|-------------------------------------------------------------------------------|-------------------------------|
| Level                  | The level title (though I just use #s)                                        | 11b – “Carnage” – Sparklydell |
| Total Evil Rating      | Score                                                                         | 5k-1.2m                       |
| Specials Found         | The number of secret specials you found                                       | 0-Total Specials              |
| Total Specials         | The total number specials available                                           | 0-11                          |
| Level Won              | Did you succeed or fail?                                                      | Yes/No                        |
| Time Taken             | Total level time                                                              | 5m – 1.5h                     |
| Enemy Creatures Killed | Total kills of creatures controlled by other dungeon keepers, including imps. | 0-200                         |
| Heroes Destroyed       | Total kills of “Good-Guys”, “Wandering Heroes”, or rebels                     | 0-50                          |
| Rooms Captured         | Total rooms claimed by imps                                                   | 0-40                          |
| Land Owned             | Each square of land claimed at the end                                        | 20-2500                       |
| Gold Mined             | Total Gold or Gems harvested by imps                                          | 0-800k (* Infinite)           |
| Mana Stored            | The total mana left in storage at the end of the level.                       | 0-200k                        |
| Items Manufactured     | Total items created in your workshop (even if never installed)                | 0-50                          |
| Creatures Commanded    | Your creature count at the end, including imps                                | 0-75                          |
| Creatures Converted    | The total creatures gained via torture chamber conversion                     | 0-40                          |
| Creature Training      | Average creature level at the end                                             | 0.00-10.00                    |
| Attempts at Level      | How many tries did it take you to win                                         | 0-5                           |

Step 1: Gather data – One needs lots of data to work out patterns, especially when you have 17 potential variables to work with.   Some data I got just from playing through the levels and copying down the results.  However, note that even the first level uses 14 of the 17 fields, so I’d need another way to eliminate fields and solve for the remaining ones.  When I got serious about this I started back at level one and played it through five times using various strategies, and similarly I played level two another three times.

Step 2: Initial analysis – When you play a level through multiple times, no matter how you change your strategy some things will remain constant.  Taking the results from one play, I subtracted out the results from similar plays to see what was actually contributing to the score variation.  When one field started to stand out I approximated a multiplier for that field, updated my overall score equation, and then checked that back against the original score.

Step 3: Iterate – When I had some rough numbers that looked promising it was time to go back and re-play the level attempting control (and maximize) that given field to see if my math worked out.  If it didn't work, at least I had more data.  If it worked then it's time to look for other patterns.  If no other fields are standing out, then maybe it’s time to move on to the next level.

<details>
  <summary>Data collected</summary>
https://docs.google.com/spreadsheets/d/1GO8WPQvnhvWq2Y4bXqznJs8lGJVA2Dy8Z168P6EowNs/edit#gid=0
  
| ID | Level     | Score   | Specials Found | Total Specials | Victory | Time    | Creature Kills | Hero Kills | * Rooms Captured | Land Owned | Gold Mined | Mana Stored | Items made | Creatures | Converts | Training | Attempts |   | Calculated score | Diff | Probobly room area captured |
|----|-----------|---------|----------------|----------------|---------|---------|----------------|------------|------------------|------------|------------|-------------|------------|-----------|----------|----------|----------|---|------------------|------|-----------------------------|
|  1 |         1 |   89887 |              1 |              1 | Yes     | 0:06:51 |              0 |          3 |                1 |        170 |      27000 |       30763 |          0 |        11 |        0 |     2.72 |        1 |   |            89887 |    0 |                           0 |
|  2 |         1 |   60214 |              1 |              1 | Yes     | 0:04:18 |              0 |          3 |                1 |        130 |      27000 |       16035 |          0 |        10 |        0 |     2.39 |        1 |   |            60194 |   20 |                 6.666666667 |
|  3 |         1 |  139017 |              1 |              1 | Yes     | 0:09:28 |              0 |          3 |                1 |        205 |      27000 |       55234 |          0 |        12 |        0 |     2.58 |        1 |   |           139017 |    0 |                           0 |
|  6 |         1 |  129446 |              0 |              1 | Yes     | 0:07:57 |              0 |          3 |                1 |        199 |      27000 |       50470 |          0 |        13 |        0 |     1.92 |        1 |   |           129446 |    0 |                           0 |
|  7 |         1 |  428684 |              0 |              1 | Yes     | 0:23:18 |              0 |          3 |                1 |        213 |      27000 |      200000 |          0 |        19 |        0 |     1.68 |        1 |   |           428684 |    0 |                           0 |
|  4 |         2 |  331413 |              1 |              1 | Yes     | 0:15:02 |              0 |         18 |                1 |        313 |      99000 |      114663 |          0 |        24 |        0 |     2.75 |        1 |   |           331413 |    0 |                           0 |
|  5 |         2 |  277057 |              1 |              1 | Yes     | 0:14:45 |              0 |         18 |                1 |        368 |      99000 |       87305 |          0 |        27 |        0 |     3.25 |        1 |   |           277057 |    0 |                           0 |
|  8 |         2 |  502372 |              1 |              1 | Yes     | 0:18:19 |              0 |         18 |                1 |        381 |      99000 |      200000 |          0 |        20 |        0 |     3.25 |        1 |   |           502372 |    0 |                           0 |
|  9 |         3 |  466432 |              1 |              1 | Yes     | 0:32:36 |              0 |         18 |                3 |        682 |      61364 |      200000 |          2 |        26 |        0 |      4.3 |        1 |   |           466434 |   -2 |               -0.6666666667 |
| 10 |         4 |  718063 |              4 |              4 | Yes     | 0:44:44 |              0 |         19 |                9 |       1326 |     309000 |      200000 |         11 |        41 |        0 |     5.87 |        1 |   |           717793 |  270 |                          90 |
| 11 |         5 |  606180 |              4 |              5 | Yes     | 0:34:04 |              0 |          8 |                2 |        735 |     201000 |      200000 |          5 |        36 |        0 |     4.36 |        1 |   |           606048 |  132 |                          44 |
| 12 | 6a        |  774409 |             11 |             11 | Yes     | 0:54:14 |              0 |         21 |               10 |       2156 |     360000 |      200000 |         37 |        40 |       16 |     5.39 |        1 |   |           773934 |  475 |                 158.3333333 |
| 13 |         7 |  550339 |              6 |              6 | Yes     | 1:08:00 |              0 |         16 |               10 |        898 |     270000 |      136155 |          7 |        53 |       19 |     4.81 |        1 |   |           549935 |  404 |                 134.6666667 |
| 14 |         8 |  563168 |              8 |             10 | Yes     | 0:53:55 |              0 |         50 |               17 |        556 |     156000 |      200000 |          0 |        28 |        0 |     3.92 |        1 |   |           562121 | 1047 |                         349 |
| 15 | Duckshoot |  402445 |              0 |              0 | Yes     | 0:03:21 |              0 |         42 |                0 |         55 |          0 |      200000 |          0 |         1 |        0 |        1 |        1 |   |           402445 |    0 |                           0 |
| 16 | Duckshoot |  400445 |              0 |              0 | Yes     | 0:04:09 |              0 |          2 |                0 |         55 |          0 |      200000 |          0 |         1 |        0 |        1 |        1 |   |           400445 |    0 |                           0 |
| 17 | Golf      |   10275 |              0 |              0 | No      | 0:01:05 |              0 |          0 |                0 |         79 |          0 |        4940 |          0 |         0 |        0 |        0 |        1 |   |            10275 |    0 |                           0 |
| 18 |         9 |  672722 |              2 |              5 | No      | 0:24:57 |              0 |          3 |                2 |        674 |     268313 |      200000 |          0 |        29 |        0 |     3.82 |        1 |   |           672614 |  108 |                          36 |
| 19 |         9 | 1138321 |              5 |              5 | Yes     | 0:50:18 |              0 |          7 |                3 |       1286 |     730950 |      199221 |          0 |        59 |       13 |     5.44 |        2 |   |          1138289 |   32 |                 10.66666667 |
| 20 |        10 |  817554 |              7 |              9 | Yes     | 0:38:33 |              6 |         26 |               10 |       1203 |     407600 |      200000 |         43 |        36 |        0 |      4.2 |        1 |   |           816350 | 1204 |                 401.3333333 |
| 21 | Maze      |  402960 |              0 |              0 | No      | 0:02:51 |              0 |          0 |                0 |        544 |          0 |      200000 |          0 |         7 |        0 |        2 |        1 |   |           402960 |    0 |                           0 |
| 22 | Maze      |  403051 |              0 |              0 | Yes     | 0:03:43 |              0 |          1 |                0 |        558 |          0 |      200000 |          0 |         6 |        0 |     1.83 |        3 |   |           403051 |    0 |                           0 |
| 23 | 11b       | 1190855 |              0 |              0 | Yes     | 1:26:00 |            177 |          0 |               39 |       2262 |     764858 |      200000 |          8 |        61 |       15 |     5.13 |        1 |   |          1185709 | 5146 |                 1715.333333 |
| 24 | 11b       |  757378 |              0 |              0 | Yes     | 1:14:00 |            145 |          0 |               33 |       1422 |     337637 |      200000 |          0 |        51 |       15 |     4.84 |        1 |   |           752724 | 4654 |                 1551.333333 |
| 25 | 11b       |  757451 |              0 |              0 | Yes     | 1:22:00 |            149 |          0 |               33 |       1409 |     337637 |      200000 |          8 |        47 |       15 |        5 |        1 |   |           752787 | 4664 |                 1554.666667 |
| 26 | 11b       |   48431 |              0 |              0 | No      | 0:15:01 |              0 |          0 |                1 |         27 |      48000 |           0 |          0 |         9 |        0 |     2.22 |        0 |   |            48431 |    0 |                           0 |
| 27 | 11b       |    6360 |              0 |              0 | No      | 0:16:19 |              3 |          0 |                0 |         26 |       6000 |           0 |          0 |         3 |        0 |        1 |        0 |   |             6360 |    0 |                           0 |
| 28 | 11b       |   13246 |              0 |              0 | No      | 0:26:03 |            171 |          0 |                0 |         33 |       6000 |           0 |          0 |         8 |        0 |     1.62 |        0 |   |            13246 |    0 |                           0 |
| 29 | 11b       |  127159 |              0 |              0 | No      | 0:21:40 |             15 |          0 |                2 |         32 |     126000 |           0 |          0 |        14 |        0 |     1.64 |        0 |   |           127132 |   27 |                           9 |
| 30 | 11b       |  127664 |              0 |              0 | No      | 0:22:28 |             26 |          0 |                3 |         31 |     126000 |           0 |          0 |        12 |        0 |     2.25 |        0 |   |           127562 |  102 |                          34 |
| 31 | 11b       |  128827 |              0 |              0 | No      | 0:21:15 |             29 |          0 |                4 |        229 |     126000 |           0 |          0 |        10 |        0 |      2.5 |        0 |   |           128650 |  177 |                          59 |
| 32 | 11b       |  128968 |              0 |              0 | No      | 0:20:46 |             31 |          0 |                4 |        243 |     126000 |           0 |          0 |         9 |        0 |     2.66 |        0 |   |           128788 |  180 |                          60 |
| 33 | 11b       |  100738 |              0 |              0 | No      | 0:15:49 |              0 |          0 |                1 |        205 |      99000 |           0 |         38 |        22 |        0 |     1.36 |        0 |   |           100728 |   10 |                 3.333333333 |
| 34 | 11b       |   50486 |              0 |              0 | No      | 0:12:31 |              1 |          1 |                1 |         99 |      49546 |           0 |          6 |        11 |        0 |        2 |        0 |   |            50486 |    0 |                           0 |
| 35 | 11b       |   52214 |              0 |              0 | No      | 0:11:12 |              0 |          0 |                1 |        133 |      51183 |           0 |          6 |        12 |        0 |     1.83 |        0 |   |            52214 |    0 |                           0 |
| 36 | 11b       |   52499 |              0 |              0 | No      | 0:13:19 |              3 |          1 |                1 |        207 |      50911 |           0 |          6 |        12 |        0 |     2.16 |        0 |   |            52499 |    0 |                           0 |
| 37 |        12 |  640040 |              6 |              7 | Yes     | 0:48:20 |             28 |         48 |                6 |       1135 |     228273 |      200000 |          0 |        27 |        0 |     4.77 |        1 |   |           638276 | 1764 |                         588 |
| 38 |        12 |  540011 |              0 |              7 | Yes     | 0:42:09 |             32 |         48 |                6 |        448 |     132000 |      200000 |          0 |        11 |        0 |     2.63 |        1 |   |           538301 | 1710 |                         570 |
| 39 |        13 | 1110310 |              6 |              8 | Yes     | 1:16:00 |             94 |         22 |               24 |       1839 |     686925 |      200000 |          0 |        71 |       40 |     5.94 |        1 |   |          1104817 | 5493 |                        1831 |
| 40 | Bowling   |   17181 |              0 |              0 | No      | 0:00:00 |              0 |          2 |                0 |        319 |          0 |        7743 |          0 |         0 |        0 |        0 |        1 |   |            17181 |    0 |                           0 |
| 41 |        14 |   28141 |              0 |              8 | No      | 0:11:26 |              0 |          1 |                0 |        176 |      27000 |           0 |          0 |         7 |        0 |     1.42 |        0 |   |            28141 |    0 |                           0 |
| 42 |        14 |  490260 |              8 |              8 | Yes     | 0:58:46 |              0 |         62 |                3 |        598 |     114000 |      184515 |          0 |        37 |        0 |     7.27 |        2 |   |           490238 |   22 |                 7.333333333 |

</details>

Actual analysis:

Comparing replays of the first level, the first thing that stood out was the mana.  This wasn’t even a field I’d expected to be relevant, but it’s huge range and variation made it a primary influencer in the final score.  It was easy enough from here to guess that it was using a 2x multiplier, meaning it could contribute 0-400k towards your total score (mana storage tops out at 200k).  Sure enough, replaying the level and waiting for my mana to fully charge instantly quadrupled my score.

With mana accounted for Gold became the next large outlier, using a simple 1x multiplier.  This left land with a 5x multiplier.  Everything else on level one was fairly constant so it was hard to get much further there.  However, just these three fields accounted for 99% of the overall score on most levels, so I already had a rough answer to my initial question of how to get a high score – max out mana, mine all the gold, and dig out and capture all of the land.  This can get a bit tedious, but luckily time never turned out to be a score contributor.

But why stop the science when you’re only 99% of the way there?  Here’s some other interesting things I found trying to work out the rest of the equation:

Bonus levels turned out to be very helpful.  The average bonus level used fewer fields than normal, and they tended to complete faster so it was easy to gather lots of data about specific fields.  For example, on duckshoot I had just one level one creature and 70 points un-accounted for.  From here I was able to do a bit of trial and error guessing of the distribution (20x & 50x) and verify the results against prior data.

Sometimes it is easier to control variables by losing on purpose.  On level 11b for example, it takes 10-15m to lose, but 1.5h to win.  If you intend to lose then there are few limits to how crazy your experiments can be.

You don’t get any mana points if your dungeon heart is destroyed, but you do if you lose for other reasons (time limits, etc.).

The following fields do not appear to affect your score: Level, Level won, Time, Specials, and Attempts.

Creature training is the only decimal field reported.  After identifying that there was a 50x multiplier I was still left with fractional points in my results.  To clear this up you have to add a Floor function around the result (a.k.a. round down / truncate).  It’s not clear if they did this on purpose, or if they just stored the result from their decimal multiplication into an integer field (which will truncate by default).

Figuring out Rooms Captured was a pain.  This is the only field with inadequate information reported to completely solve.  To start with, there is a 5x multiplier for each captured room, including portals.  Capturing a room, losing a room to an enemy player, and then re-capturing it counts as two separate captures.  So far I have not verified if captured bridges count as rooms, though you get a similar audio report.  What makes Captured Rooms difficult is that there is an additional 3x multiplier for the area of each room captured from the enemy (e.g. a 3x3 room has area 9 and is worth 3*9=27 points, + 5 for capturing a room = 32).  The total area of captured rooms is not reported in the level statistics, so we can at best approximate it by dividing the un-accounted for score by 3.  This approximation does not always work out to a believable result, implying that there are still a few points gained from unconfirmed sources.

Fun Bug: Lightning bolt the Lord-Of-The-Land while he’s walking past a torture chamber.  The normal mechanic for loading a torture chamber is picking up a captured enemy creature from your prison and dropping it in the torture chamber on a floor rack or next to a wall rack.  Dropping it near a wall rack stuns it on the floor, and then when it tries to get up it gets grabbed by a wall rack.  Lightning bolts cause a similar stun to creatures.  I managed to get a Lord-of-the-Land stuck, tortured, and converted.  The level wouldn’t end until I dropped him out the portal.

Results: Multiply each field by the given multiplier below, and then add the results together to get your approximate score.

| Field                  | Multiplier |
|------------------------|------------|
| Level                  | 0          |
| Specials Found         | 0          |
| Total Specials         | 0          |
| Level Won              | 0          |
| Time Taken             | 0          |
| Enemy Creatures Killed | 40         |
| Heroes Destroyed       | 50         |
| Rooms Captured*        | 5          |
| Land Owned             | 5          |
| Gold Mined             | 1          |
| Mana Stored            | 2          |
| Items Manufactured     | 5          |
| Creatures Commanded    | 20         |
| Creatures Converted    | 50         |
| Creature Training      | Floor(50x) |
| Attempts at Level      | 0          |

At this point I also want to give a shout out to the developers of DK2.  Bullfrog has always made my favorite games (Theme Park, Theme Hospital, and DK1&2).  To specifically mention folks that IMDB says worked on more than one of these: Nick Goldsworthy, David Amor, Shintaro Kanaoya, Alex Peters, and Peter Molyneux.  Thanks Guys!  Can any of you verify my results?

<details>
  <summary>Background</summary>
Originally posted at https://tracher.livejournal.com/119711.html
 <details> 
