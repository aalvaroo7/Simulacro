# Simulacro

https://github.com/aalvaroo7/Simulacro.git

# Parte I: Capa de red
## Pregunta 1

### a) Algoritmo de Dijkstra

Dijkstra encuentra la ruta más corta desde un nodo origen hacia todos los demás en un **grafo ponderado** sin pesos negativos.

###  Pasos Básicos:

1. Inicializa la distancia a todos los nodos en ∞, excepto el origen (0).
2. Marca todos los nodos como no visitados.
3. Selecciona el nodo no visitado con menor distancia.
4. Actualiza la distancia de sus vecinos si se encuentra un camino más corto.
5. Marca el nodo como visitado.
6. Repite hasta visitar todos los nodos o llegar al destino.

###  Ejemplo
    A --2-- B

    | /

    1 3

    | /

    C



| Nodo | Distancia desde A | Visitado | Predecesor |
|------|-------------------|----------|-------------|
| A    | 0                 | ✅       | -           |
| B    | 4                 | ✅       | C           |
| C    | 1                 | ✅       | A           |

Ruta más corta de A a B: **A → C → B** con costo **1 + 3 = 4**.

### b) Enrutamiento por Inundación (Flooding)

El enrutamiento por inundación consiste en que cada nodo envía el paquete recibido a todos sus vecinos, excepto al que se lo envió. Este proceso continúa hasta que el paquete llega a su destino o se descarta.

### Comparación: Flooding vs. Dijkstra

| Característica       | Flooding                            | Dijkstra                                 |
|----------------------|-------------------------------------|------------------------------------------|
| Tipo                 | Dinámico, no dirigido               | Algoritmo determinista                   |
| Envío de paquetes    | A todos los vecinos                 | Solo por la ruta más corta               |
| Redundancia          | Alta (muchas copias de paquetes)    | Baja                                     |
| Uso de recursos      | Ineficiente                         | Eficiente                                |
| Tiempos de cómputo   | Nulo (no necesita cálculo)          | Requiere procesamiento                   |
| Adaptabilidad        | Alta (bueno para redes dinámicas)   | Menor (requiere actualización de rutas)  |
| Evita bucles         | No (requiere TTL o historial)       | Sí                                       |

### Ventajas del Flooding

- Simple de implementar.  
- Alta confiabilidad: llega al destino incluso si hay múltiples fallos.  
- Ideal para redes desconocidas o cambiantes.  

### Desventajas del Flooding

- Uso excesivo de ancho de banda.  
- Duplicación de paquetes.  
- Riesgo de tormentas de red si no se controla con TTL o historial.

## Pregunta 2

### a) Para la subred 172.29.152.0 con máscara 255.255.248.0, determina la dirección de broadcast.

#### Paso 1: Convertir la máscara a binario
- Máscara: `255.255.248.0`
- En binario:  
  `11111111.11111111.11111000.00000000` → **/21** (21 bits de red)

#### Paso 2: Identificar el rango de la subred
- Subred base: `172.29.152.0`
- Bloque de salto:  
  La subred cambia cada `2^(32 - 21) = 2048` direcciones.

- La subred `172.29.152.0/21` abarca desde:
  - Primera IP: `172.29.152.0`
  - Última IP del bloque:  
    `172.29.159.255` (porque 152 + 7 = 159 en el tercer octeto)

####  Dirección de Broadcast:
- **172.29.159.255**

---

### b) Dado el bloque 172.18.26.0/23, calcula la dirección de broadcast y justifica el proceso.

#### Paso 1: Interpretar el prefijo `/23`
- `/23` equivale a máscara `255.255.254.0`
- 23 bits de red, 9 bits para hosts → `2^9 = 512` direcciones

#### Paso 2: Determinar el rango del bloque
- Bloque: `172.18.26.0/23`
- Cubre desde:
  - Primera IP: `172.18.26.0`
  - Última IP del bloque: `172.18.27.255`

####  Dirección de Broadcast:
- **172.18.27.255**

## Pregunta 3: Última Dirección Válida y Rango de Hosts

### a) Subred: 172.30.67.192 / Máscara: 255.255.255.192

#### Paso 1: Convertir la máscara
- 255.255.255.192 → en binario: `11111111.11111111.11111111.11000000` → **/26**
- 26 bits de red → 6 bits para hosts → `2^6 = 64` direcciones por subred

