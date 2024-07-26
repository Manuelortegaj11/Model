# Modelo de Optimización para Gestión de Demanda de Queso Costeño

## Descripción

El modelo de optimización presentado está diseñado para gestionar la demanda de queso costeño a través de una plataforma de marketing, utilizando múltiples centros de acopio. El objetivo principal es minimizar los costos asociados con el cumplimiento de la demanda del cliente, considerando los costos de transporte, tiempos de alistamiento y producción potencial en los centros de acopio.

## Objetivo

El objetivo del modelo de optimización es asignar de manera eficiente cada demanda de queso a un centro de acopio principal, asegurando que se minimice el costo total del producto/s. En situaciones en las que el centro de acopio principal no tenga suficiente stock para satisfacer completamente la demanda, este debe poder solicitar cantidades adicionales a otros centros de acopio disponibles. El modelo considera varias restricciones críticas para garantizar la viabilidad de la solución: se asegura de que la cantidad total de queso enviada desde los centros de acopio satisfaga la demanda total, que el stock y la producción potencial de cada centro sean respetados, y que el tiempo combinado de alistamiento y transporte no exceda un límite máximo permitido. Además, se implementan restricciones para equilibrar el transporte entre centros de acopio y asegurar que el centro de acopio principal maneje efectivamente la cantidad total de demanda. La solución final debe identificar el centro de acopio principal más adecuado para cada demanda, optimizando la asignación de queso y el transporte entre centros de manera que se mantenga dentro de las restricciones de tiempo y capacidad, garantizando así una operación eficiente y costo-efectiva.

## Variables del Problema

- **N**: Número de centros de acopio.
- **CAi**: Identificador del centro de acopio \( i \) para \( i=0 \ldots N \), donde \( i \neq p \). Estos centros de acopio complementan las unidades de producto de la demanda que el centro de acopio principal no tiene disponibles. Los centros de acopio **CAi** despachan hacia el centro de acopio principal.
- **CAp**: Identificador del centro de acopio principal \( p \) (\( p \in [0, N] \) y \( p \neq i \)). Este centro de acopio atiende directamente al cliente y es responsable de enviar la demanda completa al cliente.
- **K(CAi)**: Cantidad del producto que se despacha desde el centro de acopio **CAi**, incluyendo unidades en stock y unidades potenciales que pueden estar listas en poco tiempo.
- **Precio(CAi)**: Precio por kilo del producto despachado desde el centro de acopio **CAi**.
- **cTransp(CAi)**: Costo del transporte del pedido desde el centro de acopio **CAi** a su destino.
- **TiempoAlistam(CAi)**: Tiempo en horas para alistar el pedido desde el centro de acopio **CAi** a su destino.
- **TiempoMaxDefinido**: Tiempo máximo definido para considerar la producción potencial.
- **TiempoTransp(CAi)**: Tiempo de transporte desde el centro de acopio **CAi** a su destino.
- **Tiempo(CAi)**: Tiempo total en horas para que el pedido llegue desde el centro de acopio **CAi** a su destino, sumando el tiempo de alistamiento y el tiempo de transporte.
- **cTiempo**: Costo adicional por cada unidad de tiempo contemplado en la variable **Tiempo(CAi)**.
- **Demanda**: Cantidad de producto solicitada por el cliente.
- **Stock(CAi)**: Stock del producto en el centro de acopio **CAi**.
- **Ppotencial(CAi)**: Cantidad de producto que potencialmente puede estar disponible en poco tiempo (potencial del día).
  
---

## Datos de Entrada

- **demanda**: Cantidad de producto de acuerdo con la categoría del pedido a satisfacer.
- **costo_transporte**: Costo por unidad de tiempo de espera para satisfacer la demanda.
- **id**: Identificadores de Centro de Acopio (**CAi**).
- **kg**: Stock del Producto en el Centro de Acopio (**Stock(CAi)**).
- **produccion_potencial**: **Ppotencial(CAi)**.
- **costos_transporte**: **cTransp(CAi)**.
- **precio**: Precio del Producto por Kilo (**Precio(CAi)**).
- **tiempos_transporte**: Tiempos de Transporte (**TiempoTransp(CAi)**).
- **tiempo_alistamiento**: Tiempos de Alistamiento (**TiempoAlistam(CAi)**).

Claro, aquí tienes la traducción al español:

---

## Esquema

Los centros de acopio $` n `$ se representan como un vector, cada uno con una cantidad definida $` x `$.
La cantidad para la posición $` i `$ representa la cantidad de la demanda total $` D `$ que el centro de acopio $` j_i `$ va a suministrar.

$$
\begin{array} {|r|r|r|r|r|r|}
    \hline x_0 & x_1 & x_2 & x_3 & \cdots & x_n \\
    \hline
\end{array}
\quad \therefore \quad x_i = cacopios_i
$$

---
## Función Objetivo

Minimizar:

$$
\sum_{i=1, i \neq p}^{N} \left[ K(CA_i) \cdot Precio(CA_i) + K(CA_i) \cdot cTransp(CA_i) + Tiempo(CA_i) \cdot cTiempo \right] + \left[ K(CA_p) \cdot Precio(CA_p) + Demanda \cdot cTransp(CA_p) + Tiempo(CA_p) \cdot cTiempo \right]
$$

## Restricciones

1. **Restricción de Demanda:**

$$
\sum_{i=0}^{N} K(CA_i) = Demanda
$$

2. **Restricción de Stock y Producción Potencial:**

$$
K(CA_i) \leq Stock(CA_i) + P_{\text{potencial}}(CA_i) \quad \text{para } i=0 \ldots N
$$

3. **Cálculo del Tiempo Total:**

$$
Tiempo(CA_i) = Tiempo_{\text{Alistam}}(CA_i) + Tiempo_{\text{Transp}}(CA_i)
$$

4. **Restricción de Tiempo de Alistamiento:**

$$
Tiempo_{\text{Alistam}}(CA_i) \leq Tiempo_{\text{MaxDefinido}} \quad \text{para } i=0 \ldots N
$$

