Utilities
=========

Logging
-------

.. cpp:function:: void ipc::Logger::Instance().SetLogs(log)

	Logs the given string to the renderer console

	**Parameters:**

		.. cpp:var:: std::string log

			The string to print on the console

	.. highlight:: cpp
	Example usage::

		ipc::Logger::Instance().SetLogs("Units are attacking!");

Actor ID
--------

.. cpp:type:: int64_t state::act_id_t

	Type for Actor IDs

	An Actor ID uniquely identifies an Actor

List of Actor IDs
-----------------

.. cpp:type:: std::vector<int64_t> state::list_act_id_t

	Type for a list of Actor IDs

Actor Types
-----------

.. cpp:enum-class:: state::ActorType

	Enumerator for Actor types

	.. cpp:enumerator:: MAGICIAN

		Actor type for Magicians

	.. cpp:enumerator:: FIREBALL

		Actor type for Fireballs

	.. cpp:enumerator:: BASE

		Actor type for Bases

	.. cpp:enumerator:: FLAG

		Actor type for Flags

	.. cpp:enumerator:: KING

		Actor type for Kings

	.. cpp:enumerator:: SCOUT

		Actor type for Scouts

	.. cpp:enumerator:: SWORDSMAN

		Actor type for Swordsmen

	.. cpp:enumerator:: TOWER

		Actor type for Towers

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

.. cpp:class:: state::FormationMaker

	Inherit from this class to be able to define formations

	A formation is basically a list of vectors (:cpp:class:`physics::Vector2D` instances)

	The first element must be ``(0, 0)``, which is the leader's position

	The rest of the units follow the leader, and their elements contain positions relative to the leader's

	.. highlight:: cpp
	Example usage::

		using namespace std;
		using namespace physics;
		using namespace state;

		class SimpleFormation : public FormationMaker {
			vector<Vector2D> ReturnFormation(int64_t formation_size) {
				// Creates and returns a list of Vector2D's, all set to (0, 0)
				// This means all units will move together
				return vector<Vector2D>(
					formation_size,
					Vector2D(0, 0)
				);
			}
		};

		class RectangleFormation : public FormationMaker {
			vector<Vector2D> ReturnFormation(int64_t formation_size) {
				// This returns a rectangle formation
				// It is as close to a square as possible
				int length = floor(sqrt(formation_size));
				vector<Vector2D> positions;
				int j = 0;
				int k = 0;
				for (int i = 0; i < formation_size; ++i) {
					positions.push_back(Vector2D(k * 10, j * 10));
					j = (j + 1) % length;
					if (j == 0) {
						k++;
					}
				}
				return positions;
			}
		};

	.. cpp:function:: virtual std::vector<physics::Vector2D> ReturnFormation(formation_size) = 0

		This method must be overriden and implemented

		It returns the list of vectors that define a formation

		The formation may vary depending on the ``formation_size``

		**Parameters:**

			.. cpp:var:: int64_t formation_size

				The number of units that are in the formation

				This method must return a vector whose size is equal to ``formation_size``