#### Paso 2: Calcular el rango de la subred
- Subred comienza en `172.30.67.192`
- Tamaño del bloque: 64 direcciones
- Broadcast: `192 + 63 = 255` → `172.30.67.255`

#### Paso 3: Última dirección de host válida
- Broadcast: `172.30.67.255`
- Último host válido: **`172.30.67.254`**

---

### b) Host: 172.22.53.199 / Máscara: 255.255.252.0

#### Paso 1: Convertir la máscara
- 255.255.252.0 → en binario: `11111111.11111111.11111100.00000000` → **/22**
- 22 bits de red → 10 bits para hosts → `2^10 = 1024` direcciones por subred

#### Paso 2: Determinar a qué subred pertenece
- Tercer octeto del host: 53
- Subred de /22 cambia cada 4 en el tercer octeto (porque 256 - 252 = 4)
- 53 pertenece al rango de subred que comienza en **52**

#### Paso 3: Calcular el rango
- Primera IP de la subred: `172.22.52.0`
- Última IP: `172.22.55.255`
- Rango de hosts válidos:
  - Primera: `172.22.52.1`
  - Última: `172.22.55.254`

####  Resultado:
- **Rango de direcciones válidas:**  
  **172.22.52.1** a **172.22.55.254**

## Pregunta 4: Capacidad y Segmentación de Subredes

### a) ¿Cuántos hosts pueden conectarse en la red 172.26.0.0 con máscara 255.255.255.192?

#### Paso 1: Analizar la máscara
- Máscara: 255.255.255.192 → en binario: `11111111.11111111.11111111.11000000` → **/26**
- Bits de host: 32 - 26 = 6
- Total de direcciones: `2^6 = 64`
- Resta 2 direcciones reservadas:
  - Dirección de red
  - Dirección de broadcast

####  Resultado:
- **Número de hosts útiles:** `64 - 2 = 62`

---

### b) Host: 172.18.171.190/23 → ¿A qué subred pertenece?

#### Paso 1: Interpretar la notación CIDR
- Prefijo /23 → Máscara: 255.255.254.0
- Abarca bloques de 512 direcciones (`2^9`), agrupando dos subredes de clase C

#### Paso 2: Calcular el bloque correspondiente
- Dirección: 172.18.171.190
- El tercer octeto es 171
- Como 254 → salta de 2 en 2 (256 - 254 = 2), el bloque al que pertenece es el que empieza en el múltiplo de 2 más cercano hacia abajo:

  - `171 ÷ 2 = 85` → `85 × 2 = 170`

#### Resultado:
- **Subred base:** `172.18.170.0/23`
- Rango de la subred: `172.18.170.0` a `172.18.171.255`
- El host `172.18.171.190` **pertenece a la subred 172.18.170.0/23**

  
## Pregunta 5: Número de Subredes Necesarias

### Fórmula para calcular el número de subredes:
Nº de subredes
=2^s

Donde:
- `s` es el número de **bits prestados** del campo de **host** para usarlos como parte del **identificador de subred**.

---

### ¿Cómo funciona?

En una red con una máscara por defecto, podemos "tomar prestados" bits del campo de host para crear más subredes. Cada bit prestado **duplica** la cantidad de subredes posibles.

---

### Ejemplo: Necesitamos al menos 4 subredes

1. Buscamos el valor mínimo de `s` tal que `2^s ≥ 4`.
2. Probamos:

   - `2^1 = 2` → insuficiente  
   - `2^2 = 4` → suficiente  

3. Por lo tanto, debemos **prestar 2 bits** al campo de subred.

---

### Resultado

- Con **2 bits prestados**, podemos crear exactamente **4 subredes**.
- Esto puede aplicarse, por ejemplo, a una red de clase C con máscara original `255.255.255.0 (/24)`:
  - Si prestamos 2 bits → nueva máscara: `/26` (24 + 2)
  - Subredes disponibles: `2^2 = 4`

---

### Subredes resultantes de un /26:

