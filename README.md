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

6. Authenticate the gcloud SDK. In this step, you will be given a URL to navigate to and approve. This will return a code you need to enter.

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

9. You can remove the archive.

  ```
  rm gcloud-sdk.tgz
  ```

10. If you want to begin using gloud now, source the following:

  ```
  source ~/.bashrc
  ```
  
11. Validate it works:

  ```
  $ gcloud config list
  Your active configuration is: [default]

  [core]
  account = jdoe@distelli.com
  disable_usage_reporting = True
  project = jdoe-project
  ```

Great. You can now do Google App Engine deploys on successful builds. Log out of your build server.

## Prepare your Distelli manifest

You will need a Distelli manifest in your repository to define your build instructions and deploy your application to Google App Engine. Below is an example working manifest:

```
jdoe/gcloud-gae-example:
  Build:
    - echo "Building"
    - pip install -r requirements.txt -t lib
  AfterBuildSuccess:
    - export PATH=$PATH:~/google-cloud-sdk/bin
    - gcloud -q app deploy app.yaml --stop-previous-version
```

### Feedback
[bmcgehee@distelli.com](mailto://bmcgehee@distelli.com)


