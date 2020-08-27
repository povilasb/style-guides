======================
C++ coding style guide
======================

.. highlight:: c++
	:linenothreshold: 5

Why yet another C++ coding style? Because there is no standard style. Each
company, organization has it's own. Most of them don't satisfy me. They are
similar to java coding style. Personally, I want to stay close to Bjarne
Stroustrup's and STL, Boost coding styles. Why? Because this looks more like
C++ and code becomes more consistent when it integrates nicer with standard
libraries.


Formatting
==========


Lines
-----

Maximum of 80 charactes should be used on a single line. Why?:

* Humans read narrower columns faster.
* http://www.emacswiki.org/emacs/EightyColumnRule


Indentation
-----------

Tabs. Tab size is 8 spaces.


Namespaces
-----------

::

	namespace log
	{

	...

	}


Classes
-------

::

	class employee : public person {
	public:
		employee(const std::string& name, const std::string& profession);

	protected:
		...

	private:
		...
	};


Enums
-----

::

	enum severity_level {
		debug, info, warning, error
	}

Or ::

	enum severity_level {
		debug, // Most verbose logs.
		info, // General info logs.
		warning, //Llogs that need attention.
		error // Something unexpected happened.
	}


Try, catch
----------

::

	try {
		new int[10000000000];
	}
	catch (std::bad_alloc e) {
		cout << e.what() << '\n';
	}


If, else
--------

::

	bool success = false;
	...
	if (success) {
		// on success.
	}
	else {
		// on error.
	}


Switch
------

::

	switch (http_method) {
	case HTTP_GET:
		break;

	case HTTP_POST:
		breaj;

	default:
	}


Naming
======


Files
-----

To easier distinguish between C and C++ code header files should be named
`*.hpp` and source files `*.cpp`.


Macros
------

In general, macros should be avoided, but if you have ones, you should
capitalize them::

	#define VERSION 0x010A03


Classes, enums
--------------

Their names consist of all lower case letters and words are separated with an
unserscore. underscore_based_classes simply read easier than
CamelCaseClassNames.

::

	class http_server {
	...
	};

	enum http_methods {
	...
	};


Class fields, methods
+++++++++++++++++++++

They start with lower case letters and each word is separated with underscore.

::

	class http_server {
	public:
		void set_uri_handler(...);
	};


Private fields
++++++++++++++

Private class fields end with underscore::

	class http_server {
	private:
		unsigned int port_;
	};


Constants
+++++++++

Use same naming convention as for usual variables, no UPPER CASE NAMES::

	class http_server {
	public:
		static const std::string protocol_version = "1.1";
	...
	};


Setter, getter methods
++++++++++++++++++++++

Setters and getters have the same name. They are named after the variable they
set. Setter accepts parameter to set. Getter method does not accept any
parameters.

::

	class http_server {
	public:
		void port(unsigned int port_);
		unsigned int port(void) const;

	private:
		unsigned int port_;

	};


	void
	http_server::port(unsigned int port_)
	{
		this->port_ = port_;
	}

	unsigned int
	Http_server::port(void) const
	{
		return this->port_;
	}


Error handling
==============

Different forms of error reporting should be used as follows:[#f1]_

* *Static assertions* To prevent invalid instantiations of templates and to
  check other compile-time conditions.
* *Exceptions* To let some calling code know that a function was unable to
  fulfil its contract due to some run-time problems.
* *Error codes* To report run-time conditions that are part of a function's
  contract and considered normal behavior.
* *Run-time assertions* To perform sanity checks on internal operations at
  run-time and ensure that major bugs do not enter production builds.


Exceptions
----------

Catch exceptions by reference::

	try {
		// ...
	}
	catch (const std::runtime_error& e) {
		// ...
	}


Misc
====


Accessing class members
-----------------------

When accessing private class members always refer to them via ``this``::


	class person {
	public:
		std::string
		name() const
		{
			return this->name_;
		}

	private:
		std::string name_;

	};

This makes it clear where variable ``name_`` came from without further
code investigation. And avoids errors in some situations [#f2]_.


TODO
====

* In source documentation: do not document what's obvious. E.g. std::string get_name();


.. rubric:: References

.. [#f1] http://josephmansfield.uk/articles/exceptions-error-codes-assertions-c++.html
.. [#f2] http://www.parashift.com/c++-faq-lite/nondependent-name-lookup-members.html
