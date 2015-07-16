# Prueba de programación
- Escriba una función que ordene las claves en un hash por el tamaño de la
clave convertida en cadena

Respuesta en Compilador Online: http://repl.it/xIq/18
```
def ordenar(hash)
    hash.keys.sort_by{|k|k.to_s.length}.map(&:to_s)
end

ordenar({ abc: 'hello', 'another_key' => 123, 4567 => 'third' }
)
```


- ¿Cuál es la diferencia entre una clase y un módulo?

La diferencia es que un modulo solo contiene metodos y constantes agrupados(pero no un estado), no se pueden instanciar y solo puede incluirse en clases a través de mixins. La clase Class hereda de la clase Module pero Class añade la capacidad a las clases de tener un estado a través de las variables de instancia.

- ¿Cuál es la diferencia entre un symbol :foo y un string "foo"?
  
La diferencia es que un string "foo" genera un nuevo objecto con un nuevo object_id cada vez que aparece en el programa. Por otro lado, un symbol :foo referencia a un solo object_id en todas sus apariciones en el programa, ocupando menos memoria.

- Al momento de hacer testing, ¿cuál es la diferencia entre usar fixtures y usar
factories?

Ambos sirven para poblar la base de datos para realizar pruebas. La diferencia es que los fixtures son simples archivos de texto plano(por ejemplo YAML) que se cargan en masa por el framework(puede ser lento si se cargan muchos fixtures innecesarios para el test), mientras que los factories son codigo (por ejemplo un archivo .rb) y se puede usar estos factories para generar instancias y guardar en la base de datos dinamicamente en tiempo de ejecucion segun los requerimientos de un test especifico.

- Explique algunos beneficios de utilizar Redis

Al ser una base de datos en memoria, permite un performance mucho mayor comparado con las bases de datos tradicionales en los tiempo de lectura/escritura. Debido a que sus estructuras estan basadas en clave-valor, tiene una estructura ma ssimple y más eficiente para casos de uso específicos.

- Explique el aggregation framework de MongoDB

El aggregation framework de MongoDB sirve para hacer consultas aggregadas (sort, group by, etc) de manera eficiente. Es una alternativa más sencilla que usar el MapReduce de MongoDB para el mismo fin.

- ¿Qué beneficio tiene utilizar background jobs? Mencione las diferencias entre las gemas más utilizadas para background jobs (resque, sidekiq, delayed_job)

Los background jobs permiten que una aplicacion (por ejemplo basada en Rails) no demore esperando por atender una tarea especifica que tome demasiado tiempo, sino que trabaje esa tarea de manera asincrona poniendola en una cola cuyo procesamiento se realiza en un proceso distinto. 

Delayed_job es la gema mas sencilla de usar pero mezcla el codigo sincrono y asincrono; y solo tiene soporte estable para ActiveRecords relativamente lento (solo soporte expermiental para Redis). Resque hace una separacion entre el codigo sincrono y aincrono y esta basado en Redis, por lo cual es mas veloz al usar la base de datos en memoria. Sidekiq tiene los beneficios de Resque de la separacion de codigo síncrono/asíncrono y la velocidad de usar Redis; es mas veloz debido a su arquitectura basada en threads en lugar de procesos pero esto hace mas dificil su uso al requerir que solo se utilicen librerias y codigo thread safe.

- ¿Qué son los proc?

Proc es la clase cuyos objetos son bloques de codigo reutilizables que tienen variables locales de manera similar a los methodos. Los bloques no son objetos pero pueden convertirse a objetos de la clase Proc. 

- Explique la diferencia entre require, include y load en Ruby

La instruccion include se utiliza para incluir modulos (mix-in) que ya se encuentran en memoria, mientras que require y load se usan para cargar archivos. La diferencia entre los 2 ultimos es que require carga una sola vez el archivo, mientras que load cargará el archivo cada vez que sea llamado sin importar si ya esta en memoria.

- Describe un poco tu entorno de desarrollo (de preferencia en Ruby o RoR)

Actualmente utilizo un entorno cloud en cloud9 (www.c9.io) basado en Ubuntu (Antes usaba un servicio similar www.nitrous.io). Sin embargo también he utilizado localmente Ubuntu con SublimeText y tambien entorno Windows con una shell basada en Cygwin llamada Babun, conectando remotamente via ssh a una maquina virtual con Ubuntu en mi pc o a una instancia de Amazon EC2 con Ubuntu, utilizando Vim o Emacs. Normalmente uso git por consola, Github y Heroku para desplegar.

- Explique de qué manera implementaría una sección de reportes que realizan
consultas de gran cantidad de datos, sin que esto afecte el rendimiento normal
de la aplicación. Ejemplos de reportes pueden ser: usuarios que realizaron
nuevas compras en un rango de fechas, usuarios registrados en la aplicación
y no han realizado ninguna compra. Considerar a la aplicación como el
backend para una tienda en línea que ofrece un API para sus aplicaciones
móviles y un dashboard para monitorear y mantener toda la información
registrada.

Si al momento de generar el reporte no se requiere que la data este actualizada hasta ese instante (real-time),una posible solución seria implementar una base de datos adicional (datamart) para reportes que solo contenga la data necesaria para los reportes y tenga una estructura especialmente diseñada para generar los reportes. Se realizaria una carga incremental a traves de una herramienta ETL o un proceso de replicación a intervalos definidos (tomando en cuenta los requisitos de los reportes y los intervalos con menor carga en la base de datos).

Si existe un requerimiento de tiempo real y se necesita que los reportes esten actualizados hasta el mismo instante de la generacion del reporte, migraría la base de datos a un tipo de base de datos NewSQL como NuoDB, la cual hace uso de tecnologia in-memory para poder optimizar los tiempos de lectura/escritura y poder abastecer los requerimientos transaccionales y de reportes con grandes cantidades de datos con un buen performance.





