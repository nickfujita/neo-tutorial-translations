# NEO Dev Environment Setup Tutorial

This is a quick tutorial on starting up a NEO private net on either PC, Mac, or Linux with Docker and neo-python v0.5.3 (python v3.6), without locally installing python.

## Install Docker
Mac OSX
Windows PC
Other

## Create folder for smart contract code
Open a terminal:


*Very important*: Navigate to, or create a folder to hold your smart contract code. We will be linking this folder to be shared with the docker container, so that you can access your smart contract files from within the container.

For example:


## Start the docker container
We will be using neo-privatenet. It contains the neo private net instance with the NEO/GAS already in a wallet.

Run the command:
```
docker run -d --name neo-privatenet -p 20333-20336:20333-20336/tcp -p 30333-30336:30333-30336/tcp -v "$(pwd)":/neo-python/smartContracts cityofzion/neo-privatenet
```

Check to make sure the container is running:
```
docker ps
```

## Connect to NEO docker container

SSH into the docker container by running:
```
docker exec -it neo-privatenet /bin/bash
You should now be in the neo-python directory within the docker image, and should see the smartContracts folder. It is linked to the local directory on your host machine.
```

The pre-made wallet should also be present: neo-privnet.wallet

Jack into the neo-python prompt using either the full command.

```
python3 prompt.py -p
```

Or there is already a bash script shortcut:

```
neopy
```

You should now be in the neo command line prompt. This will be where you interact with your neo private net.

Open the pre-made wallet
```
open wallet neo-privnet.wallet
```

Enter the wallet password
```
coz
```

Rebuild the wallet
```
wallet rebuild
```

Check the wallet balance
```
wallet
```

The wallet should have the 100m NEO and ~16k GAS

Congrats! You are now officially set up, and have taken the first step on your way to start writing your own dapps and smart contracts!
