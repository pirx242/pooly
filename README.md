#### POOLY - A POUNDCTL WRAPPER WITH PRETTY FORMATTING

_pooly_ is a simple Python script that provides a more user friendly interface to Pound (than poundctl).
Actually though, it's a wrapper around poundctl.

The focus for pooly is to handle _pools_ (a service that contains more than one backend) of backends.
For instance if you have backends that exist in more than one pool, and you want to disable that particular
backend in all pools, pooly will do this easily for you.
The reason for this is that disabling backends in services that only contain that single backend makes
less sense, because that essentially disables the whole listener, and then you might just as well just
shut down the backend.
(NOTE: i havent looked in to how this works with emergency backends though)

This wrapper script also does some sanity checking for you. It will not disable a backend in a service
if that is the last enabled backend, unless -f is used.

To provide you with more secure info about the health of backends, it does its own checking of backend
health (a simple tcp connect). A backend that answers a connect will here be known as _alive_.

#### EXAMPLES

Lets assume that you have two Listeners: mydomain:80, mydomain:443
In each listener you have a pool with the same two backends: backend1, backend2
Additionally, in mydomain:443 you have a special service that filters on some url pattern, and that service only contains backend2.

This will disable backend1 in both services that contain both backends.
```$ sudo pooly -d backend1```

This will disable backend2 in both services that contain both backends, but *not* in that third special service.
```
$ sudo pooly -d backend2
```

This will disable backend2 in all three services.
```
$ sudo pooly -f -d backend2
```

This will disable backend2 in only the pool that is in the Listener that listens on port 80.
```
$ sudo pooly -L mydomain:80 -d backend2
```

This will disable the whole ListenHTTPS listener.
$ sudo pooly -D mydomain:443

This will print all your listeners and pools.
$ sudo pooly

This will print all your listeners and services, even those with just one single backend in them.
$ sudo pooly -s


#### Lastly...

Feature requests are *encouraged*.
