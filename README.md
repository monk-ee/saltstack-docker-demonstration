# SaltStack Master-Minion Environment for the time poor and curious

Just a repository to help you have a play with [Saltstack]( https://github.com/saltstack). 
I could not find an easy way to do this off the shelf.

With some little effort you can standup a saltstack master ( with [SaltGUI](https://github.com/erwindon/SaltGUI) ) and a minion.
For bonus points the master is a minion too!

## Assumptions

+ A reasonably modern docker environment
+ docker-compose is installed

## Build Images locally

    docker build --tag salt-master:latest -f Docker.master
    docker build --tag salt-minion:latest -f Docker.minion
    
## Docker compose up

    docker-compose up
    
## Sign keys and get saltstack usable ( login to gui)
Exec onto master and accept keys from minions ( the master is a minion too)

    docker exec -it salt-master /bin/bash
    salt-key -A ( say Y)

Open a browser and go to GUI; login details saltuser:saltuser

    https://localhost:8000/
    
## Enjoy

    go eat cheeseburgers, your work here is done
    
## Caveats

+ Careful consideration for PKI directory will needed to ensure you dont lose all the keys on termination or respawn
+ external cache is good - I tried the postgres one - and it tasted good
+ BEWARE - self signed certs for fun and profit
+ salt-gui MUST run on salt-master - don't ask
+ didn't bother with pillars or custom grains; but you could care about that
+ this is a linux only test - best of debians
+ don't go below this version 3000.3 - due to horrible security hole
