
<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../4noobsAssets/header_4noobs.svg">
  </a>
</p>

<p align="center">
  <h2 align="center">Flask4noobs</h2>
  <h1 align="center"><img src="https://flask.palletsprojects.com/en/1.1.x/_static/flask-icon.png" alt="Flask" width="120"></h1>
  <p align="center">
    <br />
    <a href="../README.md"><strong>Explore a documentação »</strong></a>
    <br />
    <br />
    <a href="https://github.com/freazesss/flask4noobs/issues/new">Report Bug</a>
    ·
    <a href="../README.md#como-contribuir">Request Feature</a>
  </p>
</p>



## Conteudo

- 1.1 [Hello World](#hello-world)
- 1.2 [Render Template](#render-template)
- 1.3 [Static Files](#static-files)
- 1.4 [HTTP Methods](#http-methods)
- 1.5 [Redirects and Errors](#redirects-and-errors)
- 1.6 [File Uploads](#file-uploads)
- 1.7 [APIs with JSON](#APIs-with-JSON)
- 1.8 [Cookies](#Cookies)
- 1.9 [Logging](#Logging)
- 2.0 [New...](#New)

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

A Saida sera:

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

Gerar html dentro de python não é legal, Por isso o flask configura o **jinja2 Mecanismo de template** para você renderizar um html. Você pode utilizar o metodo **render_template()**. O Flask ira procurar o arquivo "html" na pasta **templates/**.

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

Aplicações dinâmicas web também precisam de arquivos estáticos. Usamos **css** e **javascript**. precisamos criar uma pasta chamada ``/static``. Para gerar a **URL** para arquivos estáticos use o ``/static``.
A Estrutura dos arquivos ficaria:

```s
/<nome_do_seu_arquivo>.py

/static
  /style.css
/templates
    /home.html
```

Como ficaria no meu html?

```html
<!DOCTYPE html>
<html lang="pt-br" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>Flask4noobs</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css')}}">
  </head>
  <body>
    <h1>Olá, Mundo!</h1>
  </body>
</html>
```

## Http Methods

Aplicações Web utilizam diferentes métodos HTTP quando acessam URLS. Você pode se familiarizar com o Método HTTP, Por padrão a rota ira retornar ``GET``. Você pode usar o método ``route()``. para lidar com diferentes métodos HTTP.

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

Para redirecionar o usuário para outra pagina **html**, utilize a função ``redirect()``; para abortar uma requisição antes com um erro de codigo, use a função ``abort()``:

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

Se você quer customizar o erro da pagina, você pode usar o **decorador** ``errorhandler()``:

```py
from flask import render_template

@app.errorhandler(404)
def page_not_found(error):
    return render_template('404.html'), 404
```

## File Uploads

##### Requirements
- Instale o framework flask: _pip install flask_

##### Passo a passo

Para começarmos iremos criar uma pasta com o nome _UploadFiles_ e dentro dela criaremos nosso ambiente virtual, usando o comando _virtualenv -p python3 venv_ (caso você tenha somente a versão 3 do python no sistema operacional, basta fazer: _virtualenv venv_). Depois disso, ainda dentro da pasta _UploadFiles_, iremos criar um arquivo chamado _app.py_, o qual irá conter nosso codigo fonte, e além disso, criaremos uma outra pasta com o nome _templates_, que terá dentro dela o arquivo _index.html_, o qual irá conter nosso formulário html que fará o upload do arquivo.

- Nossa estrutura de pastas ficará assim:
```
-> UploadFiles/
    -> templates/
        -> index.html
    -> app.py
```

Agora, ja podemos começar e escrever nosso código, começando pela importação dos métodos que usaremos.

```python

    from flask import Flask, request, render_template, url_for, redirect, flash
    from werkzeug.utils import secure_filename
```

Do flask, importamos a própria classe do framework, o método _request_, *render_template*, *url_for*, _redirect_ e _flash_.

A proxima importação é da biblioteca __Werkzeug__ que, basicamente, é uma biblioteca abrangente de aplicativos da Web com varios utilitários.

Importamos o método **secure_filename()**, que tem como objetivo prevenir inserção de arquivos protegidos, ou que o usuário tente inserir dados incorretos/falsificados no formulário de upload.

Na sequencia, iremos declarar nosso método _Flask_ e definir uma secret_key (obrigatório para realizar qualquer requisição em formulários, utilizando flask):

```python

    app = Flask(__name__)
    app.secret_key = b'set_your_secret_key_here'
```

Com nosso Objeto _Flask()_ declarado e nossa *secret_key* definida, vamos criar nossa rota para a página do formulário:

```python

    @app.route('/', methods=['GET', 'POST'])
    def upload_file():
        return render_template('index.html')
```

- Nesse trecho de código definimos a URL de acesso da nossa rota: *localhost:5000/*;
- definimos os métodos de requisição aceitos nessa pagina: *methods=['GET', 'POST']*;
- Criamos a função *upload_file()*, que retorna o template da nossa página.

Repare na ultima linha desse trecho, que citamos o arquivo *index.html*, nós ja criamos (foi criado no começo desse tópico), mas ainda esta em branco. Por ser um tutorial sem foco no frontend, usaremos o seguinte trecho html:

```html

<!DOCTYPE html>
<html lang="pt-br">
   <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
      <title>Flask File Uploads</title>
   </head>
   <body>
      <h1 class="text-center">Flask File Upload Form</h1><hr>
      <form action="{{url_for('upload_file')}}" method="POST" enctype="multipart/form-data">
         <label for="filefield" class="ml-2">File Field:</label>
         <input type="file" class="form-control col-sm-6 ml-2" name="filefield" id="filefield"><br>
         <button type="submit" class="btn btn-outline-info ml-2">Submit File</button>
      </form><hr>
      {% with messages = get_flashed_messages() %}
         {% if messages %}
            {% for message in messages %}
               <div class="alert alert-light" role="alert">
                  {{ message }}
               </div>
            {% endfor %}
         {% endif %}
      {% endwith %}
   </body>
</html>
```

- Nosso formulário é basico, composto apenas por um _input field_, definido como _type=file_;

- No trecho de código abaixo, usamos o método _flash()_, importado no nosso backend. Basicamente, se for retornado algum erro, o sistema irá mostrar no frontend a mensagem retornada pelo flask:
```html

{% with messages = get_flashed_messages() %}
    {% if messages %}
        {% for message in messages %}
            <div class="alert alert-light" role="alert">
                {{ message }}
            </div>
        {% endfor %}
    {% endif %}
{% endwith %}
```

Com nossa rota e nosso html prontos, ja podemos complementar o nossa função __upload_files()__ para realizar submit do formulário e, consequentemente, o uplaod do nosso arquivo. Por fim, nossa função completa ficará assim:

```python

@app.route('/', methods=['GET', 'POST'])
def upload_file():
    if request.method == 'POST':
        f = request.files['filefield']
        f.save('/home/wendrew/Documentos/Projetos/UploadFiles/src/' + secure_filename(f.filename))
        flash('File uploaded successfully.')
        return redirect(url_for('upload_file'))

    return render_template('index.html')
```

- Adicionamos uma condição que verifica se o método enviado no submit do formulãrio foi _POST_;
- Criamos uma variavel (f) que recebe uma requisição de um arquivo qualquer e com essa mesma variavel, definimos onde iremos salvar o arquivo e utilizamos o método *secure_filename()* para garantir que tudo ocorra bem no upload do arquivo:

```python

    f = request.files['filefield']
    f.save('/home/wendrew/Documentos/Projetos/UploadFiles/src/' + secure_filename(f.filename))
```

- Quanto ao local onde salvaremos nosso arquivo, criaremos uma pasta dentro do nosso diretorio raiz do projeto, com o nome _src_.

Por fim, adicionaremos o trecho de código abaixo:

```python

    if __name__ == "__main__":
        app.run(debug = True)
```

Nosso código final ficará da seguinte forma:

**App**
```python

    from flask import Flask, request, render_template, request, url_for, redirect, flash
    from werkzeug.utils import secure_filename


    app = Flask(__name__)
    app.secret_key = b'set_your_secret_key_here'

    @app.route('/', methods=['GET', 'POST'])
    def upload_file():
        if request.method == 'POST':
            f = request.files['filefield']
            f.save('/home/wendrew/Documentos/Projetos/UploadFiles/src/' + secure_filename(f.filename))
            flash('File uploaded successfully.')
            return redirect(url_for('upload_file'))
        return render_template('index.html')


    if __name__ == "__main__":
        app.run(debug = True)
```

**Html**
```html

<!DOCTYPE html>
<html lang="pt-br">
   <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
      <title>Flask File Uploads</title>
   </head>
   <body>
      <h1 class="text-center">Flask File Upload Form</h1><hr>
      <form action="{{url_for('upload_file')}}" method="POST" enctype="multipart/form-data">
         <label for="filefield" class="ml-2">File Field:</label>
         <input type="file" class="form-control col-sm-6 ml-2" name="filefield" id="filefield"><br>
         <button type="submit" class="btn btn-outline-info ml-2">Submit File</button>
      </form><hr>
      
   </body>
</html>
```

E, nossa disposição de pastas ficará assim:

```
-> UploadFiles/
    -> src/ (Local onde nosso aquivo será salvo)
    -> templates/
        -> index.html
    -> app.py
```

## Apis With Json

Um resposta comum formatar quando escrevemos uma API é JSON. Facil de começar escrevemos tal API com Flask. se você retorna um ``dict`` de uma view, isto ira ser convertido em um JSON response.

```py
@app.route("/")
def me_api():
    return {
        "Name": "Gustavo",
        "Job": "Back End",
    }
```

Dependendo do design da sua ``API``, voce quer criar ``JSON responses`` para outros tipos de dict. Nesse caso, utilize a função ``jsonify()``, o qual ira serializar um tipo de dado ``JSON`` suportado. Ou iremos olhar em comunidades flask extensões que suportam aplicaçoes mais complexas.

```py
@app.route("/")
def users_api():
    return jsonify({
    'Ola' : 'Mundo',
    'Lins' : 'Dict'
    })
```

## Cookies

Para acessar os ``cookies`` você pode usar os ``cookies attribute``. Para setar cookies você pode utilizar o ``set_cookie`` metodo de uma resposta de objetos. Os cookies atribuidos de request objects e um dict com todos os cookies o cliente transmite. Se voce quer usar sessioes, nao use os cookies diretamente mas em vez de usar as Sessions no Flask isso adiciona uma segurança no topo dos cookies para voce.

### Lendo os cookies

```py
from flask import request

@app.route('/')
def index():
    username = request.cookies.get('username')

    # utilize cookies.get(key) em vez de cookies[key] para não ter um
    # KeyError se o cookie esta faltando.
```

### Guardando os cookies

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

## New

Sendo feito...

[Início](../README.md), [Anterior](./2-Instalacao.md), [Próximo](./4-Desafios.md)


<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../4noobsAssets/footer_4noobs.svg" width="380">
  </a>
</p>
