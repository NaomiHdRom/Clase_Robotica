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

Este robot consta de 3GDL y un punto de solución del sistema como efector final.

figura 1


### Paso 1. Planteamos los sistemas de referencia en los actuadores y en el efector final sobre nuestro sistema de  referencia {O}. Posteriormente se obtienen las transformaciones homogéneas compuestas por la matriz de rotación que gira en z0.

figura 2



$$T_{i,j}=\begin{pmatrix}
\ R_{i,j}&p_{i,j}\\
O^{T}&1\\
\end{pmatrix}=R_{z}(\theta_{i,j})Ry(O)Rx(0)$$

$$=\begin{pmatrix}
\ cos(\theta_{i,j})&-sin(\theta_{i,j})&0\\
sin(\theta_{i,j}&\cos(\theta_{i,j})&0\\
0&0&1\\
\end{pmatrix}$$

Támbien obtenemos el vector de posición que sólo cuenta con los componentes (x,y) en el plano.

$$p_{i,j}=\begin{pmatrix}
\ x_{i,j}\\
y_{i,j}\\
0\\
\end{pmatrix}$$


### Paso 2. Realizar las transformaciones que relacionan los sistemas de referencia entre sí.

figura3

Se tiene que:


$$T_{i,j}=\begin{pmatrix}
\cos(\theta_{i,j})&-sin(\theta_{i,j})&0&x_{i,j}\\
sin(\theta_{i,j})& cos(\theta_{i,j})&0&y_{i,j}\\
0&0&1&0\\
0&0&0&1
\end{pmatrix}$$

Por lo que para la transformación de nuestro sistema de referencia {O} con el sistema {1}

$$T_{0,1}=\begin{pmatrix}
\cos(\theta_{0,1})&-sin(\theta_{0,1})&0&x_{0,1}\\
sin(\theta_{0,1})& cos(\theta_{0,1})&0&y_{0,1}\\
0&0&1&0\\
0&0&0&1
\end{pmatrix}=\begin{pmatrix}
\ R_{0,1}&p_{0,1}\\
O^{T}&1\\
\end{pmatrix}$$

Para la transformación de nuestro sistema de referencia {1} con el sistema {2}, nótese que se modifica el vector de posición por la longitud del eslabón de donde parte el vector.

$$T_{1,2}=\begin{pmatrix}
\cos(\theta_{1,2})&-sin(\theta_{1,2})&0&L1\\
sin(\theta_{1,2})& cos(\theta_{1,2})&0&0\\
0&0&1&0\\
0&0&0&1
\end{pmatrix}=\begin{pmatrix}
\ R_{1,2}&p_{1,2}\\
O^{T}&1\\
\end{pmatrix}$$

Para la transformación de nuestro sistema de referencia {2} con el sistema {3}.

$$T_{2,3}=\begin{pmatrix}
\cos(\theta_{2,3})&-sin(\theta_{2,3})&0&L2\\
sin(\theta_{2,3})& cos(\theta_{2,3})&0&0\\
0&0&1&0\\
0&0&0&1
\end{pmatrix}=\begin{pmatrix}
\ R_{2,3}&p_{2,3}\\
O^{T}&1\\
\end{pmatrix}$$

En el caso de la transformación de nuestro sistema de referencia {3} con el sistema {P} se puede observar que ambos sistemas referencia tienen la misma orientación es decir la matriz no rota, solo esta desplazada.

$$T_{3,P}=\begin{pmatrix}
1&0&0&L3\\
0& 1&0&0\\
0&0&1&0\\
0&0&0&1
\end{pmatrix}=\begin{pmatrix}
\ R_{3,P}&p_{3,P}\\
O^{T}&1\\
\end{pmatrix}$$

### Paso 3. Descripción de las relaciones de posición y orientación del efector final con respecto al sistema inercial de la postura de los eslabones que conforman la estructura mecánica.

Esto se obtiene multiplicando todas las transformaciones obtenidas anteriormente.

$$T_{O,P}=T_{0,1}T_{1,2}T_{2,3}T_{3,P} =\begin{pmatrix}
\ R_{O,P}&p_{0,P}\\
O^{T}&1\\
\end{pmatrix}$$

Realizando la operación y sustituyendo con las variables obtenemos:

$$T_{O,P}=\begin{pmatrix}
\cos(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})&-sin(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})&0&x_{O,1}+L1cos(\theta_{0,1})+L2cos(\theta_{0,1}+\theta_{1,2})+L3cos(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})\\
sin(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})& cos(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})&0&y_{O,1}+L1sin(\theta_{0,1})+L2sin(\theta_{0,1}+\theta_{1,2})+L3sin(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})\\
0&0&1&0\\
0&0&0&1
\end{pmatrix}$$

De esta matriz podemos extraer el vector de posición p respecto a {P}

$$ p{O,P}(q)= \begin{pmatrix}
\ x_{O,1}+L1cos(\theta_{0,1})+L2cos(\theta_{0,1}+\theta_{1,2})+L3cos(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})\\
y_{O,1}+L1sin(\theta_{0,1})+L2sin(\theta_{0,1}+\theta_{1,2})+L3sin(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})\\
0\\
\end{pmatrix}  $$

Mientras que la orientación del sistema {P} se obtiene sumando los angulos de las transformaciones en los actuadores.

$$\theta_{O,P}(q)= \theta_{O,1}+\theta_{1,2}+\theta_{2,3}  $$

## Planteamiento del modelo cinemático directo de la postura

