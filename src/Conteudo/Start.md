<p align="center">
  <img src="https://miro.medium.com/max/6000/1*Ou6FFJJD3zhcIUU8wBZqIw.png" width="500">
</p>

# Começo

- 2.1 [Hello World](#Hello-World)
- 2.2 [Render Template](#Render-Template.md)
- 2.3 [Static Files](#Static-Files.md)
- 2.4 [HTTP Methods](#HTTP-Methods.md)
- 2.5 [Redirects and Errors](#Redirects-and-Errors.md)
- 2.6 [File Uploads](#File-Uploads.md)


# Hello World

```py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def homepage():
	return '<h1>Ola Mundo!</h1>'

app.run(debug=True)
```
## Rodar:
#### Abra o seu cmd e digite:

```sh
python <nome_do_seu_arquivo>.py
```

#### A Saida sera:
```sh
* Serving Flask app "nome_do_seu_arquivo" (lazy loading)
* Environment: production
  WARNING: This is a development server. Do not use it in a production deployment.
  Use a production WSGI server instead.
* Debug mode: on
* Restarting with stat
* Debugger is active!
* Debugger PIN: 200-368-601
* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

## Oque fizemos nesse codigo?
1. Importamos o Flask do flask
2. Criamos uma instância dessa class. O Primeiro argumento é o nome da sua Aplicação.
3. Utilizamos o route para dizer a Url exemplo:

```
http://127.0.0.1:5000/
````


# Render Template
##### Gerar html dentro de python não é legal, Por isso o flask configura o **jinja2 Mecanismo de template** para você...
##### Renderizar um html. você pode utilizar o metodo **render_template()**.
##### O Flask ira olhar a pasta **templates/**.

```
/<nome_do_seu_arquivo>.py
/templates
    /home.html
```

```py
from flask import render_template

app = Flask(__name__)

@app.route('/')
def homepage():
	return render_template('home.html')

app.run(debug=True)
```

# Static Files
##### Aplicações dinamicas web tambem precisam de arquivos staticos. Usamos css e JavaScript. precisamos criar uma pasta chama ``/static``.
##### Para gerar a Url para arquivos staticos use o ``/static``.

# A Estrutura ficaria:

```
/<nome_do_seu_arquivo>.py
/static
  /style.css
/templates
    /home.html
```

# Como ficaria no meu html?

```html
<!DOCTYPE html>
<html lang="pt-br" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>Flask4noobs</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css')}}">
  </head>
  <body>
    <h1>Ola Mundo!</h1>
  </body>
</html>
```

# Http Methods
##### Aplicações Web utilizam difrentes metodos HTTP quando acessam URLs. Você pode se familiarizar com o Metodo HTTP Por padrão, a rota ira responder o ``GET``. Você pode usar o metodo ``route()``. para lidar com difrentes metodos HTTP.

```py
from flask import request

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        return faca_o_login()
    else:
        return volte_para_o_login_formulario()
```

# Redirects e Errors
##### Para redirecionar o usuario para outra html, utilize a função ``redirect()``; para abortar uma requisição antes com um erro de codigo, use a função ``abort()``:

```py
from flask import abort, redirect, url_for

@app.route('/')
def index():
    return redirect(url_for('login'))

@app.route('/login')
def login():
    abort(401)
    isso_nunca_sera_executado()
```

#### Se você quer costumizar o erro da page, você pode usar o decorador ``errorhandler()``:

```py
from flask import render_template

@app.errorhandler(404)
def page_not_found(error):
    return render_template('404.html'), 404
```

# Fazendo.......
## Olhe aqui amanhã.. :purple_heart:
## [Me de um feedback.](https://twitter.com/freazesss) :purple_heart:

