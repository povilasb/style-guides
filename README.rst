.. highlight:: c++
        :linenothreshold: 5

======================
C++ coding style guide
======================

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

Maximum of 80 charactes should be used on a single line.


Indentation
-----------

Tabs.


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
        class Employee : public Person {
        public:
                Employee(const std::string& name, const std::string& profession);

        protected:
                ...

        private:
                ...
        };


Enums
-----

::
        enum Severity_level {
                debug, info, warning, error
        }

Or ::
        enum Severity_level {
                debug,  // Most verbose logs.
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
        HTTP_GET:
                break;

        HTTP_POST:
                breaj;

        default:
        }


Naming
======


Classes, enums
--------------

They start with a capital letter but any additional word is separated with an
unserscore. Underscore_based_classes simply read easier than
CamelCaseClassNames. And the first capital letter lets easier distinguish
between standard c++, Boost and your project specific classes.

::

        class Http_server {
        ...
        };

        enum Http_methods {
        ...
        };


Class fields, methods
+++++++++++++++++++++

They start with lower case letters and each word is separated with underscore.

::

        class Http_server {
        public:
                void set_uri_handler(...);
        };


Private fields
++++++++++++++

Private class fields end with underscore::

        class Http_server {
        private:
                unsigned int port_;
        };


Setter, getter methods
++++++++++++++++++++++

Setters and getters have the same name. They are named after the variable they
set. Setter accepts parameter to set. Getter method does not accept any
parameters.

::

        class Http_server {
        public:
                void port(unsigned int port_);
                unsigned int port(void) const;

        private:
                unsigned int port_;

        };


        void
        Http_server::port(unsigned int port_)
        {
                this->port_ = port_;
        }

        unsigned int
        Http_server::port(void) const
        {
                return this->port_;
        }
