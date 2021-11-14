Create virtualenv with the following command

```bash
python3 -m venv /path/to/new/virtual/environment
source /path/to/new/virtual/environment/bin/activate
```

The lets install the two packages that we need i.e django and gunicorn

We can verify that these packages has been verified on the virtual env with the help of the **which** command

![enter image description here](https://i.imgur.com/dsqAxhc.png)

From the command line, `cd` into a directory where you’d like to store your code, then run the following command:

```
django-admin startproject samplesite
```

This creates a sample project from django. Next, lets edit the settings.py file to add our ip address on the ALLOWED_HOSTS section and turn debug to false since we are deploying the production version

![enter image description here](https://i.imgur.com/IxJZT08.png)

Now lets create a config file for the gunicorn, we'll keep this config file on the conf folder on the home directory

![enter image description here](https://i.imgur.com/e4SOkK1.png)

Here we have binded the deployed application to port **8089** and set the number of workers to 3

Now, lets allow the newly added port on our firewall

![enter image description here](https://i.imgur.com/ZV9FQl8.png)

To deploy the site with the help of the gunicorn we have to start it pointing at our config file. To do so, enter the following command

```bash
gunicorn -c /path/to/config/file projectname.[wsgi]
```

![enter image description here](https://i.imgur.com/ruvhc2E.png)

We can verify that the site is deployed by visiting the ip address of the machine

![enter image description here](https://i.imgur.com/4wc4XOy.png)
