# BipHelp
Community Help Desk, Help for the community by the community.

Setup for developers (Unix)
---------------------------

1. Make sure you have installed Python 3.6, [pip3](https://pip.pypa.io/en/latest/) and [virtualenv](http://www.virtualenv.org/en/latest/).
1. If working behind a proxy, make sure your environment variables are properly set up. If
   you still get an error due to proxy, use "-E" flag along with "sudo" to export all the
   environment variables.
1. Make sure you have python3-dev installed on your operating system. For Debian, you would additionally require libpq-dev.
   Install by using `sudo apt-get install libpq-dev python3-dev` and `python3-dev` + `MySQL` headers using `sudo apt-get install python3-dev libmysqlclient-dev`
1. Make sure you have [MySQL](https://www.mysql.com/) installed. For a tutorial on installing
   MySQL see, [Digital Ocean's Configuring MySQL on Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-16-04) and 
   [How to create Django and connect it to MySQl](https://www.digitalocean.com/community/tutorials/how-to-create-a-django-app-and-connect-it-to-a-database) for more detail.
1. Clone the repo - `git clone https://github.com/BipHelp/BipHelp.git`  and cd into
  the `BipHelp` directory. If working behind a proxy, follow the instructions [here](https://cms-sw.github.io/tutorial-proxy.html).
1. Create a virtual environment (preferably outside project folder) with Python 3 and install dependencies:

     ```bash
     $ virtualenv -p python3.6 venv 
     $ source venv/bin/activate
     $ pip install -r requirements/dev.txt
     ```
1. Create `biphelpdb` database, where `biphelpdb` might be any suitable name.
    ```
    $ mysql -u 'root or whatever your username is' -p 
    $ CREATE USER '<username>'@'localhost' IDENTIFIED BY '<password>';
    $ CREATE DATABASE biphelpdb;
    $ GRANT ALL PRIVILEGES ON DATABASE biphelpdb to <password>;
    ```
1. Update the database details in `BipHelp/BipHelp/database.cnf`.
1. Run `export SECRET_KEY=foobarbaz` in your terminal, ideally the secret key
  should be 40 characters long, unique and unpredictable. Optionally to set the
  shell variable every time you activate the virtualenv, edit `venv/bin/activate`
  and add to the bottom the export statement.
1. Run `python manage.py migrate`.
1. Run `python manage.py createsuperuser` to create a superuser for the admin panel.
  Fill in the details asked.
1. Run `python manage.py runserver` to start the development server. When in testing
  or production, feed the respective settings file from the command line, e.g. for
  testing `python manage.py runserver --settings=BipHelp.settings`.
1. Before commiting run `flake8 BipHelp` and fix PEP8 warnings.
1. Run `python manage.py test --settings=BipHelp.testing`
  to run all the tests.


If you face some issues while installing and making Portal up in your local, have a look at issues labelled as [While Setting up Portal](https://github.com/BipHelp/BipHelp/labels/%20Setting%20Up%20BipHelp).
