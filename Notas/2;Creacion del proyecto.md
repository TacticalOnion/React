# Creación del proyecto 

## 📝 Notas

### Crear proyecto React
1. Instalar bun
    ```shell
    curl https://bun.sh/install | bash
    ```
2. Crear un proyecto con bun
    ```shell
    # Default
    bun create react-app react-app
    # Con Typescript
    bun create vite@latest react-app
    cd react-app
    bun install
    bun run dev
    ```
* Opcional : Ejecutar la app
    ```shell
    cd react-app
    npm start
    ```
3. Separamos la aplición en `/dist`
    ```shell
    bun run build
    ```

### Metadata
Es información extra que agregamos para que los buscadores tengan información sobre la página. 

### Bundler
* Este se encarga
* Proceso
    * Minificar -> Resume el codigo a su minimo
    * Uglyfing -> Ofusca el codigo
    * Treeshacking -> Elimina (En producción) archivos que no son usados
* Vite es un bundler

### /private
Podemos crear una carpeta `private`, la cual tendra componentes que solo los usuarios que esten logeados puedan acceder a los datos. 

* El browser no carga ningun componente de `/private`

### Ecma Script Module
Conjunto de reglas de JS que se crea periodicamente y que siguen los navegadores.

* React permite importar facilmente ES modules y plugins 

    ```react
    import module from '...'
    ```

### Strict mode
Controla la manera en que funcionan los componentes

```tsx title:"main.tsx"
<StrictMode>
    <App />
</StictMode>
```

#### Proceso
1. Crea componente
2. Lo monta (renderizar)
3. Lo rompe
4.  Lo vuelve a cargar
5.  Verifica el estado del componente
    * Verifica que sea igual el estado del componente antes y despues de ser destruido

### CreateRoot
Crea el root (la base) de la app

```tsx title:"main.tsx"
createRoot(document.getElementById('root')!).render
```

### Import
React permite importar metodos especificos facilmente:

```tsx
import { metodo } from "biblioteca";
```

### Arquitectura SPA
```tsx title:"index.html"
<body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
</body>
```

---

## 💡Ideas clave
* Bun nos permite crear proyectos react de forma rapida
* Se debe bundlerizar la aplicación para mejorar su performance y reduce los vectores de ataque al ofuscar el código
    ```shell
    bun run build
    ```
* Los modulos ECMA es el estandar JS de los navegadores
* StrictMode permite identificar fallos pontenciales en el renderizado al renderizarlos dos veces 
* La arquitectura SPA hace que el navegador cargue un solo archivo indes.html, que luego carga el bundle JS como main.tsx dinamicamente en el cliente
* El main.tsx tiene toda la lógica y los componentes

--- 

## ❓Preguntas
* ¿Qué es alacritty?
    * Emulador de terminal acelerado por GPU, escrito en Rust

* ¿Qué es bun?
    * Runtime para JavaScript y TypeScript
* ¿Qué es vite?
    * Bundler y servidor de desarrollo
* ¿Qué es homebrew?
    * Gestor de paquetes de código abierto
* ¿Qué es transpilar? 
    * Transformar código fuente de un lenguaje a otro que tiene un nivel de abstracción similar
* ¿Qué es un bundler? 
    * Herramienta que toma múltiples archivos de código fuente (JavaScript, CSS, imágenes, etc.) y los combina en uno o varios archivos optimizados para ser usados en producción
* ¿Qué es Progressive Web Application? 
    * Es una aplicación web que se instala como app móvil nativa offline  
* ¿Qué es bootstraping?
    * Inicializar una app o carga de componentes base
* ¿Qué hace el export en React?
    * Es la forma en la que un archivo permite que otros archivos puedan acceder a sus funciones, componentes o constantes

---

## ⏪Resumen
Se deben bundlerizar los archivos para mejorar su performance y "seguridad" mediante la minificación, ofuscación (Uglify) y treeshaking.

Aunado a lo anterior React mejora la permormance gracias a los siguientes puntos:

* Importa principalmente modulos ES
* Permite importa solo el codigo que se necesita de bibliotecas
* Sigue la arquitectura SPA: lo que hace que toda la lógica sea gestionada por `main.tsx` (quien importa los componentes, rutas, etc.) y se renderice dinamicamente en `index.html` del lado del cliente
* Tiene herramientas que ayudan al dev para detectar errores a tiempo, por ejemplo `StrictMode`