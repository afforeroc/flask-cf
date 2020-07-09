# Create and configure a Flask app to deploy on Cloud Foundry
This is a tutorial about how to create and configure a simple web app to deploy on cloud using Cloud Foundry service.<br>

## Tutorial
This tutorial was designed to be done on a personal computer.

### Required software
* Command-line interpreter like [Terminal](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).
* Text editor like [Visual Studio Code](https://code.visualstudio.com/).

### 1. Install Python and Flask
1.1 Install stable/latest version of [Python](https://www.python.org/downloads/).

1.2 Verify Python installation.
```
python3 --version
```
```
pip3 --version
```

1.3 Install and verify the framework.
```
pip3 install Flask>=0.12
```
```
flask --version
```

1.4 If you can't see the framework version on Windows. Launch a PowerShell window as an administrator and enter this following command. Later, try again to verify.
```
Set-ExecutionPolicy Unrestricted
```

### 2. Create and run the app
2.1 Create `flask-app\` folder and go inside it.
```
mkdir flask-app
```
```
cd flask-app
```

2.2 Create `app.py` file and edit it with following template.
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

2.3 If you downloaded the web app sample, please install requeriments.
```
pip3 install -r requirements.txt
```

2.4 Run the app locally and later, open your favorite web browser on `localhost:3000`. Remember give access to Python to use local network.
```
python3 app.py
```

2.5 Stop the app with <kbd>ctrl</kbd> + <kbd>C</kbd>.

### 3. Configure the app to deploy
3.1 Enter to `flask-app\` folder

3.2 Create `Procfile` file (without file extension) and edit it with following template.
```
web: python app.py
```

3.3 Create `requeriments.txt` file and edit it with following template.
```
Flask>=0.12
```

3.4 Create `manifest.yml` file and edit it with following template. It's necessary customize and use a **unique** value for `name` attribute, because this will used as part of an **URL** string where your app will deployed.
```
---
applications:
- name: flask-app-<initials>-<date>
  memory: 64M
```

3.5 The web app is configurated. Now, you can learn how to [Deploy a web application on Cloud Foundry Service](https://github.com/afforeroc/deploy-on-cloudfoundry).

## Reference links
* [Simple Python Flask app on Cloud Foundry](https://gist.github.com/ihuston/e87c1d4719f7e72e9760)
* [CF Sample App Python](https://github.com/swisscom/cf-sample-app-python)

## Information links
* [Flask Documentation](http://flask.pocoo.org/)
* [Cloud Foundry Documentation](https://docs.cloudfoundry.org/) 
* [Deploying with App Manifests](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html)
