# Taller: Introducción a React
*María José Fonseca Mendoza - T00065024*
*Desarrollo Front-end - 1807*
## Punto 1. ¿Qué es React?

React es una **librería de JavaScript** utilizada para construir interfaces de usuario, especialmente en aplicaciones web que necesitan mostrar información e interactuar constantemente con el usuario.
\
Su principal función es **facilitar la creación de interfaces dinámicas mediante componentes reutilizables**. Esto permite organizar mejor el código, evitar repeticiones y actualizar partes de la página sin tener que recargarla completamente.
\
Puede utilizarse para desarrollar formularios, menús interactivos, tiendas virtuales, redes sociales y paneles administrativos.


## ¿Quién creó React y en qué año apareció?

React fue creado por **Jordan Walke**, ingeniero de software de Meta. Se utilizó inicialmente dentro de Facebook y posteriormente fue presentado públicamente como proyecto de código abierto en 2013.


## ¿React es una librería o un framework?

React es una librería, porque se especializa principalmente en construir interfaces de usuario, sin imponer una estructura completa para desarrollar aplicaciones.
\
React permite elegir herramientas adicionales para manejar rutas, solicitudes a servidores y otras funcionalidades. En cambio, un framework suele proporcionar soluciones más integradas.


## ¿Qué significa que React sea declarativo?
Significa que el desarrollador indica cómo debe verse la interfaz según los datos actuales, en lugar de programar manualmente cada modificación que debe realizarse sobre la página. 

**Por ejemplo:** En el siguiente codigo declara una función saludo que utiliza el valor de la variable nombre. El desarrollador describe el resultado que quiere mostrar y React se encarga de representarlo en la interfaz.

```
function Saludo() {
  const nombre = "María";

  return <h1>Hola, {nombre}!</h1>;
}
```



## Punto 2. ¿Qué problema resuelve React?
### ¿Cuál era la dificultad de construir interfaces manipulando el DOM manualmente?
Antes de utilizar herramientas como React, los desarrolladores debían modificar directamente el DOM (Document Object Model) utilizando JavaScript. Esto implicaba buscar elementos HTML, cambiar su contenido, modificar atributos y controlar cuándo debían actualizarse.
\
En aplicaciones grandes, estas operaciones podían volverse repetitivas, difíciles de mantener y propensas a errores, especialmente cuando muchos elementos dependían de los mismos datos.
### Diferencia entre enfoque imperativo y declarativo

El enfoque imperativo indica paso a paso cómo realizar una operación. Por otro lado, el enfoque declarativo describe el resultado que se desea obtener.


```
const titulo = document.getElementById("titulo");
titulo.textContent = "Hola, mundo!"; 

```
Aquí se busca manualmente un elemento HTML y se modifica su contenido.


```
function Titulo() {
  return <h1>Hola, mundo!</h1>;
}

```

Aquí simplemente se describe qué elemento debe mostrarse.


### ¿Cómo mantiene React sincronizada la interfaz con el estado?
React utiliza el estado para almacenar información que puede cambiar durante la ejecución de una aplicación. Cuando el estado se actualiza mediante su función correspondiente, React vuelve a renderizar el componente y calcula los cambios necesarios para actualizar la interfaz.

**Ejemplo:** Cada vez que el usuario presiona el botón, el estado numero aumenta y React actualiza automáticamente el texto mostrado.

```
import { useState } from "react";

function Contador() {
  const [numero, setNumero] = useState(0);

  return (
    <button onClick={() => setNumero(numero + 1)}>
      Clics: {numero}
    </button>
  );
}

```


### ¿Qué rol tienen los componentes reutilizables?
Los componentes permiten dividir una interfaz en partes independientes que pueden utilizarse varias veces. Esto ayuda a:
- Evitar la repetición de código.
- Facilitar el mantenimiento.
- Organizar mejor las aplicaciones y mantener una apariencia consistente.


## Punto 3. Principales elementos de React
### 3.1. Componentes
Los componentes son bloques de código reutilizables que representan una parte de la interfaz de usuario. Entre sus características principales se encuentran:

- Se pueden crear mediante funciones de JavaScript.
- Sus nombres comienzan con mayúscula.
- Reciben información mediante props.
- Pueden contener otros componentes.
- Dividen aplicaciones grandes en partes pequeñas.

**Ejemplo:** Declaración de un **componente Bienvenida**, que muestra un título y que luego se utiliza dentro del componente principal **App**

