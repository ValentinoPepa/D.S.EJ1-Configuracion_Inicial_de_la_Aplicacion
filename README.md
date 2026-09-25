# D.S.EJ1-Configuracion_Inicial_de_la_Aplicacion

[ConfiguracionApp.java](https://github.com/user-attachments/files/32664630/ConfiguracionApp.java)

<img width="523" height="233" alt="image" src="https://github.com/user-attachments/assets/41e0ceb7-513a-4a4c-8f1d-fa6cdc78644d" />

LOGICA (Pilares del Patron Singleton)

Para garantizar la unicidad de instancia y proveer un punto de acceso centralizado, la solución se apoya en cuatro decisiones clave de diseño

- **Constructor Privado (_private ConfiguracionApp()_):** Oculta la posibilidad de instanciar el objeto libremente desde afuera de la clase, bloqueando el operador _new_  para cualquier otra parte del sistema.
- **Campo estático privado (_private static ConfiguracionApp instancia_):** Es la variable que pertenece a la propia clase (y no a una instancia) donde se almacena en cache la ultima referencia existente.
- **Método estático publico (_obtenerInstancia()_):** Funciona como el canal de acceso global controlado. Aplica la **inicialización diferida** (_lazy initialization_): evalúa si el atributo _instancia_ es _null_; si lo es, invoca al constructor privado por única vez y guarda el objeto; en las siguientes llamadas, simplemente devuelve esa misma referencia guardada.
- **Encapsulamiento del estado (_Map<string, string>_):** guarda los parametros clave-valor dentro de una estructura interna pretegida, permitiendo la lectura y modificacion unincamente a traves de metodos expuestos como _obtenerParametro_

  EJECUCION
- **Primera solicitud (inicialización):** Cuando un modulo (por ejemplo, el Modulo de Autenticación) ejecuta _ConfiguracionApp.obtenerInstancia()_, el método verifica que _instancia == null_. En ese momento, ejecuta el constructor privado, carga los parámetros iniciales del sistema y  guarda el objeto en la variable estatica.
- **Solicitudes posteriores (Reutilización):** Cuando otro modulo (como el Modulo de Reportes) llama a _obtenerInstancia()_, la condición _null_ ya no se cumple, por lo que devuelve inmediatamente la referencia previa sin crear un nuevo objeto.
- **Verificación de la fuente de verdad:** Al comparar las referencias (_config1 == config2_), el resultado es _true_, demostrando que ambos módulos operan sobre el mismo espacio de memoria e interactúan con la misma fuente de verdad compartida. 
  

