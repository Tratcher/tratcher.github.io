---
layout: page
title: Scotland Yard
---
###### 2010 June 29<br>
 So my nerdy thoughts of the week have been focused on the board game Scotland Yard.  Think fugitive the board game.  Mr X has to survive 30 rounds without getting caught.  Five collaborating detectives have to track him down.  Each turn everybody can take a taxi, bus, or subway (if available at your location).  Mr X almost always has to reveal what mode of transportation he used, but only actually shows himself on the board every 4ish turns.  True to the bureaucratic spirit of a police force, the detectives have a limited numbers of taxi, bus, and subway fair tickets to get the job done.

At first glance it looked like a very strait forward graph problem.  Then I realized there were lots of special considerations to the algorithms.
1. Mr X doesn't have a destination, he is simply taking evasive action.
2. The detectives have a moving target that they can only see every 4ish turns.  They have to extrapolate where he might be the rest of the time.
3. Collisions - Only one detective may be in a specific location at a time.
4. Collaboration - you must coordinate all of the detectives together to effectively coral Mr X.
5. Resources - All links have a cost of one, but of three (actually 4) different kinds of resources.  A taxi fair ticket does not work on the bus or subway and vice versa.  You will run out of at least one kind and be significantly limited in your effectiveness.  Mr X has unlimited fairs, except for the special black ticket that lets him use any type of transit (and swim across the river) without telling you what type he took.

(I can't decide if I want to actually implement the game / algorithms, or just discuss them.  For a change of pace I'm actually doing a reasonable amount of coding at work, so this might have to wait.)

Thoughts?

###### 2010 July 15<br>
So I decided to give it a start.  I spent way too much time on a fancy map editor, and learned all sorts of things about the game in the process:
The board I have must be very old (1985).  There's no 108 on the board.  Later editions fixed this by getting ride of 200 and shifting a few numbers around.  The artwork also appears to have been updated.
Board Game Geek has all sorts of useful links to user generated content including a high-res board image with real satellite images mapped under it.  The spreadsheet list of routes was handy too, except for the dozen or so inaccuracies and typos.  I haven't even tried looking through the alternate scenarios people have posted (Blade Runner, etc).

Once I had built the map editor and generated a very detailed data file, I finally started on a simple game engine.  It's up and running to the point where I have an AI that just picks randomly from the available moves, and a simple overall infrastructure to let me run x number of games in a row just to see how this random AI works.  It turns out that when everybody starts at a random location and moves randomly, the Fugitive wins ~40% of the time.  Interestingly it didn't seam to matter if you picked random locations from the dozen specified in the rules, or from anywhere on the board.

Now is a good time for all the AI nerds reading this to put in ideas (while I slush out the engine a little).  What optimizations can be made to help either the detectives or the fugitive, starting with the simplest possible optimizations.  Here's a few thoughts:

Fugitive
- Don't get yourself caught by moving into a location currently occupied by a detective.  You can always see the detectives.
- Prefer moves that don't put you adjacent to a detective.  (May be overridden by a more risky strategy later)
- Use a double move ticket if you're adjacent to a detective, especially if you're visible.
- Use black tickets when leaving a visible location, or when all possible destinations are adjacent to a detective.

