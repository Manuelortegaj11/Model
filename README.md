# Modelo de Optimización para Gestión de Demanda de Queso Costeño

## Descripción

El modelo de optimización presentado está diseñado para gestionar la demanda de queso costeño a través de una plataforma de marketing, utilizando múltiples centros de acopio. El objetivo principal es minimizar los costos asociados con el cumplimiento de la demanda del cliente, considerando los costos de transporte, tiempos de alistamiento y producción potencial en los centros de acopio.

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

\sum_{i=1, i \neq p}^{N} \left[ K(CAi) \cdot Precio(CAi) + K(CAi) \cdot cTransp(CAi) + Tiempo(CAi) \cdot cTiempo \right] + \left[ K(CAp) \cdot Precio(CAp) + Demanda \cdot cTransp(CAp) + Tiempo(CAp) \cdot cTiempo \right]

## Restricciones

1. **Restricción de Demanda:**
\sum_{i=0}^{N} K(CAi) = Demanda

2. **Restricción de Stock y Producción Potencial:**
K(CAi) \leq Stock(CAi) + P_{\text{potencial}}(CAi) \quad \text{para } i=0 \ldots N

3. **Cálculo del Tiempo Total:**
Tiempo(CAi) = Tiempo_{\text{Alistam}}(CAi) + Tiempo_{\text{Transp}}(CAi)

4. **Restricción de Tiempo de Alistamiento:**
Tiempo_{\text{Alistam}}(CAi) \leq Tiempo_{\text{MaxDefinido}} \quad \text{para } i=0 \ldots N