| Subred         | Rango de Hosts         | Broadcast         |
|----------------|------------------------|-------------------|
| 192.168.1.0/26 | 192.168.1.1 - 62       | 192.168.1.63      |
| 192.168.1.64/26| 192.168.1.65 - 126     | 192.168.1.127     |
| 192.168.1.128/26| 192.168.1.129 - 190   | 192.168.1.191     |
| 192.168.1.192/26| 192.168.1.193 - 254   | 192.168.1.255     |


# Parte II: Capa de Transporte

### Pregunta 6: Comparación entre TCP y UDP

---

### a) Comparación entre TCP y UDP

| Característica                   | TCP (Transmission Control Protocol)     | UDP (User Datagram Protocol)         |
|----------------------------------|------------------------------------------|--------------------------------------|
| Establecimiento de conexión     | Sí (conexión orientada, requiere 3-way handshake) | No (sin conexión)                    |
| Fiabilidad y control de errores | Alta: retransmisiones, verificación y acuse de recibo | Baja: no hay confirmaciones ni corrección de errores |
| Control de flujo y congestión   | Sí (controla velocidad y congestión)     | No                                   |
| Velocidad de transmisión        | Menor (más control, más sobrecarga)      | Mayor (menor sobrecarga)             |

---

### b) Aplicaciones donde se prefiere UDP

1. **Streaming de video/audio (Ej. YouTube Live, videollamadas)**
   - Se prioriza la **velocidad** sobre la fiabilidad.
   - Algunos paquetes perdidos no afectan tanto como el retraso.

2. **Juegos en línea (Ej. FPS, MMO)**
   - Se necesita **respuesta rápida**.
   - Retransmitir paquetes antiguos no tiene sentido en entornos en tiempo real.

---

UDP se elige cuando la **rapidez y baja latencia** son más importantes que la fiabilidad de la entrega.

## Pregunta 7: Establecimiento y Terminación de Conexión en TCP

### Establecimiento de Conexión: Three-Way Handshake

El proceso de conexión en TCP se realiza en tres pasos, conocidos como **Three-Way Handshake**, para garantizar que ambos extremos están listos para la comunicación:

1. **SYN (Synchronize)**  
   - El cliente envía un segmento con el bit `SYN` activado e incluye un número de secuencia inicial (ISN).  
   - Indica que el cliente desea iniciar una conexión.

2. **SYN-ACK (Synchronize + Acknowledge)**  
   - El servidor responde con un segmento que tiene los bits `SYN` y `ACK` activados.  
   - Acepta la solicitud del cliente y envía su propio número de secuencia.

3. **ACK (Acknowledge)**  
   - El cliente responde con un segmento con el bit `ACK` activado.  
   - Confirma que recibió correctamente la respuesta del servidor.

 **Conexión establecida**: a partir de aquí, los datos pueden intercambiarse de manera confiable.

---

### Terminación de Conexión: Four-Way Handshake

La terminación de una conexión TCP se hace en cuatro pasos para cerrar la conexión de forma ordenada en ambos sentidos:

1. **FIN (Finish) - desde el cliente**  
   - El cliente indica que ha terminado de enviar datos y quiere cerrar la conexión.

2. **ACK - desde el servidor**  
   - El servidor reconoce la solicitud del cliente.

3. **FIN - desde el servidor**  
   - El servidor también indica que ha terminado de enviar datos.

4. **ACK - desde el cliente**  
   - El cliente confirma la finalización de la conexión.

 **Conexión cerrada**: ambas partes han acordado terminar la comunicación.

---

### Importancia de cada proceso

- **Three-Way Handshake** asegura que ambas partes acuerdan los parámetros de comunicación y están listas para intercambiar datos.
- **Four-Way Handshake** garantiza que cada extremo cierre la conexión de forma independiente, evitando la pérdida de datos.

## Pregunta 8: Multiplexación y Demultiplexación en la Capa de Transporte

### ¿Qué es la Multiplexación?

La **multiplexación** es el proceso mediante el cual múltiples aplicaciones pueden compartir una misma conexión de red a través de un protocolo de transporte (como TCP o UDP).  
Se utilizan **puertos** para distinguir las diferentes comunicaciones.

---

### Multiplexación Ascendente

- **Definición:**  
  Proceso por el cual varios procesos de distintas aplicaciones en el **host origen** envían datos a través de una única conexión de red hacia el destino.

