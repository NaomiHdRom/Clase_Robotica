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
