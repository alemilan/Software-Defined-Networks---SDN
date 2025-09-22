This tutorial describes ONOS 2.6.0 building and configuration for work with mininet and suport onos-apps-creation.<br/>
For user convenience, would be good (but maybe not so secure) to allow the admin user to performe some sudo commands without providing password every time. For this, follow these steps:


```sheel
sudo visudo
```


add at the end of the file:
```
<username> ALL=(ALL) NOPASSWD:ALL
```

Considering a fresh Ubuntu 20.04 host, follow these steps to update Ubuntu packages:

```sheel
sudo apt-get update
sudo apt-get upgrade
```
This tutorial follows ONOS installation throught Bazelisk. Firstly, install the required dependencies as described in [ONOS wiki](https://wiki.onosproject.org/display/ONOS/Installing+required+tools):

```
sudo apt install python
sudo apt install python3
sudo apt install python3-pip python3-dev python3-setuptools
pip3 install --upgrade pip
pip3 install selenium

#installing git requirements

sudo apt-get install git
sudo apt-get install git-review
```


Donwload and install bazelisk throught Bazel:


```
wget https://github.com/bazelbuild/bazelisk/releases/download/v1.18.0/bazelisk-linux-amd64
chmod +x bazelisk-linux-amd64
sudo mv bazelisk-linux-amd64 /usr/local/bin/bazel
bazel --version
```

Following line clones onos gerrit project but may be insecure, even though it is a workaround to 'server certificate verification failed. CAfile: none CRLfile: none'.


```
git -c http.sslVerify=false clone https://gerrit.onosproject.org/onos
```

Than, enter in ONOS directory and use bazel do build onos:


```
cd onos
bazel build onos
```

Run ONOS locally with the following command (it will take a while):


```
bazel run onos-local -- clean debug
```


Export the environment variables into .bashrc file as follows:


```
sudo nano ~/.bashrc
```

At the end of the file add:


```
export ONOS_ROOT=$HOME/onos/
source $ONOS_ROOT/tools/dev/bash_profile
```


Source the .bashrc file with:


```
source ~/.bashrc
```