```

function Bienvenida() {
  return <h2>Bienvenido a mi página</h2>;
}

function App() {
  return <Bienvenida />;
}

```

### 3.2. JSX
JSX es una extensión de sintaxis de JavaScript que permite escribir estructuras similares a HTML dentro del código JavaScript.

**Características principales:**
- Facilita la descripción visual de los componentes.
- Permite insertar expresiones JavaScript usando llaves {}.
- Un componente debe devolver un único elemento raíz o un fragmento.
- Se utiliza className en lugar de class para asignar clases CSS.

**Ejemplo:** JSX permite combinar etiquetas similares a HTML con variables JavaScript. En este caso, el nombre de la estudiante aparece dentro de un encabezado.

```
function Usuario() {
  const nombre = "Ana";

  return (
    <div className="perfil">
      <h2>{nombre}</h2>
      <p>Estudiante de ingeniería</p>
    </div>
  );
}

```


### 3.3. Props
Las props son propiedades que permiten enviar información desde un componente padre hacia un componente hijo. 

**Características principales:**
- Permiten personalizar componentes reutilizables.
- Se reciben como argumentos del componente.
- Pueden contener textos, números, objetos y funciones.
- Son de solo lectura para el componente que las recibe.

**Ejemplo:** El componente Saludo recibe una prop llamada nombre. Esto permite reutilizar el mismo componente para mostrar diferentes saludos.

```
function Saludo({ nombre }) {
  return <h2>Hola, {nombre}</h2>;
}

function App() {
  return (
    <div>
      <Saludo nombre="Carlos" />
      <Saludo nombre="Laura" />
    </div>
  );
}

```

### 3.4. Estado (useState)

El estado es la información que un componente necesita recordar y que puede cambiar durante la interacción con el usuario. UseState es un Hook de React que permite declarar una variable de estado y una función para actualizarla.

**Características principales:**
- Permite almacenar valores que cambian.
- Cuando se actualiza el estado, React solicita una nueva renderización.
- Puede almacenar números, cadenas de texto, booleanos, arreglos y objetos.
- Debe utilizarse siguiendo las reglas de los Hooks, normalmente en el nivel superior de un componente.

**Ejemplo:** Inicialmente, el estado encendido es false. Cada vez que se presiona el botón, cambia entre true y false, modificando el texto mostrado.

```

import { useState } from "react";

function Interruptor() {
  const [encendido, setEncendido] = useState(false);

  return (
    <button onClick={() => setEncendido(!encendido)}>
      {encendido ? "Encendido" : "Apagado"}
    </button>
  );
}
```


### 3.5. Eventos (onClick, onChange)
Los eventos permiten ejecutar acciones cuando el usuario interactúa con los elementos de la interfaz.

**Características principales:**
- onClick detecta clics sobre elementos.
- onChange permite responder a cambios en campos de entrada.
- Los eventos se manejan mediante funciones de JavaScript.
- Pueden utilizarse para actualizar el estado de los componentes.

**Ejemplo onClick:** Cuando el usuario presiona el botón, se ejecuta la función mostrarMensaje, que muestra una alerta.

```
function Boton() {
  function mostrarMensaje() {
    alert("¡Botón presionado!");
  }

  return <button onClick={mostrarMensaje}>Presionar</button>;
}
```

**Ejemplo de onChange:** Cada vez que el usuario escribe en el campo, onChange actualiza el estado nombre. React muestra inmediatamente el texto ingresado.

```
import { useState } from "react";

function Formulario() {
  const [nombre, setNombre] = useState("");

  return (
    <div>
      <input
        value={nombre}
        onChange={(e) => setNombre(e.target.value)}
      />
      <p>Hola, {nombre}</p>
    </div>
  );
}
```



## Punto 4. Importancia de React en la industria

La importancia de React radica en la facilidad que ofrece para el desarrollo y mantenimiento de aplicaciones web modernas, especialmente aquellas que requieren interfaces interactivas. 

React permite:

- Reutilización de código: los componentes pueden utilizarse en diferentes partes de una aplicación.
- Modificar componentes sin tener que reescribir toda la interfaz.
- Facilita organizar proyectos que crecen con el tiempo.
- Mejor organización entre programadores al poder trabajar en componentes separados.
- Adminitrar los cambios necesarios en el DOM cuando se modifican los datos.

