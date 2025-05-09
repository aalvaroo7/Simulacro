# Simulacro

https://github.com/aalvaroo7/Simulacro.git

# Parte I: Capa de red
## Ejercicio 1

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

## Ejercicio 2

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

