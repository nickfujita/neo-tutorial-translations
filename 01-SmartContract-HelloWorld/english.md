# NEO Smart Contracts Tutorial: helloWorld

This is a tutorial on creating, deploying, and running your first smart contract on NEO.

If you have not already set up your dev environment with a private neo net in a docker container with gas, please first run though that tutorial before proceeding.

Quick Setup: NEO Private Net

## Start docker container
If you already have your docker instance up and running in your terminal, please skip this step.

Check to see if your neo privnet docker container is running
```
docker ps
```

If the container is not running


but you have already created it. Check for the container id, and start the container.
```
docker ps -a
```

Copy the CONTAINER ID and run
```
docker start CONTAINER_ID
```

SSH into the docker container
```
docker exec -it neo-privatenet /bin/bash
```

## Writing your first smart contract
Open your favorite text editor
Create a new file, and save it to the directory that you created in the setup tutorial (in the step marked as “very important”). This is the folder that is shared with the docker image. So it allows you to access files on your host computer from within the docker container.
In this file we will create a very simple function that logs a string and returns a boolean
```
def Main():
  print("hello world");
  return True
```

This code can also be found here.

Save the file

## Compile the python smart contract file
Back in your terminal loaded with your docker container SSH session, assuming you are still in the neo-python directory, open the neo cli
```
python3 prompt.py -p
```

or
```
neopy
```

Run the compile command
```
build smartContracts/helloWorld.py
```

NOTE: This also assumes that you created your shared folder with the name smartContracts as stated in the setup tutorial. If not, please change the folder name to the name that you designated.

You should now have a compiled helloWorld.avm in your smartContracts folder as indicated in the success confirmation message.

## Importing the contract
Open your wallet with NEO/GAS
```
open wallet neo-privnet.wallet
```

Enter wallet password
```
coz
```

Import the smart contract with the following command
```
import contract CONTRACT_FILE INPUT_TYPES OUTPUT_TYPES NEEDS_STORAGE NEEDS_DYNAMIC_INVOKE
```

I will go over these options in a later post, but for the time being, our command should look similar to the following

```
import contract ./smartContracts/helloWorld.avm "" 01 False False
```

You will then be prompted to fill out details about this contract. For the time being just enter a name, and leave the rest blank.


Enter the wallet password `coz` to confirm deployment of this contract, and wait for a feedback message indicating a successful deployment.


## Invoking the contract
Confirm the contract is deployed
```
contract search CONTRACT_NAME
```

In our case
```
contract search helloWorld
```

Copy the contract hash value. In this case it’s a89e1bc8437cfce24a523829a71a35d73fc18bb2, but will be different in your case.

Run a testinvoke on the contract
```
testinvoke CONTRACT_HASH
```

As you can see the test invoke was successful, and there is a log with our string “hello world”, and a result of “1” (which equates to True)

Hit return instead of entering the wallet password, as doing so will actually run the contract and post the transaction to the neo blockchain.

Congrats! You have written, deployed, and run your very first smart contract with NEO!
