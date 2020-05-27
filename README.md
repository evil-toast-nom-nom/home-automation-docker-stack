# home-automation-docker-stack

This is a simple docker-compose file and a collection of usefull resources to bootstrap someone wanting to run a home automation stack on a raspberry PI. 
The stack contains:
* [home-assistant](https://www.home-assistant.io/)
* [node-red](https://nodered.org/)
* [mosquitto (mqtt server)](https://mosquitto.org/)

## Getting Started

This will take you through the process of setting this stack up on a fresh raspberry pi.

### Prerequisites

* Terminal emulator like [putty](https://www.putty.org/) so that you can [SSH](https://phoenixnap.com/kb/ssh-to-connect-to-remote-server-linux-or-windows) into the Pi
* Raspberry PI 3 or better
* An internet connection for the Pi

### Installing

#### Preparing the Pi
1. Install Docker on your Pi
```
curl -sSL https://get.docker.com | sh
```

2. Allow the pi user to run docker commands without sudo.
```
sudo usermod -aG docker pi
```

3. Install dependencies for docker-compose
```
sudo apt-get install -y libffi-dev libssl-dev
sudo apt-get install -y python3 python3-pip
```

4. Remove the python-configparser
```
sudo apt-get remove python-configparser
```

5. Install Docker Compose
```
sudo pip3 install docker-compose 
```

#### Deploying the stack

1. Make a new directory 
```
sudo mkdir /var/opt/appstack
sudo cd /var/opt/appstack
```
2. Copy the file: docker-compose to the directory
```
cp /path/to/extracted-repo/docker-compose.yaml /var/opt/appstack
```

3. Run docker-compose to start the stack (This will take a while)
```
docker-compose up -d
```

#### Checking that the containers started up properly
Run the command
```
sudo docker ps -a
```
You should be able to see something like this:
```
CONTAINER ID        IMAGE                                 COMMAND                  CREATED             STATUS                PORTS                              NAMES
a9qw9qnv993n        homeassistant/home-assistant:stable   "/bin/entry.sh pytho…"   6 weeks ago         Up 2 mins                                                home-assistant
300d57354e8d        nodered/node-red                      "npm start -- --user…"   6 weeks ago         Up 4 mins (healthy)   0.0.0.0:1880->1880/tcp             node-red
e656331951a3        eclipse-mosquitto                     "/docker-entrypoint.…"   6 weeks ago         Up 6 mins             0.0.0.0:1883->1883/tcp             mosquitto
```




## Contributing

Feel free to submit a request.


## Acknowledgments

* Thanks to [Rohan Sawant](https://dev.to/rohansawant) for his [guide](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl) on setting up docker & docker-compose on a Pi.
