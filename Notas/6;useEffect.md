# useEffect

## 📝 Notas
App.tsx
```tsx
import {useState} from 'react'
import './App.css'

function App(){
    /*Estados*/
    const [data, setData] = useState([])
    const [loading, setLoading] = useState(false)
    const [error, setError] = useState("")

    /*Metodos*/
    const consoleLoader = (loadingValue: boolean) => {
        setLoading(loadingValue)
        console.info(loading)
    }
    const fetchData = async () => {
        consoleLoader(true)
        try {
            const response = await fetch("https://api.example.com/data")
            if (!response.ok){
                throw new Error("Error al obtener datos")
            }
            const jsonData = await response.json()

            setData(jsonData)
        } catch (err){
            console.error(err as string)
        } finally {
            consoleLoader(false)
        }
    }

    /*Hook*/
    useEffect(() => {  
        fetchData()
    }, []) /*Arreglo de dependencias*/

    if(loading){
        return <div>Cargando</div>
    }

    if(error){
        return <div>Hay un error : {error} </div>
    }

    return(
        <div>{JSON.stringify(data)}</div>

    )
}

export default App
```

### Endpoint
Es una entidad externa al componente

### useEffect
* ❌ No controla el ciclo de vida del componente
* Se utiliza para sincronizar con entidades externas
    * Endpoints
    * Parametros de entrada
    * Ejecución asincrona
* Se ejecuta cuando se monta el componente
* Se ejecuta cada vez que se modifique uno de los valores del State
    * El que esta en el arreglo de dependencias
    * Cuando no se indica el arreglo de dependencias se ejecuta cada vez que cambie cualquier valor de los states
* El `return () => {}` se utiliza para manejar el estado de la memoria
    * En especial en funciones asincronas
    * Se ejecuta cada vez que el componente muera
* Se puede usar +1 useEffect a la vez
* Debemos siempre mantener los estados, metodos y hooks por separado

#### Arreglo de dependencias
* Es un trigger del hook
* Cada vez que una dependencia cambie se ejecuta el hook

### Hook
* Los hooks inicia con use
* Engancha un estado de la aplicación
* Da la posibilidad de acceder y modificar el estado


#### Tipos
* Nativo
* Custom

### useCallBack
* Se asegura de que la referencia a un meotodo va a ser exactamente la misma siempre y cuando no cambie algo

```tsx
import {useState} from 'react'
import './App.css'

function App(){
    /*Estados*/
    const [data, setData] = useState([])
    const [loading, setLoading] = useState(false)
    const [error, setError] = useState("")

    /*Metodos*/
    const consoleLoader = useCallbac((loadingValue: boolean) => {
        setLoading(loadingValue)
        console.info(loading)
    }, [loading])

    const fetchData = useCallback(
        async () => {
            consoleLoader(true)
            try {
                const response = await fetch("https://api.example.com/data")
                if (!response.ok){
                    throw new Error("Error al obtener datos")
                }
                const jsonData = await response.json()

                setData(jsonData)
            } catch (err){
                console.error(err as string)
            } finally {
                consoleLoader(false)
            }
        },[consoleLoader])

    /*Hook*/
    useEffect(() => {  
        fetchData()
    }, [fetchData]) /*Arreglo de dependencias*/

    if(loading){
        return <div>Cargando</div>
    }

    if(error){
        return <div>Hay un error : {error} </div>
    }

    return(
        <div>{JSON.stringify(data)}</div>

    )
}

export default App

```

---

## 💡Ideas clave
* useEffect es un hook que permite ejecutar efectos en componentes
* Un efecto es una operación secundaria
* Ejemplos operaciones secundarias: llamadas a APIs, manipulación del DOM, temporizadores, etc. 
* Un endpoint es una entidad externa al componente
* A algunos hooks se les debe de especificar su trigger mediante un arreglo de dependencias
* `useSte` o `usRef` son hooks que no necesitan arreglos de dependencias
* El arreglo de dependencias le indica a React cuando debe ejecutar un efecto según cambie un valor
* El arreglo de dependencias optimiza el uso de recursos de los hooks
* El arreglo de dependencias regula la reactividad del hook
* Podemos usar `useCallback` para memorizar funciones que dependen de datos externos, evitando que se redefinan en cada render y causando renders innecesarios en componentes hijos
* Se puede utilizar mas de un hook a la vez en un componente funcional


--- 

## ❓Preguntas
* ¿Qué es un arreglo de dependencias?
    * Lista de valores que le indican a React cuándo debe ejecutar el efecto o memorizar el valor. 
    * Es la forma en al que se controla su reactividad
* ¿En que casos se debe usar callback?
    *  Cuando se necesita memorizar una función para evitar que se vuelva a crear en cada renderizado
        * Pasar funciones como props a componentes hijos optimizados
        * Mantener la misma referencia de función entre renders
        * Evitar calculos costosos indirrectamente 
* ¿En que casos no se debe usar callback?
    * La función pasa como prop
    * La función se usa como dependencia
* ¿Qué es la reactividad? 
    * Capacidad del sistema de actualizar la UI automaticamente ante cambios de estado o datos
    * Activación
        * Cambios de estado
        * Cambios de props
        * Cambios de contexto
        * Cambios de valores derivados
* ¿Un efecto es lo mismo que un hook?
    | Hook | Effect |
    | --- | --- |
    |  Función que permite usar características de React dentro de componentes funcionales | Operación que interactua con entendidas externas |
* ¿Por qué no todos los hooks tienen arreglo de dependencias? 
    * Porque no todos necesitan “reaccionar” a cambios en valores externos

---

## ⏪Resumen
Los hooks son funciones que permiten regular la reactividad de un componente funcional, su reactividad puede derivarse de: 

* Cambios de estado (`useState`, `useReducer`)
* Cambios de props (cuando el componente recibe nuevos valores)
* Cambios de contexto (`useContext`)
* Cambios de valores derivados (u`seMemo`, `useCallback`) 

Si el cambio depende de alguna entidad externa al componente (como une efecto en `useEffect`) se les especifica estas dependencias mediante un arreglo de dependencias, la cual le indica a React cuando debe ejecutar la lógica de un hook. 

Además  los hooks pueden usar variables y funciones del componente, los cuales si dependen de datos externos y deben manternese entre renderizados, se les puede encapsular dentro de un `useCallback` para evitar que se redefinan en cada renderizado.