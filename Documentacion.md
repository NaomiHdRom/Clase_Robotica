# Primer examen parcial de Robótica semestre 2024-1
### _Modelo de un Robot RRR_
## Objetivo

Este examen tiene como objetivo comprobar el aprovechamiento de los conocimientos relacionados
con los conceptos y conocimientos para establecer el modelado cinemático de la postura,
cinemático directo e inverso de las velocidades, y el modelo dinámico del robot, y el uso de
herramientas computacionales empleadas para la realización de simulaciones en la robótica.

## Puntos a desarrollar

1. Planteamiento del modelo cinemático directo de la postura de un robot RRR.
2. Planteamiento del modelo cinemático directo de las velocidades del robot.
3. Planteamiento del modelo cinemático inverso de las velocidades del robot.
4. Planteamiento de la solución de la cinemática inversa del robot.
5. Diseño e implementación de un robot en una simulación en la cual el robot recorra una
trayectoria según el tipo de examen, para garantizar que el robot realice la tarea se pueden
modificar la longitudes del primer eslabón y del segundo eslabón.

## Trayectoria a seguir

x_{O,P}(t)
y_{O,P}(t)

$$\begin{pmatrix}
\ x_{O,P}(t)\\
y_{O,P}(t)\\
0\\
\end{pmatrix}= \begin{pmatrix}
\ x_{O,C}+r\cdot(\cos\theta(t))\\
y_{O,C}+r\cdot(\cos\theta(t))\\
0\\
\end{pmatrix}
$$

Los parámetros de la trayectoria son: 
$$x_{O,C}= 0.6m$$
$$y_{O,C}= 0.4m$$
$$r=0.2m$$

## Modelo cinemático de un Robot RRR

figura 1

Este robot consta de 3GDL y un punto de solución del sistema como efector final.

figura 2

Paso 1. Planteamos los sistemas de referencia en los actuadores y en el efector final sobre nuestro sistema de referencia {O}.
 Posteriormente se obtienen las transformaciones homogéneas compuestas por la matriz de rotación que gira en z0.

$$T_{i,j}=\begin{pmatrix}
\ R_{i,j}&P_{i,j}\\
O^{T}&1\\
\end{pmatrix}=R_{z}(\theta_{i,j})Ry(O)Rx(0)$$

$$=\begin{pmatrix}
\ cos(\theta_{i,j})&-sin(\theta_{i,j}&0\\
sin(\theta_{i,j}&\cos(\theta_{i,j}&0\\
0&0&1\\
\end{pmatrix}$$

Támbien obtenemos el vector de posición que sólo cuenta con los componentes (x,y) en el plano.

$$P_{i,j}=\begin{pmatrix}
\ x_{i,j}\\
y_{i,j}\\
0\\
\end{pmatrix}$$


 
