# Roadmap del Proyecto: Sistema de Facturación

Este documento presenta el plan tentativo de entrega de las Historias de Usuario distribuidas en las dos iteraciones del proyecto, según lo definido en la especificación de requisitos.

La estrategia adoptada es desarrollar un Producto Mínimo Viable en la Iteración 1, este Producto Minimo Viable se centrará en el negocio: la gestión de las entidades principales (Clientes, Cuentas, Servicios) y la capacidad de generar una factura individual, esto nos permitirá tener una base funcional del 50%.

La Iteración 2 se enfocará en completar el ciclo comercial (Pagos, Anulaciones), añadir la funcionalidad de automatización (Facturación Masiva) y realizar una reestructuracion de la primera entrega para mejorar la calidad del código.

---

## Iteración 1
En esta primera iteracion el objetivo es establecer el modelo de dominio principal y la funcionalidad básica de gestión y facturación.
Al final de la iteración, el sistema debe ser capaz de gestionar clientes con sus servicios y generar una factura individual funcional, calculando el IVA correctamente.

### Historias de Usuario Iteración 1

**Gestión de Clientes y Cuentas**
* **HU-01:** Como usuario, quiero poder dar de alta, modificar y consultar Clientes, registrando su Razón Social, CUIT y Condición Fiscal (IVA), para tener toda la informacion de los clientes en un solo lugar.
* **HU-02:** Como usuario, quiero poder crear una o más Cuentas asociadas a un Cliente, definiendo su estado (Activa o Inactiva), para saber a quién se le debe facturar.

**Gestión de Servicios**
* **HU-03:** Como usuario, quiero poder gestionar un Catálogo de Servicios (definiendo nombre, precio unitario e impuestos aplicables) para saber qué servicios ofrece la empresa.
* **HU-04:** Como usuario, quiero poder asociar servicios del catálogo a una Cuenta de cliente, para definir qué se le debe cobrar en cada período.

**Facturación Individual**
* **HU-05:** Como usuario, quiero poder generar una Factura individual para una Cuenta específica, para poder facturar a demanda o fuera del ciclo periódico.
* **HU-06:** Como usuario, al generar una factura, quiero que el sistema calcule automáticamente los subtotales, el desglose de IVA y el total a pagar, basándose en los servicios contratados y la condición fiscal del cliente.

---

## Iteración 2: Funcionalidad Completa y Refactor

En la segunda iteracion el objetivo es completar el ciclo comercial (pagos, anulaciones), automatizar procesos (facturación masiva) y reestructurar el código de la Iteración 1.
Entregar el 100% de la funcionalidad requerida, con un código robusto y mantenible.

### Historias de Usuario Iteración 2

**Facturación Masiva**
* **HU-07:** Como usuario, quiero poder iniciar un proceso de Facturación Masiva para que el sistema genere automáticamente las facturas de todas las Cuentas con estado "Activa".
* **HU-08:** Como usuario, quiero poder consultar un registro de las ejecuciones de facturación masiva, para saber qué se facturó en cada lote.

**Registro de Pagos**
* **HU-09:** Como usuario, quiero poder registrar un Recibo de Pago, seleccionando una o más facturas para saldarlas (pago total).
* **HU-10:** Como usuario, quiero poder registrar un pago parcial imputando un monto específico a una factura, para que esta quede con un saldo pendiente (pago a cuenta).

**Gestión de Excepciones**
* **HU-11:** Como usuario, quiero poder Anular una factura emitida (generando la Nota de Crédito correspondiente o marcándola como anulada) para corregir errores.
