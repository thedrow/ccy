A python module for currencies. The module compiles a dictionary of
currency objects containing information useful in financial analysis.
Not all currencies in the world are supported yet. You are welcome to
join and add more.


:Master CI: |master-build|_ |coverage-master|
:Dev CI: |dev-build|_ |coverage-dev|
:Dowloads: http://pypi.python.org/pypi/ccy
:Source: https://github.com/lsbardel/ccy


.. |master-build| image:: https://travis-ci.org/lsbardel/ccy.png?branch=master
.. _master-build: http://travis-ci.org/lsbardel/ccy?branch=master
.. |dev-build| image:: https://travis-ci.org/lsbardel/ccy.png?branch=dev
.. _dev-build: http://travis-ci.org/lsbardel/ccy?branch=dev
.. |coverage-master| image:: https://coveralls.io/repos/lsbardel/ccy/badge.png?branch=master
  :target: https://coveralls.io/r/lsbardel/ccy?branch=master
.. |coverage-dev| image:: https://coveralls.io/repos/lsbardel/ccy/badge.png?branch=dev
  :target: https://coveralls.io/r/lsbardel/ccy?branch=dev


.. contents::
    :local:


Currency object
======================
To use it::

    >>> import ccy
    >>> c = ccy.currency('aud')
    >>> c.printinfo()
    code: AUD
    twolettercode: AD
    roundoff: 4
    default_country: AU
    isonumber: 036
    order: 3
    name: Australian Dollar
    >>> c.as_cross()
    'AUDUSD'
    >>> c.as_cross('/')
    'AUD/USD'

a currency object has the following properties:

* *code*: the `ISO 4217`_ code.
* *twolettercode*: two letter code (can't remeber the ISO number). Very useful for financial data providers such as Bloomberg.
* *default_country*: the default `ISO 3166-1 alpha-2`_ country code for the currency.
* *isonumber*: the ISO 4217 number.
* *name*: the name of the currency.
* *order*: default ordering in currency pairs (more of this below).
* *roundoff*: number of decimal places

Currency Crosses
~~~~~~~~~~~~~~~~~~~~~~~~~~

You can create currency pairs by using the ``currency_pair`` function::

    >>> import ccy
    >>> p = ccy.currency_pair('eurusd')
    >>> p
    ccy_pair: EURUSD
    >>> p.mkt()  # market convention pair
    ccy_pair: EURUSD
    >>> p = ccy.currency_pair('chfusd')
    >>> p
    ccy_pair: CHFUSD
    >>> p.mkt()  # market convention pair
    ccy_pair: USDCHF


Some shortcuts::

    >>> import ccy
    >>> ccy.cross('aud')
    'AUDUSD'
    >>> ccy.crossover('eur')
    'EUR/USD'
    >>> ccy.crossover('chf')
    'USD/CHF'

Note, the Swiss franc cross is represented as 'USD/CHF', while the Aussie Dollar
and Euro crosses are represented with the USD as denominator.
This is the market convention which is handled by the **order** property
of a currency object.

Country information
~~~~~~~~~~~~~~~~~~~~~~~~~~

To use it::

    >>> import ccy
    >>> c = ccy.country('us')
    >>> c
    'United States'
    >>> ccy.countryccy('us')
    'USD'


Not all the country codes are standard `ISO 3166-1 alpha-2`_.
There is a function for adding extra pseudo-countries::

    import ccy
    ccy.set_new_country('EU','EUR','Eurozone')

Set a new country with code 'EU', currency 'EUR' named 'Eurozone'.
This pseudo country is set in the library already.


Date and Periods
===================

The module is shipped with a ``date`` module for manipulating time periods and
converting dates between different formats. The *period* function can be used
to create ``Period`` instances::

    >>> from ccy import period
    >>> p = period('1m')
    >>> p
    1M
    >>> p += '2w'
    >>> p
    1M2W
    >>> P += '3m'
    >>> p
    4M2W


Requirements
================

* Python 2.6 or above, including Python 3
* pytz_ for Countries information.


Installation
~~~~~~~~~~~~~~~~

This library works for Python 2.6 and higher, including Python 3.

Using `easy_install`::

    easy_install ccy

Using `pip`::

    pip install ccy

From source::

    python setup.py install

It requires the pytz_ package.

Runnung tests
~~~~~~~~~~~~~~~~~~~~~

From within the package directory::

    python runtests.py


.. _pytz: http://pytz.sourceforge.net/
.. _`ISO 3166-1 alpha-2`: http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
.. _`ISO 4217`: http://en.wikipedia.org/wiki/ISO_4217