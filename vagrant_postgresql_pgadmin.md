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
    
    To install ubuntu 16 (xenial) 
    $ vagrant init ubuntu/xenial64
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
            sudo apt-get install -y python3-dev sqlite python-pip
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

      [PostgreSQL with Django app](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-14-04)
      
      $ sudo apt-get update
      $ ssudo apt-get install postgresql postgresql-contrib
      
      To create a new database and database user to manage the database:
      $ sudo adduser postgres_user
      
      Log into the default PostgreSQL user (called "postgres") to create a database and assign it to the new user:
      $ sudo su - postgres
      $ psql
      
      Now you are in PostgreSQL command prompt
      
      Create a new user that matches the system user you created.
      Then create a database managed by that user:
      $ CREATE USER postgres_user WITH PASSWORD 'password';
      $ CREATE DATABASE my_postgres_db OWNER postgres_user;
      
      ```
      ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
      ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';
      ALTER ROLE myprojectuser SET timezone TO 'UTC';
      ```
      
      ```
      GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;
      ```
      
      To exit out of interface
      $ \q
      
      Exit out of the default "postgres" user account and log into the user you created with the following 
      $ exit
      $ sudo su - postgres_user
      
      Sign into the database you created 
      $ psql my_postgres_db
      
      Now you are connected to the new database you've just created.
      To list all databases:
      $ \l
      
 Now we've the new database with db_user_name and db_user_password credentials
 So we can view and manage this data base using pgAdmin4 GUI tool from local windows host.
 
 To connect to vagrant's postgres and manage databases from local machine:
 
 1.vagrant configurations:
 
      first connect to vagrant server
      ```
      $ vagrant up
      $ vagrant ssh
      ```
      
      edit the file `/etc/postgresql/9.4/main/pg_hba.conf` and add the below line
      ```
      host all all 0.0.0.0/0 md5
      ```
          
      edit the file `postgresql.conf`
      ```
      listen_addresses = '*'            #uncomment this
      ```
      
      Restrart the postgresql server to reflect the modification in config files
      ```
      $ sudo service postgresql restart
      ```
      
To use pgAdmin 4 to inspect database on a Vagrant vm:


   [Vagrant, PostgreSQL, pgAdmin 4](https://snakeycode.wordpress.com/2015/01/02/vagrant-postgresql-and-pgadmin/)
       
   [alternative](https://gielberkers.com/how-to-connect-to-mysql-in-vagrant-from-your-host-machine/)
    
       Vagrant already has SSH setup 
       so we can connect to the database is using pgAdmin's SSH tunneling feature(secured)
       
       To do:
       `click create new server` and fill these
       
       Name: 'any name of your choice(eg: Vagrant)
       Host: 'localhost'      #not the vagrant ip address
       Username: 'database_username`
       Password: 'database_password/db_user_password'
       
       DO NOT CLICK OK & TRY TO CONNECT. THIS IS NOT OVER YET.
       
       Click the SSH Tunnel tab:
       
       Tunnel host: 'ip address of the Vagrant VM'
       Username: 'Linux username when we used when you use SSH to the vm'     # generally vagrant user
       Identify file: 'SSH private key for this virtual machine`
       
       when you run `vagrant up` it creates a .vagrant folder.
       The private key file path:
       ```~/my_project/.vagrant/machines/default/virtualbox/private_key```
       
       Then click ok. we're done
       
       Now we can see the database of Vagrant vm in our local windows machine's pgAdmin 4.
       


  To create virtualenv and activate:
  
      To install virtualenv
      ```
      $ sudo pip install virtualenv
      ```
      
      To create virtualenv
      ```
      virtualenv venv_name
      ```
      
      To activate:
      ```
      source venv_name/bin/activate
      ```
      
      Install psycopg2: To allow to use the database configured
      ```
      pip install django psycopg2
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


Forgot sudo password:

```
$ sudo passwd ubuntu
```










