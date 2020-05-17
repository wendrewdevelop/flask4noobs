<p align="center">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTVGrRyh-Q55ckT98qshfXU3Fmh7-F_HD7WBSetZkwgqQKU7RW2&usqp=CAU">
</p>

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

- [Proximo](./)
