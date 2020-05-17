<p align="center">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTVGrRyh-Q55ckT98qshfXU3Fmh7-F_HD7WBSetZkwgqQKU7RW2&usqp=CAU">
</p>

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

- [Proximo](./Static-Files.md)
