====================
Makefile style guide
====================

.. highlight:: makefile
	:linenothreshold: 5

Makefile is a text file that defines targets and rules which are executed by
Make utility. This document describes conventions for writing the Makefiles.


Naming
======


Files
-----

The recommended name for make files is *Makefile* [f2]_. Misc make files with
common targets or variables should have extension **.mk**. This helps
text redactors to identify that this is a makefile and enable syntax
highlighting.


Targets
-------

Target names should use lower case letters. Words are separated with a
hyphen '-'. E.g.::

	test-debug:
		$(build_dir)/debug/bin


Variables
---------

Variables which are not special to make or inherited from the environment
should be in lowercase. Words should be separated with underscore symbol '_'.
E.g.::

	src_dir = $(CURDIR)/src
	build_dir = $(CURDIR)/build


Special targets
===============


Phony targets
-------------

Phony target declarations should follow appropriate target declarations rather
than be defined in one place [f1]_. This way it's easier to maintain targets.

Good::

	all: build test
	.PHONY: all

Bad::

	.PHONY: all build test

	all: build test


.. rubric:: References

.. [f1] http://clarkgrubb.com/makefile-style-guide#phony-targets
.. [f2] https://www.gnu.org/software/make/manual/html_node/Makefile-Names.html
