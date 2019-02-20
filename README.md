# Desplegar una aplicación web de Flask en Cloud Foundry de IBM Cloud

> Presentación [Introducción a Cloud Foundry](https://ibm.box.com/v/cf-ppt)

Este tutorial te indicará como desplegar una aplicación web de `Flask` sobre Cloud Foundry de IBM Cloud usando la ventana de comandos. Una vez la aplicación este desplegada, esta será accesible desde cualquier navegador web. 

## Servicios Incluidos
* [IBM Cloud - Cloud Foundry](https://www.ibm.com/cloud/cloud-foundry): Servicio en la nube que ejecuta código fuente en una plataforma como servicio (PaaS). Open source, serverless y altamente escalable.

## Requisitos básicos
* Ventana de comandos como `Terminal` o `PowerShell`
* Editor de texto/código como `Notepad++` o `Visual Studio Code`
* Cuenta activa de [IBM Cloud](https://console.bluemix.net)

## 1. Opción A: Crear, probar y configurar la aplicación web

### Instalar Node.js y Express
* Instala la última versión de [Python](https://www.python.org/downloads/)
* Verifica la instalación de Python: `$ python --version`
* Verifica la instalación de Pip Installs Packages: `$ pip --version`
* Instala Flask: `$ pip install Flask>=0.12`
* Verifica la instalación de Flask: `$ flask --version`

### Crear y probar la aplicación web
* Crea la carpeta del proyecto con nombre: `flask-cf`
* Accede a la mencionada carpeta y crea el archivo `app.py` y edita con lo siguiente:
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
* Abre el navegador web en: http://localhost:3000/
* Detén la aplicación: `(Ctrl + C)`

### Configurar la aplicación para el despliegue
Desde la carpeta raíz del proyecto
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

## 1. Opción B: Clonar el repositorio
Al clonar este repositorio, la aplicación `flask-cf` tendrá los archivos de configuración para el despliegue.
* Descarga/clona este repositorio localmente: `$ git clone https://github.com/afforeroc/flask-cf`

## 2. Instalar IBM Cloud CLI
Instala según tu sistema operativo
* Instala en Mac/Linux: `$ curl -sL https://ibm.biz/idt-installer | bash`
* Instala en Windows: https://clis.ng.bluemix.net/download/bluemix-cli/latest/win64
* Verifica la versión del CLI: `$ ibmcloud -v`

## 3. Iniciar sesión con IBM Cloud CLI
Sigue las instrucciones interactivas del CLI en cada paso 
* Inicia sesión en IBM Cloud: `$ ibmcloud login`
* Apunta al espacio de trabajo de Cloud Foundry: `$ ibmcloud target --cf`
* Si deseas hacer cambios a tu sesión: `$ ibmcloud target -r <REGION> -o <ORG> -s <SPACE>`

## 4. Desplegar la aplicación usando el CLI
* Dentro del archivo `manifest.yml`, cambia el valor del atributo `- name` colocando un nombre **único**, ya que este será usado como parte de la URL generada. Puedes usar la plantilla para colocar tus iniciales y una fecha.
* Dentro del archivo `Profile`, verifica que exista el comando `web: python app.py`, ya que este permitirá ejecutar la aplicación en la nube.
* Posicionate en la carpeta raíz de la aplicación web
* Sube la aplicación a Cloud Foundry de IBM Cloud: `$ ibmcloud app push`
* Visualiza tu aplicación web accediendo al [Dashboard de IBM Cloud](https://console.bluemix.net/dashboard/apps)

## Links de interés:
* Documentación de Flask: http://flask.pocoo.org/
* Documentación de IBM Cloud: https://console.bluemix.net/docs/
* Documentación de IBM Cloud CLI: https://console.bluemix.net/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_cli
* Documentación de Cloud Foundry: https://docs.cloudfoundry.org/ 
* Documentación sobre manifest.yml: https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html