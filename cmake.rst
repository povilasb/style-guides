========================
CMake coding style guide
========================

.. highlight:: cmake
	:linenothreshold: 5


Naming
======


Commands
--------

Use lowercase letters::

	add_executable(main main.cpp)


Variables
---------

Local variable names should use all lowercase letters::

	set(src_dir "${CMAKE_CURRENT_SOURCE_DIR}/src)


.. rubric:: References

.. [f1] https://techbase.kde.org/Policies/CMake_Coding_Style