- **Ejemplo práctico:**  
  En un equipo, el navegador web (puerto 50000), un cliente de correo (puerto 50001) y un cliente FTP (puerto 50002) se comunican simultáneamente con distintos servicios externos por Internet, todos usando la misma dirección IP del host origen.

---

### Multiplexación Descendente (Demultiplexación)

- **Definición:**  
  Proceso por el cual el **host destino** recibe segmentos TCP/UDP y los dirige al proceso de aplicación correcto basándose en el **número de puerto de destino**.

- **Ejemplo práctico:**  
  Un servidor con IP pública recibe múltiples conexiones entrantes:
  - Las peticiones HTTP (puerto 80) se envían al servidor web.
  - Las peticiones SSH (puerto 22) se envían al servidor SSH.
  - Las peticiones DNS (puerto 53) se envían al servicio DNS.

---

### Resumen

| Tipo                  | ¿Dónde ocurre?         | Función principal                                       |
|-----------------------|------------------------|---------------------------------------------------------|
| Multiplexación ascendente | En el host origen        | Identifica el proceso que envía datos salientes         |
| Multiplexación descendente | En el host destino       | Entrega los datos entrantes al proceso correcto         |

# Pregunta 9: Cálculo del Tamaño de Ventana en TCP

### Datos proporcionados:

- RTT (Tiempo de ida y vuelta) = **50 ms**
- Ancho de banda = **100 Mbps**
- MSS (Tamaño máximo de segmento) = **1,500 bytes**

---

### Paso 1: Convertir unidades

- RTT = 50 ms = **0.05 segundos**
- Ancho de banda = 100 Mbps = **100 × 10⁶ bits/segundo**

---

### Paso 2: Calcular el tamaño óptimo de la ventana

**Fórmula:**
Ventana 
óptima
=
Ancho de banda
×
RTT


**Sustituyendo valores:**

Ventana óptima = 100,000,000 bits/s × 0.05 s = 5,000,000 bits

Convertimos a **bytes**:
5,000,000 bits ÷ 8 = 625,000 bytes

---

### Paso 3: Calcular número de segmentos MSS
Número de MSS = Ventana óptima en bytes ÷ MSS
Número de MSS = 625,000 ÷ 1,500 ≈ 416.67
---

###  Resultado Final

- **Tamaño óptimo de ventana:**  
  - **5,000,000 bits**  
  - **625,000 bytes**

- **Número aproximado de segmentos MSS en tránsito:**  
  - **417 segmentos**

---

### Interpretación

Para aprovechar completamente el enlace de 100 Mbps con un RTT de 50 ms, el tamaño de ventana TCP debería ser de **625,000 bytes**, permitiendo que unos **417 segmentos MSS** estén en tránsito al mismo tiempo.

## Pregunta 10: Control de Congestión en TCP

TCP utiliza varios mecanismos para evitar la congestión en la red y garantizar un rendimiento eficiente. A continuación, se describen tres algoritmos clave:

---

### 1. Algoritmo de Arranque Lento (Slow Start)

**Objetivo:**  
Evitar sobrecargar la red al inicio de una conexión.

**Funcionamiento:**  
- Comienza enviando solo 1 segmento (MSS).
- Cada vez que se recibe una confirmación (ACK), la ventana de congestión (`cwnd`) se **duplica**, creciendo exponencialmente.
- Este crecimiento continúa hasta alcanzar un umbral llamado **ssthresh**.
- Una vez alcanzado, cambia a crecimiento lineal (conocido como *congestion avoidance*).

**Contribución al rendimiento:**  
Evita inyectar muchos datos de golpe en la red, reduciendo el riesgo de congestión inicial.

---

### 2. Algoritmo de Nagle

**Objetivo:**  
Reducir el número de pequeños paquetes enviados, especialmente en aplicaciones que generan muchos mensajes cortos.

**Funcionamiento:**  
- TCP agrupa pequeños segmentos y los retiene si hay datos sin confirmar.
- Solo se envía un paquete si no hay datos pendientes o si se ha recibido una confirmación.

**Contribución al rendimiento:**  
Mejora la eficiencia del uso del ancho de banda al reducir el tráfico innecesario de paquetes pequeños (minimiza la sobrecarga).

---

### 3. Algoritmo de Clark

