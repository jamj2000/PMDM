> PROGRAMACIÓN MULTIMEDIA Y DISPOSITVOS MÓVILES

# Tema 4: ARQUITECTURA DE JUEGOS 2D Y 3D <!-- omit in toc -->
> Motores de juegos  
> CONCEPTOS



- [1. Introducción](#1-introducción)
- [2. Principales motores](#2-principales-motores)
- [3. Otros motores (Javascript)](#3-otros-motores-javascript)
- [4. Referencias](#4-referencias)




---


# 1. Introducción


# 2. Principales motores


| Característica              | **Unity**                         | **Godot**                         | **Unreal Engine**               |
| --------------------------- | --------------------------------- | --------------------------------- | ------------------------------- |
| Soporte 2D/3D               | Excelente en ambos                | Muy bueno en 2D, bueno en 3D      | Excelente en 3D, limitado en 2D |
| Lenguajes                   | C#                                | GDScript, C#, C++                 | C++, Blueprints (visual)        |
| Facilidad de uso            | Media                             | Alta                              | Media-baja                      |
| Rendimiento                 | Alto                              | Medio-alto                        | Muy alto                        |
| Calidad gráfica             | Alta                              | Media                             | Muy alta (AAA)                  |
| Plataformas                 | PC, móvil, web, consolas          | PC, móvil, web                    | PC, consolas, móvil             |
| Exportación multiplataforma | Excelente                         | Muy buena                         | Excelente                       |
| Coste                       | Gratis + licencias según ingresos | Totalmente gratuito (open source) | Gratis + royalties (5%)         |
| Código abierto              | No                                | Sí                                | Parcial (acceso al código)      |
| Comunidad                   | Muy grande                        | En crecimiento                    | Muy grande                      |
| Asset Store / recursos      | Muy amplio                        | Limitado pero creciendo           | Amplio (Marketplace)            |
| Curva de aprendizaje        | Media                             | Baja                              | Alta                            |
| Uso típico                  | Indie, móvil, VR, AA              | Indie, proyectos pequeños         | AAA, gráficos avanzados         |
| Editor visual               | Completo                          | Ligero y rápido                   | Muy potente                     |
| Soporte VR/AR               | Sí                                | Limitado                          | Sí (muy avanzado)               |
| Documentación               | Muy completa                      | Buena                             | Muy completa                    |

**Resumen**

- **Unity** → equilibrio entre facilidad, potencia y multiplataforma
- **Godot** → ideal para empezar y proyectos 2D open source
- **Unreal Engine** → mejor opción para gráficos avanzados y juegos AAA


# 3. Otros motores (Javascript)

| Motor      | Tipo | Lenguaje      | Plataformas        | Licencia     | Nivel        | Características destacadas               |
| ---------- | ---- | ------------- | ------------------ | ------------ | ------------ | ---------------------------------------- |
| Phaser     | 2D   | JavaScript    | Web (HTML5)        | MIT (gratis) | Principiante | Muy fácil, ideal para juegos 2D rápidos  |
| Three.js   | 3D   | JavaScript    | Web (WebGL)        | MIT (gratis) | Intermedio   | Renderizado 3D, no es motor completo     |
| Babylon.js | 3D   | JavaScript/TS | Web (WebGL/WebGPU) | Apache 2.0   | Intermedio   | Motor 3D completo, potente y moderno     |
| PlayCanvas | 3D   | JavaScript    | Web                | Freemium     | Intermedio   | Editor online colaborativo               |
| MelonJS    | 2D   | JavaScript    | Web                | MIT (gratis) | Intermedio   | Ligero, orientado a juegos simples       |
| A-Frame    | 3D   | JavaScript    | Web (VR/AR)        | MIT (gratis) | Principiante | Ideal para realidad virtual en navegador |


**Resumen**

- **Phaser** → El más popular para juegos 2D en navegador (tipo plataformas, puzzles)
- **Three.js** → Ideal para gráficos 3D, pero necesitas construir lógica de juego tú mismo
- **Babylon.js** → Alternativa más completa a Three.js (motor real)
- **PlayCanvas** → Muy potente con editor en la nube tipo Unity

> [!TIP] 
> **Recomendación rápida**
>
> - Juego 2D sencillo → Phaser
> - 3D básico → Three.js
> - 3D completo/proyecto serio → Babylon.js o PlayCanvas
> - VR en navegador → A-Frame


# 4. Referencias

- [GameFromScratch - canal youtube](https://www.youtube.com/gamefromscratch)
- [js13kgame - js web game development competition with 13KB size limit](https://js13kgames.com/)
