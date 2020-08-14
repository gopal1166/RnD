To install Python new version:
```
sudo add-apt-repository ppa:deadsnakes/ppa   
sudo apt-get update   
sudo apt install python3.7 
```

To switch python versions system wide:

Default is 2.7, need to change the default to 3.4
`$ python --version`

```
$ update-alternatives --list python
update-alternatives: error: no alternatives for python
```

Now we need to alternatives

```
$ update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
update-alternatives: using /usr/bin/python2.7 to provide /usr/bin/python (python) in auto mode

$ update-alternatives --install /usr/bin/python python /usr/bin/python3.4 2
update-alternatives: using /usr/bin/python3.4 to provide /usr/bin/python (python) in auto mode
```

@ highest number will be default version i.e 2
