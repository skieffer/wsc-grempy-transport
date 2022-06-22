This package helps you use [gremlinpython](https://pypi.org/project/gremlinpython/),
when you can't use `asyncio`.


## Problem

In some settings, e.g. an [eventlet](https://pypi.org/project/eventlet/)
web server with monkey patching, you may run into errors if you try to run code
that relies on Python's `asyncio` framework.
(Demonstration [here](https://github.com/skieffer/grempy-monkey-patch-issue-demo).)

If you want to use `gremlinpython` in such a setting, then you need an
alternative to the built-in `AiohttpTransport` class.


## Solution

This package provides the `WebsocketClientTransport` class. It relies on the popular
[websocket-client](https://pypi.org/project/websocket-client/) package,
which runs without `asyncio`.


## Usage

```python
from gremlin_python.driver.driver_remote_connection import DriverRemoteConnection
from wsc_grempy_transport.transport import websocket_client_transport_factory

remote = DriverRemoteConnection(
    'ws://localhost:8182/gremlin',
    transport_factory=websocket_client_transport_factory)
```


## Development

The `WebsocketClientTransport` class is very rudimentary. It is essentially
just a wrapper for the `websocket.WebSocket` class, and could probably benefit
from some error checking to make it more robust.

Contributions are welcome!
