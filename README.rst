WSGIserver
==========

**WSGIserver** is a high-speed, production ready, thread pooled, generic WSGI server with **SSL support**.

WSGIserver suppport both Python 2 and Python 3.

WSGIserver is developed by Florent Gallaire fgallaire@gmail.com.

Website: http://fgallaire.github.io/wsgiserver.

Download and Install
--------------------

To install the last stable version from PyPI::

    $ sudo pip install wsgiserver

To install the development version from GitHub::

    $ git clone https://github.com/fgallaire/wsgiserver
    $ cd wsgi
    $ sudo python setup.py install

Documentation and Caveats
-------------------------

-  WSGIserver support Python 2.6 and above and Python 3.1 and above

-  WSGIserver require six

Usage
-----

Simplest example on how to use WSGIserver::

    import wsgiserver

    def my_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type','text/plain')]
        start_response(status, response_headers)
        return ['WSGIserver is running!']

    server = wsgiserver.WSGIServer(('0.0.0.0', 8070), my_app)
    server.start()

WSGIserver can serve as many WSGI applications as you want in one
instance by using a ``WSGIPathInfoDispatcher``::

    d = wsgiserver.WSGIPathInfoDispatcher({'/': my_app, '/blog': my_blog_app})
    server = wsgiserver.WSGIServer(('0.0.0.0', 80), d)

To add SSL support, just set ``server.ssl_adapter`` to an ``SSLAdapter`` instance::

    server.ssl_adapter = wsgiserver.SSLAdapter('certificate.pem', 'privatekey.pem')

Naming
------

-  *WSGIserver* is the project name

-  *wsgiserver* is the Python module name

-  *WSGIServer* is the main class name

License
-------

WSGIserver files are released under the GNU LGPLv3 or above license.

WSGIserver codebase from CherryPy by CherryPy Team (team@cherrypy.org) under the 3-clause BSD license.
