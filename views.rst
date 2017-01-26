UnitViews
=========

PathPlannerHelperView
---------------------

.. cpp:class:: state::PathPlannerHelperView

	Helps units path plan

	Provides utility methods for units

	.. cpp:function:: bool IsPathPlanning()

		Returns ``true`` if the unit is path planning, ``false`` otherwise

UnitView
--------

.. cpp:class:: state::UnitView

	Provides you with an interface to work with your own units

	.. cpp:function:: state::act_id_t GetId()

		Gets the Actor ID of your unit

	.. cpp:function:: int64_t GetHp()

		Gets your unit's current HP

	.. cpp:function:: int64_t GetMaxHp()

		Gets your unit's maximum HP

	.. cpp:function:: int64_t GetMaxSpeed()

		Gets the maximum speed at which your unit can travel

	.. cpp:function:: state::ActorType GetActorType()

		Gets your unit's ActorType

	.. cpp:function:: state::EnemyUnitView GetAttackTarget()

		Gets the EnemyUnitView of the target that this unit is currently attacking

		Returns ``nullptr`` if not attacking any unit

	.. cpp:function:: physics::Vector2D GetVelocity()

		Gets the velocity vector of this unit

	.. cpp:function:: physics::Vector2D GetPosition()

		Gets the position vector of this unit

	.. cpp:function:: GetPathPlannerHelper()

		Gets this unit's PathPlannerHelper

EnemyUnitView
-------------

.. cpp:class:: state::EnemyUnitView

	Provides you with a restricted interface to work with your enemy's units

	.. cpp:function:: state::act_id_t GetId()

		Gets the ID of the enemy unit

	.. cpp:function:: physics::Vector2D GetPosition()

		Gets the position vector of the enemy unit in cartesian coordinates

	.. cpp:function:: state::ActorType GetActorType()

		Gets the ActorType of the enemy unit

SwordsmanView
-------------

.. cpp:type:: state::UnitView state::SwordsmanView

	Provides you with an interface to work with your own Swordsmen

EnemySwordsmanView
------------------

.. cpp:type:: state::EnemyUnitView state::EnemySwordsmanView

	Provides you with a restricted interface to work with your enemy's Swordsmen

TowerView
---------

.. cpp:class:: state::TowerView: public state::UnitView

	Provides you with an interface to work with your own Towers

	.. cpp:function:: GetFireBallTtl()

		The time that a FireBall fired by this Tower is alive for

	.. cpp:function:: GetFireBallSpeed()

		Gets the speed of FireBalls that are fired by this Tower

	.. cpp:function:: GetContentionRadius()

		Gets the radius within which units must be present to contend for 
		ownership of the Tower after its HP has been reduced to zero

EnemyTowerView
--------------

.. cpp:class:: state::EnemyTowerView: public state::EnemyUnitView

	Provides you with a restricted interface to work with your enemy's Towers

	.. cpp:function:: int64_t GetContentionRadius()

		Gets the radius within which units must be present to contend for 
		ownership of the Tower after its HP has been reduced to zero

MagicianView
------------

.. cpp:class:: state::MagicianView: public state::UnitView

	Provides you with an interface to work with your own Magicians

	.. cpp:function:: GetFireBallTtl()

		The time that a FireBall fired by this Magician is alive for

	.. cpp:function:: GetFireBallSpeed()

		Gets the speed of FireBalls that are fired by this Magician

EnemyMagicianView
-----------------

.. cpp:type:: state::EnemyUnitView state::EnemyMagicianView

	Provides you with a restricted interface to work with your enemy's Magicians

ScoutView
---------

.. cpp:type:: state::UnitView state::ScoutView

	Provides you with an interface to work with your own Scouts

EnemyScoutView
--------------

.. cpp:type:: state::EnemyUnitView state::EnemyScoutView

	Provides you with a restricted interface to work with your enemy's Scouts

KingView
--------

.. cpp:type:: state::UnitView state::KingView

	Provides you with an interface to work with your own Kings

EnemyKingView
-------------

.. cpp:type:: state::EnemyUnitView state::EnemyKingView

	Provides you with a restricted interface to work with your enemy's Kings

FlagView
--------

.. cpp:type:: state::UnitView state::FlagView

	Provides you with an interface to work with your own Flags

EnemyFlagView
-------------

.. cpp:type:: state::EnemyUnitView state::EnemyFlagView

	Provides you with a restricted interface to work with your enemy's Flags

BaseView
--------

.. cpp:type:: state::UnitView state::BaseView

	Provides you with an interface to work with your own Bases

EnemyBaseView
-------------

.. cpp:type:: state::EnemyUnitView state::EnemyBaseView

	Provides you with a restricted interface to work with your enemy's Bases
