Overview
########

Welcome to Code Character!

Set in a 2D world, each player is given an army that can be controlled with
everyone's favourite programming language, C++ :)

The objective is simple enough. Implement a strategy that allows your army to
capture the enemy's flag more times than the enemy captures yours. Oh yeah,
there's a timer too.

The AIs could be as simple as a couple lines of code or as complex as rocket
science.

Good luck!

Plot
====

On a beautiful autumn day, you take a stroll through your garden, watching the 
brown leaves dance in the wind.

Suddenly, you hear a voice in your head. It whispers to you, caresses, embraces 
you. Then it tells you that in a hundred other kingdoms, a hundred other
kings are enjoying the exact same day, each content with their own little
piece of land.

'Your people are poor, there is no trade between kingdoms, and winter is coming.
Yet you choose to walk in your garden, content with your accomplishments, such as they are.'

On hearing these words, you are filled with shame, for you know them to be true.

'What do I do?' you ask desperately. 'How do I bring light to my kingdom cast in darkness?'

'Unite these kingdoms. Conquer them with fire and sword. Bring them all under your rule.

'Only where there is unity can there be peace.'

Game Elements Overview
======================

The world has 2 main components that you'll be interacting with:

- The actors
- The terrain

Actors
------

====================  ======  ======  ======  ========  ======  =========  ======
Property              Base    Flag    King    Magician  Scout   Swordsman  Tower
====================  ======  ======  ======  ========  ======  =========  ======
Number of units*      1       1       1       10        1       20         3
HP                    \-      \-      400     150       300     200        600
Can Move              False   False   True    True      True    True       False
Can Attack            False   False   False   True      False   True       True
Speed                 \-      \-      10      30        37      20         \-
Attack Power          \-      \-      \-      50        \-      20         80
Attack Range          \-      \-      \-      600       \-      30         1000
Attack recharge time  \-      \-      \-      0.83s     \-      0.33s      1.33s
Respawn Time          \-      \-      7s      2s        3s      1.5s       \-
LOS Radius**          5       0       1       3         6       2          5
====================  ======  ======  ======  ========  ======  =========  ======

| \*  Per team at the start of the game
|
| ** LOS Radius is in terms of ``TerrainElements``
|
|

There are 4 types of moveable actors that the user can control:

