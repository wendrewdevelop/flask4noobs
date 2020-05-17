<p align="center">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTVGrRyh-Q55ckT98qshfXU3Fmh7-F_HD7WBSetZkwgqQKU7RW2&usqp=CAU">
</p>

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

- [Proximo](./File-Uploads.md)