**Objetivo:**  
Evitar el envío de muchos pequeños paquetes debido a una ventana de recepción parcialmente abierta.

**Funcionamiento:**  
- El receptor **no anuncia pequeñas aperturas** de su ventana (por ejemplo, 1 o 2 bytes).
- Espera hasta tener suficiente espacio antes de notificar al emisor.

**Contribución al rendimiento:**  
Reduce la fragmentación y previene el envío de datos ineficientes, mejorando el uso del canal y evitando congestión innecesaria.

---

### Resumen

| Algoritmo     | Objetivo principal                  | Beneficio para la red                         |
|---------------|-------------------------------------|------------------------------------------------|
| Slow Start    | Evitar congestión inicial           | Controla el crecimiento del tráfico al inicio |
| Nagle         | Reducir tráfico de paquetes pequeños| Optimiza uso del ancho de banda               |
| Clark         | Evitar envíos ineficientes          | Mejora rendimiento y reduce fragmentación     |

# Parte III: Capa de Aplicación y Aplicaciones Multimedia

## Pregunta 11: Funcionamiento de DNS

### ¿Qué es DNS?

El **Sistema de Nombres de Dominio (DNS)** traduce nombres de dominio legibles por humanos (como `www.ejemplo.com`) en direcciones IP necesarias para localizar servidores en la red.

---

### Proceso de Resolución de Nombres

1. **El usuario ingresa un dominio en el navegador**
   - Ejemplo: `www.ejemplo.com`

2. **Consulta a la caché local del sistema operativo**
   - Se verifica si la IP ya está almacenada en la caché DNS local.

3. **Consulta al servidor DNS configurado (generalmente del proveedor de Internet)**
   - Si no está en caché, el sistema envía una **consulta recursiva** al DNS local.

4. **El servidor DNS local consulta a un servidor raíz**
   - Si tampoco tiene la respuesta, pregunta a un **servidor raíz DNS**, que responde con la dirección del **servidor TLD** correspondiente (`.com`, `.org`, etc.).

5. **Consulta al servidor TLD**
   - El TLD devuelve la dirección del **servidor autoritativo** para el dominio.

6. **Consulta al servidor autoritativo**
   - Este servidor proporciona la dirección IP exacta asociada al nombre de dominio solicitado.

7. **Respuesta al navegador**
   - El DNS local guarda la respuesta en caché y envía la IP al navegador.

8. **El navegador establece la conexión con la IP obtenida**
   - Se inicia una conexión HTTP/HTTPS con el servidor usando la dirección IP.

---

### Ejemplo simplificado

Usuario → DNS local → Servidor raíz → Servidor TLD (.com) → Servidor autoritativo → IP del dominio


---

### Importancia

- **Velocidad**: gracias a la caché, muchas resoluciones se hacen rápidamente.
- **Escalabilidad**: el sistema jerárquico distribuye la carga.
- **Fiabilidad**: si un servidor falla, se pueden usar réplicas o alternativas.



## Pregunta 12: Protocolos de Correo Electrónico

Los protocolos POP3, IMAP y SMTP son esenciales para el envío y recepción de correos electrónicos. A continuación se presentan sus diferencias clave:

---

### Comparación de Protocolos

| Protocolo | Función Principal                | Tipo de Uso y Acceso                            | Modo de Almacenamiento de Correos                    |
|-----------|----------------------------------|--------------------------------------------------|------------------------------------------------------|
| **POP3**  | Descargar correos del servidor   | Acceso desde un solo dispositivo                | Correos se descargan y eliminan del servidor         |
| **IMAP**  | Sincronizar correos con el servidor | Acceso desde múltiples dispositivos             | Correos permanecen en el servidor                    |
| **SMTP**  | Envío de correos electrónicos    | Utilizado para enviar mensajes a otros servidores | No almacena correos; solo se encarga del envío       |

---

### Ejemplos de uso adecuados

- **POP3**  
  - Ideal cuando se desea guardar los correos localmente y liberar espacio del servidor.
  - Ejemplo: usuarios con almacenamiento limitado en la nube y que solo usan un único dispositivo.

- **IMAP**  
  - Recomendado para usuarios que acceden al correo desde diferentes ubicaciones o dispositivos.
  - Ejemplo: usuarios que usan su cuenta en un teléfono, computadora y webmail.

