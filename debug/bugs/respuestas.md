Con make all compilamos y tenemos los 4 ej

add_array_dynamic.c: algo raro: en la func add_array() i va hasta
n + 1 en vez de n. No obstante, parece andar para n=3 y n=4.
Lo corregimos. Ese es el bug que encontramos.

Lo pasamos por gdb y no obtuvimos nada.