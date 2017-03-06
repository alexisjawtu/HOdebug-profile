Con make all compilamos y tenemos los 4 ej

**add_array_dynamic.c**:
algo raro: en la func add_array() i va hasta
n + 1 en vez de n. No obstante, parece andar para n=3 y n=4. Lo corregimos.
Ese es el bug que encontramos.

Lo pasamos por gdb y no obtuvimos nada.

**add_array_segfault**:
-cambio '<= n+1' por '< n' como antes.
-Para que la memoria se maneje din'amicamente, incluimos las instrucciones con
malloc, para lo cual tuvimos que incluir stdlib.h

-Si volvemos a poner los errores y corremos con '-g' tenemos:

_Program received signal SIGSEGV, Segmentation fault.
0x00000000004005f2 in main (argc=1, argv=0x7fffffffde58) at add_array_segfault.c:22
22      b[i] = i;_

Suponemos que esto quiere decir que inmediatamente antes no pudo hacer 'a[0] = 0;'
por estar mal alocada la memoria.

-Flag de optim para debuggear: -O0, que hace que el compilador use literalmente
nuestro c'odigo. Recibimos

_Program received signal SIGSEGV, Segmentation fault.
0x00000000004005f2 in main (argc=1, argv=0x7fffffffde58) at add_array_segfault.c:22
22      b[i] = i;_

Lo interpretamos como en el caso del flag '-g' m'as arriba.

-Incluimos el flag '-Wall': ahora nos damos cuenta de que no est'a encontrando abs()
y el linker lo resuelve de alguna manera. Probamos con **#include <math.h>** y no
cambi'o. Probamos con **#include <stdlib.h>** y desapareci'o el warning.
Suponemos algo an'alogo para todos los source files sin **#include <stdlib.h>**
que usen abs().

**add_array_static.c**
-cambio '<= n+1' por '< n' como antes.
Sin este cambio mostraba una suma, que creemos que es el resultado de sumar
los n'umeros en los lugares de memoria contiguos al 'ultimo lugar de nuestros
arreglos.