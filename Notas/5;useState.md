# useState

## 📝 Notas
### useState
* Usestate permite conectar el render y el contenido de la función
También posee un metodo para cambiar el valor de una variable

### Ejemplo
En este ejemplo la variable local no hace un cambio de estado, por lo cual no se renderiza el valor que tiene

```tsx
import { useState } from 'react'
import './App.css'
import {Button} from './components'

function App() {
    let localCount = 0;
    const [count, setCount] = useState(0)

    const countMore = () => {
        setCount((count) => count + 1)
    }

    const increaseLocalCount = () => {
        localCount = localCount + 1;
    }

    return (
        <>
            /*❌No funciona*/
            <Button label={'Count is ${count}`} parentMethod={increaseLocalCount}>
            

            /*✅Si funciona*/
            <Button label={'Count is ${count}`} parentMethod={countMore}>
        </>
    )
}

export default App
```

#### Funcionamiento
El siguiente código es una abstracción de como funciona state

```ts
class useState {
    value: any;

    get () {
        return this.value
    }

    set (value: any) {
        this.value = value
    }
}
```
### Batching
Agrupar múltiples actualizaciones de estado para ejecutar un solo renderizado en lugar de varios.

Solo se ejecuta 1 vez 
Por que solo esta consultando el valor (get) no esta haciendo cambios en el render (set)
```ts
setCount(count + 1)
setCount(count + 1)
setCount(count + 1)
setCount(count + 1)
setCount(count + 1)
```

Se ejecuta muchas veces
Por que ejecuta un metodo: (count)
```ts
setCount((count) => count + 1 )
setCount((count) => count + 1 )
setCount((count) => count + 1 )
```

---

## 💡Ideas clave
* useState es un hook
* useState mantienen el estado entre renderizados
*  useState permite conectar el render y el contenido de la función
* El batching agrupa multiples actulizaciones de estado en un solo render y solo ejecuta multiples actulizaciones si se utiliza setState el cual provoca el renderizado
* useState devuelve el valor actual del estado y una función para actualizarlo
--- 

## ❓Preguntas
* ¿Qué es un hook en react?
    * Función especial que te permite “enganchar” funcionalidades de React (como estado, ciclo de vida, contexto, etc.) dentro de componentes funcionales — sin necesidad de usar clases
* ¿Qué es un string template en JS? 
    * Forma moderna de escribir cadenas de texto en JS `Texto ${variable}, un poco mas de texto`
* ¿En que caso se utiliza useState?
    * Se utiliza cuando necesitas mantener y actualizar valores dinámicos dentro de un componente funcional, y quieres que esos cambios se reflejen automáticamente en el render
---

## ⏪Resumen
useState es un hook de React que permite mantener y actualizar valores dinámicos dentro de un componente funcional. Estos valores se preservan entre renderizados, y al actualizarlos con su función setState, React vuelve a renderizar el componente para reflejar los cambios.

Este proceso de re-render se ve optimizado gracias al batching, una técnica que React utiliza para agrupar múltiples actualizaciones de estado en una sola operación de renderizado. Así, solo se renderiza cuando se detectan cambios efectivos en el estado, mejorando el rendimiento de la aplicación.