1. install python3, virtualenv
```
$ sudo apt update 
$ sudo apt install software-properties-common 
$ sudo add-apt-repository ppa:deadsnakes/ppa   
$ sudo apt-get update   
$ sudo apt install python3.9 python3.9-distutils
```

2. swith to latest python3 installed
```
$ update-alternatives --list python
$ update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
$ update-alternatives --install /usr/bin/python python /usr/bin/python3.9 2

$ python --version
Python 3.9
```

3. install virtualenv
```
$ sudo apt install virtualenv
```

4. install apache2, mod_wsgi
```
$ sudo apt install apache2
$ wget https://github.com/GrahamDumpleton/mod_wsgi/archive/4.7.1.tar.gz
$ tar xvfz 4.7.1.tar.gz

$ which python
$ ./configure --with-python=/usr/bin/python3.9
$ make
$ make install

[download file here](https://github.com/GrahamDumpleton/mod_wsgi/releases)
[mod_wsgi docs](https://modwsgi.readthedocs.io/en/develop/user-guides/quick-installation-guide.html)
```

5. verify the python version (in second line) used by mod_wsgi.so
```
$ cd /usr/lib/apache2/modules
$ ldd mod_wsgi.so
```

6. Create virtualenv and activate, install django latest version
```
$ which python
$ cd /var/wwww
$ virtualenv --python=/usr/bin/python3.9 wtf-venv --always-copy

$ source wtf-venv/bin/activate
$ python -v
PYthon 3.9

$ pip install Django==3.1.2
```

6. Create a demo django project in /var/www location, run using runserver
```
$ cd /var/www
$ source wtf-venv/bin/activate
$ django-admin startproject project

```
