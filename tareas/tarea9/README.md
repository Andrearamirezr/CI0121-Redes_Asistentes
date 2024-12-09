# Solución de la tarea 9

El resultado final debería ser el siguiente:

| Paquete | Tiempo de LLegada | Tamaño | Tiempo de finalización | Orden de salida |
| ------- | :---------------: | :----: | :--------------------: | :-------------: |
| A       |         0         |   8    |           8            |        1        |
| B       |         5         |   6    |           8            |        2        |
| C       |         5         |   10   |           15           |        4        |
| D       |         8         |   20   |          12,5          |        3        |
| E       |         8         |   14   |           23           |        6        |
| F       |        10         |   16   |           16           |        5        |
| G       |        11         |   19   |           33           |        8        |
| H       |        20         |   28   |           24           |        7        |

## Solución

Para resolver la tarea se debe utilizar la siguiente formula para calcular el tiempo de finalización:

$$
\text{Finalización} = max(\text{Finalización anterior}, \text{Tamaño del paquete}) + \frac{\text{Tamaño del paquete}}{\text{Peso de la cola}}
$$

Entonces por ejemplo para el paquete E sería:

$$
\text{Finalización}_E = max(15, 8) + \frac{8}{1}
$$

$$
\text{Finalización}_E = 15 + 8 = 23
$$

> [!NOTE]  
> Cada paquete va a una cola en especifica, Cola superior (A, F), Cola intermedia (B, D, H), Cola inferior (C, E, G).
