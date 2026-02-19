> PROGRAMACIÓN MULTIMEDIA Y DISPOSITVOS MÓVILES

# Tema 3: INTEGRACIÓN DE CONTENIDO MULTIMEDIA Y LIBRERÍAS ESPECÍFICAS <!-- omit in toc -->
> Imagen, audio, vídeo, persistencia de datos  
> BIBLIOTECAS


> PROGRAMACIÓN MULTIMEDIA Y DISPOSITVOS MÓVILES

# Tema 3: INTEGRACIÓN DE CONTENIDO MULTIMEDIA Y LIBRERÍAS ESPECÍFICAS <!-- omit in toc -->
> Audio, vídeo, persistencia de datos  
> LIBRERÍAS

- [1. Introducción](#1-introducción)
- [2. Bibliotecas de React útiles para React Native](#2-bibliotecas-de-react-útiles-para-react-native)
  - [2.1. Estado global](#21-estado-global)
    - [2.1.1. useContext](#211-usecontext)
    - [2.1.2. Redux](#212-redux)
    - [2.1.3. Zustand](#213-zustand)
    - [Comparativa](#comparativa)
  - [2.2. Gestión de datos asíncronos](#22-gestión-de-datos-asíncronos)
    - [2.2.1. Tanstack Query](#221-tanstack-query)
      - [Consultas (GET)](#consultas-get)
      - [Mutaciones (POST, PUT, DELETE)](#mutaciones-post-put-delete)
- [3. Contenido multimedia](#3-contenido-multimedia)
  - [3.1. Imagen](#31-imagen)
  - [3.2. Audio](#32-audio)
  - [3.3. Video](#33-video)
- [4. Componentes propios de un dispositivo móvil](#4-componentes-propios-de-un-dispositivo-móvil)
  - [4.1. Cámara](#41-cámara)
  - [4.2. GPS](#42-gps)
  - [4.3. Sensores](#43-sensores)
- [5. Referencias](#5-referencias)



# 1. Introducción

Las aplicaciones móviles modernas no solo gestionan datos y navegación, sino que integran **contenido multimedia**, acceso a **hardware del dispositivo** y comunicación constante con servicios externos. En este tema se abordarán las principales herramientas y bibliotecas que permiten ampliar las capacidades de una aplicación desarrollada con **React Native y Expo**, centrándonos en:

- Gestión del estado global.
- Manejo de datos asíncronos y peticiones a APIs.
- Integración de imágenes, audio y vídeo.
- Acceso a componentes físicos del dispositivo como cámara, GPS y sensores.

El objetivo es comprender cómo estructurar aplicaciones más complejas, escalables y preparadas para entornos reales.



# 2. Bibliotecas de React útiles para React Native

Aunque React Native proporciona una base sólida, en proyectos reales es habitual apoyarse en bibliotecas externas que resuelven problemas comunes como la gestión del estado o la sincronización con servidores.

## 2.1. Estado global

En aplicaciones medianas o grandes es necesario compartir información entre múltiples pantallas y componentes: usuario autenticado, tema visual, carrito de compra, configuración, etc.

Para ello disponemos de 3 métodos, de más antiguo a más moderno son:

### 2.1.1. useContext

`useContext` es una API nativa de React que permite compartir datos sin necesidad de pasar props manualmente por cada nivel del árbol de componentes.

**Ventajas:**
- No requiere librerías externas.
- Fácil de implementar.
- Ideal para estados globales simples (tema, idioma, usuario).

**Limitaciones:**
- No está optimizado para estados muy grandes o altamente dinámicos.
- Puede provocar renders innecesarios si no se estructura correctamente.

Uso típico:
- Crear un `Context`.
- Envolver la aplicación con un `Provider`.
- Consumir los datos mediante `useContext`.


**Ejemplo: Contexto para gestionar el usuario autenticado**

Seguir los 3 pasos siguientes:

1. Crear el Contexto

```js
// UserContext.js
import React, { createContext, useState } from "react"

// 1. Crear el contexto
export const UserContext = createContext()

// 2. Crear el proveedor
export const UserProvider = ({ children }) => {
  const [user, setUser] = useState(null)

  const login = (name) => {
    setUser({ name })
  }

  const logout = () => {
    setUser(null)
  }

  return (
    <UserContext.Provider value={{ user, login, logout }}>
      {children}
    </UserContext.Provider>
  )
}
```

Hemos creado un contenedor global con **`createContext()`**

Hemos creado un componente **`UserProvider`**, el cual mantiene el estado (`user`) y expone los valores mediante la prop `value`.


2. Envolver la aplicación con el Proveedor

```js
// App.js
import React from "react"
import { UserProvider } from "./UserContext"
import HomeScreen from "./HomeScreen"

export default function App() {
  return (
    <UserProvider>
      <HomeScreen />
    </UserProvider>
  )
}
```


Ahora cualquier componente dentro de **`UserProvider`** podrá acceder al contexto.

3. Consumir el contexto con **useContext**

```js
// HomeScreen.js
import React, { useContext } from "react"
import { View, Text, Button } from "react-native"
import { UserContext } from "./UserContext"

export default function HomeScreen() {
  const { user, login, logout } = useContext(UserContext)

  return (
    <View style={{ padding: 20 }}>
      {user ? (
        <>
          <Text>Bienvenido, {user.name}</Text>
          <Button title="Cerrar sesión" onPress={logout} />
        </>
      ) : (
        <>
          <Text>No has iniciado sesión</Text>
          <Button title="Iniciar sesión" onPress={() => login("Carlos")} />
        </>
      )}
    </View>
  )
}
```

Para que acceder a esos valores desde cualquier componente hijo usamos **`useContext(UserContext)`** 


Resultado

- Si el usuario no ha iniciado sesión → aparece botón de login.
- Al pulsarlo → el estado global cambia.
- La UI se actualiza automáticamente en todos los componentes que consuman el contexto.


### 2.1.2. Redux

Redux es una biblioteca de gestión de estado basada en un **store centralizado**, acciones y reducers.

**Características principales:**
- Estado global único.
- Flujo de datos predecible.
- Ideal para aplicaciones grandes.
- Excelente integración con herramientas de depuración.

**Conceptos clave:**
- Store
- Actions
- Reducers
- Dispatch

Es especialmente útil cuando:
- Hay múltiples fuentes de actualización del estado.
- Se necesita trazabilidad de cambios.
- Se trabaja en equipos grandes.


**Ejemplo: Gestionar el usuario autenticado**

Redux requiere más estructura, pero es más robusto y escalable.

Seguir los 5 pasos siguientes:

1. Instalar paquetes

```sh
npm install @reduxjs/toolkit  react-redux
```

2. Crear el *slice*

```js
// userSlice.js
import { createSlice } from "@reduxjs/toolkit";

const userSlice = createSlice({
  name: "user",
  initialState: {
    user: null,
  },
  reducers: {
    login: (state, action) => {
      state.user = { name: action.payload };
    },
    logout: (state) => {
      state.user = null;
    },
  },
});

export const { login, logout } = userSlice.actions;
export default userSlice.reducer;
```

3. Configurar el *store*

```js
// store.js
import { configureStore } from "@reduxjs/toolkit";
import userReducer from "./userSlice";

export const store = configureStore({
  reducer: {
    user: userReducer,
  },
});
```

4. Envolver la *app* con *Provider*

```js
// App.js
import React from "react";
import { Provider } from "react-redux";
import { store } from "./store";
import HomeScreen from "./HomeScreen";

export default function App() {
  return (
    <Provider store={store}>
      <HomeScreen />
    </Provider>
  );
}
```

5. Consumir el estado

```js
// HomeScreen.js
import React from "react";
import { View, Text, Button } from "react-native";
import { useSelector, useDispatch } from "react-redux";
import { login, logout } from "./userSlice";

export default function HomeScreen() {
  const user = useSelector((state) => state.user.user);
  const dispatch = useDispatch();

  return (
    <View style={{ padding: 20 }}>
      {user ? (
        <>
          <Text>Bienvenido, {user.name}</Text>
          <Button title="Cerrar sesión" onPress={() => dispatch(logout())} />
        </>
      ) : (
        <>
          <Text>No has iniciado sesión</Text>
          <Button
            title="Iniciar sesión"
            onPress={() => dispatch(login("Carlos"))}
          />
        </>
      )}
    </View>
  );
}
```

### 2.1.3. Zustand

Zustand es una alternativa ligera a Redux que simplifica la gestión del estado global.

**Ventajas:**
- Sintaxis sencilla.
- No requiere reducers obligatorios.
- Menos configuración inicial.
- Buen rendimiento.

Es una opción recomendable cuando:
- Se desea una solución más simple que Redux.
- La aplicación no requiere una arquitectura excesivamente estructurada.


**Ejemplo: Gestionar el usuario autenticado**

Zustand no necesita `Provider`. El estado se crea como un *hook* global.

Seguir los 3 pasos siguientes:

1. Instalar paquete

```sh
npm install zustand
```

2. Crear el *store*

```js
// userStore.js
import { create } from "zustand"

export const useUserStore = create((set) => ({
  user: null,
  login: (name) => set({ user: { name } }),
  logout: () => set({ user: null }),
}))
```

3. Usarlo en un componente

```js
// HomeScreen.js
import React from "react"
import { View, Text, Button } from "react-native"
import { useUserStore } from "./userStore"

export default function HomeScreen() {
  const { user, login, logout } = useUserStore()

  return (
    <View style={{ padding: 20 }}>
      {user ? (
        <>
          <Text>Bienvenido, {user.name}</Text>
          <Button title="Cerrar sesión" onPress={logout} />
        </>
      ) : (
        <>
          <Text>No has iniciado sesión</Text>
          <Button title="Iniciar sesión" onPress={() => login("Carlos")} />
        </>
      )}
    </View>
  )
}
```

Características de Zustand

- No necesita Provider
- Muy poco *boilerplate*
- Código limpio y directo
- Ideal para proyectos pequeños y medianos


### Comparativa

| Característica            | useContext       | Zustand       | Redux Toolkit |
| ------------------------- | ---------------- | ------------- | ------------- |
| Librería externa          | ❌ No             | ✅ Sí          | ✅ Sí          |
| Necesita Provider         | ✅ Sí             | ❌ No          | ✅ Sí          |
| Boilerplate               | Bajo             | Muy bajo      | Medio         |
| Curva de aprendizaje      | Baja             | Baja          | Media         |
| Escalabilidad             | Media            | Alta          | Muy alta      |
| DevTools avanzadas        | ❌ Limitadas      | ⚠️ Opcional    | ✅ Sí          |
| Arquitectura estructurada | ❌ No obligatoria | ❌ Flexible    | ✅ Sí (Slices) |
| Ideal para                | Estados simples  | Apps medianas | Apps grandes  |

**🎯 Recomendación práctica**

- **useContext** → Ideal para estados globales simples (tema, autenticación básica).
- **Zustand** → Excelente equilibrio entre simplicidad y potencia.
- **Redux Toolkit** → Recomendado para aplicaciones grandes con múltiples dominios de estado.



## 2.2. Gestión de datos asíncronos

Las aplicaciones móviles suelen interactuar con APIs remotas para obtener o enviar información. La gestión manual de estados como `loading`, `error` y `success` puede volverse repetitiva.

### 2.2.1. Tanstack Query

Tanstack Query (antes React Query) es una biblioteca diseñada para la **gestión de datos asíncronos y sincronización con servidores**.

**Funcionalidades destacadas:**
- Cache automática.
- Refetch inteligente.
- Gestión automática de estados de carga y error.
- Reintentos automáticos.
- Actualizaciones en segundo plano.

Beneficios:
- Reduce código repetitivo.
- Mejora la experiencia de usuario.
- Simplifica la sincronización con APIs REST o GraphQL.

Es especialmente útil en aplicaciones que:
- Consumen múltiples endpoints.
- Requieren datos actualizados frecuentemente.
- Necesitan optimización de rendimiento mediante cache.

> [!IMPORTANT]
>
> Tanstack Query no reemplaza al estado global, sino que gestiona el “estado del servidor” (server state), mientras que Redux/Zustand gestionan el “estado de la aplicación” (client state).

Las aplicaciones móviles modernas consumen datos desde APIs externas, bases de datos remotas o servicios en la nube. Esto implica trabajar con **operaciones asíncronas**, como:

- Peticiones HTTP (GET, POST, PUT, DELETE)
- Autenticación con servidor
- Sincronización de datos
- Actualizaciones en tiempo real

En React Native, la forma más básica de gestionar datos asíncronos es mediante:

- `fetch`
- `axios`
- `async/await`
- `useEffect` + `useState`

Ejemplo básico sin librerías externas:

```js
import React, { useEffect, useState } from "react";
import { View, Text, ActivityIndicator } from "react-native";

export default function UsersScreen() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => {
        setUsers(data);
        setLoading(false);
      });
  }, []);

  if (loading) return <ActivityIndicator />;

  return (
    <View>
      {users.map((user) => (
        <Text key={user.id}>{user.name}</Text>
      ))}
    </View>
  );
}
```

> [!CAUTION]
> 
> Problemas de este enfoque
>
> - Gestión manual de loading
> - Gestión manual de errores
> - No hay cache automática
> - No hay refetch inteligente
> - Código repetitivo en cada pantalla
> - Difícil escalabilidad

Para resolver estos problemas existen bibliotecas especializadas como **Tanstack Query**.

Tanstack Query (anteriormente React Query) es una librería diseñada para la gestión avanzada de datos asíncronos y sincronización con servidores.

> [!TIP]
> 
> Su objetivo es:
>
> Facilitar la obtención, almacenamiento en cache, sincronización y actualización de datos remotos.
>


**Ventajas frente a useEffect + fetch**

| Característica                  | useEffect + fetch | Tanstack Query |
| ------------------------------- | ----------------- | -------------- |
| Gestión de loading              | Manual            | Automática     |
| Gestión de errores              | Manual            | Automática     |
| Cache de datos                  | ❌ No              | ✅ Sí           |
| Refetch automático              | ❌ No              | ✅ Sí           |
| Reintentos en error             | ❌ No              | ✅ Sí           |
| Sincronización en background    | ❌ No              | ✅ Sí           |
| Compartir datos entre pantallas | Manual            | Automático     |
| Escalabilidad                   | Media             | Alta           |
| Código repetitivo               | Alto              | Bajo           |


**Instalación**

```sh
npm install @tanstack/react-query
```

**Configuración inicial**

```js
// App.js
import React from "react"
import { QueryClient, QueryClientProvider } from "@tanstack/react-query"
import UsersScreen from "./UsersScreen"

const queryClient = new QueryClient()

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <UsersScreen />
    </QueryClientProvider>
  )
}
```

> [!TIP]
>
> **Cuándo usar Tanstack Query**
>
> - Apps que consumen APIs REST o GraphQL.
> - Aplicaciones con múltiples pantallas que comparten datos.
> - Proyectos que necesitan sincronización constante.
> - Apps con datos que deben mantenerse actualizados.





#### Consultas (GET)

Para consultar datos se usa **`useQuery`**.


```js
// UsersScreen.js
import React from "react"
import { View, Text, ActivityIndicator } from "react-native"
import { useQuery } from "@tanstack/react-query"

const fetchUsers = async () => {
  const response = await fetch("https://jsonplaceholder.typicode.com/users")
  return response.json()
}

export default function UsersScreen() {
  const { data, isLoading, error } = useQuery({
    queryKey: ["users"],
    queryFn: fetchUsers,
  })

  if (isLoading) return <ActivityIndicator />
  if (error) return <Text>Error al cargar usuarios</Text>

  return (
    <View>
      {data.map((user) => (
        <Text key={user.id}>{user.name}</Text>
      ))}
    </View>
  )
}
```

> [!TIP]
> 
> Usa siempre un Identificador único de la consulta. Por ejemplo:
>
> queryKey: ["users"]


**Ventajas del uso de useQuery:**

- Cache automática
  - Guarda los datos en memoria.
  - Evita peticiones innecesarias.
  - Refresca en segundo plano.
  - Comparte datos entre pantallas.
- Refetch automático y selectivo
  - Reejecutar la consulta al volver a la pantalla.
  - Reintentar en caso de error.
  - Actualizar datos en segundo plano.


#### Mutaciones (POST, PUT, DELETE)

Para modificar datos se usa **`useMutation`**.

```js
import { useMutation, useQueryClient } from "@tanstack/react-query"

const queryClient = useQueryClient()

const mutation = useMutation({
  mutationFn: (newUser) =>
    fetch("https://jsonplaceholder.typicode.com/users", {
      method: "POST",
      body: JSON.stringify(newUser),
    }),

  onSuccess: () => {
    queryClient.invalidateQueries(["users"])
  },

})
```


**Ventajas del uso de useMutation:**

- Actualizar el servidor
- Invalidación cache de consultas
- Refrescar automáticamente los datos

> [!TIP]
> 
> **Buenas prácticas**
>
> - Separar funciones de fetch en archivos de servicios.
> - Usar claves de query estructuradas (`["users", userId]`).
> - Invalidar queries tras mutaciones.
> - No usar estado local para datos que provienen del servidor.


# 3. Contenido multimedia

React Native y Expo proporcionan APIs para trabajar con distintos tipos de contenido multimedia.

## 3.1. Imagen

El componente `Image` permite mostrar imágenes locales o remotas.

**Fuentes posibles:**
- Archivos locales.
- URLs externas.
- Recursos estáticos.

Aspectos importantes:
- Control del tamaño mediante estilos.
- Uso de `resizeMode`.
- Optimización de rendimiento.
- Manejo de carga y errores.

Expo facilita además la selección de imágenes desde la galería del dispositivo mediante módulos específicos.



## 3.2. Audio

Para trabajar con audio (reproducción o grabación), Expo proporciona módulos específicos.

Casos de uso:
- Reproductores de música.
- Notas de voz.
- Efectos de sonido.
- Podcasts.

Funcionalidades habituales:
- Reproducir, pausar y detener.
- Control de volumen.
- Gestión del estado de reproducción.
- Reproducción en segundo plano (según configuración).

Es importante gestionar correctamente:
- Permisos.
- Ciclo de vida del componente.
- Liberación de recursos.



## 3.3. Video

La reproducción de vídeo permite integrar contenido educativo, promocional o multimedia interactivo.

Características habituales:
- Reproducción desde archivo local o URL.
- Controles personalizados.
- Modo pantalla completa.
- Streaming.

Aspectos a considerar:
- Consumo de datos.
- Rendimiento en dispositivos de gama baja.
- Gestión del buffer.
- Orientación de pantalla.



# 4. Componentes propios de un dispositivo móvil 

Uno de los mayores atractivos de las aplicaciones móviles es el acceso al hardware del dispositivo.

## 4.1. Cámara

Permite:
- Tomar fotografías.
- Grabar vídeo.
- Escanear códigos QR.

Requiere:
- Solicitud explícita de permisos.
- Gestión de estados (cámara activa/inactiva).
- Manejo seguro de archivos generados.

Usos comunes:
- Aplicaciones sociales.
- Escaneo de documentos.
- Realidad aumentada.
- Identificación mediante QR.



## 4.2. GPS

El acceso a la geolocalización permite:

- Obtener ubicación actual.
- Seguimiento en tiempo real.
- Mostrar mapas.
- Calcular distancias.

Aspectos importantes:
- Permisos en primer y segundo plano.
- Consumo de batería.
- Precisión (alta vs. balanceada).
- Privacidad del usuario.

Aplicaciones típicas:
- Delivery.
- Deportes.
- Transporte.
- Mapas y turismo.



## 4.3. Sensores

Los dispositivos móviles incorporan múltiples sensores:

- Acelerómetro.
- Giroscopio.
- Magnetómetro.
- Sensor de luz.
- Sensor de proximidad.

Permiten crear:
- Juegos interactivos.
- Aplicaciones de actividad física.
- Experiencias inmersivas.
- Interfaces basadas en movimiento.

Es fundamental:
- Controlar la frecuencia de actualización.
- Minimizar el consumo energético.
- Liberar suscripciones al desmontar componentes.



# 5. Referencias

- [Colección de demos realizada con Reanimated, Gesture Handler y Skia](https://github.com/enzomanuelmangano/demos)
- [Documentación de React Native Skia](https://shopify.github.io/react-native-skia/docs/getting-started/installation)
- [Tutoriales de React Native Skia](https://shopify.github.io/react-native-skia/docs/tutorials)
- [Build Expo apps for TV](https://docs.expo.dev/guides/building-for-tv/)
