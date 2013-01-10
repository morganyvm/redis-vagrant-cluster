Vagrant Setup for testing Redis
==============================

When developing a client its important to have a consistent and easy test environment.

Initially these scripts will be tailored for the java jedis client but I hope it can be used for other clients and 
others testing redis integration in the future.

* Sets up two nodes, and forwards ports to 6379 and 6380.
* Both nodes are configured with password "foobared".

How to Use
==============

To start up the servers simply run:

```
vagrant up
```

It will take a few minutes the first time to download the base image but after that it will be fast to start up a new server.

To stop the server use the following:

```
vagrant destory
```
