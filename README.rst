loginform
=========

loginform is a library for filling HTML login forms given the login url,
username & password. Which form and fields to fill are inferred automatically.

It's implemented on top of `lxml form filling`_, and thus depends on lxml.
Running tests also requires `requests`_.

Usage
-----

Usage is very simple and best illustrated with an example::

    >>> from loginform import fill_login_form
    >>> import requests
    >>> url = "https://github.com/login"
    >>> r = requests.get(url)
    >>> fill_login_form(url, r.text, "john", "secret")
    ([('authenticity_token', 'FQgPiKd1waDL+pycPH8IGutirTnP69SiZgm0zXwn+VQ='),
      ('login', 'john'),
      ('password', 'secret')],
     u'https://github.com/session',
     'POST')

Testing
-------

A collection of real-world samples is used to keep this library tested. Those
samples are managed as follows:

First, you select a site to try, find out its login url, and run the following
command to try loginform on it::

    $ python test.py https://github.com/login
    [
       "https://github.com/login", 
       [
          [
             [
                "authenticity_token", 
                "NsdVWGpzxKmn7zSJSOdgnDcLIzIdJlCTO754LiEv2W4="
             ], 
             [
                "login", 
                "USER"
             ], 
             [
                "password", 
                "PASS"
             ]
          ], 
          "https://github.com/session", 
          "POST"
       ]
    ]

From the output you can judge if it worked or not. If it worked, great. If it
didn't, you would hack ``loginform.py`` to make it work and then add the sample
with::

    $ python test.py https://github.com/login -w github

Note that we gave the sample a name (``github`` in this case).

To list all availabe samples use::

    $ python test.py -l

To run all tests, install nosetests and run::

    $ nosetests

.. _lxml form filling: http://lxml.de/lxmlhtml.html#forms
.. _requests: http://docs.python-requests.org/
.. _nosetests: https://nose.readthedocs.org/en/latest/
