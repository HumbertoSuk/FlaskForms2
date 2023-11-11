#  Explicación del Código

## Descripción del Proyecto


## Estructura del Proyecto
La estructura de directorios del proyecto es la siguiente:

- `database`: Contiene archivos relacionados con la base de datos del proyecto.
- `src`: Aquí se encuentra el código fuente del proyecto.
  - `models`: Contiene módulos relacionados con los modelos de datos.
    - `entities`: Módulos que definen las entidades del proyecto.
  - `static`: Almacena archivos estáticos utilizados por la aplicación.
    - `css`: Archivos de hojas de estilo CSS.
    - `img`: Imágenes y recursos gráficos.
  - `templates`: Contiene plantillas HTML utilizadas en la aplicación.
    - `auth`: Plantillas relacionadas con la autenticación y el inicio de sesión.
- `env`: Directorio para el entorno virtual (virtual environment) del proyecto.



## Código Implementado
Import:

- Flask: Importa la clase Flask del framework Flask, que se utiliza para crear y configurar la aplicación web.
- redirect: Importa la función redirect, que se utiliza para redirigir a los usuarios a otras páginas.
- render_template: Importa la función render_template, que se utiliza para renderizar plantillas HTML.
- request: Importa el objeto request, que proporciona información sobre la solicitud HTTP actual.
- url_for: Importa la función url_for, que se utiliza para generar URLs para rutas de la aplicación.

## Rutas
La aplicación define tres rutas:

- /: La ruta raíz que redirige a los usuarios a la página de inicio de sesión.
- /login: La ruta de inicio de sesión que maneja tanto las solicitudes GET como POST.
- /home: La ruta de inicio que renderiza una plantilla HTML de página de inicio.


### Ruta raiz

``` python
@app.route("/")
def index():
    return redirect("login")

```

Esta función maneja las solicitudes a la ruta raíz /. Cuando un usuario accede a la raíz, la función redirige al usuario a la página de inicio de sesión (/login).

### login

``` python
@app.route("/login", methods=["GET", "POST"])
def login():
    if request.method == "POST":
        _user = request.form["username"]
        _pass = request.form["password"]
        print(_user)
        print(_pass)
        if _user == "admin" and _pass == "123":
            return redirect(url_for("home"))
        else:
            return render_template("auth/login.html")
    else:
        return render_template("auth/login.html")

```

Esta función maneja las solicitudes a la ruta /login. Puede manejar tanto solicitudes GET como POST debido a la especificación methods=["GET", "POST"].

Si la solicitud es un POST (es decir, se envía un formulario), la función obtiene los valores del campo "username" y "password" del formulario utilizando el objeto request.form. Luego, verifica si las credenciales son válidas (en este caso, "admin" y "123"). Si las credenciales son válidas, el usuario es redirigido a la página de inicio (/home). Si no son válidas, se renderiza la plantilla HTML de inicio de sesión.

Si la solicitud es un GET (por ejemplo, cuando un usuario accede directamente a la página de inicio de sesión), simplemente se renderiza la plantilla HTML de inicio de sesión.

### home


``` python
@app.route("/home")
def home():
    return render_template("/home.html")


```

Esta función maneja las solicitudes a la ruta /home. Cuando un usuario accede a esta ruta, se renderiza una plantilla HTML de página de inicio (/home.html).


### Inicio de la aplicación:

``` python
if __name__ == '__main__':
    app.config.from_object(config['development'])
    app.run()

```

Este bloque verifica si el script app.py se está ejecutando directamente (no importado como módulo). Si es así, se configura la aplicación Flask para utilizar la configuración de desarrollo (config['development']) y se inicia el servidor de desarrollo con app.run().


## Implementaciones nuevas
