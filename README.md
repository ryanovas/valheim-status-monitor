# Valheim Status Monitor
vhstatus provides a status page for a dedicated [Valheim](http://valheimgame.com) server.
It shows a list of online and offline players. To run it you'll need [Node.js](https://nodejs.org/en/) and access to the server log file.

I found this repo looking for a simple status page to attach to my simple running Valheim server. I love how simple it is, but I want it to do more so I forked it with the intention to make the following upgrades:

- introduce sqllite so everyone sees the same user list
- convert the config.js to env vars
- add an optional name map so we can see our own names next to our character names
- add a Discord integration to post updates in our server
- add more things to catch in the logs, like raid events starting
- enhance the UI
- host a public docker image so you don't need to build to run it
- enhance the readme to make it easier to install
- probably more once I get into it (maybe gamedig one day idk)

## To install and run

Copy and edit `config.json.example` to `config.json` with your server name, path to server log and optional update frequency and port.


```
cp config.json.example config.json
vi config.json
npm install
npm run start
```

Now access the status page on, e.g., http://localhost:3000

## Docker Instructions
```
docker build -t vhstatus .
docker run -d -p 3000:3000 -v $(pwd)/logs/:/usr/src/app/logs/ vhstatus
```

## Rsync server.log
Use SSH Keys to rsync without password
```
ssh-keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub steam@valheim

rsync -a steam@valheim:/opt/valheim/server.log /opt/vhstatus/logs/server.log
```
