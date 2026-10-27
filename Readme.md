# Desafío de Integración Numérica · La Paz, Bolivia

Sitio web interactivo para el **Desafío grupal de Métodos Numéricos**: integración numérica con **trapecio compuesto**, **Simpson 1/3** y **Simpson 3/8**, aplicada a problemas de transporte, ingeniería, agua, geometría y energía (ejercicios 19 al 27).

> Los escenarios relacionados con La Paz son adaptaciones didácticas. Los datos de los ejercicios no son mediciones reales de Bolivia.

🔗 **Sitio publicado:** `https://sparkly-halva-24cc9d.netlify.app`

## Contenido del sitio

| Sección | Descripción |
| --- | --- |
| Resumen | Informe técnico condensado y matriz de resultados de los 9 ejercicios, con errores donde hay valor exacto |
| Ejercicios 19–27 | Enunciado, integral, resultados (trapecio y Simpson), error y observaciones de cada ejercicio |
| Calculadora | Herramienta interactiva para ingresar datos nuevos y obtener resultados |
| Guía y evaluación | Formulario permitido, rúbrica de 100 puntos, asignación por grupos y roles |

## Calculadora interactiva

- Entrada de **pares x, y** (uno por línea) o de una **función f(x)** con límites `a`, `b` y número de subintervalos `n`.
- Métodos: trapecio compuesto, Simpson 1/3, Simpson 3/8, combinado 1/3 + 3/8 (n impar) y Simpson 1/3 + trapecio final (n impar), o comparación de todos los aplicables.
- Resultados con **6 decimales** y unidades, junto con `h` y `n`.
- **Error absoluto y porcentual** cuando se ingresa un valor de referencia.
- Tabla de nodos con los **pesos de integración** y gráfico del área bajo la curva.
- Factor final configurable (por ejemplo `1/3600` para convertir de mi/h·s a mi) y transformaciones de y para el ejercicio 27.
- **Validaciones:** datos no numéricos, líneas incompletas, x no creciente, espaciamiento no uniforme, `n` inválido o incompatible con el método, `a ≥ b` y funciones no finitas.

### Sintaxis de f(x)

Variable `x`; constantes `pi`; potencias con `^`; funciones `sin`, `cos`, `tan`, `sinh`, `cosh`, `tanh`, `sqrt`, `exp`, `log`, `abs`.

Ejemplos: `x^2`, `cosh(x/24)`, `20*sin(x/2)`. Los límites también aceptan expresiones, como `2*pi`.

## Fórmulas utilizadas

- Paso: `h = (b − a) / n`, con nodos igualmente espaciados.
- **Trapecio compuesto:** `T = h [ (f₀ + fₙ)/2 + Σ fᵢ ]`, con `i = 1 … n−1`.
- **Simpson 1/3** (n par): `S = (h/3) [ f₀ + fₙ + 4 Σ fᵢ (i impar) + 2 Σ fᵢ (i par interior) ]`.
- **Simpson 3/8** (n múltiplo de 3): `S = (3h/8) [ f₀ + fₙ + 3 Σ fᵢ (i no múltiplo de 3) + 2 Σ fᵢ (i múltiplo de 3 interior) ]`.
- **Error absoluto:** `Eₐ = |I_ref − I_aprox|`. **Error porcentual:** `E% = 100·Eₐ / |I_ref|`, con `I_ref ≠ 0`.

Con 7 subintervalos se combinan Simpson 1/3 (4 subintervalos) y Simpson 3/8 (3 subintervalos). Si no se conoce un valor exacto o de referencia, no se puede calcular el error verdadero.

## Ejercicios incluidos

| Ej. | Problema | Integral |
| --- | --- | --- |
| 19 | Distancia de un vehículo | `∫₀⁷ v(t) dt` |
| 20 | Trabajo de una banda elástica | `∫₀²·⁸ F(x) dx` |
| 21 | Área de un perfil topográfico | `∫₁¹⁰ y(x) dx` |
| 22 | Longitud de una catenaria | `∫₋₁₂²⁶ cosh(x/24) dx` |
| 23 | Caudal en una tubería | `∫₀⁰·²⁵ 160πr(1 − r/0.25)^(1/7) dr` |
| 24 | Longitud de una cardioide | `∫₀²π 20 sin(t/2) dt` |
| 25 | Energía potencial de un satélite | `m g₀ ∫₀ʰ R²/(R+y)² dy` |
| 26 | Superficie de un lago | `∫₄₀²⁶⁰ w(x) dx` (requiere tabla de anchuras) |
| 27 | Volumen de un objeto alargado | `π ∫₀¹² r² dz`, con `r = d/2` |

Los resultados que dependen de curvas digitalizadas (ejercicios 21 y 26) son estimaciones y requieren una tabla común para comparar. En el ejercicio 27, la fórmula simplificada `2π∫r dz` omite la pendiente y no es el área exacta de revolución.

## Pruebas y evidencias

**Verificación mínima:** `∫₀² x² dx = 8/3 ≈ 2.666667`.

| n | Trapecio | Error | Simpson 1/3 | Error |
| --- | --- | --- | --- | --- |
| 4 | 2.750000 | 0.083333 | 2.666667 | ≈ 0 |
| 8 | 2.687500 | 0.020833 | 2.666667 | ≈ 0 |

El botón **Verificar f(x)=x²** de la calculadora reproduce esta tabla.

**Comparación con el solucionario** (n = 8 en los ejercicios con función):

| Ej. | Trapecio | Simpson | Exacto |
| --- | --- | --- | --- |
| 19 | 0.147083 mi | 0.147072 mi (combinado) | — |
| 21 | 36.40 u² | 36.85 u² (1/3 + trapecio final) | — |
| 23 | 11.681778 in³/s | 12.151244 in³/s | 12.828170 in³/s |
| 24 | 78.969264 | 80.010767 | 80 |

Agrega aquí capturas de pantalla de la calculadora en funcionamiento (carpeta `evidencias/`).

## Tecnologías

- HTML, CSS y JavaScript en un **único archivo** (`index.html`).
- [Bootstrap 5](https://getbootstrap.com/) para la interfaz.
- [MathJax 3](https://www.mathjax.org/) para las fórmulas.
- [Chart.js 4](https://www.chartjs.org/) para los gráficos.

Las librerías se cargan por CDN, por lo que se necesita conexión a internet.

## Cómo ejecutarlo

1. Clona el repositorio o descarga `index.html`.
2. Ábrelo en el navegador, o con la extensión *Live Server* de VS Code.

### Publicar con GitHub Pages

1. En el repositorio, ve a **Settings → Pages**.
2. En *Build and deployment*, elige **Deploy from a branch**.
3. Selecciona la rama `main` y la carpeta `/ (root)`, y guarda.
4. Después de un par de minutos, el sitio quedará disponible en la URL indicada arriba.

## Estructura del repositorio

```
├── index.html
├── README.md
└── evidencias/        (capturas de las pruebas)
```

## Equipo

Métodos Numéricos · Desafío grupal de integración · La Paz, Bolivia

- Integrante 1: interpretación y modelo
- Integrante 2: operaciones manuales
- Integrante 3: algoritmos web
- Integrante 4: pruebas, informe y publicación

*(Reemplaza por los nombres del grupo.)*
