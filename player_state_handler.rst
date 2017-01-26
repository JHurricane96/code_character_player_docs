PlayerStateHandler
==================

TerrainElementView
------------------

.. cpp:class:: state::TerrainElementView

	The terrain is a grid of TerrainElements

	This is an interface for TerrainElements

	.. cpp:member:: physics::Vector2D position

		Position of the TerrainElement in cartesian coordinates

	.. cpp:member:: int64_t size

		The size of this TerrainElement

	.. cpp:member:: state::TERRAIN_TYPE terrain_type

		The type of terrain in this TerrainElement

	.. cpp:member:: state::LOS_TYPE los_type

		The Line of Sight you have to this TerrainElement

PlayerStateHandler
------------------

.. cpp:class:: state::PlayerStateHandler

	The interface for accessing and manipulating the internal state of the game

	.. cpp:function:: state::list_act_id_t GetPlayerUnitIds()

		Gets Actor IDs of your units

	.. cpp:function:: state::list_act_id_t GetPlayerEnemyIds()

		Gets Actor IDs for enemy units visible to you

	.. cpp:function:: std::vector<state::MagicianView> GetMagicians()

		Gets your Magicians

	.. cpp:function:: std::vector<state::EnemyMagicianView> GetEnemyMagicians()

		Gets your enemy's Magicians that are in your Line Of Sight

	.. cpp:function:: std::vector<state::ScoutView> GetScouts()

		Gets your Scouts

	.. cpp:function:: std::vector<state::EnemyScoutView> GetEnemyScouts()

		Gets your enemy's Scouts that are in your Line Of Sight

	.. cpp:function:: std::vector<state::SwordsmanView> GetSwordsmen()

		Gets your Swordsmen

	.. cpp:function:: std::vector<state::EnemySwordsmanView> GetEnemySwordsmen()

		Gets your enemy's Swordsmen that are in your Line Of Sight

	.. cpp:function:: std::vector<state::TowerView> GetTowers()

		Gets your Towers

	.. cpp:function:: std::vector<state::EnemyTowerView> GetEnemyTowers()

		Gets the enemy's Towers

	.. cpp:function:: state::KingView GetKing()

		Gets your King

	.. cpp:function:: state::EnemyKingView GetEnemyKing(success)

		Gets your enemy's King if it's in your Line Of Sight
		
		The parameter success's value is set if not ``NULL`` and it indicates the outcome of the call
		
		success is:

		* ``0``  if the enemy King is not in your Line Of Sight
		* ``1``  if the King is retrieved

		Returns ``nullptr`` if the enemy King isn't in your LOS

		**Parameters:**

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of the function call

	.. cpp:function:: state::FlagView GetFlag()

		Gets your Flag

	.. cpp:function:: state::EnemyFlagView GetEnemyFlag()

		Gets your enemy's Flag

	.. cpp:function:: state::BaseView GetBase()

		Gets your Base

	.. cpp:function:: state::EnemyBaseView GetEnemyBase()

		Gets your enemy's Base

	.. cpp:function:: state::TerrainElementView CoordinateToTerrainElement(\
		position, \
		success)
		
		Gets TerrainElementView corresponding to position vector
		
		The parameter success's value is set if not ``NULL`` and it indicates the outcome of the call
		
		success is:

		* ``0``  if coordinate given is out of bounds
		* ``1``  if successful

		**Parameters:**

			.. cpp:var:: physics::Vector2D position

				The position vector in x, y coordinates

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of the function call

	.. cpp:function:: state::TerrainElementView OffsetToTerrainElement(\
		offset, \
		success)

		Gets TerrainElement corresponding to grid offset
		
		The parameter success's value is set if not ``NULL`` and it indicates the outcome of the call
		
		success is:

		* ``0``  if offset given is out of bounds
		* ``1``  if successful

		**Parameters:**

			.. cpp:var:: physics::Vector2D offset

				The position vector in offset form.

				``offset.x`` = row number

				``offset.y`` = column number

				Rows and columns are zero-indexed.
			
			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of the function call

	.. cpp:function:: state::UnitView GetUnitFromId(actor_id, success)

		Gets an Actor (UnitView) belonging to you from its ID

		Returns an empty UnitView on an unsuccessful call
		
		The parameter success's value is set if not ``NULL`` and it indicates the outcome of the call
		
		success is:

		* ``0``  if Actor ID is invalid
		* ``-1`` if Actor does not belong to you
		* ``1``  if successful

		**Parameters:**

			.. cpp:var:: state::act_id_t actor_id

				The Actor's ID

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of function call


	.. cpp:function:: state::EnemyUnitView GetEnemyUnitFromId(actor_id, success)

		Gets an Actor (EnemyUnitView) belonging to your enemy from its ID

		Returns an empty EnemyUnitView on an unsuccessful call
		
		The parameter success's value is set if not ``NULL`` and it indicates the outcome of the call
		
		success is:

		* ``0``  if actor id is invalid
		* ``-1`` if actor does not belong to the enemy
		* ``1``  if successful

		**Parameters:**

			.. cpp:var:: state::act_id_t actor_id

				The enemy's Actor's ID

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of function call

	.. cpp:function:: state::list_act_id_t GetRespawnables()

		Gets Actor IDs of your dead units that are ready to respawn

	.. cpp:function:: void MoveUnits(\
							unit_ids, \
							destination, \
							formation_maker, \
							terrain_weights, \
							path, \
							success\
						)

		Sets units into motion.

		This method has a built-in path planner that you can use.

		The path planner can be used to implement formations and terrain preference.

		The actual path and its cost are returned.

		The parameter success's value is set if not ``NULL`` and it
		indicates the outcome of the call.
		
		success is:

		* ``0``  if unit_ids is empty
		* ``-1`` if any unit's Actor ID is invalid
		* ``-2`` if any unit doesn't belong to you
		* ``-3`` if any unit is dead
		* ``-4`` if any of the units isn't capable of moving (Flag, Base)
		* ``-5`` if destination is not on the map
		* ``-6`` if formation is not valid
		* ``-7`` if terrain_weights isn't of size 3
		* ``-8`` if terrain_weights has non-positive weights
		* ``1``  if successful

		**Parameters:**

			.. cpp:var:: state::list_act_id_t unit_ids

				Actor IDs of the units to be moved

		   	.. cpp:var:: physics::Vector2D destination

		   		The destination

		   	.. cpp:var:: state::FormationMaker* formation_maker

		   		The formation maker

		   	.. cpp:var:: std::vector<int64_t> terrain_weights

		   		The weights to be assigned to the terrain elements

		   		This vector is indexed by :cpp:enum:`state::TERRAIN_TYPE`, so it must be of size ``3``

		   		* ``0`` index is :cpp:enumerator:`state::PLAIN`
		   		* ``1`` index is :cpp:enumerator:`state::FOREST`
		   		* ``2`` index is :cpp:enumerator:`state::MOUNTAIN`

		   		Each weight is a number greater than zero

		   		The higher the weight, the less preference you're giving to a path along that terrain

		   	.. cpp:var:: std::vector<physics::Vector2D>& path

		   		The path the leader will move along is stored in this vector after the function call

		   	.. cpp:var:: int* success

		   		If valid pointer (not ``NULL``), holds success of the function call

	.. c:function:: void MoveUnits(\
		unit_ids, \
		destinations, \
		formation_maker, \
		success)
		
		Sets units into motion.
		
		The path is given by you, no path planning is done in this method.

		However, the facility to move in formation is still present.
		
		The parameter success's value is set if not ``NULL`` and it
		indicates the outcome of the call.
		
		success is:
		
		* ``0`` if unit_ids is empty
		* ``-1`` if any unit's Actor ID is invalid
		* ``-2`` if any unit doesn't belong to you
		* ``-3`` if any unit is dead
		* ``-4`` if any of the units isn't capable of moving (Flag, Base)
		* ``-5`` if destinations is empty
		* ``-6`` if any member of destinations is not on the map
		* ``-7`` if formation is not valid
		* ``1`` if successful

		**Parameters:**

			.. cpp:var:: state::list_act_id_t unit_ids

		   		Actor IDs of the units to be moved

		   	.. cpp:var:: std::vector<physics::Vector2D> destinations

				The path along which the units should move
				
				It's a list of 2D vectors of coordinates
			
		   	.. cpp:var:: state::FormationMaker* formation_maker

		   		The formation maker

		   	.. cpp:var:: int* success

		   		If valid pointer (not ``NULL``), holds success of the function call

	.. cpp:function:: void AttackUnit(\
		attacker_ids, \
		attack_target_id, \
		success\
		)

		Command your units to attack a single enemy unit

		Units stop attacking when the enemy goes out of range/Line Of Sight and become idle
		
		The parameter success's value indicates the outcome of the call
		
		success is:

		* ``0`` if attacker_ids is empty
		* ``-1`` if any attacker's Actor ID is invalid
		* ``-2`` if any attacking unit doesn't belong to you
		* ``-3`` if any attacking unit is dead
		* ``-4`` if any of the units isn't capable of attacking
		* ``-5`` if the target's Actor ID is invalid
		* ``-6`` if the target is in your team
		* ``-7`` if the target is dead
		* ``-8`` if the target isn't in your LOS
		* ``1`` if successful

		**Parameters:**

			.. cpp:var:: state::list_act_id_t attacker_ids

				List of Actor IDs of attacking units

			.. cpp:var:: state::act_id_t attack_target_id

				Actor ID of the target

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of function call

	.. cpp:function:: void FlagCapture(success)

		Instructs your King to capture the enemy's Flag

		Your King must be at the enemy's Flag to capture it, 
		it doesn't move automatically
		
		The parameter success's value indicates the outcome of the call
		
		success is:

		* ``0`` if the King is dead
		* ``-1`` if the King isn't near enough to the Flag
		* ``-2`` if the King already has the Flag
		* ``1`` if successful

		**Parameters:**

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of function call

	.. cpp:function:: void FlagDrop(success)

		Instructs a player's King to drop the enemy's Flag

		Your King must be at your Base to drop it, it doesn't move automatically
		
		The parameter success's value indicates the outcome of the call
		
		success is:

		* ``0`` if the King is dead
		* ``-1`` if the King isn't near enough to his Base
		* ``-2`` if the King doesn't have a Flag
		* ``1`` if successful

		**Parameters:**

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of function call

	.. cpp:function:: float PlanPath(\
		start, \
		destination, \
		terrain_weights, \
		path, \
		success\
		)

		Calculates the total weight of the best (shortest) 
		path between the given points and returns it
		
		The parameter success's value indicates the outcome of the call
		
		success is:

		* ``0`` if start is not on the map
		* ``-1`` if destination is not on the map
		* ``-2`` if terrain_weights isn't of size 3
		* ``-3`` if terrain_weights has non-positive weights
		* ``1``  if successful

		**Parameters:**

			.. cpp:var:: physics::Vector2D start

				The starting point's cartesian coordinates

			.. cpp:var:: physics::Vector2D destination

				The destination's cartesian coordinates

			.. cpp:var:: std::vector<int64_t> terrain_weights

				The weights to be assigned to the terrain elements

				This vector is indexed by :cpp:enum:`state::TERRAIN_TYPE`, so it must be of size ``3``

				* ``0`` index is :cpp:enumerator:`state::PLAIN`
				* ``1`` index is :cpp:enumerator:`state::FOREST`
				* ``2`` index is :cpp:enumerator:`state::MOUNTAIN`

				Each weight is a number greater than zero

				The higher the weight, the less preference you're giving to a path along that terrain

			.. cpp:var:: std::vector<physics::Vector2D>& path

				The shortest path is stored in this vector after the function call
				
				This is a list of 2D vectors from start (excluding it) to destination (including it)
			
			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of function call

	.. cpp:function:: void RespawnUnit(\
		actor_id, \
		respawn_location, \
		success\
		)

		Command one of your units to respawn if it's dead and 
		it's ready to respawn
		
		The parameter success's value indicates the outcome of the call
		
		success is:

		* ``0`` if actor_id is an invalid Actor ID
		* ``-1`` if the Actor to respawn yours
		* ``-2`` if the Actor isn't dead
		* ``-3`` if the Actor's time_to_respawn isn't 0
		* ``-4`` if the respawn_location is an invalid Actor ID
		* ``-5`` if the respawn_location isn't yours
		* ``-6`` if the respawn_location isn't a Tower/Base
		* ``1`` if successful

		**Parameters:**

			.. cpp:var:: state::act_id_t actor_id

				The ID of the Actor to respawn

			.. cpp:var:: state::act_id_t respawn_location

				The Actor ID of the Base/Tower to respawn the dead Actor at

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of function call
