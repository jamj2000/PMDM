> PROGRAMACIÓN MULTIMEDIA Y DISPOSITVOS MÓVILES

# Tema 2: DESARROLLO DE APLICACIONES PARA DISPOSITIVOS MÓVILES <!-- omit in toc -->
> Desarrollo usando React Native y Expo  
> CONCEPTOS



- [1. Introducción](#1-introducción)
- [2. React Native](#2-react-native)
  - [2.1. Estilos](#21-estilos)
    - [2.1.1. Ejemplo básico:](#211-ejemplo-básico)
    - [2.1.2. Características principales:](#212-características-principales)
- [3. Expo](#3-expo)
- [4. Referencias](#4-referencias)







---


# 1. Introducción


# 2. React Native



## 2.1. Estilos


En React Native, **StyleSheet** es un módulo que se usa para definir y organizar los estilos de los componentes, de forma similar al CSS en la web, pero adaptado al entorno móvil.

En lugar de escribir CSS tradicional, **en React Native se usan objetos de JavaScript para aplicar estilos**. StyleSheet ayuda a:

- Crear estilos más legibles y reutilizables.
- Validar propiedades de estilo, mostrando advertencias si usas una que no es válida.
- Optimizar el rendimiento, ya que internamente convierte los estilos en una representación más eficiente para que el motor nativo los procese.

### 2.1.1. Ejemplo básico:

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

### 2.1.2. Características principales:

- **Sintaxis tipo objeto**: Los estilos se definen como objetos de JS.
- **Unidades implícitas**: No se usan px, todos los valores numéricos se interpretan como píxeles independientes de la densidad.
- **Soporta herencia limitada**: No hay cascada como en CSS tradicional. Cada componente recibe explícitamente sus estilos.
- **Composición de estilos**: Puedes pasar un array a style para combinar varios estilos:


```js
<Text style={[styles.texto, styles.destacado]}>Texto</Text>
```

👉 En resumen: StyleSheet en React Native es la forma recomendada de definir estilos optimizados y estructurados para tus componentes, reemplazando el uso de CSS tradicional.






# 3. Expo





# 4. Referencias


