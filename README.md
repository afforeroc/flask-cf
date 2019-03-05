# Configurar una aplicación web de Flask para desplegarla en Cloud Foundry

Este tutorial te indicará como configurar una aplicación web de `Flask` para desplegarla en Cloud Foundry.

* Nota: Al descargar este repositorio, la aplicación tendrá los archivos de configuración para el despliegue, pero es necesario que realices el paso 4.

## Requisitos básicos
* Ventana de comandos como `Terminal` o `PowerShell`
* Editor de texto/código como `Notepad++` o `Visual Studio Code`

### 1. Instalar Python y Flask
* Instala la última versión de [Python](https://www.python.org/downloads/)
* Verifica la instalación de Python: `$ python --version`
* Verifica la instalación de PIP: `$ pip --version`
* Instala Flask: `$ pip install Flask>=0.12`
* Verifica la instalación de Flask: `$ flask --version`

### 2. Crear y probar la aplicación web
* Crea la carpeta: `flask-cf\`
* Accede a la carpeta creada: `$ cd flask-cf`
* Desde la carpeta, crea el archivo `app.py` y editalo con lo siguiente información:
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
* Corre la aplicación: `$ python app.py`
> AAbre una pestaña en tu navegador web en: http://localhost:3000/
* Detén la aplicación: `(Ctrl + C)`

### 3. Configurar la aplicación para el despliegue
Desde la carpeta raíz de la aplicación
* Crea el archivo `Procfile` y editalo con la siguiente información:
```
web: python app.py
```
* Crea el archivo `requeriments.txt` y editalo con la siguiente información:
```
Flask>=0.12
```
* Crea el archivo `manifest.yml` y editalo con la siguiente información:
```
---
applications:
- name: flask-cf-<initials>-<date>
  memory: 64M
```

### 4. Colocar un nombre a la aplicación
* Dentro del archivo `manifest.yml`, cambia el valor del atributo `- name` colocando un nombre **único**. Puedes usar la plantilla para colocar tus iniciales y la fecha de hoy.

## Links de referencia
* Simple Python Flask app on Cloud Foundry: https://gist.github.com/ihuston/e87c1d4719f7e72e9760
* CF Sample App Python: https://github.com/swisscom/cf-sample-app-python

## Links de interés
* Documentación de Flask: http://flask.pocoo.org/
* Documentación de Cloud Foundry: https://docs.cloudfoundry.org/ 
* Documentación sobre manifest.yml: https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html