---
title: C++
draft: false

---

## Plantilla de clase
`std::function` es una plantilla de clase de la librería estándar `functional`. Sirve para guardar y usar funciones “como objetos”. Puedes guardar dentro una función normal, una lambda, o cualquier objeto que se comporte como una función (functor). Su plantilla es:
```
template <typename Signature>
class std::function;
```

Por ejemplo, `std::function<float(double)>`, es una función que recibe un double y devuelve un float

## Funciones lambda
Una lambda es una forma rápida de escribir una función “anónima”, es decir, sin tener que darle un nombre ni declararla antes. La plantilla general de una lambda es:
```
[captures](parameters) -> return_type {
    // cuerpo de la función
}
```

Por ejemplo:
```
auto f = [] (float x) { return std::sin(x); };
float result = f(3.14f / 2); // → 1
```
- `[]` → zona de captura (variables externas que quieres usar dentro del cuerpo). En este caso está vacía → no captura nada.
- `(float x)` → los parámetros de la función.
- `{ return std::sin(x); }` → el cuerpo.
- `auto f` = → la guardas en una variable

## Punteros
Un puntero es una variable que guarda una dirección de memoria. No guarda el valor directamente, sino dónde está el valor. Por ejemplo:
```
int x = 10;   // x ---> [10]
int* p = &x;  // p ---> guarda la dirección de x
```

### Referencias Vs Punteros
C++ incluye un nuevo concepto para gestionar punteros: la referencia. Cuando pasas una variable por referencia en C++, la función recibe otro nombre (alias) de la variable original, no una copia.
Por tanto, si modificas la referencia, modificas directamente la variable original.

El caracter `&` tiene dos usos diferentes dependiendo del contexto:
- En una declaración de variable o parámetro, declara una **referencia**: `int& ref = x;`. Una referencia evita copiar el objeto, que ya existe en otro lugar, para conseguir ahorro en CPU y memoria.
- En una expresión, devuelve la dirección de memoria (uso como **puntero**): `p = &x;`

De igual forma, el caracter `*` también tiene dos usos (igual que en C):
- En una declaración, donde declara un puntero: `int* ptr;`
- En una expresión, donde **desreferencia** un puntero (accede al valor apuntado): `int y = *ptr;`

### Diferencia con C
C y C++ comparten punteros, pero C no tiene referencias. En C, para modificar una variable dentro de una función, hay que pasar un puntero (la dirección de memoria). Esto no implica un gran coste de CPU o memoria, porque solo se copia la dirección, no el valor completo.

En C++, las referencias son una forma más segura y cómoda de gestionar los punteros para hacer lo mismo.

Ejemplo en C:
```
void f(int* x) { *x = 10; }

int main() {
    int a = 5;
    f(&a); // paso la dirección
    // a ahora vale 10
}
```
Ejemplo en C++:
```
void f(int& x) { x = 10; }

int main() {
    int a = 5;
    f(a); // paso la variable directamente
    // a ahora vale 10
}
```

### Punteros únicos
C++ introduce los llamados `unique pointers`: punteros inteligentes que manejan memoria automáticamente. Es memoria dinámica, el equivalente en C a usar `malloc` y `free`, pero en C++ la gestión de la memoria se realiza de forma automática: cuando el `unique_ptr` sale de ámbito, libera la memoria sin que tengas que llamar manualmente a `delete`.

Un puntero único tiene utilidad, por ejemplo, cuando queremos que el objeto viva más tiempo que el ámbito de la función. Solo puede haber un único puntero propietario de un objeto a la vez.

Ejemplo: creación de un puntero único del tipo `juce::RangedAudioParameter`:
```
std::vector<std::unique_ptr<juce::RangedAudioParameter>> params;
```


## Inicialización uniforme
C++11 introdujo la llamada inicialización uniforme (uniform initialization), también conocida como brace initialization:
```
AudioBlock<float> audioBlock { buffer }; // inicialización con llaves
AudioBlock<float> audioBlock (buffer);    // inicialización clásica con paréntesis
```
Ambas formas llaman al mismo constructor, pero usar `{}` tiene algunas ventajas: evita conversiones implícitas inesperadas (más seguro), permite inicialización con múltiples parámetros de forma uniforme y funciona con listas de inicialización, incluso para arrays o agregados.
