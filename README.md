# Caso de Estudio: Modelo Entidad-Relación para Tienda de Maquillaje "Beauty Glam"

## Objetivo de la Asignación
Diseñar y comprender el Modelo Entidad-Relación (MER) utilizando llaves primarias (PK), llaves foráneas (FK) y definiendo correctamente la cardinalidad entre las entidades, aplicado a un entorno real de gestión de inventario, clientes y pedidos en una tienda de maquillaje.

---

## 1. Prompt Utilizado (One-Shot Prompt)
Para iniciar la conceptualización de este proyecto y estructurar el caso de estudio, se utilizó la siguiente instrucción estructurada dirigida a un modelo de Inteligencia Artificial. Este "One-Shot Prompt" define el rol, el alcance y los requerimientos técnicos en una sola petición:

> "Actuarás como experto en manejo de base de datos. Quiero aprender el modelo entidad relación, usando primary key (PK) y foreign key (FK), así que he decidido tomar un caso de estudio basado en una tienda de maquillaje online. Crea un plano conceptual, buscando enfatizar ejemplos con la relación de cardinalidad para entender cómo se conectan las tablas de clientes, pedidos, detalles de pedidos y productos de maquillaje (como bases, labiales, paletas, etc.)."

---

## 2. Explicación del Modelo Conceptual (Notación de Chen)
A partir del análisis generado, se diseñó el diagrama conceptual adjunto (referenciado como `image_2.png` en el contexto del taller). El sistema se compone de cuatro entidades principales y sus respectivas relaciones:

*   **CLIENTE:** Almacena la información de contacto de los compradores. Su atributo principal (PK) es `ID_cliente`.
*   **PEDIDO:** Representa la orden de compra generada. Su PK es `ID_pedido`. Contiene la llave foránea `ID_cliente` para establecer una relación de cardinalidad **1:N** (Un cliente realiza muchos pedidos, pero un pedido pertenece a un solo cliente).
*   **PRODUCTOS:** Representa el inventario físico de maquillaje (ej. Bases de maquillaje, Labiales Mate, Paletas de Sombra). Su PK es `ID_producto`. Posee atributos adicionales como `Tipo_producto` y `Marca` para una correcta clasificación.
*   **DETALLE_PEDIDO:** Actúa como la entidad intermedia que resuelve la cardinalidad de Muchos a Muchos (N:M) entre los pedidos y los productos. 
    *   Posee una cardinalidad **1:N** con Pedido (Un pedido contiene muchos detalles).
    *   Posee una cardinalidad **N:1** con Productos (Muchos detalles incluyen un mismo tipo de producto de maquillaje).
    *   Utiliza `ID_pedido` y `ID_producto` como llaves foráneas para registrar la cantidad pedida y el precio de venta histórico en el momento exacto de la transacción, para mantener la integridad de la facturación.

## 3. Conclusión del Diseño
El uso de la entidad `detalle_pedido` garantiza que no exista duplicidad de datos y que el modelo cumpla con las reglas de normalización de bases de datos relacionales, separando correctamente la cabecera de la factura (Pedido) de los ítems individuales comprados (Detalle_Pedido). Esto permite llevar un control preciso de qué productos de maquillaje componen cada pedido sin redundancia.
