# elk
A compose file to quickly setup and ELK stack

Try it out with:

    $ docker-machine create -d virtualbox elk
    $ eval $(docker-machine env elk)
    $ git clone git@github.com:MBuffenoir/elk.git
    $ cd elk
    $ docker-compose up -d
    $ echo "Hi syslog" | nc -u $(docker-machine ip elk) 5000

# On a cloud machine

Running the compose file on a distant machine will require a copy of the `conf-files` folder on it.
You can use docker-machine for this purpose:

    $ docker-machine scp -r conf-files machine_name:

The file `docker-compose-ubuntu.yml` is an example to be used with an ubuntu machine.
