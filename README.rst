========
Overview
========

.. image:: https://secure.travis-ci.org/jamesls/semidbm.png?branch=master
   :target: http://travis-ci.org/jamesls/semidbm

.. image:: https://coveralls.io/repos/jamesls/semidbm/badge.png?branch=master
   :target: https://coveralls.io/r/jamesls/semidbm?branch=master


SemiDBM is an attempt at improving the dumbdbm in the python standard library.
It's a slight improvement in both performance and in durability.  It can be
used anywhere dumbdbm would be appropriate to use, which is basically when you
have no other options available.  It uses a similar design to dumbdbm which
means that it does inherit some of the same problems as dumbdbm, but it also
attempts to fix problems in dumbdbm, which makes it only a semi-dumb dbm :)
It supports a "dbm like" interface::

    import semidbm
    db = semidbm.open('testdb', 'c')
    db['foo'] = 'bar'
    print db['foo']

    db.close()
    # Then at a later time:
    db = semidbm.open('testdb', 'r')
    # prints "bar"
    print db['foo']


A design goal of semidbm is to remain a pure python dbm.  This makes
installation easy and allows semidbm to be used on any platform that
supports python.

Supported Python Versions
=========================

Semidbm supports python 2.6, 2.7, and 3.3.

=============
Official Docs
=============

Read the `semidbm docs <http://semidbm.readthedocs.org>`_ for more information
and how to use semidbm.


============
Improvements
============

Below are a list of some of the improvements semidbm makes over dumbdbm.


Single Data File
================

Instead of an index file and a data file, the index and data have been
consolidated into a single file.  This single data file is always appended to,
data written to the file is never modified.


Data File Compaction
====================

Semidbm uses an append only file format.  This has the potential to grow to
large sizes as space is never reclaimed.  Semidbm addresses this by adding a
``compact()`` method that will rewrite the data file to a minimal size.


Performance
===========

Semidbm is significantly faster than dumbdbm (keep in mind both are pure python
libraries) in just about every way.  The documentation shows the
`results <http://semidbm.readthedocs.org/en/latest/benchmarks.html>`_
of semidbm vs. other dbms, along with how to run the benchmarking
script yourself.


===========
Limitations
===========

* Not thread safe; can't be accessed by multiple processes.
* The entire index must fit in memory.  This essentially means that all of the
  keys must fit in memory.


Post feedback and issues on `github issues`_, or check out the
latest changes at the github `repo`_.


.. _github issues: https://github.com/jamesls/semidbm/issues
.. _repo: https://github.com/jamesls/semidbm