Estas características hacen que React sea útil para aplicaciones empresariales, plataformas comerciales y servicios digitales.

### ¿Qué aporta React al ecosistema de desarrollo?
React cuenta con un ecosistema de herramientas que complementan sus funcionalidades y permiten desarrollar aplicaciones más completas.


- **Vite:**	Facilita la creación de proyectos y proporciona un servidor de desarrollo rápido.
- **Next.js:**	Framework basado en React que incorpora enrutamiento y opciones de renderizado en servidor.
- **React Router:**	Permite gestionar la navegación entre diferentes páginas o vistas.
- **React DevTools:**	Ayuda a inspeccionar componentes, props y estados durante el desarrollo.
- **React Native**	Permite desarrollar aplicaciones móviles utilizando React.


**Ejemplo:** Creación de proyecto básico utilizando Vite:

```
> npm create vite@latest mi-proyecto -- --template react
> cd mi-proyecto
> npm install
> npm run dev
```

Estos comandos crean un proyecto, instalan sus dependencias e inician un servidor de desarrollo local.

### Qué papel tienen la comunidad y el mantenimiento de React?
React cuenta con una comunidad internacional de desarrolladores que contribuyen con documentación, bibliotecas, herramientas y soluciones a problemas comunes.
Su desarrollo comenzó en Facebook, pero actualmente participan ingenieros de empresas como Meta y Vercel, además de colaboradores independientes.
\
En 2026 se anunció la React Foundation, alojada por la Linux Foundation, como parte de la evolución de la gobernanza del proyecto. Su desarrollo técnico continúa siendo coordinado por colaboradores de distintas organizaciones. 
\
La comunidad también facilita el aprendizaje mediante tutoriales, foros, proyectos de código abierto y documentación oficial.


### ¿Por qué React es relevante para un desarrollador front-end?
Aprender React es importante porque permite desarrollar interfaces modernas y adquirir conocimientos utilizados en numerosos proyectos profesionales. Ayuda también a fortalecer habilidades relacionadas con JavaScript, manejo de estados, arquitectura de componentes y comunicación con APIs.
\
Conocer React también facilita aprender herramientas relacionadas, como Next.js y React Native, ampliando las posibilidades de desarrollo web y móvil.


## Punto 5. Grandes empresas que utilizan React
### 5.1. Meta Platforms
*Facebook, especialmente su interfaz web.*
React nació como una tecnología desarrollada dentro de Facebook para facilitar la construcción de interfaces dinámicas. Facebook es una plataforma con una gran cantidad de elementos interactivos, como publicaciones, comentarios y botones de reacción.
\
El uso de componentes permite organizar estas funcionalidades y facilitar su mantenimiento. Además, Meta utiliza React ampliamente en sus productos, lo que demuestra su capacidad para trabajar en aplicaciones de gran escala.



### 5.2. Airbnb
*Componentes de su plataforma web y herramientas internas de desarrollo.*
Airbnb utiliza React para construir componentes de interfaz y ha desarrollado herramientas propias relacionadas con esta tecnología.
\
React facilita la reutilización de componentes y permite mantener una estructura consistente en aplicaciones complejas. La empresa también ha desarrollado herramientas como visx, una colección de componentes de visualización basados en React. Además, Airbnb ha documentado procesos de migración de miles de pruebas de componentes React, lo que demuestra su utilización a gran escala.

# Referencias bibliográficas. 
La información utilizada para la realización de este taller se extrajo de las siguientes fuentes:
- *React. (s. f.).* Quick Start. https://react.dev/learn
- React. (*s. f.).* Describing the UI. https://react.dev/learn/describing-the-ui
- React. (*s. f.).* useState. https://react.dev/reference/react/useState
- React. (*s. f.).* Responding to Events. https://react.dev/learn/responding-to-events
- React. (*s. f.).* Meet the Team. https://react.dev/community/team
- *Meta Engineering. (2013).* 2013: A Year of Open Source at Facebook. https://engineering.fb.com/2013/12/20/web/2013-a-year-of-open-source-at-facebook/
- *Airbnb Engineering. (s. f.).* visx. https://airbnb.tech/opensource/visx/
- *Airbnb Engineering. (s. f.).* Accelerating Large-Scale Test Migration with LLMs. https://airbnb.tech/infrastructure/accelerating-large-scale-test-migration-with-llms/
- *Vite. (s. f.). Getting Started. https://vite.dev/guide/