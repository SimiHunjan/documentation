# Virtual Environment Set-up

Enables developers to run the HCS Hyperledger Fabric sample network using a virtual environment set-up.

## Requirements

* [Hedera testnet](https://docs.hedera.com/guides/testnet/testnet-access) account ID and account private key
* [fabric-hcs repository](https://github.com/hashgraph/fabric-hcs/tree/hcs-dev) 
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [Virtual Box](https://www.virtualbox.org/wiki/Downloads)
* Terminal/IDE

## 1. Open your terminal/IDE and CD to where you would like to clone the fabric-hcs project

* Clone the repository and rename the project folder to "fabric"

```text
git clone https://github.com/hashgraph/fabric-hcs.git fabric
cd fabric
```

* You should now be in the fabric project folder

## 2. Switch to the hcs-dev branch

```text
git checkout hcs-dev
git branch
```

## 3. Navigate to the vagrant folder and start your virtual machine

```text
cd vagrant
vagrant up
vagrant ssh
```

* You should now be back in the fabric folder



Now you have your virtual envrionment ready to go. Please refer to step two Build Fabric Binaries and Docker Images in the master tutorial to continue.

{% page-ref page="./" %}

