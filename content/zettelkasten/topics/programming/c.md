---
title: C 🌱
draft: false

---


## Memoria dinámica
Hay varios casos que nos pueden llevar a necesitar usar memoria dinámica:

#### 1: Necesitas memoria cuyo tamaño no conoces en tiempo de compilación
Ejemplo: leer un archivo cuyo tamaño no sabes.
```
// <- No podemos hacer esto, porque file_size no es una constante en tiempo de compilación
char buffer[file_size];
```


#### 2: Necesitas estructuras que “vivan” después de que salga una función
```
int *create_number() {
    int x = 10;
    return &x;   // ¡ERROR! x desaparece al salir de la función
}
```

#### 3. Necesitas crear un número variable de elementos (listas, arrays crecientes, árboles...)
Ejemplo: un array dinámico que crece:
```
int *arr = malloc(10 * sizeof(int)); // empieza con 10
arr = realloc(arr, 20 * sizeof(int)); // ahora tiene 20
```
Si usaras memoria estática, tendrías que decidir el tamaño máximo antes de compilar, lo cual es absurdo en muchos casos.

#### 4. Otros casos
- Necesitas grandes cantidades de memoria. La memoria de stack (automática) suele ser muy pequeña comparada con el heap.
- Datos compartidos entre hilos: La memoria automática está ligada al stack de cada hilo. Si quieres compartir datos entre threads, el heap es obligatorio.
