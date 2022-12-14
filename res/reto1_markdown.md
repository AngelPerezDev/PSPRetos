馃搧 [Descargar en PDF](./reto1_arraylist.pdf)

# 脥ndice
- [脥ndice](#铆ndice)
- [Definici贸n y creaci贸n de un ArrayList](#definici贸n-y-creaci贸n-de-un-arraylist)
- [M茅todos y propiedades generales](#m茅todos-y-propiedades-generales)
- [A帽adir datos a la colecci贸n](#a帽adir-datos-a-la-colecci贸n)
    - [A帽adir elementos desde el constructor](#a帽adir-elementos-desde-el-constructor)
    - [A帽adir elementos a partir de otras colecciones](#a帽adir-elementos-a-partir-de-otras-colecciones)
    - [A帽adir elementos mediante c贸digo](#a帽adir-elementos-mediante-c贸digo)
    - [Eliminar elementos mediante c贸digo](#eliminar-elementos-mediante-c贸digo)
- [Recorrer la colecci贸n](#recorrer-la-colecci贸n)
- [B煤squeda de elementos](#b煤squeda-de-elementos)
- [Obtenci贸n de subcolecciones](#obtenci贸n-de-subcolecciones)
- [Ordenaci贸n de elementos](#ordenaci贸n-de-elementos)
    - [Con funciones de Collection](#con-funciones-de-collection)
    - [Con expresiones lambda](#con-expresiones-lambda)
    - [Con API Stream](#con-api-stream)
- [Webgraf铆a](#webgraf铆a)

<a name="definicion"></a>

# Definici贸n y creaci贸n de un ArrayList

La clase ArrayList en Java permite almacenar datos en memoria de forma similar a los Arrays con la ventaja de que el numero de elementos que almacena lo hace de forma **din谩mica**, es decir, que **no es necesario declarar su tama帽o como pasa con los Arrays.** Los elementos pueden a帽adirse o eliminarse seg煤n necesidad. 

La clase Arraylist implementa la interface List, la cual extiende la interface `java.util.Collection`.

![Esquema ArrayList - Collection](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200624184403/ArrayList.png)

Para crear un ArrayList, podemos importar o bien solo la clase `java.util.ArrayList` o todo el paquete `java.util`. Un ArrayList se puede declarar de diferentes elementos u objetos (String, Integer, float, Boolean, Object...). Adem谩s **existen 3 sobrecargas del constructor** que veremos a continuaci贸n.

Para el ejemplo que vamos a seguir en este manual, utlizaremos el IDE Netbeans y declararemos un ArrayList de objetos *Coche* al que llamaremos *garaje* y en el que almacenaremos objetos de la clase *Coche*, la cual deberemos de crear tambi茅n con el siguiente c贸digo:

```Java
 // Creamos una clase Coche que usaremos para el ejemplo y
 // se guardar谩 en Coche.java
public class Coche
{
    //Atributos de la clase
    private String marca;
    private String modelo;
    private String version;
    private double precio;

    //Constructor con el mismo nombre de la clase
    public Coche(String marca, 
                  String modelo, 
                  String version, 
                  double precio) {
        this.marca = marca;
        this.modelo = modelo;
        this.version = version;
        this.precio = precio;
    }

    //M茅todos de la clase
    public String getMarca() {
        return marca;
    }

    public String getModelo() {
        return modelo;
    }

    public String getVersion() {
        return version;
    }

    public double getPrecio() {
        return precio;
    }

    //String de la clase
    @Override
    public String toString() {
        return "Coche: " + marca + " / " 
                          + modelo + " / " 
                          + version + " / " 
                          + precio;
    } 
}
```
Una vez creada la clase *Coche*, declaramos el ArrayList *garaje* y le a帽adimos 3 coches de la siguiente manera:

``` Java
// SOBRECARGA 1

// Importamos la clase ArrayList
import java.util.ArrayList; 

// Creamos 3 objetos Coche
Coche seatArosa = new Coche("Seat", "Arosa", "2.0", 25000);
Coche fordFocus = new Coche("Ford", "Focus", "1600", 21000);
Coche audiA4 = new Coche("Audi", "A4", "v6", 45000);

// Creamos un ArrayList garaje al que le a帽adimos los 3 coches
ArrayList<Coche> garaje = new ArrayList<Coche>(); 
```
Al hacerlo de esta manera, estamos creando un ArrayList sin longitud, es decir, es una lista vac铆a, aunque por defecto tiene una capacidad de 10. Esto no quiere decir que s贸lo podamos a帽adir 10 objetos, sino que se dimensiona con una capacidad de 10 para optimizar recursos (aunque la lista est谩 vac铆a, si se consultara el tama帽o de la lista ser铆a 0). Si m谩s adelante queremos a帽adir objetos, el ArrayList es capaz de redimensionarse. 

Vamos ahora a a帽adir los 3 coches creados y a mostrar que est谩n en la lista:

``` Java
garaje.add(seatArosa); // A帽adimos elementos a la lista garaje
garaje.add(fordFocus);
garaje.add(audiA4);

for (Coche coche : garaje) // Recorremos el ArrayList y mostramos sus objetos
{
  System.out.println(coche);
}
```
Si por el contrario, quisieramos darle una longitud inicial al ArrayList, la declaraci贸n ser铆a la siguiente:

``` Java
// SOBRECARGA 2

// Creamos el objeto ArrayList con una capacidad de 30
ArrayList<Coche> garaje = new ArrayList<Coche>(30); 
```
Si sabemos de antemano cual va a ser la capacidad que se necesita de ArrayList, es mejor crearlo de esta manera, ya que aunque un ArrayList es una lista din谩mica y permite el crecimiento agregando elementos, conlleva un coste muy alto de recursos cada vez que se redimensiona.

Existe una tercera sobrecarga del constructor `ArrayList(Collection<? extends E> c) ` donde podemos crear/aumentar el ArrayList pas谩ndole una colecci贸n espec铆fica. De esta manera, el ArrayList se generar谩 con los valores de dicha colecci贸n seg煤n se los vaya pasando el iterador. Por ejemplo:

``` Java
// SOBRECARGA 3

// Creamos una lista parking a partir de la lista garaje
ArrayList<Coche> parking = new ArrayList<Coche>(garaje);

// Mostramos la lista parking donde se ve que tiene los 
// mismos coches que el ArrayList garaje
for (Coche coche : parking) {
  System.out.println(coche);
}
```

<a name="metodos_y_propiedades"></a>

# M茅todos y propiedades generales

En la documentaci贸n oficial de Oracle se pueden encontrar todos los m茅todos de la `Class ArrayList<E>` (https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html#ArrayList-java.util.Collection-). En este manual indicamos los m谩s utilizados que son:

``` Java
// A帽adir un objeto Coche al final del ArrayList
garaje.add(fordFocus);

// A帽ade el elemento al ArrayList en la posici贸n 'n'
garaje.add(3, setArosa);

// Devuelve el numero de elementos del ArrayList
garaje.size();

// Devuelve el elemento que esta en la posici贸n '2' del ArrayList
garaje.get(2);

// Comprueba si existe del objeto Coche que se le pasa como parametro
garaje.contains(audiA4);

// Devuelve la posici贸n del primer objeto Coche fordFocus encontrado en el ArrayList  
garaje.indexOf(fordFocus);

// Devuelve la posici贸n del 煤ltimo objeto Coche fordFocus en el ArrayList   
garaje.lastIndexOf(fordFocus);

// Borra el elemento de la posici贸n '2' del ArrayList   
garaje.remove(2); 

// Borra el primer objeto Coche fordFocus encontrado en el ArrayList que se le pasa como parametro.  
garaje.remove(fordFocus);

//Borra todos los elementos de ArrayList   
garaje.clear();

// Devuelve True si el ArrayList esta vacio. Sino Devuelve False   
garaje.isEmpty();  

// Pasa el ArrayList a un Array 
Object[] array = garaje.toArray();   
```

<a name="a帽adir"></a>

# A帽adir datos a la colecci贸n

Aunque previamente hemos mostrado algunos m茅todos para a帽adir y eliminar datos, vamos a describirlos con m谩s detalle en este ep铆grafe.

### A帽adir elementos desde el constructor

La clase ArrayList es una colecci贸n que no permite desde los constructores 1 `public ArrayList()` y 2 `public ArrayList(int initialCapacity)` a帽adir elementos en su creaci贸n. 

### A帽adir elementos a partir de otras colecciones

S贸lo a trav茅s del constructor 3 `public ArrayList(Collection<? extends E> c)` es posible, tal y como hemos visto en el ejemplo anterior:

``` Java
// Creamos una lista parking a partir de la lista garaje
ArrayList<Coche> parking = new ArrayList<Coche>(garaje);

// Mostramos la lista parking donde se ve que tiene los mismos coches 
// que el ArrayList garaje
for (Coche coche : parking) {
  System.out.println(coche);
}
```

### A帽adir elementos mediante c贸digo

Aun con todo lo anterior, lo interesante de los ArrayList es su **capacidad de adaptaci贸n a a帽adir nuevos elementos a la lista**. Por tanto, sea cual sea la forma en la que hemos creado el ArrayList, podemos a帽adir elementos a la misma con los siguiente m茅todos: 

鉁忥笍 **.add(E e)**

El m茅todo `.add(E e)` a帽ade el elemento que indiquemos en su argumento al final del ArrayList e incrementa su longitud en +1:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje. Nos devolver谩 valor = 3
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Creamos un nuevo objeto Coche
Coche opelCorsa = new Coche("Opel", "Corsa", "2000", 27000);

// A帽adimos el nuevo Coche al ArrayList
garaje.add(opelCorsa);

// Revisamos de nuevo la cantidad de elementos del ArrayList
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}
```

鉁忥笍 **.add(int index, E element)**

El m茅todo `.add(int index, E element)` es una variante del anterior en donde podemos especificar en el primer argumento la posici贸n en la que queremos insertar el nuevo elemento dentro del ArrayList:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje. Nos devolver谩 valor = 4
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}

// Creamos un nuevo objeto Coche
Coche hondaAccord = new Coche("Honda", "Accord", "1800", 31000);

// A帽adimos el nuevo Coche al ArrayList en la posici贸n 2
garaje.add(2, hondaAccord);

// Revisamos de nuevo la cantidad de elementos del ArrayList para ver que se ha incrementado en 1
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos y comprobar 
// que en la posici贸n 2 se encuentra el nuevo coche
for (Coche coche : garaje) {
  System.out.println(coche);
}
```

鉁忥笍 **.addAll(Collection<? extends E> c)**

El m茅todo `.addAll(Collection<? extends E> c)` a帽ade una lista completa de elementos que indiquemos en su argumento al final del ArrayList e incrementa su longitud en la misma cantidad de elementos que tiene la lista del argumento:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje. Nos devolver谩 valor = 5
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Revisamos la cantidad de elementos del ArrayList parking. Nos devolver谩 valor = 3
int cantidadElementosEnArrayList = parking.size();
System.out.println("La cantidad de elementos en el ArrayList parking es: " 
                    + cantidadElementosEnArrayList);

// Aplicamos el m茅todo
garaje.addAll(parking);

// Revisamos de nuevo la cantidad de elementos del ArrayList
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}
```

鉁忥笍 **.addAll(int index, Collection<? extends E> c)**

El m茅todo `.addAll(int index, Collection<? extends E> c)` es una variante del anterior en donde podemos especificar en el primer argumento la posici贸n en la que queremos insertar la lista de elementos dentro del ArrayList:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje. Nos devolver谩 valor = 8
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Revisamos la cantidad de elementos del ArrayList parking. Nos devolver谩 valor = 3
int cantidadElementosEnArrayList = parking.size();
System.out.println("La cantidad de elementos en el ArrayList parking es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}

// Aplicamos el m茅todo insertando la lista en la posici贸n 2
garaje.addAll(2, parking);

// Revisamos de nuevo la cantidad de elementos del ArrayList
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}
```

### Eliminar elementos mediante c贸digo

De la misma manera que a帽adir elementos a ArrayList es lo que lo hace interesante, tambi茅n tiene la capacidad de poder eliminarlos. Hay **5 m茅todos** para eliminar elementos de un ArrayList:

鉁忥笍 **.remove(int index)**

El m茅todo `.remove(int index)` elimina el elemento que se encuentra en la posici贸n que le indiquemos del ArrayList:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje. Nos devolver谩 valor = 11
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}

// Eliminamos el elemento de la posici贸n 2
garaje.remove(2);

// Revisamos de nuevo la cantidad de elementos del ArrayList
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}
```

鉁忥笍 **.remove(Object o)**

El m茅todo `.remove(Object o)` elimina el primer elemento del ArrayList que coincide con el elemento pasado como argumento al m茅todo:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje.
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}

// Eliminamos el elemento fordFocus
garaje.remove(fordFocus);

// Revisamos de nuevo la cantidad de elementos del ArrayList
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}
```

鉁忥笍 **.removeAll(Collection<?> c)**

El m茅todo `.removeAll(Collection<?> c)` elimina del ArrayList todos aquellos elementos que coinciden con los indicados en la lista que pasamos como argumento al m茅todo:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje.
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}

// Eliminamos la lista parking
garaje.removeAll(parking);

// Revisamos de nuevo la cantidad de elementos del ArrayList
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}
```

鉁忥笍 **.removeRange(int fromIndex, int toIndex)**

El m茅todo `.removeRange(int fromIndex, int toIndex)` elimina del ArrayList todos aquellos elementos que se encuentran entre la posici贸n inicial `fromIndex` y la posici贸n final `toIndex`:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje.
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// A帽adimos la lista parking para incrementar la cantidad de elementos en ArrayList
garaje.addAll(parking);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}

// Eliminamos de la posici贸n 1 a 3
garaje.removeRange(1,3);

// Revisamos de nuevo la cantidad de elementos del ArrayList
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}
```
鉁忥笍 **.removeIf(Predicate<? super E> filter)**

El m茅todo `.removeIf(Predicate<? super E> filter)` elimina del ArrayList todos aquellos elementos que cumplen con el predicado (la condici贸n) descrita como argumento en el m茅todo e indicada como expresi贸n lambda:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje.
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// A帽adimos la lista parking para incrementar la cantidad de elementos en ArrayList
garaje.addAll(parking);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}

// Eliminamos aquellos que tengan un precio > 30000
garaje.removeIf(coche -> (coche.getPrecio() > 30000));

// Revisamos de nuevo la cantidad de elementos del ArrayList
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos el ArrayList para que nos muestre sus elementos
for (Coche coche : garaje) {
  System.out.println(coche);
}
```

<a name="recorrer"></a>

# Recorrer la colecci贸n

Aunque ya hemos visto a lo largo de este manual una forma de recorrer un ArrayList, vamos a explicar en este ep铆grafe las distintas maneras que tenemos de obtener los datos que contiene el mismo:

鉁忥笍 **Bucle for**

El bucle `for` recorre el ArrayList posici贸n a posici贸n. Podemos recorrerlo entre las posiciones que indiquemos o especificar que lo recorra hasta el final con la propiedad `.size()`:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje.
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// A帽adimos la lista parking para incrementar la cantidad de elementos en ArrayList
garaje.addAll(parking);

// Recorremos el ArrayList desde la posici贸n 1 a 3
for (int i=1; i<=3; i++) {
  System.out.println(garaje.get(i));
}

// Recorremos el ArrayList completo
for (int i=0; i<garaje.size(); i++) {
  System.out.println(garaje.get(i));
}
```

鉁忥笍 **M茅todo .forEach()**

El m茅todo `.forEach()` nos permite simplificar el c贸digo cuando queremos recorrer por completo el ArrayList:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje.
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Recorremos todo el ArrayList con una expresi贸n lambda
garaje.forEach((coche) -> System.out.println(coche));
```

鉁忥笍 **M茅todo .iterator()**

El m茅todo `.iterator()` es una construcci贸n que se utiliza para recorrer colecciones. Es aplicable a ArrayList:

``` Java
// Revisamos la cantidad de elementos del ArrayList garaje.
int cantidadElementosEnArrayList = garaje.size();
System.out.println("La cantidad de elementos en el ArrayList garaje es: " 
                    + cantidadElementosEnArrayList);

// Generamos el Iterator y lo arrancamos con un bucle while
Iterator<Coche> it = garage.iterator();
while(it.hasNext())
    System.out.println(it.next());
```
鉁忥笍 **Con expresiones lambda**

En el caso de recorrer un ArrayList completo, las expresiones lambda solo se utilizan junto con el m茅todo `.forEach()` tal y como hemos visto. La expresi贸n lambda que hay que utilizar es

``` Java

(coche) -> System.out.println(coche)
```
En ella se indica que para cada elemento de la lista (que se le ha nombrado con la variable `coche` pero podr铆a ser cualquier otro nombre) se realice la acci贸n `System.out.println`.

Es en la b煤squeda de elementos concretos donde estas expresiones tienen m谩s potencial. Esto lo veremos en el siguiente punto.

<a name="buscar"></a>

# B煤squeda de elementos

鉁忥笍 **Con un bucle (for / foreach / Iterator)**

Combinando un bucle `for / foreach / Iterator` junto con un condicional `if`, nos permite hacer una b煤squeda dentro del ArrayList y cuando salte la condici贸n, realizar la acci贸n que programemos:

``` Java
// Hacemos un bucle for de principio a fin y dentro realizamos un if
for (int i=0; i<garaje.size(); i++) {  
        if (coche.getMarca().equals("Ford"))  {
                System.out.println(coche);
            }
};   
```

鉁忥笍 **Con expresiones lambda**

Con la misma funcionalidad que el anterior pero con menos c贸digo, existe una variante del m茅todo `.foreach()` en la que podemos especificar mediante expresiones lambda una condici贸n que en caso de cumplirse nos permita realizar sobre ella la acci贸n que explicitemos, en este caso es un sencillo `System.out.println`:

``` Java
// Condicionamos la busqueda a mostrar aquellos que sean marca Ford
garaje.forEach((coche) -> {
            if (coche.getMarca().equals("Ford"))  {
                System.out.println(coche);
            }
        });
```

鉁忥笍 **Con API Stream**

Los API Stream nos permiten aplicar la llamada *Programaci贸n Funcional* a la b煤squeda de un elemento en un ArrayList mediante el uso de `.filter` que se apoya en expresiones lambda:

``` Java
// Condicionamos la busqueda a mostrar aquellos que sean marca Ford
garaje.Stream().filter(coche -> coche.getMarca().equals("Ford"));
```

<a name="subcolecciones"></a>

# Obtenci贸n de subcolecciones

Entendemos como subcolecci贸n un nuevo ArrayList de menor longitud que el ArrayList original y cuyos elementos se encuentran ordenados (o no) en la misma posici贸n relativa en ambos. Para obtenerlos podemos aplicar lo aprendido en el anterior punto `B煤squeda de elementos` donde buscaremos elemento a elemento y, cuando se cumpla una condici贸n especificada, a帽adir los elementos encontrados a una nueva coleccion (o subcolecci贸n) tal y como se ha aprendido en `A帽adir datos a la colecci贸n`.

<a name="ordenar"></a>

# Ordenaci贸n de elementos

### Con funciones de Collection

Para la ordenaci贸n del ArrayList con la clase `Collections` implementamos la colecci贸n de la siguiente manera:

``` Java
// Iniciamos la colecci贸n
import java.util.Collections;
```

Esta clase consta exclusivamente de m茅todos est谩ticos que operan o devuelven colecciones. Para la ordenaci贸n de elementos, utilizaremos el m茅todo `.sort()` contenido en la clase `Collections`, el cual implementa 2 sobrecargas:

鉁忥笍 **.sort(List<T> list)**

Ordena la lista especificada en orden ascendente, seg煤n el orden natural de sus elementos:

``` Java
Collections.sort(garaje);
garaje.forEach((coche) -> System.out.println(coche));
```
馃毇 鈿狅笍隆OJO!鈿狅笍 馃毇 Esto no va a funcionar porque el m茅todo `.sort()` se puede utilizar de esta manera s贸lo con tipos primitivos (String, Integer, float...). Para que funcione con un Arraylist de objetos, hemos de utlizar la interfaz `Comparator`. Lo vemos en el siguiente punto 猬囷笍

鉁忥笍 **.sort(List<T> list, Comparator<? super T> c)**

Existen clases comparadoras predefinidas que nos permiten ordenar de alguna otra forma los ArrayList de tipos primitivos. Una de ellas muy utilizada es `Collections.reverseOrder()`, la cual permite ordenar de forma descendente un ArrayList. Vamos a hacer un ejemplo fuera de la linea de este manual -ya que este manual se est谩 realizando sobre el objeto `Coche`- para que se vea:

``` Java
ArrayList<String> lenguajesProgramacion = new ArrayList<String>();
  
        lenguajesProgramacion.add("Java");
        lenguajesProgramacion.add("C#");
        lenguajesProgramacion.add("Go");
        lenguajesProgramacion.add("Phyton");
        lenguajesProgramacion.add("PHP");
  
        System.out.println("ArrayList no ordenado: "
                           + lenguajesProgramacion);
  
        Collections.sort(lenguajesProgramacion, Collections.reverseOrder());
  
        System.out.println("Array ordenado de forma descendente: " + lenguajesProgramacion);
```

Para ordenar un ArrayList de objetos no primitivos, hemos de crear una clase vac铆a que implementar谩 la interfaz `Comparator` y en la que dise帽aremos el c贸digo de comparaci贸n de dos objetos. Primero importamos la clase `Comparator` con `import java.util.Comparator;` y a continuaci贸n escribimos:

``` Java
public class CompararCoches implements Comparator<Coche>{
     
     @Override
     public int compare(Coche coche1, Coche coche2){
        if(coche1.getPrecio()<coche2.getPrecio()){
            return -1;
        }else if(coche1.getPrecio()<coche2.getPrecio()){
            return 0;
        }else{
            return 1;
        }
    }     
}
```
De esta manera, nos permitir谩 ordenar el ArrayList `garaje` por precio ascendente de los coches o por cualquier atributo de la clase `Coche`:

``` Java
Collections.sort(garaje, new CompararCoches());
garaje.forEach((coche) -> System.out.println(coche));
```

### Con expresiones lambda

El uso de expresiones lambda nos permite simplificar el anterior c贸digo sin tener que incluir la clase `CompararCoches`. Esta clase, con una expresi贸n lambda pasar铆a de esto:

``` Java
public class CompararCoches implements Comparator<Coche>{
     
     @Override
     public int compare(Coche coche1, Coche coche2){
        if(coche1.getPrecio()<coche2.getPrecio()){
            return -1;
        }else if(coche1.getPrecio()<coche2.getPrecio()){
            return 0;
        }else{
            return 1;
        }
    }     
}
```
a esto:

``` Java
(Coche coche1, Coche coche2)->coche1.getPrecio().compareTo(coche2.getPrecio());
```

Por tanto se escribir铆a el c贸digo de esta forma:

``` Java
garaje.sort((Coche coche1, Coche coche2)->coche1.getPrecio().compareTo(coche2.getPrecio()));
```

Y para ordenar por orden inverso, s贸lo deber铆amos de cambiar el orden de los coches:

``` Java
garaje.sort((Coche coche1, Coche coche2)->coche2.getPrecio().compareTo(coche1.getPrecio()));
```

### Con API Stream

Ordenar un ArrayList con la programaci贸n funcional que nos permite API Stream es mucho m谩s sencillo en el caso de un ArrayList de objetos, pero debemos hacerlo a una lista auxiliar. Para ello inicializaremos con `.stream()`, ordenaremos con `.sorted()` y escribiremos con `.collect(Collectors.toList())` en la nueva lista:

``` Java
List<Coche> nuevoGaraje = garaje.stream().sorted().collect(Collectors.toList());
nuevoGaraje.forEach((Coche) -> System.out.println(Coche));
```
Interesante indicar dos funcionalidades m谩s: orden invertido con `Comparator.reverseOrder()` y comparar por atributo con `Comparator.comparing(Class::getter)`:

``` Java
// Con Comparator.reverseOrder()
List<Coche> nuevoGaraje = garaje.stream()
                                .sorted(Comparator.reverseOrder())
                                .collect(Collectors.toList());
nuevoGaraje.forEach((Coche) -> System.out.println(Coche));

// Con Comparator.comparing(Class::getter)
List<Coche> nuevoGaraje = garaje.stream()
                                .sorted(Comparator.comparing(Coche::getPrecio))
                                                  .collect(Collectors.toList());
nuevoGaraje.forEach((Coche) -> System.out.println(Coche));
```
<a name="webgraf铆a"></a>

# Webgraf铆a

- https://www.geeksforgeeks.org/arraylist-in-java/?ref=lbp
- https://www.w3schools.com/java/java_arraylist.asp
- https://guru99.es/how-to-use-arraylist-in-java/
- https://www.javadevjournal.com/java/java-arraylist/
- https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html
- https://www.discoduroderoer.es/formas-de-ordenar-un-arraylist/
- https://www.baeldung.com/java-sorting
- https://www.javatpoint.com/how-to-sort-arraylist-in-java