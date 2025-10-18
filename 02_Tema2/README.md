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
  - [3.1. Componentes incorporados en Expo](#31-componentes-incorporados-en-expo)
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

## 3.1. Componentes incorporados en Expo



# 4. Referencias


