# ¿Cuando usar React Vanilla y Frameworks?

## 📝 Notas
### Sobre React
* React es una biblioteca de JavaScript
* React surge como una alternatica a Client Site Rendering
* React es una biblioteca sirve para generar aplicaciones basadas en componentes

### Arquitectura
* Arquitectura VMC
    * View          Muestra lo que hay en la pantalla
    * Model         Guarda los datos
    * Controller    Aplica las reglas de negocio
* Arquitectura de React
    * Modelo-Vista y Vista-Modelo 
    * El controller no es el unico que puede modificar los datos

### Elementos
* Componente
    * HTML -> puede modificar el modelo ⭐
    * CSS
    * JS/TS
* Controller
    * TS -> Modifica el modelo -> Se ve en la vista
    * La vista puede modificar el modelo
    * Dual binding?

### Ventaja clave de React
* No es verboso

### ¿Cuándo usar React Vanilla?
* Para hacer apps a medida
* Para evitar usar codigo innecesario de frameworks mas complejos
* Cuando se quiere minimizar el peso de la app
* Para realizar prototipado
* Para realizar SPA

### Frameworks de React
* SolidJS
    * ✅ Ideal de React
    * ❌ No tiene oferta laboral
* NextJS
    * ✅ Ideal para apps privadas y públicas (buen SEO)
    * ➖ Enfocado en Server Side Rendering 
* Remix
    * ✅ Tiene buen performance, SEO y routing
    * ➖ Enfocado en SRR
    * ❌ No hay oferta laboral

---

## 💡Ideas clave
* React es una biblioteca de JS
* React sigue una arquitectura orientada a los componentes (MV-VM)
* El caso de uso de React son las SPA y llos prototipos
* Recomendación: Iniciar el prototipado con React y luego integrar frameworks 

--- 

## ❓Preguntas
* ¿Qué es dual binding? 
    * Se refiere a una sincronización bidireccional entre el estado de la aplicación y la interfaz de usuario
    * Funcionamiento
        * El valor de un elemento del formulario (como un <input>) está controlado por el estado de React
        * Cuando el usuario modifica el valor del input, se dispara un evento onChange que actualiza el estado
        * Al actualizar el estado, React re-renderiza el componente y actualiza el valor del input
        
---

## ⏪Resumen
React es una biblioteca JS que utiliza la arquitectura MV y VM que esta orientada Componentes, esta aquitectura se se caracteriza por hacer que los controladores no sean los unicos que pueden modificar datos, lo cual permite simplicidad y flexibilidad en el desarrollo de paginas web. 

Su flexibilidad hace que sea ideal para SPA y prototipos. 

