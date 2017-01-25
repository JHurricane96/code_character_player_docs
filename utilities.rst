Utilities
=========

Actor ID
--------

.. cpp:type:: int64_t state::act_id_t

	Type for Actor IDs

List of Actor IDs
-----------------

.. cpp:type:: std::vector<int64_t> state::list_act_id_t

	Type for a list of Actor IDs

Terrain Type
------------

.. cpp:enum:: state::TERRAIN_TYPE

	Enumerator for the terrain types

	.. cpp:enumerator:: PLAIN

		Plain terrain type

	.. cpp:enumerator:: FOREST

		Forest terrain type

	.. cpp:enumerator:: MOUNTAIN

		Mountain terrain type

	.. cpp:enumerator:: UNDEFINED

		Undefined terrain type

		Returned when you try to get the terrain type of unexplored regions

Line Of Sight Types
-------------------

.. cpp:enum:: state::LOS_TYPE

	Enumerator for the types of Lines Of Sight

	.. cpp:enumerator:: UNEXPLORED

		Terrain that is unexplored by you

		You have not visited this region yet

	.. cpp:enumerator:: EXPLORED

		Terrain that has been explored by you

		You have visited this region at least once, but don't have a direct LOS on it

	.. cpp:enumerator:: DIRECT_LOS

		Terrain over which you have direct Line Of Sight

		Enemy units in these regions are visible to you

FormationMaker
--------------

.. cpp:class:: FormationMaker

	Inherit from this class to be able to define formations

	A formation is basically a list of vectors (``physics::Vector2D`` instances)

	The first element must be ``(0, 0)``, which is the leader's position

	The rest of the units follow the leader, and their elements contain positions relative to the leader's

	.. cpp:function:: virtual std::vector<physics::Vector2D> ReturnFormation(formation_size) = 0

		This method must be overriden and implemented

		It returns the list of vectors that define a formation

		The formation may vary depending on the ``formation_size``

		**Parameters:**

			.. cpp:var:: int64_t formation_size

				The number of units that are in the formation

				This method must return a vector whose size is equal to ``formation_size``
