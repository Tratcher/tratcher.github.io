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

Data collected:<br/>
https://docs.google.com/spreadsheets/d/1GO8WPQvnhvWq2Y4bXqznJs8lGJVA2Dy8Z168P6EowNs/edit#gid=0

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
</details> 
