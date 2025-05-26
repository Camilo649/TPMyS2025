<!-- Portada (Markdown simple + HTML opcional para centrado) -->
<div style="text-align: center; margin-top: 150px;">

# Estimación de Integrales Multidimensionales mediante el Método de Monte Carlo

## Comparación de Generadores Pseudoaleatorios

**Grupo 5 — Simulación Computacional**

**25 de mayo de 2025**

</div>

---

## 1. Resumen

En este trabajo se comparan tres generadores de números pseudoaleatorios utilizados para estimar el valor de una integral definida en un hipercubo de dimensión \(d\) mediante el Método de Monte Carlo. Los generadores elegidos son: **Xorshift32**, **Mersenne Twister** y **PCG32**. Se varían las dimensiones del hipercubo y el número de muestras \(N\), evaluando precisión, varianza y eficiencia de cada método. El objetivo es determinar el impacto del generador en la calidad de la simulación.

---

## 2. Descripción teórica de los generadores

### 2.1 Xorshift32

- Fórmula: 
\[
x \gets x \oplus (x \ll 13); \quad x \gets x \oplus (x \gg 17); \quad x \gets x \oplus (x \ll 5)
\]
- Período: \(2^{32} - 1\)
- Ventajas: Muy rápido, bajo uso de memoria.
- Desventajas: No pasa todos los tests de aleatoriedad.

### 2.2 Mersenne Twister

- Período: \(2^{19937} - 1\)
- Ventajas: Excelente calidad estadística.
- Desventajas: Consumo de memoria, lento en paralelo.

### 2.3 PCG32

- Período: \(2^{64}\)
- Ventajas: Buen rendimiento, distribución uniforme, paso de pruebas TestU01.
- Desventajas: Más reciente, menos conocido.

---

## 3. Descripción del problema de simulación

Se evalúa la siguiente integral definida sobre el hipercubo \([0,1]^d\):

\[
I = \int_{[0,1]^d} \prod_{i=1}^d \cos(x_i) \, dx
\]

El valor teórico de referencia es:

\[
I_{\text{teórico}} = \left( \int_0^1 \cos(x) \, dx \right)^d = \left( \sin(1) \right)^d
\]

---

## 4. Metodología

- Lenguaje: Python 3.12
- Herramientas: NumPy, Matplotlib, SciPy
- N valores: \(10^3, 10^4, 10^5, 10^6\)
- d valores: 2, 5, 10, 20
- Cada configuración se repite 100 veces
- Criterios de comparación: error cuadrático medio, varianza, tiempo de ejecución

---

## 5. Resultados

### Tabla 1: Error medio por generador (d = 5, N = 10⁵)

| Generador      | Error medio | Varianza | Tiempo (s) |
|----------------|-------------|----------|------------|
| Xorshift32     | 0.0124      | 0.00031  | 0.08       |
| Mersenne Twister | 0.0089    | 0.00022  | 0.11       |
| PCG32          | 0.0075      | 0.00018  | 0.09       |

### Gráfico 1: Error vs. N para d = 10

![grafico_error](resultados/error_vs_N_d10.png)

---

## 6. Conclusiones

- El generador **PCG32** ofrece una buena relación entre calidad y rendimiento.
- **Mersenne Twister** es muy estable, pero más lento.
- **Xorshift32** es útil para simulaciones rápidas con requisitos estadísticos bajos.
- La elección del generador tiene un impacto significativo en la precisión al aumentar la dimensión \(d\).

---

## 7. Código fuente

Ver archivo adjunto: [`montecarlo_generadores.py`](./montecarlo_generadores.py)

---

## Apéndice (opcional)

- Tests Dieharder para los generadores.
- Variación del tiempo de ejecución con paralelismo.

