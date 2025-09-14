> PROGRAMACIÓN MULTIMEDIA Y DISPOSITVOS MÓVILES

# Tema 1: TECNOLOGÍAS DE DESARROLLO PARA DISPOSITIVOS MÓVILES <!-- omit in toc -->
> Ánalisis de tecnologías disponibles para el desarrollo para móvil
> CONCEPTOS



- [1. Introducción](#1-introducción)


---


# 1. Introducción




# Estilos

En React Native, **StyleSheet** es un módulo que se usa para definir y organizar los estilos de los componentes, de forma similar al CSS en la web, pero adaptado al entorno móvil.

En lugar de escribir CSS tradicional, **en React Native se usan objetos de JavaScript para aplicar estilos**. StyleSheet ayuda a:

- Crear estilos más legibles y reutilizables.
- Validar propiedades de estilo, mostrando advertencias si usas una que no es válida.
- Optimizar el rendimiento, ya que internamente convierte los estilos en una representación más eficiente para que el motor nativo los procese.

### Ejemplo básico:

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

### Características principales:

- **Sintaxis tipo objeto**: Los estilos se definen como objetos de JS.
- **Unidades implícitas**: No se usan px, todos los valores numéricos se interpretan como píxeles independientes de la densidad.
- **Soporta herencia limitada**: No hay cascada como en CSS tradicional. Cada componente recibe explícitamente sus estilos.
- **Composición de estilos**: Puedes pasar un array a style para combinar varios estilos:

<Text style={[styles.texto, styles.destacado]}>Texto</Text>


👉 En resumen: StyleSheet en React Native es la forma recomendada de definir estilos optimizados y estructurados para tus componentes, reemplazando el uso de CSS tradicional.



