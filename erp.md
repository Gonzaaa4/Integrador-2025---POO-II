# Especificación de Requisitos de Software
# Proyecto: Sistema de Facturación 

## 1. Introducción


### Alcance

El sistema gestionará el ciclo de vida completo de la facturación de los clientes de una empresa de servicios, el alcance incluye:

* Gestión de Clientes, sus Cuentas y los servicios que contratan. 
* Generación de facturación, tanto de forma individual como masiva por período.
* Registro de pagos, permitiendo pagos totales y parciales.
* Anulación de facturas emitidas.

El sistema no incluye la liquidación de impuestos o la presentación de declaraciones juradas, pero sí debe manejar la información fiscal (IVA) necesaria para facturar correctamente.


---

## 2. Descripción General

El sistema esta diseñado para automatizar y ordenar el proceso de cobro de servicios recurrentes, reemplaza o formaliza un proceso que de otra manera sería manual (ej. en planillas de cálculo), propenso a errores y lento.


### Restricciones 

* El sistema debe operar conforme a la legislación argentina, específicamente en el manejo de las condiciones fiscales de los clientes frente al IVA (ej. Consumidor Final, Monotributista, Responsable Inscripto).

---

## 3. Requisitos Funcionales 

#### Gestión de Clientes y Cuentas

El sistema debe ser el repositorio central de la información de los clientes y sus cuentas.
* Se debe poder crear, leer, actualizar y eliminar la ficha de un Cliente, esta ficha debe contener datos básicos (Razón Social, CUIT/DNI) y su condición fiscal.
* Un Cliente puede tener una o más Cuentas, la Cuenta es la entidad que se factura.
* La Cuenta debe almacenar los Datos de la cuenta del usuario (ej. email de contacto para facturación, dirección, alias de la cuenta).
* La Cuenta debe tener un estado (ej. "Activa", "Inactiva", "Suspendida"), este estado es crucial para la facturacion masiva.
Esto es la base del sistema, sin clientes y cuentas activas no se puede saber a quién ni cómo facturar, el estado "Activa" es el criterio de filtro para la facturación masiva.

#### Gestión de Servicios

El sistema debe permitir definir los servicios que la empresa ofrece y asignarlos a las cuentas.
* Debe existir un catálogo de servicios (ej. "Hosting Básico", "Soporte Premium") con su precio unitario e impuestos aplicables.
* Se debe poder asociar uno o más servicios del catálogo a una Cuenta de cliente.
* La factura se genera de acuerdo a los servicios contratados, esta asociación es el motor de la facturación, define qué se le cobra a cada cliente.

#### Facturación

El sistema debe poder generar los comprobantes que representan la deuda del cliente por los servicios prestados.
* Toda factura debe incluir un detalle claro:
    * Datos del cliente.
    * Líneas de ítem con los servicios contratados, con sus precios.
    * Subtotal, desglose de IVA y Total.
    * Fecha de emisión y fecha de vencimiento.
* El sistema debe dar libertad para facturar individualmente, esto permite facturar a un cliente específico a demanda, fuera del ciclo normal.
* Se debe poder anular una factura emitida, esto es vital para corregir errores sin borrar registros, el sistema deberá manejar la lógica de negocio (ej. generar Nota de Crédito o simplemente marcarla como "Anulada").

#### Facturación Masiva

Siendo este un sistema de servicios, debe existir un proceso automático para facturar a todos los clientes de una sola vez.

* El criterio para la facturación masiva debe ser todas las cuentas activas.
* El usuario es el que inicia este proceso.
* El sistema debe guardar un registro de cada ejecución masiva, este registro debe incluir: "fecha de emisión, vencimiento" del lote y un listado de "facturas generadas" (o errores, si los hubo).
Esta es una funcionalidad reduce el trabajo manual de horas a un solo clic, minimizando errores y asegurando que se facture a todos los clientes activos.

#### Registro de Pagos

El sistema debe permitir el registro de pagos para saldar las facturas emitidas y completar el ciclo comercial.

* Al registrar un pago, se debe generar un "recibo por el pago hecho", este recibo debe tener su propio "Detalle de recibo" (qué facturas se pagan, monto, fecha de pago).
* El sistema debe permitir la forma de pago más simple, pagar el total de una o varias facturas.
* El sistema debe permitir un pago parcial donde el usuario puede marcar lo que quiero pagar seleccionando facturas específicas de una lista y pagar el 100% de esas, dejando otras impagas.
* El sistema debe permitir la imputación de pagos a cuenta., es decir el que paga pone el monto de cuánto quiere pagar de cada factura, esto implica que una factura puede tener un saldo restante (Deuda = Total Factura - Pagos Imputados).
Sin registro de pagos, el sistema solo genera deuda pero no la cancela, la flexibilidad en las formas de pago es fundamental para reflejar la realidad operativa, donde los clientes no siempre pagan el total exacto.

