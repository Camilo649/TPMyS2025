
<div style="border: 3px solid #4A90E2; border-radius: 10px; padding: 20px; background-color: #f5f8fc; color: #000000; font-family: sans-serif;">

<h1 style="color: #DAA520;">Comparación de Generadores Pseudoaleatorios mediante el Método de Monte Carlo</h1>

<div style="font-family: 'Palatino Linotype', serif; font-size: 1.3em; margin-bottom: 1em;">
  <p><strong>Integrantes:</strong></p>
  <ul style="list-style-type: disc; margin-left: 30px;">
    <li>ARIAS, Eliana</li>
    <li>GUTIÉRREZ, Camilo</li>
  </ul>
  <p><strong>Fecha:</strong> Junio 2025</p>
</div>


<hr>

<h2 style="color: #DAA520;">Resumen</h2>

<p>
Este informe analiza y compara el desempeño de distintos generadores de números pseudoaleatorios aplicados a la estimación de una integral definida mediante el método de Monte Carlo. Se utilizan generadores clásicos como <code>LCG</code> y variantes más modernas como <code>Xorshift</code> y <code>Xoshiro</code>. Se evalúan su eficiencia, precisión, distribución y varianza obtenida en las simulaciones.
</p>

<hr>

<h2 style="color: #DAA520;">1. Generadores estudiados</h2>

<h3 style="color: #DAA520;">1.1 LCG (Linear Congruential Generator)</h3>
<ul>
<li><strong>Fórmula:</strong> Xₙ₊₁ = (a * Xₙ) mod m</li>
<li><strong>Parámetros usados:</strong> a = 16807, m = 2³¹ - 1</li>
<li><strong>Ventajas:</strong> Implementación sencilla, rápida.</li>
<li><strong>Desventajas:</strong> Correlaciones a largo plazo, no adecuado para aplicaciones criptográficas.</li>
</ul>

<h3 style="color: #DAA520;">1.2 Xorshift (32, 64, 128 bits)</h3>
<ul>
<li>Utiliza operaciones XOR y desplazamientos bit a bit.</li>
<li><strong>Ventajas:</strong> Muy rápido, buena distribución estadística.</li>
<li><strong>Desventajas:</strong> No es criptográficamente seguro.</li>
</ul>

<h3 style="color: #DAA520;">1.3 Xoshiro128++</h3>
<ul>
<li>Uno de los generadores modernos más robustos.</li>
<li><strong>Ventajas:</strong> Buena calidad, velocidad, adecuada para simulaciones numéricas.</li>
<li><strong>Desventajas:</strong> Complejidad levemente mayor.</li>
</ul>

<hr>

<h2 style="color: #DAA520;">2. Descripción del problema de simulación</h2>

<p>
Se desea estimar la siguiente integral múltiple sobre el hipercubo [0,1]^d:
</p>

<pre><code>I_d = ∫_[0,1]^d e^(-∑ x_i²) dx</code></pre>

<p>
Esta integral tiene una solución teórica conocida basada en el producto de funciones error:
</p>

<pre><code>I_d = ((√π * erf(1)) / 2)^d</code></pre>

<p>
Se utiliza el método de Monte Carlo para estimar su valor con diferentes generadores y distintas combinaciones de dimensión y cantidad de muestras.
</p>

<hr>

<h2 style="color: #DAA520;">3. Metodología</h2>

<ul>
<li><strong>Lenguaje usado:</strong> Python 3</li>
<li><strong>Librerías:</strong> NumPy, Matplotlib, math, time</li>
<li><strong>Muestras:</strong> N = 10⁴, 10⁵, 10⁶</li>
<li><strong>Dimensiones:</strong> d = 2, 5, 10</li>
<li><strong>Comparaciones:</strong> estimación de la integral, error absoluto, varianza de la muestra, tiempo de ejecución.</li>
<li><strong>Tests adicionales:</strong> comparación gráfica de la distribución de los generadores (histogramas).</li>
</ul>

<hr>

<h2 style="color: #DAA520;">4. Resultados y análisis</h2>

<h3 style="color: #DAA520;">Distribuciones obtenidas</h3>

<p><img src="grafico.png" alt="Distribución de generadores" style="width:100%;"></p>

<p>
Como se observa en los histogramas, generadores como <code>Xorshift32</code> presentan irregularidades en la distribución, mientras que <code>Xoshiro128++</code>, <code>LCG</code>, y los demás <code>Xorshift</code> muestran comportamientos más uniformes.
</p>

<h3 style="color: #DAA520;">Estimaciones, varianza y tiempos</h3>

<p>Resultados obtenidos de las simulaciones para distintas combinaciones de dimensión y cantidad de muestras:</p>

<pre>tengo que modificar esto<code>
LCG          | d=2  | N=1000000 | Estimación=0.557745 | Error=6.03e-05 | Varianza=2.69e-08 | Tiempo=1.80s
Xorshift32   | d=2  | N=1000000 | Estimación=0.557598 | Error=9.98e-05 | Varianza=2.70e-08 | Tiempo=1.52s
Xorshift64   | d=2  | N=1000000 | Estimación=0.557674 | Error=7.30e-05 | Varianza=2.71e-08 | Tiempo=1.55s
Xorshift128  | d=2  | N=1000000 | Estimación=0.557633 | Error=8.14e-05 | Varianza=2.71e-08 | Tiempo=1.55s
Xoshiro128   | d=2  | N=1000000 | Estimación=0.557715 | Error=6.47e-05 | Varianza=2.71e-08 | Tiempo=1.57s
</code></pre>