Detectives
- If the Fugitive is visible and adjacent to your current location, move there to capture him.
- During the first two turns when the fugitive has not yet become visible, move towards the closest major transit hubs.
- Attempt to balance ticket usage, especially when there are two links of the different types to the same destination.
- Avoid moving somewhere that would leave you stranded (because you'd run out of tickets)
- Project the fugitive's possible locations based on their last visible position and subsequent moves.  Coordinate the detectives to intercept potential routes.

If you'd like to play with actual code, let me know and we'll work something out.  I learned from Dominion that most people would rather theorize than code.

Log of interesting things I've found so far (This will be updated):
- When everybody just moves randomly:
-- The fugitive wins 40% of the time.
-- Using the stock staring locations is no different than using completely random locations.
-- (Optimization) If the fugitive avoids moving into a space occupied by a detective, the fugitive wins 68% of the time.
-- (Optimization) If the fugitive avoids moving to a space adjacent to a detective, the fugitive wins 98% of the time.
- (Cheating Optimization) If the detectives always move geographically towards the fugitive (cheating to know where the fugitive currently is), the detectives win 93% of the time with the above fugitive optimizations.  Without them the detectives win 100% of the time.
- (Cheat removed) Have the fugitives move towards the last known position of the fugitive.  For a random fugitive the detectives win 99% of the time.  For a fugitive optimized as above, the fugitive wins 50% of the time.
- (Optimization) For the first two rounds when the fugitive is not visible, have the detectives move towards transit hubs.  Against a random fugitive the detectives with 99.98% of the time. Against the evasive fugitive as optimized so far the detectives win 64% of the time.

<details>
  <summary>Background</summary>
Comments:<br>
Z: I find that, when playing the best players I can find, I (nearly) always win as the coppers and (nearly) always lose as Mr. X. I *suspect* that the game is solvable, and it's been on my "todo someday" list for a number of years. I'd be interested in knocking heads together and trying to solve it, if you're game for it!<br>
C: Sounds awesome. If I'm actually going to end up coding this, I was going to start with a map maker, a basic game engine, and then a simple random play algorithm. I bet this is one of those games that random won't be very good at, so it will be easy to actually see improvements.<br>
RG: I remember seeing a drastically simplified version of this game in a puzzle book when I was a kid. The solution wouldn't be applicable though, due to the map and rules.<br>
Z:<br>
Have you considered using a simple alpha-beta pruning tree, using "possible movements of fugitive" as an evaluation metric to minmax? There is a *huge* multipliciy of moves for each "detectives" turn (I just consider the detectives to have one large "supermove"). I think, in general, an evaluation function that minimizes the number of potential moves the fugitive has is a good start.<br>
<br>
I've never lost a game (as either side, though I expect this is mostly because I haven't played against good detectives), and here is what I, personally, use as my detectives strategy, which is in three stages:<br>
<br>
Stage 1 - Become Ready For Movement: For the first few moves, ensure that you'll be at (preferred) or able to move to an underground square when Mr. X reveals himself.<br>
<br>
Stage 2 - Create A Perimeter: Once he's revealed himself, move the detectives toward him, but maintain distance and control of the underground nodes (make sure that it's not possible for the fugitive to move onto an underground square -- this requires tracking every possible location he could be). This creates a large-diameter "net" for him, and prevents him from causing you to have to repeat this stage...<br>
<br>
Stage 3 - Tighten the net: Once he's revealed himself for the third time, your detectives have likely gotten nowhere near their resource limitations, and the fugitive is somewhere between the five of them. Whittle down his possible locations, until you're certain where he is, and nab him. This usually means blocking off bus routes, so you're certain he's using taxis.<br>
<br>
So, I'm essentially playing a different game than most people. I'm actually treating it as a game of reducing the number possible nodes Mr. X could be on to zero. So, I implement it (in my head) as a simple pruning tree, where I treat the collection of possible fugitive locations as his "actual" location. This removes the "chance" aspect from the game, by and large.<br>
<br>
To implement it in a standard alpha-beta tree, the "board state" would have to include the detective's locations, the fugitive's location, *and* the collection of nodes that the fugitive could be at, as known by the detectives (this is also important to consider as the fugitive, so he doesn't give away information he doesn't have to, by doing something like taking a bus when he could take a taxi for the same route or vice versa). Then, the fugitive is attempting to max the cardinality of the "possible movements from possible locations" metric, and the detectives are trying to minimize it, and it's pluggable into whatever game decision engine you like, be it a neural net, or an alpha beta tree, or whatever.<br>
<br>
Random thought - Go players are amazingly good at this game, I've found. Might want to look into that for ideas. There are actually a lot of similarities, given the "surround and close in" nature of battles in Go.<br>
<br>
C: I was thinking much along these lines, but I'm not sure on the specifics of how to coordinate 5 detectives in such a maneuver. I think this coordination is one of the more interesting problems for both AI and real players.<br>
R: When using the defined set of starting locations, do you have the detectives work out what spots Mr. X could possibly be in?<br>
Z: If you're asking me, no, I don't bother. It rapidly becomes "the whole board" after the first couple turns. I treat that as "unknown" and head for the underground stations.<br>

Orriginally posted at:<br>
https://tracher.livejournal.com/115112.html<br>
https://tracher.livejournal.com/115689.html<br>
</details>
