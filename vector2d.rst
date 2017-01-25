Vector2D
========

.. cpp:class:: physics::Vector2D

	Implementation for 2D vectors

	.. cpp:member:: double x

		The x component of the vector

	.. cpp:member:: double y

		The y component of the vector

	.. cpp:function:: physics::Vector2D(x, y)

		Constructor for the vector class

		**Parameters:**

			.. cpp:var:: double x

				The value that the x component of the vector should take

			.. cpp:var:: double y

				The value that the y component of the vector should take

	.. cpp:function:: friend std::ostream& operator<<(std::ostream& ostream, const physics::Vector2D& vector)

		The stream operator for this class

		Prints in the format ``(x, y)``

		Example usage::

			physics::Vector2D a(1, 1);

			std::cout << a; // Prints "(1, 1)"

	.. cpp:function:: bool operator==(physics::Vector2D rhs)

		The equality operator for this class

		Two vectors are equal if their respective x and y components are equal

		Example usage::

			physics::Vector2D a(1, 1);

			if (a == physics::Vector2D(1, 1)) // True
				std::cout << "The values are equal";

	.. cpp:function:: physics::Vector2D operator+(physics::Vector2D rhs)

		The vector addition operator for this class

		Example usage::

			physics::Vector2D a(1, 1);
			physics::Vector2D b(0.5, 0.5);

			physics::Vector2D c = a + b;

			std::cout << c; // Prints "(1.5, 1.5)"

	.. cpp:function:: physics::Vector2D operator-(physics::Vector2D rhs)

		The vector subtration operator for this class

		Example usage::

			physics::Vector2D a(1, 1);
			physics::Vector2D b(0.5, 0.5);

			physics::Vector2D c = a - b;

			std::cout << c; // Prints "(0.5, 0.5)"

	.. cpp:function:: physics::Vector2D operator+(double rhs)

		The scalar addition operator for this class

		Example usage::

			physics::Vector2D a(1.5, 1);
			double b = 1.3;

			a = a + b;

			std::cout << a; // Prints "(2.8, 2.3)"

	.. cpp:function:: physics::Vector2D operator-(double rhs)

		The scalar subtration operator for this class

		Example usage::

			physics::Vector2D a(1.5, 1);
			double b = 1.3;

			a = a - b;

			std::cout << a; // Prints "(0.2, -0.3)"

	.. cpp:function:: physics::Vector2D operator*(double rhs)

		The scalar multiplication operator for this class

		Example usage::

			physics::Vector2D a(1, 1);
			double b = 2;

			a = a * b;

			std::cout << a; // Prints "(2, 2)"

	.. cpp:function:: physics::Vector2D operator/(double rhs)

		The scalar division operator for this class

		Example usage::

			physics::Vector2D a(1, 1);
			double b = 2.0,;

			a = a / b;

			std::cout << a; // Prints "(0.5, 0.5)"

	.. cpp:function:: double dot(physics::Vector2D rhs)

		Returns dot product of this vector with ``rhs``

		Example usage::

			physics::Vector2D a(1, 1);
			physics::Vector2D b(5, 6);

			std::cout << a.dot(b); // Prints "11"

	.. cpp:function:: double magnitude()

		Returns the magnitude of this vector

		Example usage::

			physics::Vector2D a(3, 4);

			std::cout << a.magnitude(); // Prints "5"

	.. cpp:function:: double distance(physics::Vector2D other)

		Returns Euclidean distance between this vector and the ``other`` vector

		Example usage::

			physics::Vector2D a(0, 0);
			physics::Vector2D b(1, 0);

			std::cout << a.distance(b); // Prints "1"
