## Installation instructions

1. Clone the repository to a VM or to your machine you want to run the proxy on.

2. Install nodejs (8+) and npm.

3. Run `npm install` in the folder you checked out.

4. `cp .env.example .env`.

5. Edit the `.env` file and change it to match your config.

6. Run `npm start` or `node server.js`

7. In your miner config switch your remote host and port to point to your local host and port provided in your config. Make sure your local host is set to your public IP or your public host name.

You can run it in a screen instance, or you can install pm2 to run your instance as a daemon.
Note: This can be used for any stratum servers not just eth.

---

## Configuration

| ENV variable | Description | Example Value |
|--|--|--|
| REMOTE_HOST | The remote hostname or IP address of the mining pool you wish to push your shares to. | eth.2miners.com |
| REMOTE_PORT | The remote port of the mining pool you wish to push your shares to. | 2020 |
| REMOTE_PASSWORD | The password of the mining pool you wish to push your shares to. | x |
| LOCAL_HOST | The hostname/IP address of your machine hosting this proxy. Do not use localhost or 127.0.0.1 | 0.0.0.0 |
| LOCAL_PORT | The port to bind to on your machine hosting this proxy. | 2020 |

----

## Windows Users

### How to create a fake WAN Network for Windows

* Run ncpa.cpl
* Right-Click on your network adapter -> Properties
* Select IPv4 (TCP/IPV4) -> Properties
* Set your LAN address in static mode (with mask, gateway and DNS)
* Click on Advanced button
* Click on the add button bellow ip address
* Type some public ip address (like 194.12.12.2) - That real address will be no longer reachable.
* Mask: 255.255.255.255
* You must have ONE gateway (LAN)
* If set some localhost entry in the past, please change it for your new fake WAN ip address
* In our case 127.0.0.1 becomes 194.12.12.2
* You have to change it in the .env file and eventually in your host file.

---

## Linux, Mac OSX

* Use dynamic dns provider and setup routing on your firewall. Or you can set up this proxy on a VPS that is off of your network.

---

## Docker container


To build the docker image: `docker build -t stratum-ethproxy .`

To run the docker image: `docker run -d --name my-stratum-proxy -e "REMOTE_HOST=eth.2miners.com" -e "REMOTE_PORT=2020" -e "REMOTE_PASSWORD=x" -p 2020:2020 stratum-ethproxy`

In the example above you can point your miner to the IP address running the proxy on port 2020.
