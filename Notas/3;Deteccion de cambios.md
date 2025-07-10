
# Detección de cambios 
## 📝 Notas
### Trigger
* Es un evento que inicia un proceso de render

#### Ejemplos
* Boton
* Llamada a la API

#### Tipos
* Inicial
    * Da inicio del renderizado (montaje) del componente

* Re-render
    * Renderiza de nuevo los componentes al deterctar cambios

### React Dom
* React trabaja con el Dom y el Dom virtual

| Dom | Dom virtual |
| --- | --- |
| React renderiza los componentes | Copia del Dom pero con los cambios donde React compara los cambios e indica el renderizado en el DOM | 

### Componente
* Es como una función

```javascript
function Dashboard(){
    return ...
}

```

### Renderizar
* Ejecuta  los componentes y muestra los resultados
* Cada ejecución es una instancia diferente

### Commit
* Es el proceso de aplicar los cambios detectados en el DOM virtual en el DOM 

---

## 💡Ideas clave
* React funciona con triggers para cargar los cambios dinamicamente
* Existen dos tipos de triggers: inicial y re-render
* React analiza los cambios del DOM mediante un DOM virtual
* Renderizar es el proceso de mostrar los componentes
* Commit es el proceso de aplicar los cambios detectados en el DOM virtual en el DOM  

--- 

## ❓Preguntas
* ¿Qué es el DOM? 
    * Document Object Model
    * Representación estructurada del documento HTML o XML que permite a los lenguajes de programación —como JavaScript— interactuar con el contenido, estructura y estilo de una página web


---

## ⏪Resumen
React al estar orientada a la arquitectura SPA debe estar constantemente detectando los cambios de los componentes para renderizarlos adecuadamente, esto lo hace mediante dos fases: initial-render y re-render, los cuales se sirven de comparar los cambios con el DOM virtual (que es una copia del DOM) y luego aplica esos cambios mediante un commit. 