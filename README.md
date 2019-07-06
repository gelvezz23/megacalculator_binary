# Megacalculadora binaria

Versión node: `11.14.0`

## Modificaciones antes de usar:

Modifica el archivo de `src/components/Calculator.vue` para poder usar la calculadora con la API.

1. Modifica la url (`HOST`) de la API en: `src/components/Calculator.vue:58`.


## API
* Calcular resultado de operación.

    operaciones: `sumadecimal`, `sumabinaria`, `restadecimal`, `restabinaria`
    * `url: /[operación]` 
    * `método: post`
    
    
    * `Response`:
    
        `status === 200`: Retornar objeto con key `resultado`. Ejemplo: `{resultado: 0100110}`
     
        `status === 400`:  Retornar objecto con key `mensaje`. Ejemplo: `{mensaje: 'Mensaje de retorno de error de la operación'}`



* Obtener Historial

    * `url: /historial`
    * `método: get`
    
    
    * `Response`:
    
        `status === 200`: Retornar array de objetos con los siguientes atributos: 
        
        ```javascript
        [
          {
              operacion: 'String con el tipo de operación registrada',
              numero1: 100010001,  // Número 1 de la operación registrada
              numero2: 100010001,  // Número 2 de la operación registrada
          }
        ]
        ```
     
        `status === 400`:  Retornar objecto con key `mensaje`. Ejemplo: `{mensaje: 'Mensaje de retorno de error de la operación'}`



## Configuración del proyecto
```
npm install
```

### Compile y recargue en desarrollo
```
npm run serve
```

### Compile y minifique para producción
```
npm run build
```

Hecho con ♥ por [Megaterios S.A.S](www.megaterios.co)
