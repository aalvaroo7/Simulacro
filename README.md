# Simulacro

https://github.com/aalvaroo7/Simulacro.git

# Ejercicio 1

## a) Algoritmo de Dijkstra

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

## b) Enrutamiento por Inundación (Flooding)

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

