# To up and running the ubuntu in vagrant in windows host for isolated development.
To connect to the vagrant postgresql server from the host windows pgAdmin 4

------------------------------------------------------------------

steps:

1. installations:

     dowload these executable files and install on windows host machine.
    `vagrant`
    `virtualbox`
    `pgadmin4`

#### use gitbash
2.initialize, up and run the vagrant server

    google for [vagrant boxes](https://app.vagrantup.com/boxes/search) and select one
    
    To install ubuntu 118 (bionic) 
    $ vagrant init ubuntu/bionic64
    $ vagrant up
    
    To connect to vagrant server:
     $ vagrant shh
     
Now we can check the new vm is up and running on host machine using virtualbox

Now disconnet and Edit the Vagrant file:

Vagrant file configurations steps:

     1.vm.box
        config.vm.box = "ubuntu/xenial64"
     2.port forwad mapping: allows specific port on host machine via 127.0.0.1 to disable the public access
          config.vm.network "forwarded_port", host_ip: "127.0.0.1", guest: 8080, host: 8080
          config.vm.network "forwarded_port", guest: 5432, host: 65431
  
    3.private network creation using specifc ip(guest ip): to allow host-only access to the machine 
        config.vm.network "private_network", ip: "192.168.33.10"          #This is the vagrant(host) ip
        
    4.enable provisioning with shell script: 
          
          To update and upgreade ubuntu
          To install the python, virtualenvwrapper  and python-pip
          To view the vagrant server details and project home
          
          ```
            config.vm.provision "shell", inline: <<-SHELL
            # Update and upgrade the server packages.
            sudo apt-get update
            sudo apt-get -y upgrade
            # Set Ubuntu Language
            sudo locale-gen en_GB.UTF-8
            # Install Python, SQLite and pip
            sudo apt-get install -y python3-dev sqlite python3-pip
            # Upgrade pip to the latest version.
            sudo pip install --upgrade pip
            # Install and configure python virtualenvwrapper.
            sudo pip install virtualenvwrapper
            if ! grep -q VIRTUALENV_ALREADY_ADDED /home/vagrant/.bashrc; then
                echo "# VIRTUALENV_ALREADY_ADDED" >> /home/vagrant/.bashrc
                echo "WORKON_HOME=~/.virtualenvs" >> /home/vagrant/.bashrc
                echo "PROJECT_HOME=/vagrant" >> /home/vagrant/.bashrc
                echo "source /usr/local/bin/virtualenvwrapper.sh" >> /home/vagrant/.bashrc
            fi
        SHELL
        ```
        
Now reload the vagrant:

     install the vagrant-reload plugin using
     $ vagrant plugin install vagrant-reload
     
     then
    $ vagrant reload

Now Vagrant server will be booted up with the modifications in Vagrantfile

---------------------------------------------------------------------------------

#### postgresql setup

1. connect to vagrant server 

        $ vagrant up
        $ vagrant ssh
    
2. postgresql db server setup, db user, db_name, db_password setup

      [PostgreSQL with Django app](https://postimg.cc/zbdnfDsp)
      
          $ sudo apt-get update
          $ sudo apt-get install postgresql postgresql-contrib
      
      To create a new database and database user to manage the database:
      
          $ sudo adduser postgres_user
      
      Log into the default PostgreSQL user (called "postgres") to create a database and assign it to the new user:
      
          $ sudo -su postgres
          $ psql
      
      Now you are in PostgreSQL command prompt
      
      ## Database creation with new user
      
      Create a new user that matches the system user you created.
      
      create a database managed by that user:
      
      ```
      $ sudo -su postgres
      $ psql
      
      $ CREATE DATABASE db_name;
      $ CREATE USER db_user WITH ENCRYPTED PASSWORD 'db_user_pass';
      $ GRANT ALL PRIVILEGES ON DATABASE db_name TO db_user;
      
      $ \l
      ```
      
 ![spsa_db_creation](https://user-images.githubusercontent.com/29883334/91632277-7066bb80-e9fd-11ea-920d-abb496dddd85.PNG)
     
    
      To exit out of interface
      $ \q
      
      Exit out of the default "postgres" user account and log into the user you created with the following 
      $ exit
      $ sudo su - postgres_user | sudo su postgres_user
      
      Sign into the database you created 
      $ psql my_postgres_db
      
      Now you are connected to the new database you've just created.
      To list all databases:
      $ \l
      
 Now we've the new database with db_user_name and db_user_password credentials
 So we can view and manage this data base using pgAdmin4 GUI tool from local windows host.
 
### Python version: 3.9 @Date: 20/10/2020

    ```
    $ sudo add-apt-repository ppa:deadsnakes/ppa
    $ sudo apt update
    $ sudo apt install python3.9
    
    $ python --version
    
    Note: To make 3.9 as default
     $ which python
     $ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.8 1
     $ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 2
    ```

  To create virtualenv and activate:
  
      To create virtualenv
      ```
      $ sudo apt install python3-pip
      $ sudo apt install virtualenv | sudo pip install virtualenv
      $ virtualenv --python=/usr/bin/python3.9 venv_name --always-copy
      ```
      
      Install psycopg2: To allow to use the database configured
      ```
      $ sudo apt-get install python3-psycopg2
      ```
      
      To activate:
      ```
      $ source venv_name/bin/activate
      ```
      
      install django3:
      ```
      $ pip install Django==3.1.2
      $ pip freeze > requirements.txt
      ```
      
 To list all virtualenvs: `lsvirtualenv -b`
      
 Create Django project, configure the postgres db to our project:
 
 ```
 django-admin startproject project_name
 ```
 
 in settings.py:
 
 ```
 DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'myproject',
        'USER': 'myprojectuser',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

ex:
[![postgres-db-creds.png](https://i.postimg.cc/k4bmyNKp/postgres-db-creds.png)](https://postimg.cc/1ns2mqWG)

Start the dev server in vagrant:
```
python manage.py runserver 0.0.0.0:8080   (port forwording from vagrant server)
```

To access the app:
`127.0.0.0:8080` in the browser

Create an app and register with settings:
```
python mange.py startapp 'app_name'
```

Register with settings:

Create a model and migate to db:
[link](https://www.digitalocean.com/community/tutorials/how-to-create-django-models)


Go to shell and check whether able to access the table:
```
python manage.py shell
```

import table from app.models and verify:

After confirm, configure in vagrant to access from host
### Configure Postgres
Update **pg_hba.conf** (most likely in /etc/postgresql/9.4/main) with -
`host all all 0.0.0.0/0 trust`

Update **postgresql.conf** to use `listen_addresses = '*'`

Be sure to `$ sudo service postgresql restart`

### Configure Vagrant
Add `config.vm.network :forwarded_port, host: 5432, guest: 5432` to the **Vagrant.configure block in your Vagrantfile**.

### Test your connection
Attempt to connect from your host using psql -h localhost -U vagrant

Now use GUI (pgAdmin):

Click New Server and give connection details. That's it.

[![pg-Admin4-vagrant-postgres.png](https://i.postimg.cc/Njc52Fqt/pg-Admin4-vagrant-postgres.png)](https://postimg.cc/F7T929HC)




Forgot sudo password:

```
$ sudo passwd ubuntu
```











