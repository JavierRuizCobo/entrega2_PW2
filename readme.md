# Vue

En Vue, tanto ref como reactive se utilizan para crear datos reactivos, lo que significa que cualquier cambio en estos datos desencadenará una actualización de la vista. Sin embargo, existen algunas diferencias clave entre las dos:

## Función ref 

La función ref puede guardar cualquier valor (no solo primitivos), esto hace que sea más polivalente que reactive. La función ref crea un objeto que envuelve el valor reactivo, así que para acceder al valor debes usar la propiedad value.

[Ejemplo](vue_reactividad/src/components/ref_example.vue)

## Función reactive

La función reactive se usa cuando quieras una colección de valores y deba ser reactiva. Vue genera un proxy cuando creamos un objeto reactivo para controlar las operaciones de sus propiedades (intercepta get y set). En esta función solo podemos guardar valores compuestos como objetos, arrays, etc. No se puede usar reactive con tipos primitivos. 

[Ejemplo](vue_reactividad/src/components/reactive_example.vue)


## Watch

Watch observa cambios en los datos y ejecutan una función de devolución de llamada cuando esos datos cambian. Se pueden usar los watchers para realizar tareas asíncronas o realizar acciones más complejas en respuesta a cambios en los datos

[Ejemplo](vue_reactividad/src/components/watch_exxample.vue) <br>

## Computed

Computed se utiliza para calcular propiedades basadas en otras propiedades reactivas. La ventaja de las propiedades computadas es que se almacena en caché y solo se recalcula cuando alguna de sus dependencias ha cambiado

[Ejemplo](vue_reactividad/src/components/computed_example.vue)

# Svelte

[Ejemplo 1](svelte_reactividad/src/lib/example1.svelte)
[Ejemplo 2](svelte_reactividad/src/lib/example2.svelte)


