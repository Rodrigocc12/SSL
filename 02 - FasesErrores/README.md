Secuencia de Pasos
1. Preprocesador
    a) Se escribió hello2.c, que es una variante de hello.c.

    b) Luego de escribir hello2.c, se lo ha preprocesado a un archivo hello2.i con el comando gcc -E hello2.c -o hello2.i
    Se ve en el hello2.i que hay lineas de codigo que muestran la ubicacion de los headers (.h) que tiene el hello2.c y procesa las directivas condicionales que corresponden.
    Por el momento no hubo un problema ya que el comando se ejecuto sin problema

    c) Se escribio hello3.c

    d) La primera linea basicamente se esta generando el prototipo de una funcion llamada printf que toma un puntero a una cadena de caracteres y (...) un numero variable de argumentos, y te devuelve un entero donde muestra la cantidad de caracteres impresos

    e) Generando el hello3.i se ve que la diferencia a simple vista con hello2.i es que tiene menos lineas de codigo ya que no incluyó a stdio.h, por lo que todas las inclusiones, declaraciones y definiciones no se tuvieron en cuenta para preprocesar.

2. Compilacion
    a) Se uso el comando gcc -S hello3.c -o hello3.s para generar el .s pero al compilar genero warning y un error, que es el de cerrar la llave "}"

    b) Se corrigio el error del hello3.c de cerrar la llave en el hello4.c y se genero el .s que da un codigo en lenguaje ensamblador donde: Reserva y 
    - gestiona el espacio de pila para variables locales.
    - Llama a funciones de inicialización.
    - Prepara y realiza una llamada a printf para imprimir un mensaje.
    - Finaliza limpiamente devolviendo 0.
    
    c) se uso el comando gcc -c hello4.s -o hello4.o para generar el .o

3. Vinculacion
    a) Para hacer el vinculo con la biblioteca estandar se uso el comando gcc hello4.o -o hello4 pero no resuelve la referencia a prontf, informando el error: "undefined reference to `prontf'".

    b) Se corrigio el error del prontf se cambio a printf en el hello5.c del cual si genero el ejecutable hello5.exe

    c) Se ejecuto el hello5.exe pero hay un bug y no imprime lo esperado

4. Correccion de bug
    a) Se ha arreglo el bug pasándole la variable i a printf en un nuevo archivo hello6.c, y funcionó como se esperaba.

5. Remoción de prototipo
    a) Se escribio una nueva variante, el hello7.c

    b) El programa sigue funcionando igual ya que gcc hace inferencias basándose en el nombre de la función 'printf' y vincula automáticamente con la biblioteca estándar, ya que asume que nuestra 'printf' es la de la biblioteca estándar.

6. Compilación Separada: Contratos y Módulos
    a) Se ha escrito studio1.c y hello8.c. En studio1.c se define 'prontf' y se la usa en hello8.c.

    b) Se ha generado hello8.exe corriendo el siguiente comando: gcc studio1.c hello8.c -o hello8.exe.
    Luego se corrió el ejecutable y funcionó como se esperaba.

    c) Si se agregan o eliminan argumentos a la invocación de prontf, sigue sin haber errores de compilación, pues en hello8.c no se le indica al compilador el cómo debe usarse 'prontf'.

    d) Se han generaron los archivos: studio.h, hello9.c y studio2.c. El header studio.h tiene el contrato, studio2.c tiene la implementación y hello9.c hace uso de ella. Ahora agregar o eliminar argumentos en la invocación del prontf tira un error de compilación, debido a que no se está cumpliendo su prototipo (o contrato) declarado en hello9.c mediante el #include.
    La ventaja es que el compilador asegura que ambas partes usan de misma forma la interfaz sin errores en la invocación por parte del cliente, ni errores en la implementación por parte del proveedor.