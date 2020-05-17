<p align="center">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTVGrRyh-Q55ckT98qshfXU3Fmh7-F_HD7WBSetZkwgqQKU7RW2&usqp=CAU">
</p>

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

- [Proximo](./Redirects-and-Errors.md)
