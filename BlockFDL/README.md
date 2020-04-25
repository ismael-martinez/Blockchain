# Hyperledger Fabric - REST API

Install the prerequisites and begin running Fabric.

## Getting Started

Hyperledger Fabric requires either a MacOS or a Linux OS to develop and run. These instructions are for Linux. 
If you are using Windows, follow the tutorial [here](https://medium.com/cochain/hyperledger-fabric-on-windows-10-26723116c636), though this should be done on a UNIX system.

### Prerequisites

Download all prerequisites with the following.

```
curl -O https://hyperledger.github.io/composer/latest/prereqs-ubuntu.sh

chmod u+x prereqs-ubuntu.sh
```

Execute and install the prerequisites.

```
./prereqs-ubuntu.sh
```
Close the command line and reopen before continuing. Once reopened, ensure you have `npm`, `node`, and `docker` installed with `npm --version`, `node --version` and `docker --version`.

For more details, visit [Hyperledger - Installing Prereqs](https://hyperledger.github.io/composer/v0.16/installing/installing-prereqs.html).



### Installing CLI Tools

Next, we install our CLI tools that are needed to start up Fabric.

```
npm install -g composer-cli
npm install -g composer-rest-server
npm install -g generator-hyperledger-composer
```
For more details visit [Hyperledger - CLI](https://hyperledger.github.io/composer/v0.16/installing/development-tools.html).

## Install Hyperledger Fabric

cd `<path_to_projectDir>/HyperledgerComposer`

We now download and start Fabric.

```
export FABRIC_VERSION=hlfv12
cd <path_to_projectDir>/HyperledgerComposer/fabric-dev-servers
./downloadFabric.sh
./startFabric.sh
./createPeerAdminCard.sh
```

If `./downloadFabric.sh` gives you a 'Permissioned Denied' error, use `sudo` prior to the command.

IBM has a great tutorial on this [here](https://developer.ibm.com/tutorials/cl-deploy-interact-extend-local-blockchain-network-with-hyperledger-composer/).

### Executing the .bna file into a REST API

We are holding our `blockchain-federated-learning.bna` file in the `HyperledgerComposer\BlockFDL` directory.

`cd <path_to_projectDir>/HyperledgerComposer/BlockDFL`

Run the network and launch the REST API with the following.

```
composer network install --card PeerAdmin@hlfv1 --archiveFile blockchain-federated-learning.bna
composer network start --networkName blockchain-federated-learning --networkVersion 0.0.2-deploy.44 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card

composer-rest-server -c admin@blockchain-federated-learning -n always -u true -w true
```


### REST API
The REST API explorer should now be viewable in the browser at `http://localhost:3000/explorer`. Use this to integrate the REST API into your code and see the effects on the network.
