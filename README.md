# BBDN-LaunchExternal

This project is set up to demonstrate the use of LTI 1.3 in Python to replace launch_external.jsp functionality.

To configure:

## configs/lti.json and configs/private.key

This [document](https://docs.blackboard.com/standards/PyLTI1p3WithBlackboardLearn.html) shows how to configure the PyLTI1.3 library, which is done through the `configs`directory.

## ConfigTemplate.py

Copy `ConfigTemplate.py` to `Config.py` and fill in your information:

```
config = {
    "verify_certs" : "True",
    "learn_rest_url" : "YOURLEARNSERVERNOHTTPS",
    "learn_rest_key" : "YOURLEARNRESTKEY",
    "learn_rest_secret" : "YOURLEARNRESTSECRET",
    "app_url" : "YOURAPPURLWITHHTTPS"
}

courses = {
    "_143_1" : "UEF Pilot Cohort"
}

courseIds = '_143_1'

contents = {
    "_3127_1" : "Demo the UEF Python Example"
}

contentIds = '_3127_1'
```

* **learn_rest_url** should be set to your learn instances domain. Be sure to avoid the request scheme, i.e. `mylearn.blackboard.edu`
* **app_url** should be set to the FQDN of your application, i.e. `https://myapp.herokuapp.com`
* **courses** maps the course Pk1 to the title you wish to to assign it
* **courseIds** is a comma-delimeted list of course ids to listen for events from
* **contents** maps content pk1 values to the title you wish to assign it
* **contentIds** is a comman-delimited list of content Ids to listen for events from

## To Run

First run `pip install -r requirements.txt`  and then `python app.py` or if you are using heroku, just check in the code to your dyno.

OR
Use the included Dockerfile and the following. The assumption is that you have Docker desktop an ngrok on your development system.

Start your ngrok tunnel. Example:
$ ngrok http -region=us -hostname=launchexternal.ngrok.io 5000
Build the Docker image. Note the period at the end.
$ docker build -t launch-external:0.1 .
Now run it. From the terminal, type:
$ docker run -p 5000:5000 --name LaunchExternal launch-external:0.1