- **SMTP**  
  - Utilizado por todos los clientes de correo para enviar mensajes.
  - Ejemplo: cuando Outlook o Gmail envía un correo, usa SMTP para entregarlo al servidor de destino.

---

### Resumen

- **POP3**: descarga y elimina → local y único acceso.
- **IMAP**: sincroniza → multiacceso y basado en servidor.
- **SMTP**: envía → solo para el envío de mensajes.

## Pregunta 13: Funcionamiento de HTTP y FTP

---

### a) Funcionamiento de HTTP (HyperText Transfer Protocol)

**HTTP** es un protocolo de nivel de aplicación que permite la transferencia de recursos (páginas web, imágenes, etc.) entre un cliente (navegador) y un servidor web, generalmente sobre el puerto **80** (o **443** con HTTPS).

#### Métodos más utilizados:

| Método  | Descripción                                                |
|---------|------------------------------------------------------------|
| **GET**     | Solicita un recurso del servidor (solo lectura)             |
| **POST**    | Envía datos al servidor, común en formularios               |
| **PUT**     | Actualiza o reemplaza un recurso existente en el servidor  |
| **DELETE**  | Elimina un recurso del servidor                            |

**Funcionamiento básico:**

1. El cliente (navegador) abre una conexión TCP al servidor.
2. Envía una solicitud HTTP (por ejemplo, `GET /index.html`).
3. El servidor responde con el contenido solicitado (por ejemplo, una página HTML).
4. Se cierra o reutiliza la conexión (según la versión del protocolo).

---

### b) Funcionamiento de FTP (File Transfer Protocol)

**FTP** permite transferir archivos entre un cliente y un servidor, generalmente usando los puertos **21** (control) y **20** (datos).

#### Características clave:

- Requiere autenticación (usuario y contraseña).
- Usa **dos conexiones separadas**:
  - **Conexión de control (puerto 21):** para comandos y respuestas.
  - **Conexión de datos (puerto 20):** para la transferencia real de archivos.

**Funcionamiento básico:**

1. El cliente establece la conexión de control.
2. Envía comandos como `LIST`, `GET`, `PUT`.
3. Se abre una conexión de datos para cada archivo transferido.
4. Se transfieren los datos y se cierra la conexión de datos (la de control permanece abierta).

---

### Diferencias principales entre HTTP y FTP

| Característica     | HTTP                               | FTP                                          |
|--------------------|------------------------------------|----------------------------------------------|
| Uso principal      | Transferencia de contenido web     | Transferencia de archivos                    |
| Conexión           | Una única conexión                 | Dos conexiones (control y datos)             |
| Autenticación      | Opcional o mediante cookies/token  | Requiere usuario y contraseña (generalmente) |
| Facilidad de uso   | Más simple y soportado por navegadores | Requiere cliente FTP o configuración especial |

## Pregunta 14: Streaming y VoIP

---

### a) Tipos de Streaming

| Tipo                     | Descripción breve                                                                 | Ejemplo de aplicación          |
|--------------------------|------------------------------------------------------------------------------------|-------------------------------|
| **UDP Streaming**        | Transmisión en tiempo real con el protocolo UDP. No hay garantía de entrega ni retransmisión. Es rápido pero menos fiable. | Transmisiones en vivo (ej. IPTV) |
| **HTTP Streaming**       | Los datos se transmiten mediante HTTP. El contenido se descarga progresivamente como una secuencia de archivos. | YouTube en calidad fija        |
| **DASH (Adaptive HTTP Streaming)** | Divide el contenido en pequeños segmentos y ajusta dinámicamente la calidad según el ancho de banda disponible. | Netflix, YouTube (adaptativo) |

---

### b) Funcionamiento de VoIP (Voz sobre IP)

**VoIP (Voice over IP)** permite la transmisión de voz mediante redes IP, convirtiendo la voz analógica en paquetes digitales.

#### Proceso básico:

1. **Captura de voz** mediante micrófono.
2. **Codificación y compresión** de la señal de voz (usando códecs como G.711, G.729).
3. **Segmentación en paquetes IP**, normalmente transportados sobre **UDP**.
4. **Transmisión de los paquetes** a través de la red IP.
5. **Recepción y reensamblaje** de los paquetes en el destino.
6. **Decodificación y reproducción** de la voz en el altavoz del receptor.

