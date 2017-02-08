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

	.. cpp:function:: int64_t GetSize()

		Gets your unit's radius

		Assumes your unit is a circle

	.. cpp:function:: state::ActorType GetActorType()

		Gets your unit's ActorType

	.. cpp:function:: bool CanAttack()

		Returns ``true`` if your unit can attack, ``false`` otherwise

	.. cpp:function:: bool CanPathPlan()

		Returns ``true`` if your unit can move, ``false`` otherwise

	.. cpp:function:: state::EnemyUnitView* GetAttackTarget(success)

		Gets the EnemyUnitView of the target that this unit is currently attacking

		Returns ``nullptr`` if not attacking any unit

		The parameter success's value is set if not ``NULL`` and it indicates the outcome of the call

		success is:

		* ``0`` if your unit is not attacking another unit at the moment
		* ``1`` if your unit is currently attacking another unit

		**Parameters**:

			.. cpp:var:: int* success

				If valid pointer (not ``NULL``), holds success of function call

	.. cpp:function:: physics::Vector2D GetVelocity()

		Gets the velocity vector of this unit

	.. cpp:function:: int64_t GetAttackRange()

		Gets the attack range of your unit

		Your unit can only attack units within its attack range

	.. cpp:function:: physics::Vector2D GetPosition()

		Gets the position vector of this unit

	.. cpp:function:: state::PathPlannerHelperView GetPathPlannerHelper()

		Gets an interface to this unit's PathPlannerHelper

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

	.. cpp:function:: bool CanAttack()

		Returns ``true`` if the enemy unit can attack, ``false`` otherwise

	.. cpp:function:: bool CanPathPlan()

		Returns ``true`` if the enemy unit can move, ``false`` otherwise

	.. cpp:function:: int64_t GetSize()

		Gets the radius of the enemy unit

		Assumes units are circles

	.. cpp:function:: int64_t GetHp()

		Gets the HP of the enemy unit

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

	.. cpp:function:: int64_t GetFireBallTtl()

		The time that a FireBall fired by this Tower is alive for

	.. cpp:function:: int64_t GetFireBallSpeed()

		Gets the speed of FireBalls that are fired by this Tower

	.. cpp:function:: int64_t GetContentionRadius()

		Gets the radius within which units must be present to contend for 
		ownership of the Tower after its HP has been reduced to zero

	.. cpp:function:: float GetContentionScore()

		Gets the contention score for this Tower. If positive, the capture
		is proceeding in your favor, if negative, the enemy is closer to capturing
		it. It is 0 for Towers that still have some HP left.

	.. cpp:function:: int64_t GetMaxContentionScore()

		The value the contention score must reach for the Tower to be captured by you.
		If it reaches the negative of this value, the Tower is captured by the enemy.

EnemyTowerView
--------------

.. cpp:class:: state::EnemyTowerView: public state::EnemyUnitView

	Provides you with a restricted interface to work with your enemy's Towers

	.. cpp:function:: int64_t GetContentionRadius()

		Gets the radius within which units must be present to contend for 
		ownership of the Tower after its HP has been reduced to zero

	.. cpp:function:: float GetContentionScore()

		Gets the contention score for this Tower. If positive, the capture
		is proceeding in your favor, if negative, the enemy is closer to capturing
		it. It is 0 for Towers that still have some HP left.

	.. cpp:function:: int64_t GetMaxContentionScore()

		The value the contention score must reach for the Tower to be captured by you.
		If it reaches the negative of this value, the Tower is captured by the enemy.

MagicianView
------------

.. cpp:class:: state::MagicianView: public state::UnitView

	Provides you with an interface to work with your own Magicians

	.. cpp:function:: int64_t GetFireBallTtl()

		The time that a FireBall fired by this Magician is alive for

	.. cpp:function:: int64_t GetFireBallSpeed()

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

.. cpp:class:: state::KingView: public state::UnitView

	Provides you with an interface to work with your own Kings

	.. cpp:function:: bool HasFlag()

		Returns ``true`` if your King is carrying the enemy's flag, ``false`` otherwise

EnemyKingView
-------------

.. cpp:class:: state::EnemyKingView: public state::EnemyUnitView

	Provides you with a restricted interface to work with your enemy's Kings

	.. cpp:function:: bool HasFlag()

		Returns ``true`` if the enemy King is carrying your flag, ``false`` otherwise

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

.. cpp:class:: state::BaseView: public state::UnitView

	Provides you with an interface to work with your own Bases

	.. cpp:function:: int64_t GetBasePoisoningRadius()

		Gets the radius within which if an excess of your units are present,
		you slowly lose points from your score

	.. cpp:function:: int64_t GetBasePoisoningThreshold()

		Gets the poisoning threshold. If the number of your units minus the number
		of enemy units within the ``base_poisoning_radius`` exceeds this threshold,
		you slowly lose points from your score

EnemyBaseView
-------------

.. cpp:class:: state::EnemyBaseView: public state::EnemyUnitView

	Provides you with a restricted interface to work with your enemy's Bases

	.. cpp:function:: int64_t GetBasePoisoningRadius()

		Gets the radius within which if an excess of the enemy's units are present,
		the enemy slowly loses points from their score

	.. cpp:function:: int64_t GetBasePoisoningThreshold()

		Gets the poisoning threshold. If the number of the enemy's units minus the number
		of your units within the ``base_poisoning_radius`` exceeds this threshold,
		the enemy slowly loses points from its score
