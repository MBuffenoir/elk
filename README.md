# elk
A compose file to quickly setup and ELK stack

Try it out with:

    $ docker-machine create -d virtualbox elk
    $ docker-machine scp -r conf-files/ elk:
    $ eval $(docker-machine env elk)
    $ git clone git@github.com:MBuffenoir/elk.git
    $ cd elk
    $ docker-compose up -d
    $ echo "Hi syslog" | nc -u $(docker-machine ip elk) 5000

# On a cloud machine

Running the compose file on a distant machine will require a copy of the `conf-files` folder on it.
You can use docker-machine for this purpose:

    $ docker-machine scp -r conf-files machine_name:

The file `docker-compose-ubuntu.yml` is an example to be used with an ubuntu machine:

    $ docker-machine -f docker-compose-ubuntu.yml up -d

This compose file should also work without issue on a swarm cluster.

# Create you first index

Once your first data has been sent to logstash, it is then possible to create your first index by logging into kibana.

Naviguate to `https://$(docker-machine ip elk):5601`.

The login is `admin` and the password is `Kibana05` (see the comments at the top of the file `/conf-files/proxy-conf/kibana-nginx.conf` to change those credentials)

Click on the `Create` button to create your first index.

Click on the Discover tab, you should now get access to your logs:

![Kibana](./kibana.png)
