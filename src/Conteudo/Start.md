# Flask f4r Noobs

## 1° Modulo

- 2.1 [Hello World](#hello-world)
- 2.2 [Render Template](#render-template)
- 2.3 [Static Files](#static-files)
- 2.4 [HTTP Methods](#http-methods)
- 2.5 [Redirects and Errors](#redirects-and-errors)
- 2.6 [File Uploads](#file-uploads)
- 2.7 [APIs com JSON](#APIs-com-JSON)
- 2.8 [Cookies](#Cookies)
- 2.9 [Logging](#Logging)

## 2° Modulo

.....

### Hello World

```py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def homepage():
 return '<h1>Ola Mundo!</h1>'

app.run(debug=True)
```

## Rodar

Abra o seu cmd e digite:

```sh
python <nome_do_seu_arquivo>.py
```

#### A Saida sera

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

## Oque fizemos nesse codigo

1. Importamos o Flask do flask
2. Criamos uma instância dessa class. O Primeiro argumento é o nome da sua Aplicação.
3. Utilizamos o route para dizer a Url exemplo:

```s
http://127.0.0.1:5000/
```

## Render Template

Gerar html dentro de python não é legal, Por isso o flask configura o **jinja2 Mecanismo de template** para você...
Renderizar um html. você pode utilizar o metodo **render_template()**.
O Flask ira olhar a pasta **templates/**.

```s
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

## Static Files

Aplicações dinamicas web tambem precisam de arquivos staticos. Usamos css e JavaScript. precisamos criar uma pasta chama ``/static``.
Para gerar a Url para arquivos staticos use o ``/static``.
A Estrutura ficaria:

```s
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

## Http Methods

Aplicações Web utilizam difrentes metodos HTTP quando acessam URLs. Você pode se familiarizar com o Metodo HTTP Por padrão, a rota ira responder o ``GET``. Você pode usar o metodo ``route()``. para lidar com difrentes metodos HTTP.

```py
from flask import request

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        return faca_o_login()
    else:
        return volte_para_o_login_formulario()
```

## Redirects e Errors

Para redirecionar o usuario para outra html, utilize a função ``redirect()``; para abortar uma requisição antes com um erro de codigo, use a função ``abort()``:

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

# APIs com JSON
Um resposta comum formatar quando escrevemos uma API é JSON. Facil de começar escrevemos tal API com Flask. se você retorna um ``dict`` de um view, isto ira ser convertido em um JSON response.

```py
@app.route("/")
def me_api():
    return {
        "name": "Gustavo",
        "sobre_nome": "Lins",
    }
```

Dependendo do design da sua ``API``, voce quer criar ``JSON responses`` para tipos de outro dict. Nesse caso, utilize a funçao ``jsonify()``, o qual ira serializar um tipo de dado ``JSON`` suportado. Ou iremos olhar em comunidades flask estensoes que suportam aplicaçoes mais complexas.

```py
@app.route("/")
def users_api():
    return jsonify({'Ola' : 'Mundo', 'Lins' : 'Dict'})
```

## Cookies

Para acessar os ``cookies`` você pode usar os ``cookies attribute``. Para setar coockies você pode utilizar o ``set_cookie`` metodo de uma resposta de objetos. Os cookies atribuidos de request objects e um dict com todos os cookies o cliente transmite. Se voce quer usar sessioes, nao use os cookies diretamente mas em vez de usar as Sessions no Flask isso adiciona uma segurança no topo dos cookies para voce.

### Lendo os cookies

```py
from flask import request

@app.route('/')
def index():
    username = request.cookies.get('username')
    # utilize cookies.get(key) em vez de cookies[key] para nao ter um
    # KeyError se o cookie esta faltando.
```

### Guardando os cookies:

```py
from flask import make_response

@app.route('/')
def index():
    resp = make_response(render_template(...))
    resp.set_cookie('username', 'the username')
    return resp
```

Note que os cookies são setados em um ``response object`` desde você normalmente so retornar ``string`` de uma ``view function`` O Flask ira converter ele em um ``response object`` para você. Se você quer explicitamente fazer isso você pode utilizar a funcão ``make_response()`` e assim modificar-lo.

As vezes você pode querer setar o cookie como um ponto onde o ``response object`` não existe assim. isso é possivel utilizando um ``Deferred Request Callbacks pattern``.

## Logging

Você pode querer fazer um ``log`` quando alguma coisa duvidosa acontecer. Isso esta aqui ``loggers`` vem acessivel. Com o Flask 0.3 e tem um logger preconfigurado para você usar.
Aqui estão alguns exemplos de logs:

```py
app.logger.debug('Um valor para debugar')
```

```py
app.logger.warning('Um aviso aconteceu, (%d apples)', 42)
```

```py
app.logger.error('Um error aconteceu.')
```
