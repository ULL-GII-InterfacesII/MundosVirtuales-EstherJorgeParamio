# Mundos virtuales. Introducción a la programación de gráficos 3D.

Esther Jorge Paramio

### 1. ¿Qué funciones se pueden usar en los scripts de Unity para llevar a cabo traslaciones, rotaciones y escalados?

Las funciones que se pueden usar en los scripts, entre otras, para llevar a cabo transformaciones son, 
usando las componentes de *Transform*, *translate* para las traslaciones, *rotate* 
para las rotaciones y *localScale* para el escalado  en el caso de objetos no físicos, a no ser que sean físicos y kinemáticos.

En el caso de objetos físicos no kinemáticos por ejemplo puedes usar *addForce* para trasladarlos.


### 2. ¿Cómo duplicarías el tamaño de un objeto en un script?

El tamaño de un objeto, en un script, lo duplicaría declarando primero la variable 
*Transform*, llamada por ejemplo *tf*. Luego en función *Start* lo inicializamos haciendo *tf = GetComponent<Transform>()* y por último para modificar el tamaño del objeto usamos la propiedad del Transform *localScale* y lo multiplicamos por dos para duplicarlo.


```C#
public Transform tf;
```
```C#
tf = GetComponent<Transform>();
```
```C#
tf.localScale *= 2.0f;
```

### 3. ¿Cómo situarías un objeto en la posición (3,5,1)?

Para situar un objeto en la posición (3, 5, 1) o bien modificaría en el inspector en el apartado de *position* las componetente X, Y y Z por 3, 5 y 1 respectivamente. 

En el caso de que lo queramos hacer con el *Transform* en un script, modificamos la propiedad *position* igualandolo a un *Vector3* que contenga dichos valores respectivamente.

```C#
Vector3 newPos = new Vector3(3, 5, 1);
tf.position = newPos;
```

### 4. ¿Cómo trasladarías 3 metros en cada uno de los ejes y luego lo rotas 30º alrededor del eje Y?

Un objeto, lo trasladaría 3 metros (asumiendo que una unidad en Unity es 1 metro) en cada uno de sus ejes creando una estructura de datos de tipo *Vector3* en los que sus componentes X, Y y Z sean 3 unidades para así mandarlo como parámetro a *Transform.Translate()* y trasladarlo 3 unidades en todas las direcciones.

```C#
Vector3 newDistance = new Vector3(3, 3, 3);
tf.Translate(newDistance);
```

Para rotarlo 30º, creamos un Vector3 a la que le pasamos como parámetros los grados que queremos rotar, en este caso (0, 30, 0) y hacemos *Transform.Rotate()* mandándole como parámetro dicho vector.

```C#
Vector3 rotation = new Vector3(0, 30, 0);
tf.Rotate(rotation);
```

### 5. ¿Cómo rotarías un objeto sobre el eje (1,1,1)?

Para rotar un objeto sobre el eje (1, 1, 1) primero creamos una estructura de datos de tipo Vector3 y le inicializamos las componentes X, Y y Z con 1. Luego, usando la componente *Transform* del objeto usamos el método *Rotation* y le mandamos como parámetro dicho vector.

```C#
Vector3 rotation = new Vector3(1, 1, 1);
tf.Rotate(rotation);
```

### 6. Rota un objeto alrededor del eje Y 30ª y desplázalo 3 metros en cada uno de los ejes. ¿Obtendrías el mismo resultado que en 4?

En el caso de que fuera un objeto físico, sí se obtendría el mismo resultado al no poder modificar el sistema de coordenadas por ser *Rigidbody*. 

En cambio, si no fuese físico, el sistemas de coordenadas sí que cambiaría.

### 7. ¿Cómo puedes obtener la distancia al plano cerca del volumen de vista desde la cámara?

La puedo obtener usando la propiedad *nearClipPlane* del componente de la cámara.

```C#
Camera cam = GetComponent<Camera>();
float nearPlaneDistance = cam.nearClipPlane;
```

### 8. ¿Cómo puedes aumentar el ángulo de la cámara?

Para aumentar el ángulo de la cámara lo puedes hacer de dos maneras. 

Desde el inspector de *Unity*, seleccionando la cámara a la que quieras cambiar el ángulo,
puedes modificar el valor de la celda *Field of view* tanto deslizando como insertando 
el valor exacto. 

En el caso de que lo quieras realizar desde un *script*, modificamos la propiedad
*fieldOfView* igualando al valor querido en flotante.

```C#
Camera cam = GetComponent<Camera>();
cam.fieldOfView = newAngle;
```
### 9. ¿Qué efecto tiene disminuir el ángulo de la cámara?

El efecto es que realiza un *zoom*, cuanto más pequeño es el ángulo de la cámara
menos objetos caben y más grandes son.

### 10. Configura un volumen de vista que recorte objetos de la escena.

Para que el volumen de vista recorte objetos de la escena cambiamos la distancia
del plano más cercano con la propiedad *newClipPlane* aumentándola hasta que dejes
dentro de la vista los objetos deseados.

### 11. ¿Cómo puedes realizar la proyección al espacio 2D?

Para realizar la proyección al espacio 2D, en el inspector de la cámara, en la
propiedad *projection* cambiamos su valor y lo ponemos a *orthographic* y podemos
cómo el rango de la cámara se vuelve cuadrada y se puede observar los objetos de frente
dando la sensación de estar en 2D.

### 12. Especifica la rotación de los apartados 4 y 6 con la utilidad quaternion.

Para hacer la rotación modificamos la propiedad *rotation*. Para rotar sobre
el eje de la *Y* usando *quaternion*, usamos el método *AngleAxis* mandándole como
parámetros el ángulo que quiero rotar y *Vector3.up* que indica que rote sobre el
eje Y.

```C#
public Transform tf = GetComponent<Transform>();
tf.rotation = Quaternion.AngleAxis(30, Vector3.up);
```

### 13. ¿Cómo puedes averiguar la matriz de proyección en perspectiva que se ha 
usado para proyectar la escena al último frame renderizado?

La matriz de proyección la obtenenemos a partir de la propiedad de la cámara *projectionMatrix*
y mostrándola por la consola. Para que sea en perspectiva tenemos que tener el valor 
de *projection* de la cámara con *perspective*.

```C# 
Camera cam = GetComponent<Camera>();
Debug.Log(cam.projectionMatrix);
```

### 14. ¿Cómo puedes averiguar la matriz de proyección en perspectiva ortográfica 
que se ha usado para proyectar la escena al último frame renderizado?

La matriz de proyección la obtenenemos a partir de la propiedad de la cámara *projectionMatrix*
y mostrándola por la consola. Para que sea en perspectiva ortográfica tenemos que tener el valor 
de *projection* de la cámara con *orthographic*.

```C# 
Camera cam = GetComponent<Camera>();
Debug.Log(cam.projectionMatrix);
```

### 15.  ¿Cómo puedes obtener la matriz de transformación entre el sistema de 
coordenadas local y el mundial?

La matriz de transformación entre el sistema de coordenadas local y el 
mundial se obtiene de la propiedad *localToWorldMatrix* de *Transform*.

```C# 
Camera tf = GetComponent<Transform>();
Debug.Log(tf.localToWorldMatrix);
```

