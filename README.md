## Distelli example deploy for Google App Engine using gcloud SDK

This repository is an example of deplpoying to Google App Engine from Distelli after successfull builds.

## Setup

To do this, you must build on your own build server. Due to gcloud SDK needing human interaction for authentication.

Please configure you own private build server in Distelli from these instructions.
[Using your own Build Server](https://www.distelli.com/docs/kb/using-your-own-build-server)


## Configure Build Server with Gcloud SDK

1. Login to your build server.

2. Swith to the **distelli** user.

  ```
  sudo su - distelli
  ```
  
3. Download the gcloud SDK.

  ```
  curl -o gcloud-sdk.tgz https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-126.0.0-linux-x86_64.tar.gz
  ```

4. Untar/Decompress the gcloud SDK.

  ```
  tar -zxvf gcloud-sdk.tgz
  ```

5. Run the gcloud SDK installer.

  ```
  ./google-cloud-sdk/install.sh --usage-reporting false --path-update true --command-completion true --rc-path ~/.bashrc
  ```

6. Authenticat the gcloud SDK. In this step, you will be given a URL to navigate to and approve. This will return a code you need to enter.

   ```
   $ gcloud auth login
   Go to the following link in your browser:

       https://accounts.google.com/o/oauth2/auth?redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&prompt=select_account&response_type=code&client_id=01234567890.apps.googleusercontent.com&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fappengine.admin+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcompute&access_type=offline


   Enter verification code:
   ```

7. Copy and paste the URL into your browser, approve, and copy the **verification code**.

8. After pasting the verification code, you should see a message similar to this:

  ```
  You are now logged in as \[jdoe@distelli.com].
  ```



## Python Flask Skeleton for Google App Engine

![status: inactive](https://img.shields.io/badge/status-inactive-red.svg)


A skeleton for building Python applications on Google App Engine with the
[Flask micro framework](http://flask.pocoo.org).

See our other [Google Cloud Platform github
repos](https://github.com/GoogleCloudPlatform) for sample applications and
scaffolding for other python frameworks and use cases.

## Run Locally
1. Install the [App Engine Python SDK](https://developers.google.com/appengine/downloads).
See the README file for directions. You'll need python 2.7 and [pip 1.4 or later](http://www.pip-installer.org/en/latest/installing.html) installed too.

2. Clone this repo with

   ```
   git clone https://github.com/GoogleCloudPlatform/appengine-python-flask-skeleton.git
   ```
3. Install dependencies in the project's lib directory.
   Note: App Engine can only import libraries from inside your project directory.

   ```
   cd appengine-python-flask-skeleton
   pip install -r requirements.txt -t lib
   ```
4. Run this project locally from the command line:

   ```
   dev_appserver.py .
   ```

Visit the application [http://localhost:8080](http://localhost:8080)

See [the development server documentation](https://developers.google.com/appengine/docs/python/tools/devserver)
for options when running dev_appserver.

## Deploy
To deploy the application:

1. Use the [Admin Console](https://appengine.google.com) to create a
   project/app id. (App id and project id are identical)
1. [Deploy the
   application](https://developers.google.com/appengine/docs/python/tools/uploadinganapp) with

   ```
   appcfg.py -A <your-project-id> --oauth2 update .
   ```
1. Congratulations!  Your application is now live at your-app-id.appspot.com

## Next Steps
This skeleton includes `TODO` markers to help you find basic areas you will want
to customize.

### Relational Databases and Datastore
To add persistence to your models, use
[NDB](https://developers.google.com/appengine/docs/python/ndb/) for
scale.  Consider
[CloudSQL](https://developers.google.com/appengine/docs/python/cloud-sql)
if you need a relational database.

### Installing Libraries
See the [Third party
libraries](https://developers.google.com/appengine/docs/python/tools/libraries27)
page for libraries that are already included in the SDK.  To include SDK
libraries, add them in your app.yaml file. Other than libraries included in
the SDK, only pure python libraries may be added to an App Engine project.

### Feedback
Star this repo if you found it useful. Use the github issue tracker to give
feedback on this repo.

## Contributing changes
See [CONTRIB.md](CONTRIB.md)

## Licensing
See [LICENSE](LICENSE)

## Author
Logan Henriquez and Johan Euphrosine