<ul>
<li><strong>Varianza:</strong> Todos los generadores modernos se comportan de manera similar en cuanto a varianza.</li>
<li><strong>Tiempo:</strong> Xorshift32 es levemente más rápido.</li>
<li><strong>Error absoluto:</strong> LCG y Xoshiro128++ muestran los mejores desempeños.</li>
</ul>




<h3 style="color: #DAA520;">Anexo: Resultados completos</h3>

<p>La siguiente tabla muestra los resultados completos de todas las simulaciones realizadas para los distintos generadores, dimensiones <code>d</code> y cantidades de muestras <code>N</code>. Incluye la estimación de la integral, el error absoluto, la varianza muestral y el tiempo de ejecución.</p>

<table style="width:100%; font-size:0.9em; border-collapse: collapse;">
  <thead style="background-color: #DAA520; color: white;">
    <tr>
      <th>Generador</th><th>d</th><th>N</th><th>Estimación</th><th>Error</th><th>Varianza</th><th>Tiempo (s)</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>LCG</td><td>10</td><td>10000</td><td>0.053766</td><td>2.08e-04</td><td>2.96e-07</td><td>0.02</td></tr>
    <tr><td>LCG</td><td>10</td><td>100000</td><td>0.053679</td><td>2.95e-04</td><td>2.96e-08</td><td>0.21</td></tr>
    <tr><td>LCG</td><td>10</td><td>1000000</td><td>0.053930</td><td>4.43e-05</td><td>2.94e-09</td><td>2.40</td></tr>
    <tr><td>Xorshift32</td><td>10</td><td>10000</td><td>0.053083</td><td>8.91e-04</td><td>2.69e-07</td><td>0.03</td></tr>
    <tr><td>Xorshift32</td><td>10</td><td>100000</td><td>0.052917</td><td>1.06e-03</td><td>2.64e-08</td><td>0.30</td></tr>
    <tr><td>Xorshift32</td><td>10</td><td>1000000</td><td>0.052935</td><td>1.04e-03</td><td>2.64e-09</td><td>3.03</td></tr>
    <tr><td>Xorshift64</td><td>10</td><td>10000</td><td>0.053523</td><td>4.51e-04</td><td>2.81e-07</td><td>0.04</td></tr>
    <tr><td>Xorshift64</td><td>10</td><td>100000</td><td>0.053826</td><td>1.48e-04</td><td>2.96e-08</td><td>0.41</td></tr>
    <tr><td>Xorshift64</td><td>10</td><td>1000000</td><td>0.053923</td><td>5.11e-05</td><td>2.95e-09</td><td>4.22</td></tr>
    <tr><td>Xorshift128</td><td>10</td><td>10000</td><td>0.053761</td><td>2.13e-04</td><td>2.94e-07</td><td>0.04</td></tr>
    <tr><td>Xorshift128</td><td>10</td><td>100000</td><td>0.053881</td><td>9.25e-05</td><td>2.91e-08</td><td>0.44</td></tr>
    <tr><td>Xorshift128</td><td>10</td><td>1000000</td><td>0.053916</td><td>5.76e-05</td><td>2.93e-09</td><td>4.86</td></tr>
    <tr><td>Xoshiro128++</td><td>10</td><td>10000</td><td>0.053834</td><td>1.40e-04</td><td>2.95e-07</td><td>0.07</td></tr>
    <tr><td>Xoshiro128++</td><td>10</td><td>100000</td><td>0.053933</td><td>4.11e-05</td><td>2.93e-08</td><td>0.73</td></tr>
    <tr><td>Xoshiro128++</td><td>10</td><td>1000000</td><td>0.053960</td><td>1.43e-05</td><td>2.94e-09</td><td>7.14</td></tr>
  </tbody>
</table>

<p>Este anexo permite observar de forma detallada el comportamiento de cada generador al aumentar la complejidad (mayor <code>d</code>) y la precisión deseada (mayor <code>N</code>). En particular, se destaca:</p>

<ul>
  <li><strong>Xoshiro128++</strong> ofrece la mejor precisión para <code>d = 10</code> con <code>N = 10⁶</code>, aunque es más costoso en tiempo.</li>
  <li><strong>Xorshift128</strong> logra excelente precisión con menor tiempo en configuraciones medianas (<code>N = 10⁵</code>).</li>
  <li><strong>Xorshift32</strong> tiende a tener mayor error, especialmente en alta dimensión, aunque es el más rápido.</li>
</ul>

<hr>

<h2 style="color: #DAA520;">5. Conclusiones</h2>

<ul>
<li>La elección del generador tiene impacto en la precisión y en la distribución de los resultados.</li>
<li><strong>Xoshiro128++</strong> es una excelente opción para simulaciones debido a su equilibrio entre uniformidad, rapidez y precisión.</li>
<li><strong>Xorshift32</strong> es rápido, pero con distribución menos pareja.</li>
<li><strong>LCG</strong> es sorprendentemente competitivo en este escenario, aunque tiene limitaciones conocidas.</li>
<li>Recomendamos evitar generadores con sesgos evidentes en distribución para simulaciones de alta sensibilidad.</li>
</ul>

<hr>

<h2 style="color: #DAA520;">6. Código fuente</h2>

<p>El código completo de simulación y generación de gráficos se incluye en el archivo <code>simulacion.ipynb</code> adjunto.</p>

</div>