#### Problemas comunes y soluciones:

| Problema        | Descripción                                | Solución                                   |
|-----------------|---------------------------------------------|--------------------------------------------|
| **Retardo**     | Tiempos de transmisión elevados             | QoS, uso de redes optimizadas para VoIP    |
| **Pérdida de paquetes** | Paquetes de voz que no llegan al destino       | Uso de códecs tolerantes, jitter buffer     |
| **Eco**         | Se escucha la propia voz con retraso        | Canceladores de eco, auriculares           |
| **Jitter**      | Variación en el tiempo de llegada de paquetes | Uso de jitter buffers                      |

---

### Resumen

- **UDP Streaming**: rápido pero sin garantía.
- **HTTP Streaming**: confiable, basado en descarga progresiva.
- **DASH**: se adapta a la calidad de conexión.
- **VoIP**: convierte la voz en paquetes IP, afectada por retardo y pérdida, pero puede mejorarse con QoS y códecs adecuados.

## Pregunta 15: Control de Congestión en Redes Multimedia

Las aplicaciones multimedia (como video en streaming o VoIP) requieren mecanismos especiales para mantener la calidad del servicio (QoS) y evitar la congestión en la red.

---

### 1. **Buffering en el cliente**

**Descripción:**  
Consiste en almacenar una parte del contenido multimedia antes de comenzar su reproducción. Esto permite absorber variaciones en la velocidad de la red (jitter) y pequeñas interrupciones.

**Cómo mejora la QoS:**
- Reduce cortes y pausas durante la reproducción.
- Permite una reproducción continua aunque haya fluctuaciones en el ancho de banda.
- Ideal para servicios como YouTube, Spotify o Netflix.

---

### 2. **Marcado de paquetes (DiffServ)**

**Descripción:**  
DiffServ (Differentiated Services) es una técnica que marca los paquetes en el encabezado IP con un valor (DSCP) que indica su prioridad. Los routers pueden tratar los paquetes multimedia con más prioridad que otros.

**Cómo mejora la QoS:**
- Prioriza el tráfico sensible al retardo (voz y video).
- Minimiza el retardo, la pérdida de paquetes y el jitter.
- Mejora el rendimiento de aplicaciones en tiempo real como videollamadas (Zoom, Skype).

---

### Conclusión

Estas técnicas ayudan a mantener una experiencia de usuario fluida y estable al gestionar eficazmente los recursos de red:

- **Buffering** actúa en el cliente para suavizar la entrega.
- **DiffServ** actúa en la red para garantizar prioridad de tráfico crítico.

## Pregunta 16: Best-Effort vs Servicios Multiclase

---

### Comparación entre Best-Effort y Servicios Multiclase

| Característica                        | **Best-Effort**                                      | **Servicios Multiclase (QoS)**                          |
|--------------------------------------|------------------------------------------------------|--------------------------------------------------------|
| **Manejo del tráfico**               | Todos los paquetes se tratan por igual, sin prioridad | Clasificación y priorización según tipo de tráfico     |
| **Garantía de calidad de servicio**  | No hay garantía de entrega, latencia o ancho de banda | Ofrece garantías (prioridad, retardo, pérdida, etc.)   |
| **Control de congestión**            | No aplica mecanismos especializados                  | Se implementan colas y políticas de gestión            |
| **Ejemplos de aplicaciones**         | Navegación web, correo electrónico                   | Videollamadas, streaming en vivo, VoIP                 |

---

### Explicación

- **Best-Effort**: modelo simple y escalable, pero no adecuado para aplicaciones sensibles al tiempo.
- **Servicios Multiclase (como DiffServ)**: permite adaptar la red para asegurar buen rendimiento a aplicaciones críticas, asignando diferentes clases de servicio.

---

### Ejemplos prácticos

- **Best-Effort**:
  - Navegar en un sitio web (HTTP).
  - Descargar un archivo mediante FTP.

- **Servicios Multiclase**:
  - Videoconferencia (prioridad alta para evitar interrupciones).
  - Tráfico de voz sobre IP (requiere baja latencia y pérdida).

# Parte IV: Seguridad en redes 


