.. _tv-login:

*************************
"Read Only" Display Login
*************************

The ZMON front end requires users to login.
However a very common way of deploying dashboards is on TV screens running across office spaces to e.g. render Grafana or ZMON dashboards.
For this ZMON provides you with a way to login a read only authenticated user via one-time tokens.
Those tokens can be created by any real user via the ZMON CLI.


Getting a token
===============

.. code-block:: bash

    zmon onetime-token get

    Retrieving new one-time token ...
    https://zmon.example.org/tv/AocciOWf/
    OK

A token can be used exactly **once** to login. However the session created will last up to 365 days.


Login with token
================

Use the above URL in the target browser to login directly. This will create a read-only session.

.. code-block:: bash

    https://<your zmon url>/tv/<your token>


.. note::

    Please make sure you access the generated URL in order to login. Appending the <token> to any other ZMON location won't work.


How does it work
================

First time a valid one time token is used to login we associate a random UUID with it and the device IP.
Both are registered within ZMON to create a persisted session, thus this will continue to work after the frontend gets deployed.

So once the token is used, it can no longer be reused and you need to create another one if you want to run additional displays.
