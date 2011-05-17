Vendor libraries are a chore to maintain, so let's make the computer do it!


Installation
------------

You'll have to install from github while I'm still figuring this out::

    pip install -e git://github.com/jbalogh/vending-machine.git#egg=vend


Usage
-----

Help::

    vend -h

All commands need to be prefixed by the path to the vendor directory. Right now
you use the ``-d`` argument, but I might change that::

    vend -d path/to/vendor

Then there are some commands for working with your vendor directory. Most
commands take a package as an argument. The package can be the name of
something on pypi or a url with a ``git:`` prefix.


Sync
====

If you're starting a new vendor library, you can use an existing
``requirements.txt`` to seed the vendor lib::

    vend -d vendor sync -r requirements.txt

Eventually this command will work with an existing vendor lib as well, to sync
new updates to requirements.txt.


Freeze
======

To generate a requirements.txt file from your vendor library::

    vend -d vendor freeze > requirements.txt

Your vendor packages must have the ``egg-info`` directories created by
setuptools embedded inside for freeze to work properly.


Add
===

Adding a new package::

    vend -d vendor add celery

Adding a new submodule::

    vend -d vendor add git://github.com/jbalogh/check#egg=check


Update
======

Updating a package::

    vend -d vendor update celery 2.1.6

Updating a submodule::

    vend -d vendor update check 03b26bc3f1
    vend -d vendor update check origin/master

Update doesn't use `git://` urls since it's clever enough to look for the name
of the package in ``vendor/src``. Maybe that's too clever.


Uninstall
=========

Uninstalling a package::

    vend -d vendor uninstall celery

Uninstalling a submodule::

    vend -d vendor uninstall check


Issues
======

 * add should take a version (you could use update for that effect)
 * add should be called install to match pip and oppose uninstall
