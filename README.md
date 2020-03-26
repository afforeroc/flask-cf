# Create and configure an Flask app to deploy on Cloud Foundry
This repository belongs to [tutorial set](https://github.com/afforeroc/deploy-on-cloudfoundry) about how to create and configure a web app to deploy on cloud. Additional, contains a web app sample for study and use.<br>

If you want to ...
>  * **Run app sample locally**- review steps 1 and 2.
>  * **Deploy app sample on cloud**- review step 3.

## Tutorial
This tutorial was designed to be done on a personal computer. Most every steps require using of console commands except when is indicated.

### 0. Required software
* Command prompt like Terminal, PowerShell, etc.
* Text editor like Notepad++, Visual Studio Code, etc.

### 1. Install Python and Flask
  **1.1** Install stable/latest version of [Python](https://www.python.org/downloads/).
  
  **1.2** Verify Python installation.
  ```
  python --version
  ```
  ```
  pip --version
  ```

  **1.3** Install and verify the framework.
  ```
  pip install Flask>=0.12
  ```
  ```
  flask --version
  ```

  > If you can't see the framework version on Windows, launch a PowerShell window as an administrator and enter this following command. Later, try again to verify.
  ```
  Set-ExecutionPolicy Unrestricted
  ```

### 2. Create and run the app
  **2.1** Create root folder `flask-app\` and go to inside.

  **2.2** Create `app.py` and edit it with following template.
  > Text<br> 
  ```
  # import dependencies
  import os
  from flask import Flask

  # bootstrap the app
  app = Flask(__name__)

  # set the port dynamically with a default of 3000 for local development
  port = int(os.getenv('PORT', '3000'))

  # our base route which just returns a string
  @app.route('/')
  def hello_world():
      return 'Congratulations! Welcome to the Swisscom Application Cloud.'

  # start the app
  if __name__ == '__main__':
      app.run(host='0.0.0.0', port=port)
  ```

  **2.3** Run the app. Later, open your favorite web browser on `localhost:3000`.
  > Remember give access to Python to use the local network
  ```
  python app.py
  ```

  **2.4** Stop the app with <kbd>ctrl</kbd> + <kbd>C</kbd>.

### 3. Configure the app to deploy
  Go to root folder and ...

  **3.1** Create `Procfile` file and edit it with following template.
  >Text
  ```
  web: python app.py
  ```

  **3.2** Create `requeriments.txt` file and edit it with following template.
  >Text
  ```
  Flask>=0.12
  ```

  **3.3** Create `manifest.yml` file and edit it with following template.
  > Text
  ```
  ---
  applications:
  - name: flask-app-<initials>-<date>
    memory: 64M
  ```

  **3.4** Edit `manifest.yml` file changing the value of `- name` attribute. The name that should be **unique** because this will used as part of an **URL** where your app will deployed.You can use previous template putting your initials and today's date.

## Reference links
* [Simple Python Flask app on Cloud Foundry](https://gist.github.com/ihuston/e87c1d4719f7e72e9760)
* [CF Sample App Python](https://github.com/swisscom/cf-sample-app-python)

## Information links
* [Flask Documentation](http://flask.pocoo.org/)
* [Cloud Foundry Documentation](https://docs.cloudfoundry.org/) 
* [Deploying with App Manifests](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html)