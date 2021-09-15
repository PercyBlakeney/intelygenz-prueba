
[![RealWorld Frontend](https://img.shields.io/badge/Vue-Framework-green)](https://vuejs.org/)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

# Reto Front APP

## Developer: jacob sosa nielsen

Aplicación construida para superar el reto de [Intelygenz](https://intelygenz.com/) 

La aplicación ha sido construida en **Vue.js** Incluyendo llamadas Get a API´s públicas mediante la libreria **"Axios"**

Es una aplicaicón ligera que consiste en implementar un lector RSS (Api) básico. Mostrando los resultados en una lista y los detalles en un modal. 

La aplicación cuenta además con conceptos de reactividad, para que la información de muestre dinámicamente según las acciones del usuario.

hay una lista de parámetros obligatorios:

- Cada fila debe contener el título, una descripción de no más de dos líneas y la imagen de la noticia
correspondiente.
- Al seleccionar una fila se debe abrir una pantalla con el detalle de la noticia.
- La pantalla de detalle contendrá el título, la descripción completa y la imagen de la noticia.
- En caso de utilizar librerías externas de terceros, justificar brevemente el motivo de cada una.



## Getting started

Instalar dependencias

```bash
# install dependencies
> npm i
```

## Librerias de terceros

Se han utilizado las siguientes librerias:

- Axios (Para poder hacer las llamadas get a la Api)
- Bootstrap (Para utilizar un framework de estilos CSS)
- esLint (Para mostrar los errores en el desarrollo)

These can be changed when the contributors reach a consensus.

## Origen de datos

El origen de datos ha sido una api publica de peliculas que no requiriese CORS ni autenticación


## Patrón de diseño

Se ha utilizado el patrón de diseño: SFC, con intención de Hacer un SPA utilizando la reactividad que aporta el Framework  **Vue.js**, El motivo de uso de este patrón de diseño es la facilidad de de encapsular en un único archivo el template, la lógica y el estilo necesarios para este componente.

Si la aplicación se escalase optaría por un patrón de Diseño MVVM y utilizar el store de VUEX.

## Testing

En un principio iba a utilizar Jest para hacer algún test, sin embargo la prueba es demasiado sencilla para aplicar un test unitario.
