#### POOLY - A POUNDCTL WRAPPER WITH PRETTY FORMATTING

_pooly_ is a simple Python script that provides a more user friendly interface to Pound (than poundctl).
Actually though, it's a wrapper around poundctl.

The focus for pooly is to handle _pools_ (a service that contains more than one backend) of backends.
For instance if you have backends that exist in more than one pool, and you want to disable that particular
backend in all pools, pooly will do this easily for you.

This wrapper script also does some sanity checking for you. It will not disable a backend in a service
if that is the last enabled backend, unless -f is used.

To provide you with more secure info about the health of backends, it does its own checking of backend
health (a simple tcp connect). A backend that answers a connect will here be known as _alive_.

## TEST

#### Lastly...

Feature requests are *encouraged*.
