# Componentes

## 📝 Notas
### Componente
* Es una función que se va a ejecutar y su resultado se va a renderizar en `index.html`
* `main.tsx` crea la base de la app con `createRoot` el cual se muestra en `<div id="root"><div/>`
* Siempre tiene que se minima unidad de lógica posible

#### Tipos
* Dummy : Componente que no tiene estado
* Statefull : Componente con estado usa `useState`

#### Ejemplo
Le damos un estilo customizado a un boton

* `BackgroundColor` y `className` es de React
* Las `{}` inidica que es de React

    ```tsx
    import { useState } from 'react'
    import './App.css'

    function App() {
    const [count, setCount] = useState(0)
    const style = { /*Esto puede estar en App.css*/
        button : {
            color: blue,
            backgroundColor: grey
        }
    }

    return (
        <>
            <button className="custom-button" style={style.button}onClick={() => setCount((count) => count + 1)}>
                count is {count}
            </button>
        </>
    )
    }

    export default App
    ```

### JSX
* Permite tener lógica de JS en HTML
* La extenxión `.tsx` o `.jsx` devuelve html con lógica ts o js.

### Modulo  CSS
* Todo lo que este dentro de un componente y sus hijos puede utilizar los estilos con un `import "./Archivo.css"` 

### Atomic thinking
* Atomizar las ideas
* Separar y asignar la lógica de los componentes

#### Ejemplo
Separamos la logica del boton

##### Original
En este codigo vemos que el boton tiene logica (ser un contador). 

```tsx title:"App.tsx"
import { useState } from 'react'
import './App.css'

function App() {
  const [count, setCount] = useState(0)

  return (
    <>
        <button onClick={() => setCount((count) => count + 1)}>
            count is {count}
        </button>
    </>
  )
}

export default App
```

##### Refactor

* Podemos agregar estilos inline
```tsx
<button className="custom-button" style={{color: blue, backgroundColor: grey}} onClick={() => setCount((count) => count + 1)}>
    count is {count}
</button>
```

* Podemos crear un componente para los estilos
```tsx
const style = {
    button{
        color: blue,
        backgroundColor: grey,
    }
}

...
function App(){
...

<button className="custom-button" style={style.button} onClick={() => setCount((count) => count + 1)}>
    count is {count}
</button>
```

* Debemos atomizar los componentes
    * El boton solo debe ejecutar un metodo cuando hacen click
    * App.tsx
    * components/
        * Button/
            * Button.css
            * Button.tsx
            * index.ts


Button.css
```css
.custom-button{
    color: blue;
    background-color: grey;
}
```

Button.tsx
```tsx 
import './Button.css' /*Importamos el estilo del boton*/

interface Props{
    label: string,
    parentMethod: () => void
}

export const Button = ({label,parentMethod}: Props) => {
    return (
        <button className="custom-button" onClick={parentMethod}>
            {label}
        </button>
    )
}
```

index.ts
```ts
import * from "./Button/Button.tsx"
```

App.tsx
```tsx
import { useState } from 'react'
import './App.css'
import {Button} from './components'

function App() {
    const [count, setCount] = useState(0)

    const countMore = () => {
        setCount((count) => count + 1)
    }

    return (
        <>
            <Button label={'Count is ${count}`} parentMethod={countMore}>
        </>
    )
}

export default App
```

### Simplifica rutas
* Creamos un indice en `Button/index.ts` para simplificar rutas
```ts
export * from "./Button/Button.tsx"
```

Ruta `import {Button} from './components'`


### Recomendaciones
* Crear una carpeta por cada componente

---

## 💡Ideas clave
* Debemos atomizar las ideas hasta convertirlas en componentes
* Los componentes son la minima unidad de lógica posible
* Existen dos tipos de componentes: dummy y statefull
* El componente dummy carece de estado solo renderiza
* El componente Statefull tiene estado
* El estado es donde se guardan las variables dinámicas que determinan cómo se renderiza un componente
--- 

## ❓Preguntas
* ¿Cuales son los pasos para simplificar las rutas en el import con el `index.ts`?
    1. Crear un index.ts en el componente
    2. Indicar los archivos `.tsx` que se podrán exportar
* ¿Cuales son los pasos para componetizar en React? 
    1. Separar los estilos y la logica
    2. Interactuar con el componente mediante interfaces
---

## ⏪Resumen
Los componentes son la base fundamental de React, por que nos permite atomizar los elementos de la app de forma que sea facil su reutilización y modificación, existiendo dos tipos: dummy y statefull, el primero solo se encarga de renderizar y el siguiente tiene estado. 

El estado almacena las variables que indican como se debe de renderizar el componente. 

Para compenetizar en React debemos separar los estilos y reducir a su minimo la logica de los elementos de la app mediante el proceso de abstracción. Esta abstracción la vamos a guardar en `components/nombre-componente` y vamos a agregar un `index.ts` para facilitar su exportación. 