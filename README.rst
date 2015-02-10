
=======================================
aiouv: a PEP-3156 compatible event loop
=======================================


Overview
========

`PEP-3156 <http://www.python.org/dev/peps/pep-3156/>`_ is a proposal for asynchronous I/O in Python,
starting with Python 3.3. The reference implementation is codenamed Tulip and can be found
`here <https://code.google.com/p/tulip/>`_. It will be part of the standard library in 3.4 and also
available in PyPI under the name **asyncio**.

aiouv is an event loop implementation for asincio based on `pyuv <https://github.com/saghul/pyuv>`_.


Installation
============

aiouv depends on asyncio >= 0.4.1 and pyuv >= 1.0.

You can install them by doing::

    pip install -U asyncio pyuv


**NOTE:** Currently aiouv might be a bit behind asyncio, if an API changed aiouv might not be updated yet.
I hope to resume development soon and make a release on PyPI. Pull requests are of course welcome :-)


Extra API functions
===================

aiouv provides a few functions to create TCP, and UDP connections as well as cross
platform named pipes support.

listen_tcp(loop, protocol_factory, addr)
----------------------------------------

Creates a TCP server listening in the specified address (IP / port tuple). On new
connections a new `TCPTransport` will be created and a protocol will be created using
the supplied factory.

Returns the listening handle.

connect_tcp(loop, protocol_factory, addr, bindaddr=None)
--------------------------------------------------------

Create a TCP connection to the specified address. If bindaddr is specified, the local
address is bound to it.

Returns a tuple with the created transport and protocol.

listen_pipe(loop, protocol_factory, name)
----------------------------------------

Creates a Pipe server listening in the specified pipe name. On new
connections a new `PipeTransport` will be created and a protocol will be created using
the supplied factory.

Returns the listening handle.

connect_pipe(loop, protocol_factory, name)
------------------------------------------

Create a Pipe connection to the specified pipe name.

Returns a tuple with the created transport and protocol.

create_udp_endpoint(loop, protocol_factory, local_addr=None, remote_addr=None)
------------------------------------------------------------------------------

Created a UDP endpoint. If local_addr is specified, the local interface will be bound
to it. If remote_addr is specified, the remote target is set and it doesn't need
to be specified when calling sendto().

Returns a tuple with the created transport and protocol.


Running the test suite
======================

From the toplevel directory, run:

::

    hg clone https://code.google.com/p/tulip/ asyncio
    export PYTHONPATH=asyncio/
    python runtests.py -v aiouv_events_test

