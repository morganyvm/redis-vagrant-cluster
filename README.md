Vagrant Setup for testing Redis
==============================

When developing a client its important to have a consistent and easy test environment.

Initially these scripts will be tailored for the java jedis client but I hope it can be used for other clients and 
others testing redis integration in the future.

* Sets up two nodes, and forwards ports to 6379 and 6380.
* Both nodes are configured with password "foobared".
