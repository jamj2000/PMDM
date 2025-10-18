> PROGRAMACIÓN MULTIMEDIA Y DISPOSITVOS MÓVILES

# Tema 2: DESARROLLO DE APLICACIONES PARA DISPOSITIVOS MÓVILES <!-- omit in toc -->
> Desarrollo usando React Native y Expo  
> COMPONENTES


- [1. Introducción](#1-introducción)
- [2. React Native](#2-react-native)
  - [2.1. Componentes incorporados en React Native](#21-componentes-incorporados-en-react-native)
    - [2.1.1. Componentes de Interfaz de Usuario](#211-componentes-de-interfaz-de-usuario)
    - [2.1.2. Componentes de Interacción](#212-componentes-de-interacción)
    - [2.1.3. Componentes de Utilidad](#213-componentes-de-utilidad)
  - [2.2. Estilos](#22-estilos)
    - [2.2.1. Ejemplo básico:](#221-ejemplo-básico)
    - [2.2.2. Características principales:](#222-características-principales)
  - [2.3. Plataforma](#23-plataforma)
    - [2.3.1. Propiedades:](#231-propiedades)
    - [2.3.2. Métodos útiles](#232-métodos-útiles)
- [3. Expo](#3-expo)
  - [3.1. Componentes básicos de RN (UI y estructura)](#31-componentes-básicos-de-rn-ui-y-estructura)
  - [3.2. Visuales y multimedia](#32-visuales-y-multimedia)
  - [3.3. APIs de hardware y sensores](#33-apis-de-hardware-y-sensores)
  - [3.4. APIs del sistema](#34-apis-del-sistema)
  - [3.5. Servicios y utilidades](#35-servicios-y-utilidades)
  - [3.6. Configuración y desarrollo](#36-configuración-y-desarrollo)
  - [3.7. Extras útiles para desarrolladores](#37-extras-útiles-para-desarrolladores)
- [4. Referencias](#4-referencias)


---



# 1. Introducción


# 2. React Native

## 2.1. Componentes incorporados en React Native

En React Native, los componentes incorporados (también llamados `built-in components`) son bloques básicos proporcionados por el propio framework para construir interfaces móviles. Estos encapsulan elementos nativos de iOS y Android y permiten construir apps sin escribir código específico para cada plataforma.

A continuación se muestra una lista breve de los más comunes.


### 2.1.1. Componentes de Interfaz de Usuario

- **`View`**  
  Contenedor básico para diseños. Similar a una `<div>` en HTML. Se usa para agrupar y posicionar otros componentes.

- **`Text`**  
  Muestra texto. Todo contenido textual debe ir dentro de un componente `Text`.

- **`Image`**  
  Muestra una imagen desde una URL o archivo local.

- **`TextInput`**  
  Campo de entrada de texto. Permite al usuario escribir texto, como formularios o búsquedas.

- **`ScrollView`**  
  Contenedor desplazable. Útil cuando el contenido excede el tamaño de la pantalla.

- **`FlatList`**  
  Lista optimizada para grandes cantidades de datos. Más eficiente que `ScrollView` para listas largas.

- **`SectionList`**  
  Lista agrupada por secciones. Ideal para datos organizados, como listas de contactos.


### 2.1.2. Componentes de Interacción

- **`Button`**  
  Botón básico que ejecuta una acción al ser presionado.

- **`TouchableOpacity`**  
  Detecta toques y reduce su opacidad al presionar. Ideal para crear botones personalizados.

- **`TouchableHighlight`**  
  Similar a `TouchableOpacity`, pero muestra un efecto de resaltado al presionar.

- **`Pressable`**  
  Componente moderno y flexible para detectar distintas interacciones táctiles.


### 2.1.3. Componentes de Utilidad

- **`SafeAreaView`**  
  Evita que el contenido se superponga con áreas del sistema (como la muesca o la barra de estado).

- **`ActivityIndicator`**  
  Muestra un indicador de carga (spinner).

- **`Modal`**  
  Muestra una ventana emergente sobre la interfaz principal.

> [!TIP]
>
> Todos estos componentes se pueden estilizar usando el sistema de estilos de React Native (`StyleSheet`) o bibliotecas externas como `styled-components` .



## 2.2. Estilos


En React Native, **StyleSheet** es un módulo que se usa para definir y organizar los estilos de los componentes, de forma similar al CSS en la web, pero adaptado al entorno móvil.

En lugar de escribir CSS tradicional, **en React Native se usan objetos de JavaScript para aplicar estilos**. StyleSheet ayuda a:

- Crear estilos más legibles y reutilizables.
- Validar propiedades de estilo, mostrando advertencias si usas una que no es válida.
- Optimizar el rendimiento, ya que internamente convierte los estilos en una representación más eficiente para que el motor nativo los procese.

### 2.2.1. Ejemplo básico:

```js
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.texto}>Hola, React Native!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1, 
    justifyContent: 'center', 
    alignItems: 'center', 
    backgroundColor: '#f5f5f5'
  },
  texto: {
    fontSize: 20, 
    color: 'blue'
  }
});
```

### 2.2.2. Características principales:

- **Sintaxis tipo objeto**: Los estilos se definen como objetos de JS.
- **Unidades implícitas**: No se usan px, todos los valores numéricos se interpretan como píxeles independientes de la densidad.
- **Soporta herencia limitada**: No hay cascada como en CSS tradicional. Cada componente recibe explícitamente sus estilos.
- **Composición de estilos**: Puedes pasar un array a style para combinar varios estilos:


```js
<Text style={[styles.texto, styles.destacado]}>Texto</Text>
```

👉 En resumen: StyleSheet en React Native es la forma recomendada de definir estilos optimizados y estructurados para tus componentes, reemplazando el uso de CSS tradicional.



## 2.3. Plataforma

En React Native, el objeto **`Platform`** se utiliza para hacer que el código sea específico para una plataforma determinada, como **iOS** o **Android**. Esto es útil cuando deseas que ciertos fragmentos de código se ejecuten solo en una plataforma en particular, sin tener que escribir código completamente diferente para cada plataforma.

### 2.3.1. Propiedades:

- **`Platform.OS`**  
  Retorna una cadena que representa la plataforma en la que se está ejecutando la aplicación. Puede ser:
  - `'ios'` — para dispositivos iOS.
  - `'android'` — para dispositivos Android.
  - `'web'` — si está ejecutándose en un navegador web (en caso de usar React Native Web).
  

```javascript
  if (Platform.OS === 'ios') {
    // Código específico para iOS
  } else if (Platform.OS === 'android') {
    // Código específico para Android
  }
```

- **`Platform.Version`**  

Retorna la versión del sistema operativo de la plataforma. Por ejemplo:

- En **iOS**, esto podría devolver algo como 14.0.
- En **Android**, devolvería una versión como 9 (correspondiente a Android Pie).

```js
console.log(Platform.Version);  // iOS: "14.0" o Android: 9
```

También puedes verificar versiones específicas del sistema operativo para hacer ajustes más detallados. Esto es útil si deseas implementar características solo en ciertas versiones de la plataforma.

```js
if (Platform.OS === 'ios' && parseInt(Platform.Version, 10) >= 12) {
  // Implementar nueva funcionalidad solo para iOS 12 y versiones posteriores
}
``` 
### 2.3.2. Métodos útiles

- **`Platform.select()`**
Permite seleccionar diferentes valores según la plataforma, de forma más limpia y concisa que un `if/else` o un `switch`.

Esto es útil cuando quieres aplicar un estilo diferente según la plataforma.

```js
const styles = StyleSheet.create({
  container: {
    padding: Platform.select({
      ios: 20,
      android: 10,
      default: 15,  // valor por defecto
    }),
  },
});
```

**Ejemplo**

```js
import React from 'react';
import { Platform, Text, View, StyleSheet } from 'react-native';

const PlatformExample = () => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>
        {Platform.OS === 'ios'
          ? 'Estás en un dispositivo iOS'
          : 'Estás en un dispositivo Android'}
      </Text>
      <Text>Versión del sistema operativo: {Platform.Version}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: Platform.select({
      ios: 20,
      android: 10,
      default: 15,
    }),
  },
  text: {
    fontSize: 18,
    color: Platform.OS === 'ios' ? 'blue' : 'green',
  },
});

export default PlatformExample;
``` 

Casos comunes para usar `Platform`:

- **Cambios en el diseño**: Puedes aplicar estilos diferentes según si la aplicación se está ejecutando en un dispositivo iOS o Android, ya que los tamaños de pantalla, las barras de estado y las áreas seguras pueden ser diferentes.

```js
const styles = StyleSheet.create({
  button: {
    backgroundColor: Platform.OS === 'ios' ? 'blue' : 'green',
  },
});
```

- **Comportamiento específico de la plataforma**: En algunas ocasiones, ciertas funcionalidades pueden requerir lógica diferente para iOS y Android. Por ejemplo, las notificaciones, los permisos o el manejo de la barra de estado pueden necesitar un tratamiento distinto.

```js
return (
  <View>
    {Platform.OS === 'ios' ? (
      <Text>Bienvenido iOS</Text>
    ) : (
      <Text>Bienvenido Android</Text>
    )}
  </View>
);
```

- **Comodidad para mantener código limpio**: Usar `Platform.select()` hace que tu código sea más limpio y fácil de leer, especialmente cuando solo necesitas aplicar variaciones pequeñas dependiendo de la plataforma.



# 3. Expo

Expo es el framework recomendado para desarrollar aplicaciones de React Native.

Podemos usar los componentes proporcionados por react-native más muchos otros que ofrece el framework Expo. La lista con los más importantes es la siguiente:

## 3.1. Componentes básicos de RN (UI y estructura)
| Componente                       | Descripción                                         |
| -------------------------------- | --------------------------------------------------- |
| `View`                           | Contenedor básico para diseño y layout.             |
| `Text`                           | Muestra texto.                                      |
| `Image`                          | Renderiza imágenes locales o remotas.               |
| `ScrollView`                     | Contenedor con desplazamiento.                      |
| `FlatList` / `SectionList`       | Listas optimizadas para grandes volúmenes de datos. |
| `SafeAreaView`                   | Respeta márgenes seguros en pantallas con notch.    |
| `Pressable` / `TouchableOpacity` | Detectan toques y gestos del usuario.               |
| `TextInput`                      | Campo de texto editable.                            |
| `Button`                         | Botón estándar.                                     |

## 3.2. Visuales y multimedia
| Módulo                   | Descripción                               |
| ------------------------ | ----------------------------------------- |
| `expo-image`             | Carga optimizada de imágenes.             |
| `expo-audio`             | Reproducción de audio.                    |
| `expo-video`             | Reproducción de video.                    |
| `expo-blur`              | Efecto de desenfoque sobre vistas.        |
| `expo-linear-gradient`   | Gradientes de color.                      |
| `expo-video-thumbnails`  | Genera miniaturas de videos.              |
| `expo-image-manipulator` | Redimensionar, recortar o rotar imágenes. |

> [!NOTE]
>
> Existe un componente **`Image`** tanto en el paquete `react-native` como en el paquete `expo-image`. La diferencia entre Image de React Native e Image de Expo (en el paquete expo-image) es importante, especialmente en temas de rendimiento, caché y funcionalidad avanzada.
>
> # Comparativa: `Image` (React Native) vs `expo-image` (Expo)
> 
> | Característica | `Image` (React Native) | `expo-image` (Expo) |
> |----------------|------------------------|----------------------|
> | **Importación** | `import { Image } from 'react-native';` | `import { Image } from 'expo-image';` |
> | **Rendimiento** | Básico, sin optimización de carga ni cacheo. | Mucho más rápido gracias a un *pipeline nativo optimizado*. |
> | **Caché de imágenes** | No tiene caché nativo (se recarga cada vez). | Soporta **caché persistente** y controlada. |
> | **Formatos soportados** | PNG, JPG, WebP (parcialmente). | PNG, JPG, WebP, HEIC, GIF, AVIF (dependiendo de la plataforma). |
> | **Placeholders / Loading** | No tiene soporte nativo (debes simularlo). | Soporta *placeholders*, *blurHash*, *transiciones de fade*, etc. |
> | **Transiciones / efectos** | Limitado a estilos CSS básicos. | Transiciones nativas suaves (fade-in, blur al cargar, etc.). |
> | **Escalado y resize** | Propiedad `resizeMode`. | Propiedad `contentFit`, con más opciones y comportamiento consistente. |
> | **Soporte de animaciones** | Animaciones con librerías externas (como `Animated`). | Incluye transiciones integradas y soporte  para animaciones ligeras. |
> | **Consumo de memoria** | Mayor, especialmente con imágenes grandes. | Optimizado con *streaming y downsampling nativo*. |
> | **Compatibilidad web** | Soporte básico en Expo Web. | Mejor integración con Expo Web (usa `<img>` debajo). |
>
>


## 3.3. APIs de hardware y sensores
| Módulo            | Descripción                                                |
| ----------------- | ---------------------------------------------------------- |
| `expo-camera`     | Uso de cámara (fotos, videos, escáner QR).                 |
| `expo-location`   | Geolocalización y GPS.                                     |
| `expo-sensors`    | Acceso a acelerómetro, giroscopio, barómetro, etc.         |
| `expo-battery`    | Nivel y estado de la batería.                              |
| `expo-device`     | Información del dispositivo (modelo, sistema, fabricante). |
| `expo-network`    | Conectividad de red.                                       |
| `expo-haptics`    | Vibraciones y respuesta háptica.                           |
| `expo-brightness` | Control de brillo de pantalla.                             |
| `expo-motion`     | Detección de movimiento y orientación.                     |

## 3.4. APIs del sistema
| Módulo                      | Descripción                                    |
| --------------------------- | ---------------------------------------------- |
| `expo-contacts`             | Acceso a contactos del dispositivo.            |
| `expo-calendar`             | Lectura y escritura de eventos del calendario. |
| `expo-notifications`        | Notificaciones locales y push.                 |
| `expo-sharing`              | Compartir archivos con otras apps.             |
| `expo-file-system`          | Lectura y escritura en el sistema de archivos. |
| `expo-clipboard`            | Acceso al portapapeles.                        |
| `expo-speech`               | Texto a voz (TTS).                             |
| `expo-local-authentication` | Autenticación biométrica (Face ID, Touch ID).  |

## 3.5. Servicios y utilidades
| Módulo              | Descripción                                    |
| ------------------- | ---------------------------------------------- |
| `expo-asset`        | Gestión de recursos como imágenes y fuentes.   |
| `expo-font`         | Carga de tipografías personalizadas.           |
| `expo-linking`      | Manejo de enlaces profundos (deep linking).    |
| `expo-auth-session` | Autenticación OAuth (Google, Facebook, etc.).  |
| `expo-secure-store` | Almacenamiento seguro (tokens, contraseñas).   |
| `expo-updates`      | Actualizaciones OTA (sin pasar por App Store). |
| `expo-random`       | Generación de números aleatorios seguros.      |
| `expo-crypto`       | Funciones criptográficas (hash, HMAC, etc.).   |
| `expo-storage`      | Almacenamiento persistente local.              |

## 3.6. Configuración y desarrollo
| Módulo                  | Descripción                                            |
| ----------------------- | ------------------------------------------------------ |
| `expo-constants`        | Datos del entorno de ejecución (ID, versión, etc.).    |
| `expo-application`      | Información de la app (nombre, versión, build).        |
| `expo-build-properties` | Configuración nativa avanzada.                         |
| `expo-dev-client`       | Cliente personalizado para desarrollo nativo.          |
| `expo-router`           | Sistema de rutas basado en archivos (como Next.js).    |
| `expo-updates`          | Control de actualizaciones OTA.                        |
| `expo-keep-awake`       | Mantiene la pantalla encendida mientras se usa la app. |

## 3.7. Extras útiles para desarrolladores
| Módulo                  | Descripción                              |
| ----------------------- | ---------------------------------------- |
| `expo-performance`      | Medición del rendimiento de la app.      |
| `expo-error-recovery`   | Recuperación ante errores críticos.      |
| `expo-task-manager`     | Tareas en segundo plano.                 |
| `expo-background-fetch` | Descarga de datos en segundo plano.      |
| `expo-splash-screen`    | Control de la pantalla de carga inicial. |



# 4. Referencias


