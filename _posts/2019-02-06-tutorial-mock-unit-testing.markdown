---
layout:     post
title:      Aprende a usar Mock en unit testing
author:     Roberto Torres
github:		rtorres90
tags: 		pruebas python2 python3 mock
subtitle:   Tutorial de uso clase Mock de unit testing
category:  
---

# Introducción.

Mediante nuestra proyectos va creciendo y aumentando su complejidad, nos daremos cuenta que crear usar unit tests a secas se nos hará tecnicamente imposible, debido a que usualmente la evolución de nuestra sistema incluirá dependencias externas. Por ejemplo, base de datos, información desde apis, etc.

La finalidad de los unit tests es testear de manera aislada el comportamiento de una unidad mínima de código, por ejemplo un módulo o un objeto.

Como son test enfocados a la más mínima unidad cualquier llamada externa rompería esta regla y convertiría nuestros unit tests en tests de integración. Para evitar esto debemos crear clases *falsas* (mocks) que actuen como las originales para crear estos unit tests.

# Entonces, ¿Qué es un Mock?

La palabra mock tiene muchos significados si la traducimos del inglés, pero en este caso la traducción más acertada es imitar o actuar como el original. La funcionalidad de la clase Mock no se aleja de esta traducción. Mock nos ayudará a crear clases que se comporten como la original, pero dichos comportamientos estarán definidos por nosotros para que podamos enforcar nuestro unit tests en  la clase/modulo objectivo y no en la librería externa.

Por ejemplo, si queremos crear unit tests para un objeto que muestre información del clima de una ciudad X, pero dicha información es obtenida de una clase que se conecta a una API que retorna información del clima. En este caso tendremos que crear un mock de la clase que se conecta con la API, es decir, crearemos una clase que se comporte como la dependencia original para crear unit tests de manera óptima para el objeto/modulo objetivo.

```python
import http.client
import json

class ApiClima:

    def getUsers():
        conn = http.client.HTTPSConnection("reqres.in")
        conn.request("GET", "/api/users")
        r1 = conn.getresponse().read()

        return json.loads(r1)['data']

    def getUser(user_id):
        conn = http.client.HTTPSConnection("reqres.in")
        conn.request("GET", "/api/user/%s" % user_id)
        r1 = conn.getresponse().read()

        return json.loads(r1)['data']


```