1. install python3, virtualenv
```
$ sudo apt update 
$ sudo apt install software-properties-common 
$ sudo add-apt-repository ppa:deadsnakes/ppa   
$ sudo apt-get update   
$ sudo apt install python3.9 
```

2. swith to latest python3 installed
```
$ update-alternatives --list python
$ update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
$ update-alternatives --install /usr/bin/python python /usr/bin/python3.9 2

$ python --version
Python 3.9
```

3. install virtualenv, create one, activate
```
$ sudo apt install virtualenv
$ virtualenv --python=/usr/bin/python3.9 venv_name --always-copy

$ source venv_name/bin/activate
$ python -v
PYthon 3.9
```

