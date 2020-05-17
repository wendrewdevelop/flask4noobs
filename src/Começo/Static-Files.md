<p align="center">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTVGrRyh-Q55ckT98qshfXU3Fmh7-F_HD7WBSetZkwgqQKU7RW2&usqp=CAU">
</p>

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

- [Proximo](./HTTP-Methods.md)
