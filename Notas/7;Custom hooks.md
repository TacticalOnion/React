# Custom hooks

## 📝 Notas
1. Crear `./hooks`
2. Crear `useFetch.ts`

* App.tsx
* /hooks
    * useFetch.ts
    * index.ts

3. Agregar la logica de `useFetch`
useFetch.ts
```ts
import { useEffect, useState} from "react";

type Data<T> = T | null;
type ErrorType = Error | null;

interface Params<T>{
    data: Data;
    loading: boolean;
    error: ErrorType;
}

export const useFetch = <T>(url: string): Params<T> => {
    const [data, setData] = useState<Data<T>>(null)
    const [loading, setLoading] = useState(true)
    const [error, setError] = useState<ErrorType>(null)

    useEffect(() => {
        let controller = new AbortController()
        setLoading(true)

        const fetchData = async () => {
            try {
                const response = await fetch(url, controller)

                if (!response.ok){
                    throw new Error("Error en la perición")
                }

                const jsonData: T = await response.json()
                setData(jsonData)
                setError(null)

            }catch (err){
                setError(err as Error)

            }finally{
                setLoading(false)
            }
        }

        fetchData();

        return () => {
            controller.abort()
        }

    }, [url])

    return { data, loading, error }
}

useFetch<User>()

```

4. Acortar el path de `useFetch`
index.ts
```ts
export * from './useFetch'
```

5. Utilizar el hook en el componente
App.tsx
```tsx
import {useState} from 'react'
import './App.css'

const url = "https://api.example.com/data";

interface Data{
    name: string;
    lastName: string;
    age: number;
}

function App(){
    const {data, error, loading} = useFetch<Data>(url)

    if(loading){
        return <div>Cargando</div>
    }

    if(error){
        return <div>Hay un error : {error.message} </div>
    }

    return(
        <div>{JSON.stringify(data)}</div>
    )
}

export default App
```

---

## 💡Ideas clave
* Los custom hooks nos ayudan moduralizar, reutilizar o encapsular lógica de componentes
* Los genéricos de TS permiten desacoplar la lógica del hook del tipo de datos específico que se maneja
* Los custom hooks permiten mantener limpio el codigo del componente
* Los custom hooks deben utilizar hooks nativos para mantener la reactividad del componente, sino solo son funciones locales

--- 

## ❓Preguntas
* ¿Qué es un generico en TS?
    *  Forma de crear componentes reutilizables que funcionan con tipos variables
* ¿Cuándo debemos crear un custom hook? 
    * Cuando se necesite modular, reutilizar o encapsular lógica basada en hooks, sin sacrificar la claridad del componente
* ¿Cuales son los pasos para crear un custom hook? 
    1. Identificar la lógica repetida
    2. Crear un hook con el prefijo `use` en `./hooks`
    3. Construir la lógica del hook, utilizando los hooks nativos como `useState`, `useEffect`, etc. 
    4. Crear el `index.ts` dentro de `./hooks` para acortar su path al importarlo
    5. Utilizar el hook creado en el componente

---

## ⏪Resumen
Los custom hooks son funciones que permiten modularizar, reutilizar o encapsular lógica relacionada con hooks dentro de los componentes. Para que conserven su carácter reactivo, deben utilizar al menos un hook nativo de React (useState, useEffect, etc.). 

Una buena practica al crear hooks es organizarlos en un directorio `./hooks` con su respectivo indice `index.ts`, ademas de utilizar genericos en TS para desacoplarlos de los tipos de datos del componente. 