- King (That's you, my liege :) )

  - Each side has one king
  - The King is the only unit that can capture and move the enemy flag

- Magician

  - The magician can conjure up fireballs that home in on the intended target
  - They make it easy to bring light to your kingdom cast in darkness

- Scout

  - The nefarious scout uses its guile to be invisible to enemies except when 
    it wanders near a base or a tower

- Swordsman

  - A sword-wielding strongman


Death and Respawning
^^^^^^^^^^^^^^^^^^^^

When Actors die, they're added to the respawn queue.

The list of actors ready to be respawned can be obtained with a call to
:cpp:func:`state::PlayerStateHandler::GetRespawnables` and the actors themselves
can be respawned by calling the
:cpp:func:`state::PlayerStateHandler::RespawnUnit` function

The other components include:

- Base

  - Each team has a base where the flag is positioned initially
  - Park too many units near the base and you get docked points, 'cause winter's coming and your 
    villagers really need that sugar from the enemy kingdom :(
  - Dead units ready to be respawned can be respawned either at the base or at
    one of the towers that you own

- Fire Ball

  - Is conjured up by a Magician when the magician wants to attack an enemy

- Flag

  - The object of everyone's desire: The other player wants it; you want to be with it

- Tower

  - Imbued with magic by your magicians, your towers are a symbol of power and a rally point for your troops
  - They can fire fireballs at enemy troops
  - Your units can be respawned at the towers too
  - Tower Ownership:

    - Towers can change ownership when their HP has been brought down to zero
      after which it is contended for.
    - During the contention period, both players try to occupy the region around the tower
    - The numerical advantage in troops at the end of every tick is added to
      the contention score.
    - When the contention score reaches 100, the player who hit the maximum
      contention score assumes tower ownership


Map
---

- The terrain is a 30x30 grid where each element is either a:

  - Plain

    - Normal stuff

  - Forest

    - Attacking range and visibility reduce when units are in the forest

  - Mountain

    - Attacking range and visibility increase when units are in the forest

Each element is called a ``TerrainElement`` (See: :cpp:class:`state::TerrainElementView`). Its size is 200x200 units.

There are two ways of addressing TerrainElements: by offsets and by cartesian coordinates.

- Cartesian coordinates:
    The origin is at the top left corner of the map.
    Right is increasing X, down is increasing Y.

- Offsets:
    The origin is at the top left corner of the map.
    It's a pair, of which the first element is the row number.
    The second number is the column number.
    Numbering starts from 0.


Line of Sight
^^^^^^^^^^^^^

Each actor has a line of sight radius defined in terms of grid elements.
For a player, each grid element is in one of 3 states:

- Unexplored

  - Self explanatory. The player's troops haven't yet set foot on this piece of
    terrain
  - The unexplored regions are shrouded in darkness and the players will not be
    able to see what lies underneath

- Explored

  - The player's troops were at this point some time in the past but are not
    there presently
  - Explored regions are partially unmasked.

    - The terrain type and towers (if present on the grid element) will continue
      to be visible to the players for the rest of the game
    - The enemy actors (again if present on this piece of terrain), however,
      will not the visible

- Direct LOS

  - A grid element is in direct LOS if any of the player's troops are on it at
    the moment.
  - Everything, including enemy actors are fully visible
  - The player's actors can only attack those troops that are in direct LOS

Game Mechanics
==============

Progressing
-----------

The preliminary round will consist of 3 levels each accompanied by an AI of
increasing intelligence bundled in with the application.

The second round has been cancelled. The top three in the leaderboard in round 1
get prizes.

The event ends on March 5th, at 23:59 hours.

Execution Order
---------------

The smallest unit of time in the game is a clock tick.

There are 2 update cycles that keep the game ticking

- The player update cycle

  - Each player gets their own thread of execution and an individual copy of the
    game state that they work with.
  - Each thread executes the code defined in the playerAI's ``Update`` method.
  - A player's update cycle may take more than one clock tick. However, at the end
    of the first clock tick, the player's copy of the game state will become stale,
    so a tradeoff between strategy and speed must be made.

- The main update cycle

  - The main update cycle has its own thread which it uses to update the state
    every clock tick.
  - Actor positions, HP and Lines Of Sight are updated.
  - If a player was done with his/her update cycle, the main thread also updates
    the player's copy of the game state.


API available
-------------

See :cpp:func:`state::PlayerStateHandler::MoveUnits`,
:cpp:func:`state::PlayerStateHandler::AttackUnit`,
:cpp:func:`state::PlayerStateHandler::FlagCapture`,
:cpp:func:`state::PlayerStateHandler::PlanPath`

For more extensive explanations and a complete list of functions, do check out
the full documentation available on this site.

Scoring
=======

- 50 points for capturing the flag, ie, Moving the flag from the enemy base all
  the way to yours.
- -ve points due to base poisoning.

  - Base poisoning is when players are docked points for camping near their base.
  - The ``base_poisoning_threshold`` is the maximum numerical advantage that a
    player can have over his opponent in terms of number of troops positioned
    near his base for which base poisoning doesn't apply.

- 1 point per tower every ten seconds you hold it. So holding 2 towers for 15 seconds
  will net you 3 points.


Victory
=======

The player with the higher score at the end of 5 minutes is the winner.

C++ language Restrictions
=========================

- No external libraries are allowed

  - You may only use the C++ standard library

- No filesystem calls

  - Files should not be created or read from

- No spawning threads/processes

- Maximum total file size submission is 8 MB

If any of the restrictions are violated, the code will not be evaluated

References
==========

- Documentation on this page
- C++ Tutorials

  - https://isocpp.org/get-started
  - http://ureddit.com/class/23620/introduction-to-c----a-video-guided-tutorial
