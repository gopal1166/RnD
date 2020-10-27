1. install python3, virtualenv
```
$ sudo apt update 
$ sudo apt install software-properties-common 
$ sudo add-apt-repository ppa:deadsnakes/ppa   
$ sudo apt-get update   
$ sudo apt install python3.9 python3.9-distutils
```

. swith to latest python3 installed
```
$ update-alternatives --list python
$ update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
$ update-alternatives --install /usr/bin/python python /usr/bin/python3.9 2

$ python --version
Python 3.9
```

. install virtualenv
```
$ sudo apt install virtualenv
```

. Create virtualenv and activate, install django latest version
```
$ which python
$ cd /var/wwww
$ virtualenv --python=/usr/bin/python3.9 wtf-venv --always-copy

$ source wtf-venv/bin/activate
$ python -v
PYthon 3.9

$ pip install Django==3.1.2
```

. Create a demo django project in /var/www location, run using runserver
```
$ cd /var/www
$ source wtf-venv/bin/activate
$ django-admin startproject project
$ python manage.py runserver 0.0.0.0:8080

Now access the app in browser using server ip:8080 
```

. install apache2, mod_wsgi
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

. verify the python version (in second line) used by mod_wsgi.so
```
$ cd /usr/lib/apache2/modules
$ ldd mod_wsgi.so
```

. configure django app with apache web server in /etc/apache2/apache2.conf  or /etc/apache2/sites-available/000-default.conf
```
<VirtualHost *:80>

	ServerAdmin webmaster@localhost
  ServerName whathefun.in
    
  # DocumentRoot is project root folder
	DocumentRoot /var/www/project

  # create a folder, and map to this. error.log automatically created
	ErrorLog /var/www/wtf-logs/error.log
	CustomLog /var/www/wtf-logs/access.log combine

  # To access the static files
	alias /static /var/www/project/static
	<Directory /var/www/project/static>
		Require all granted
	</Directory>

  # wsgi file location accessing
	<Directory /var/www/project/project>
		<Files wsgi.py>
			Require all granted
		</Files>
	</Directory>

  # python-path: project root where manage.py exists
  # python-home: path to virtualenvironment created
  # tutorial is just a process name, should be same
	WSGIDaemonProcess tutorial python-path=/var/www/project python-home=/var/www/wtf-venv
	WSGIProcessGroup tutorial
	WSGIScriptAlias / /var/www/project/project/wsgi.py	

</VirtualHost>
```