Tomando el  vector de posición y la orientación respecto a {P} 

$$ξ_{0,P}(q)=\begin{pmatrix}
\ x_{O,1}+L1cos(\theta_{0,1})+L2cos(\theta_{0,1}+\theta_{1,2})+L3cos(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})\\
y_{O,1}+L1sin(\theta_{0,1})+L2sin(\theta_{0,1}+\theta_{1,2})+L3sin(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})\\
\theta_{O,1}+\theta_{1,2}+\theta_{2,3}\\
\end{pmatrix} $$

$$=\begin{pmatrix}
\ p_{O,P(q)}\\
\theta_{O,P(q)}\\
\end{pmatrix}$$

Donde nuestro conjunto de variables q es:

$$q={\theta_{O,1},\theta_{1,2},\theta_{2,3}}$$

Por lo que:

Vector de postura

$$ξ_{O,P}(q)=\begin{pmatrix}
\ p_{O,P(q)}\\
\theta_{O,P(q)}\\
\end{pmatrix}$$

Vector de pose

$$ξ_{O,P}=\begin{pmatrix}
\ p_{O,P}\\
\theta_{O,P}\\
\end{pmatrix}=\begin{pmatrix}
\ x_{O,P}\\
\ y_{O,P}\\
\\theta_{O,P}\\
\end{pmatrix}$$

Ambas ecuaciones son equivalentes, por lo que obtenemos las restricciones cinemáticas de la postura.

$$ξ_{O,P}(q)=ξ_{O,P}$$

$$\begin{pmatrix}
\ x_{O,P}\\
\ y_{O,P}\\
\\theta_{O,P}\\
\end{pmatrix}=\begin{pmatrix}
\ x_{O,1}+L1cos(\theta_{0,1})+L2cos(\theta_{0,1}+\theta_{1,2})+L3cos(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})\\
y_{O,1}+L1sin(\theta_{0,1})+L2sin(\theta_{0,1}+\theta_{1,2})+L3sin(\theta_{0,1}+\theta_{1,2}+\theta_{2,3})\\
\theta_{O,1}+\theta_{1,2}+\theta_{2,3}\\
\end{pmatrix}$$

## Planteamiento del modelo cinemático directo de las velocidades

Para obtener este modelo se deben derivar las restricciones cinemáticas de la postura siguiento la regla de la cadena.

 $${d\over dt}ξ_{O,P}={d\over dt}ξ_{O,P}(q) $$

Derivando el lado izquierdo de la ecuación:

$${d\over dt}ξ_{O,P}={∂\over ∂x_{O,P}}ξ_{O,P} \dot{x_{O,P}}  +  {∂\over ∂y_{O,P}}ξ_{O,P}  \dot{y_{O,P}} +  {∂\over ∂\theta_{O,P}}ξ_{O,P}  \dot\theta_{O,P} = \begin{pmatrix}
\ x_{O,P}\\
\ y_{O,P}\\
\\theta_{O,P}\\
\end{pmatrix} $$

Derivando el lado derecho de la ecuación:

$${d\over dt}ξ_{O,P}(q)={∂\over ∂\theta_{O,1}}ξ_{O,P}(q) \dot{\theta_{O,1}}  +  {∂\over ∂\theta_{1,2}}ξ_{O,P}(q) \dot{\theta_{1,2}} +  {∂\over ∂\theta_{2,3}}ξ_{O,P}(q)  \dot\theta_{2,3} = \begin{pmatrix}
\ {∂\over ∂\theta_{O,1}}ξ_{O,P}(q)&{∂\over ∂\theta_{1,2}}ξ_{O,P}(q)&{∂\over ∂\theta_{2,3}}ξ_{O,P}(q)\\
\end{pmatrix} \begin{pmatrix}
\ \dot{\theta_{O,1}}\\
\ \dot{\theta_{1,2}}\\
\ \dot{\theta_{2,3}}\\ 
\end{pmatrix} $$

 De esta ecuación podemos rescatar el jacobiano y el vector de velocidades generalizadas del sistema

Jacobiano

$$J_{\theta}(q)=  \begin{pmatrix}
\ {∂\over ∂\theta_{O,1}}ξ_{O,P}(q)&{∂\over ∂\theta_{1,2}}ξ_{O,P}(q)&{∂\over ∂\theta_{2,3}}ξ_{O,P}(q)\\
\end{pmatrix} $$

Vector de velocidades generalizadas del sistema

$$\dot{q}= \begin{pmatrix}
\ \dot{\theta_{O,1}}\\
\ \dot{\theta_{1,2}}\\
\ \dot{\theta_{2,3}}\\ 
\end{pmatrix}$$

Por lo que el modelo cinemático directo de las velocidades es:

$$ \dot{ξ_{O,P}}=\dot{ξ_{O,P}}(q)= J_{\theta}(q) \dot{q}   $$

 
## Planteamiento del modelo cinemático inverso de las velocidades 

Para obtener este modelo es necesario despejar de la siguiente manera:

$$ \dot{q} =  J_{\theta}(q)^{-1}\dot{ξ_{O,P}}=\dot{ξ_{O,P}}(q)     $$

En este robot el número de variables es igual al número de actuadores por lo que se obtiene una matriz cuadrada y podemos descartar el exponente.

Por lo que el modelo cinemático incerso de las velocidades es:

$$ \dot{q} =  J_{\theta}(q)\dot{ξ_{O,P}}=\dot{ξ_{O,P}}(q)     $$








 
