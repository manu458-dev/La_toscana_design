# Documento de Visión y Alcance  
## Proyecto: Sistema de Gestión Integral – La Toscana

---

**INDICE:**
1. Introducción
2. Contexto de negocio
    1. Antecedentes y problemática
    2. Necesidades
    3. Procesos clave del negocio actuales
3. Visión de la solución
    1. Frase de visión
    2. Procesos clave del negocio futuros
    3. Funcionalidades de alto nivel del sistema (épicas)
4. Alcance del proyecto
    1. Alcance
5. Contexto del sistema
    1. Resumen de Involucrados
    2. Entorno de operación

---

## 1. Introducción
El presente documento describe la visión y el alcance del proyecto de desarrollo del Sistema de Gestión Integral para la franquicia de cafeterías **La Toscana**.

El propósito de este documento es definir claramente el problema de negocio, las necesidades organizacionales, los procesos actuales y futuros, así como delimitar el alcance funcional del sistema a desarrollar. Este documento servirá como base para la planificación, estimación y ejecución del proyecto.

## 2. Contexto de negocio

### 2.1 Antecedentes y problemática

La Toscana es una franquicia de cafeterías con cinco sucursales ubicadas en:

- Iztapalapa  
- Chalco  
- Amecameca  
- Yecapixtla  
- Cuautla  

Opera de lunes a sábado de 8:00 AM a 10:00 PM.

Actualmente, la empresa presenta las siguientes problemáticas:

- Falta de control centralizado de ventas por sucursal.
- Órdenes no registradas o modificadas sin control.
- Errores en el cálculo manual de ingresos.
- Desperdicio y pérdidas de inventario.
- Corte de caja manual que consume hasta 8 horas cada domingo.
- Falta de visibilidad consolidada para el dueño.

Se estima que las pérdidas mensuales totales de la franquicia oscilan entre **$33,000 y $58,000 MXN**, lo que justifica la inversión en una solución tecnológica integral.

---

### 2.2 Necesidades

| ID | Descripción de la necesidad |
|----|-----------------------------|
| NEC-01 | La organización necesita contar con un control sistematizado de inventarios que permita conocer existencias y reducir desperdicios y pérdidas. |
| NEC-02 | La organización necesita gestionar de manera estructurada la relación con proveedores para garantizar abastecimiento oportuno y control de compras. |
| NEC-03 | La organización necesita automatizar el control financiero y el proceso de corte de caja para reducir errores humanos y tiempo operativo. |
| NEC-04 | La organización necesita registrar digitalmente las órdenes de los clientes con trazabilidad para evitar omisiones, modificaciones indebidas y pérdidas económicas. |
| NEC-05 | La organización necesita centralizar y administrar su catálogo de productos para mantener consistencia en precios, descripciones y disponibilidad entre sucursales. |
| NEC-06 | La organización necesita gestionar recetas estandarizadas para controlar el consumo de insumos y asegurar uniformidad en la preparación de productos. |
| NEC-07 | La organización necesita generar reportes consolidados de ventas, finanzas e inventario para facilitar la toma de decisiones estratégicas del dueño. |
| NEC-08 | La organización necesita disponer de un medio digital para que los clientes consulten la oferta de productos vigente en todas las sucursales. |
| NEC-09 | La organización necesita registrar clientes para implementar programas futuros de promociones y fidelización. |


### 2.3 Procesos clave del negocio (actuales)

Los siguientes procesos describen la operación actual (AS-IS) de La Toscana, antes de la implementación del sistema. Todos se realizan de forma **manual o semi-manual**, lo que genera las problemáticas expuestas en la sección 2.1.

| ID Proceso | Nombre del proceso | Actor principal | Descripción y pasos |
| --- | --- | --- | --- |
| PROC-01 | Registro de orden de mesa | Mesero | Mediante este proceso, el mesero registra la orden que un comensal solicita en el punto de consumo. <br> **Pasos:** <br> 1. El comensal llama al mesero y le indica verbalmente lo que desea ordenar. <br> 2. El mesero anota la orden en una libreta de papel (comanda). <br> 3. El mesero verifica verbalmente la orden con el comensal. <br> 4. El mesero lleva la comanda físicamente a la barra o cocina según corresponda. <br> 5. El mesero anota en su libreta el número de mesa y los productos solicitados para llevar un control propio. |
| PROC-02 | Preparación de productos | Barista / Cocinero | Mediante este proceso, el personal de barra o cocina prepara los productos solicitados por los comensales. <br> **Pasos:** <br> 1. El barista o cocinero recibe la comanda en papel del mesero. <br> 2. El barista o cocinero lee los productos solicitados y verifica que tenga los insumos necesarios. <br> 3. El barista o cocinero prepara los productos según su conocimiento (no hay receta estandarizada documentada). <br> 4. Una vez listos, el barista o cocinero avisa verbalmente al mesero o coloca el pedido en la barra de entrega. <br> 5. El mesero recoge los productos y los lleva a la mesa del comensal. |
| PROC-03 | Cobro al comensal | Cajero | Mediante este proceso, el cajero realiza el cobro de la cuenta al comensal al finalizar su consumo. <br> **Pasos:** <br> 1. El comensal solicita su cuenta al mesero. <br> 2. El mesero recopila de su libreta los productos consumidos por la mesa y los lleva al cajero. <br> 3. El cajero calcula manualmente el total de la cuenta (sumando precios de una lista impresa o de memoria). <br> 4. El cajero informa el total al comensal. <br> 5. El comensal realiza el pago (efectivo o tarjeta). <br> 6. El cajero registra el cobro en su cuaderno o libreta de ventas. <br> 7. El cajero entrega el cambio o el comprobante de pago al comensal. |
| PROC-04 | Venta de productos para llevar | Cajero | Mediante este proceso, el cajero atiende directamente a un cliente que solicita productos para llevar sin ocupar mesa. <br> **Pasos:** <br> 1. El cliente se acerca a la caja y solicita verbalmente los productos que desea. <br> 2. El cajero consulta la disponibilidad de productos (preguntando a barra/cocina si es necesario). <br> 3. El cajero comunica la orden a barra o cocina verbalmente o mediante comanda. <br> 4. El cajero calcula el total manualmente y cobra al cliente. <br> 5. El cajero registra la venta en su cuaderno de ventas del día. <br> 6. Una vez listos los productos, el cajero los entrega al cliente. |
| PROC-05 | Corte de caja | Gerente de sucursal | Mediante este proceso, el gerente de sucursal realiza el cierre y cuadre financiero del día o de la semana. <br> **Pasos:** <br> 1. El gerente recopila las libretas de ventas de los cajeros del turno/día. <br> 2. El gerente suma manualmente todos los registros de cobro (calculadora o a mano). <br> 3. El gerente cuenta el efectivo físico disponible en la caja. <br> 4. El gerente compara el total de efectivo físico contra el total de ventas registradas. <br> 5. Si hay diferencias, el gerente intenta identificar el origen del faltante o sobrante revisando las libretas. <br> 6. El gerente registra el resultado del corte en un cuaderno de cortes. <br> 7. El gerente reporta verbalmente o por mensaje al dueño el resultado del corte. |
| PROC-06 | Consulta de productos por el comensal | Comensal | Mediante este proceso, los comensales consultan la oferta de productos disponibles antes de ordenar. <br> **Pasos:** <br> 1. El comensal se sienta en la mesa y solicita el menú al mesero. <br> 2. El mesero le entrega un menú impreso (que puede estar desactualizado en precios o disponibilidad). <br> 3. El comensal revisa los productos, precios y descripciones. <br> 4. Si el comensal tiene dudas sobre un producto, pregunta verbalmente al mesero. <br> 5. El mesero consulta a barra o cocina si no conoce la respuesta. <br> 6. El comensal decide qué ordenar basándose en la información recibida. |
| PROC-07 | Análisis financiero | Dueño / Contador | Mediante este proceso, el dueño y su contador analizan el desempeño financiero de las sucursales para la toma de decisiones. <br> **Pasos:** <br> 1. El dueño recopila los reportes de corte de caja de las cinco sucursales (vía mensajes, fotos de cuadernos o llamadas telefónicas). <br> 2. El dueño o el contador vacía los datos a una hoja de cálculo o cuaderno consolidado. <br> 3. El contador calcula ingresos, egresos y utilidades por sucursal de forma manual. <br> 4. El dueño compara el desempeño entre sucursales. <br> 5. El dueño toma decisiones operativas o estratégicas con base en los datos recopilados (que pueden tener errores o estar incompletos). |
| PROC-08 | Promoción de productos | Gerente de sucursal | Mediante este proceso, el gerente de sucursal comunica ofertas, promociones o productos nuevos a los comensales. <br> **Pasos:** <br> 1. El dueño define una promoción o producto nuevo y lo comunica al gerente vía mensaje. <br> 2. El gerente elabora carteles o pizarras escritas a mano con la información de la promoción. <br> 3. El gerente coloca los materiales promocionales en el local. <br> 4. El gerente instruye verbalmente a los meseros para que mencionen la promoción a los comensales. <br> 5. Los meseros mencionan la promoción verbalmente a cada comensal durante la toma de orden. |
| PROC-09 | Control de inventario | Gerente de sucursal | Mediante este proceso, el gerente de sucursal lleva el registro y control de los insumos y productos disponibles en la sucursal. <br> **Pasos:** <br> 1. El gerente revisa visualmente las existencias de insumos en almacén y refrigeradores al inicio o cierre del día. <br> 2. El gerente anota en un cuaderno las cantidades aproximadas de cada insumo. <br> 3. Si detecta faltantes o productos próximos a caducar, lo registra en su libreta. <br> 4. El gerente estima el consumo del día con base en su experiencia (sin datos históricos sistematizados). <br> 5. Si hay producto caducado o en mal estado, el gerente lo desecha y lo anota como merma en su cuaderno. <br> 6. El gerente comunica al dueño vía mensaje o llamada los faltantes críticos para solicitar reabastecimiento. |
| PROC-10 | Gestión de proveedores y compras | Dueño / Gerente de sucursal | Mediante este proceso, el dueño o gerente gestiona la compra de insumos a proveedores para el abastecimiento de la sucursal. <br> **Pasos:** <br> 1. El gerente identifica los insumos faltantes con base en su revisión visual del inventario. <br> 2. El gerente comunica al dueño la lista de insumos necesarios (vía mensaje o llamada). <br> 3. El dueño o gerente contacta a los proveedores por teléfono o mensaje para solicitar cotización o hacer el pedido. <br> 4. El proveedor confirma la disponibilidad, precio y fecha de entrega. <br> 5. El dueño o gerente autoriza la compra de forma verbal. <br> 6. El proveedor entrega los insumos en la sucursal. <br> 7. El gerente recibe la mercancía, verifica cantidades de forma visual y firma la nota o factura. <br> 8. El gerente guarda la nota de compra en una carpeta física sin registro digital. |

## 3. Visión de la solución

### 3.1 Frase de visión
Desarrollar un sistema integral de gestión para La Toscana que centralice las operaciones de sus cinco sucursales, reduzca pérdidas operativas, automatice el control financiero y permita la toma de decisiones basada en datos confiables.

### 3.2 Procesos clave del negocio futuros

Los siguientes procesos describen la operación futura (TO-BE) de La Toscana **con el sistema implementado**. Cada proceso corresponde a su versión actual (AS-IS) de la sección 2.3, mostrando cómo el sistema los mejora o automatiza.

| ID Proceso | Nombre del proceso | Actor principal | Descripción y pasos |
| --- | --- | --- | --- |
| PROC-01F | Registro digital de orden de mesa | Mesero | Mediante este proceso, el mesero registra la orden del comensal directamente en el sistema desde una tablet o smartphone. <br> **Pasos:** <br> 1. El comensal indica al mesero lo que desea ordenar. <br> 2. El mesero abre la aplicación en su tablet, selecciona la mesa y busca los productos en el catálogo digital. <br> 3. El mesero agrega los productos a la orden, pudiendo ver precios, disponibilidad y descripción de cada producto. <br> 4. El mesero confirma la orden en el sistema. <br> 5. La orden se envía automáticamente a la pantalla de barra y/o cocina según el tipo de producto. <br> 6. El sistema registra la hora, el mesero responsable y los productos con trazabilidad completa. |
| PROC-02F | Preparación de productos con vista digital | Barista / Cocinero | Mediante este proceso, el personal de barra o cocina recibe y gestiona las órdenes pendientes a través de una pantalla digital (TV). <br> **Pasos:** <br> 1. La orden aparece automáticamente en la pantalla de la barra o cocina al ser confirmada por el mesero. <br> 2. El barista o cocinero visualiza los productos a preparar, organizados por prioridad (orden de llegada). <br> 3. El barista o cocinero puede consultar la receta estandarizada del producto directamente en el sistema. <br> 4. Al completar la preparación, el barista o cocinero marca el producto como "listo" en la pantalla. <br> 5. El sistema notifica al mesero que el pedido está listo para entrega. |
| PROC-03F | Cobro digital al comensal | Cajero | Mediante este proceso, el cajero genera y cobra la cuenta del comensal con los datos ya registrados en el sistema. <br> **Pasos:** <br> 1. El comensal solicita su cuenta al mesero. <br> 2. El mesero indica al cajero la mesa a cobrar (o el cajero la selecciona directamente en el sistema). <br> 3. El sistema muestra automáticamente el detalle de todos los productos consumidos con precios calculados. <br> 4. El cajero confirma el total con el comensal. <br> 5. El comensal realiza el pago (efectivo o tarjeta). <br> 6. El cajero registra el método de pago en el sistema y la venta queda cerrada automáticamente. <br> 7. El sistema genera un comprobante de pago digital o impreso. |
| PROC-04F | Venta de productos para llevar con registro digital | Cajero | Mediante este proceso, el cajero atiende ventas para llevar registrándolas directamente en el sistema. <br> **Pasos:** <br> 1. El cliente solicita productos para llevar. <br> 2. El cajero busca los productos en el catálogo digital del sistema y los agrega a una orden tipo "para llevar". <br> 3. El sistema calcula automáticamente el total. <br> 4. El cajero cobra al cliente y registra el método de pago. <br> 5. La orden se envía automáticamente a barra o cocina para preparación. <br> 6. Una vez listos, el personal marca como "listo" y el cajero entrega los productos. |
| PROC-05F | Corte de caja automatizado | Gerente de sucursal | Mediante este proceso, el gerente de sucursal realiza el cierre financiero del día con datos calculados automáticamente por el sistema. <br> **Pasos:** <br> 1. El gerente accede al módulo de corte de caja en el sistema desde la PC de la sucursal. <br> 2. El sistema presenta el resumen automático: total de ventas del día, desglose por método de pago (efectivo, tarjeta) y número de transacciones. <br> 3. El gerente ingresa el conteo de efectivo físico en caja. <br> 4. El sistema calcula automáticamente la diferencia entre el efectivo esperado y el contado, señalando faltantes o sobrantes. <br> 5. El gerente agrega observaciones si hay diferencias. <br> 6. El gerente cierra el corte de caja en el sistema, quedando el registro almacenado y disponible para consulta del dueño  . |
| PROC-06F | Consulta digital de productos por el comensal | Comensal | Mediante este proceso, los comensales consultan la oferta de productos actualizada a través de un menú digital. <br> **Pasos:** <br> 1. El comensal accede al menú digital (mediante un código QR en la mesa, una tablet del local o sitio web). <br> 2. El comensal visualiza los productos disponibles con fotos, descripciones, precios actualizados e indicadores de disponibilidad  . <br> 3. El comensal puede filtrar por categoría (bebidas calientes, frías, alimentos, postres, etc.). <br> 4. Si tiene dudas, consulta al mesero, quien también puede verificar detalles en su tablet. <br> 5. El comensal decide qué ordenar con información completa y actualizada. |
| PROC-07F | Análisis financiero con reportes consolidados | Dueño / Contador | Mediante este proceso, el dueño y su contador analizan el desempeño financiero de todas las sucursales a través de reportes generados automáticamente por el sistema. <br> **Pasos:** <br> 1. El dueño o contador accede al módulo de reportes del sistema desde cualquier dispositivo con acceso autorizado. <br> 2. El sistema presenta un dashboard con indicadores clave: ventas por sucursal, comparativas entre periodos, productos más vendidos y márgenes de utilidad. <br> 3. El dueño puede filtrar reportes por sucursal, rango de fechas, categoría de producto o tipo de gasto. <br> 4. El sistema permite exportar los reportes en formatos utilizables (PDF, Excel). <br> 5. El dueño toma decisiones estratégicas con base en datos confiables, completos y  . |
| PROC-08F | Promoción digital de productos | Gerente de sucursal / Dueño | Mediante este proceso, el dueño o gerente gestiona promociones y novedades desde el sistema, reflejándose automáticamente en todos los canales digitales. <br> **Pasos:** <br> 1. El dueño o gerente crea una promoción en el módulo de catálogo del sistema (producto, descuento, vigencia). <br> 2. El sistema aplica la promoción automáticamente al catálogo digital visible para los comensales. <br> 3. Los meseros ven las promociones activas al tomar la orden en su tablet, pudiendo sugerirlas al comensal. <br> 4. Al cobrar, el sistema aplica el descuento automáticamente si el producto está en promoción. <br> 5. El sistema registra el impacto de la promoción (ventas generadas) para análisis posterior. |
| PROC-09F | Control de inventario sistematizado | Gerente de sucursal | Mediante este proceso, el gerente de sucursal gestiona el inventario con apoyo del sistema, que actualiza existencias automáticamente conforme se registran ventas. <br> **Pasos:** <br> 1. El sistema descuenta automáticamente los insumos utilizados en cada venta, con base en las recetas registradas. <br> 2. El gerente consulta el módulo de inventario para ver existencias actuales por producto e insumo. <br> 3. El sistema genera alertas automáticas cuando un insumo alcanza un nivel mínimo de stock. <br> 4. El gerente puede registrar mermas o ajustes manuales con justificación en el sistema. <br> 5. El sistema genera reportes de consumo, mermas y rotación de inventario para análisis. |
| PROC-10F | Gestión de proveedores y compras con registro digital | Dueño / Gerente de sucursal | Mediante este proceso, el dueño o gerente gestiona las compras a proveedores con apoyo del sistema, manteniendo un registro histórico completo. <br> **Pasos:** <br> 1. El sistema alerta sobre insumos en nivel bajo de stock y sugiere cantidades a reabastecer con base en consumo histórico. <br> 2. El gerente o dueño consulta el catálogo de proveedores registrados en el sistema (nombre, contacto, productos que suministran, historial de precios). <br> 3. El gerente genera una orden de compra desde el sistema y la envía al proveedor. <br> 4. Al recibir la mercancía, el gerente registra la entrada en el sistema, verificando cantidades contra la orden de compra. <br> 5. El sistema actualiza automáticamente el inventario con los insumos recibidos. <br> 6. La factura o nota del proveedor se asocia digitalmente a la orden de compra para control contable. |

### 3.3 Funcionalidades de alto nivel del sistema (épicas)

A continuación se listan las funcionalidades de alto nivel que tendrá la solución. La prioridad se asigna según el impacto en la reducción de pérdidas y la mejora operativa del negocio.

| ID | Descripción de la funcionalidad | Prioridad | Proceso de negocio asociado |
| --- | --- | --- | --- |
| EP-01 | **Gestión de órdenes.** Permitir el registro, modificación, seguimiento y cierre de órdenes de comensales (en mesa y para llevar), con trazabilidad completa del mesero, la hora y los productos solicitados. | Alta | PROC-01F, PROC-04F |
| EP-02 | **Punto de venta y cobro.** Permitir al cajero consultar las órdenes activas de cada mesa, calcular totales automáticamente, registrar el método de pago (efectivo o tarjeta) y generar comprobantes de venta. | Alta | PROC-03F, PROC-04F |
| EP-03 | **Vista de preparación (cocina/barra).** Mostrar en pantallas de TV las órdenes pendientes para el personal de barra y cocina, organizadas por prioridad, permitiendo marcar productos como "listos" y notificar al mesero. | Media | PROC-02F |
| EP-04 | **Corte de caja.** Automatizar el cierre financiero diario: calcular ventas totales, desglosar por método de pago, comparar contra el efectivo físico contado por el gerente y señalar diferencias. | Alta | PROC-05F |
| EP-05 | **Gestión de inventario.** Controlar existencias de insumos en tiempo real, descontar automáticamente por cada venta según las recetas registradas, alertar niveles mínimos de stock y permitir el registro de mermas. | Alta | PROC-09F |
| EP-06 | **Gestión de proveedores y compras.** Mantener un catálogo de proveedores, generar órdenes de compra, registrar entradas de mercancía y vincularlas con facturas para control contable. | Media | PROC-10F |
| EP-07 | **Catálogo de productos.** Centralizar la administración de productos (altas, bajas, modificaciones de precios, descripciones y fotos) con consistencia entre todas las sucursales. | Media | PROC-06F, PROC-08F |
| EP-08 | **Gestión de recetas.** Permitir registrar, consultar y actualizar las recetas estandarizadas de cada producto, vinculando ingredientes con el inventario para el control de consumo. | Baja | PROC-02F, PROC-09F |
| EP-09 | **Reportes y análisis financiero.** Generar reportes consolidados y por sucursal de ventas, inventario, cortes de caja y tendencias, con dashboard visual. | Media | PROC-07F |
| EP-10 | **Menú digital para clientes.** Proveer un medio digital (web accesible por QR) donde los comensales consulten los productos disponibles con precios, descripciones, fotos y disponibilidad actualizada. | Media | PROC-06F |
| EP-11 | **Gestión de promociones.** Permitir crear, programar y aplicar promociones y descuentos desde el sistema, reflejándose automáticamente en el menú digital y en el punto de venta al momento del cobro. | Baja | PROC-08F |
| EP-12 | **Registro de clientes.** Permitir el registro de datos básicos de clientes como base para futuros programas de fidelización y promociones personalizadas. | Baja | — |

---

## 4. Alcance del proyecto

### 4.1 Alcance

**Objetivo de liberación:** Liberar el sistema antes del **1 de abril de 2026**.

Las épicas se asignan a sprints priorizando aquellas que generan mayor valor al negocio y que resuelven las problemáticas más críticas (pérdidas económicas y tiempo operativo).

| Sprint | Épicas incluidas | Justificación de prioridad |
| --- | --- | --- |
| Sprint 1 | **EP-01** (Gestión de órdenes), **EP-02** (Punto de venta y cobro) | Son el núcleo operativo del negocio. Sin órdenes y cobro digital, el resto del sistema no tiene sentido. Atacan directamente las pérdidas por órdenes no registradas ($4,800-$8,000/mes). |
| Sprint 2 | **EP-03** (Vista de preparación), **EP-04** (Corte de caja) | Complementan el flujo de ventas. La vista de cocina/barra elimina la dependencia de comandas en papel. El corte de caja automatizado libera las 32 horas/mes del gerente. |
| Sprint 3 | **EP-05** (Inventario), **EP-08** (Recetas) | Se implementan juntas porque las recetas alimentan el descuento automático de inventario. Atacan el desperdicio (10-15% del costo de insumos). |
| Sprint 4 | **EP-07** (Catálogo de productos), **EP-06** (Proveedores y compras) | El catálogo centralizado es prerequisito del menú digital. La gestión de proveedores cierra el ciclo de aprovisionamiento. |
| Sprint 5 | **EP-09** (Reportes), **EP-10** (Menú digital) | Los reportes consolidan toda la data generada en sprints anteriores. El menú digital da valor visible al cliente final. |
| Sprint 6 | **EP-11** (Promociones), **EP-12** (Registro de clientes) | Funcionalidades de valor agregado que dependen de tener catálogo y menú digital operando. El registro de clientes es base para programas futuros. |

> **Nota:** Cada sprint tiene una duración estimada de **2 semanas**. El total de 6 sprints (12 semanas) se ajusta al plazo de liberación antes del 1 de abril de 2026.

### 4.2 Fuera de alcance

Los siguientes elementos **no** forman parte del alcance de esta versión del sistema:

- Sistema de pedidos en línea o delivery.
- Integración con plataformas de pago externas más allá de registro manual de pago con tarjeta.
- Módulo de nómina o gestión de recursos humanos.
- Aplicación móvil nativa para clientes (el menú será web responsive).
- Facturación electrónica ante el SAT.
- Programas de lealtad activos (solo se implementa el registro de clientes como base futura).

---

## 5. Contexto del sistema

### 5.1 Resumen de Involucrados

| Stakeholder | Tipo | Rol en el proyecto | Interacción con el sistema |
| --- | --- | --- | --- |
| **Dueño de la franquicia** | Interno | Patrocinador del proyecto, aprueba requerimientos y prioridades. | Consulta reportes consolidados, administra catálogo global, gestiona promociones y proveedores. |
| **Gerente de sucursal** | Interno | Usuario clave, valida que el sistema cubra las operaciones diarias. | Realiza cortes de caja, gestiona inventario local, supervisa operación de la sucursal. |
| **Cajero** | Interno | Usuario operativo. | Cobra cuentas, registra ventas para llevar, opera el punto de venta. |
| **Mesero** | Interno | Usuario operativo. | Registra órdenes en tablet, consulta menú y estado de pedidos. |
| **Barista** | Interno | Usuario operativo. | Visualiza órdenes pendientes en pantalla, consulta recetas, marca productos como listos. |
| **Personal de cocina** | Interno | Usuario operativo. | Visualiza órdenes pendientes en pantalla, consulta recetas, marca productos como listos. |
| **Contador** | Externo | Consultor financiero del dueño. | Consulta reportes financieros y exporta datos para contabilidad. |
| **Comensal / Cliente** | Externo | Beneficiario indirecto. | Consulta el menú digital; no interactúa con módulos internos del sistema. |
| **Proveedor** | Externo | Suministra insumos a las sucursales. | No interactúa directamente con el sistema; sus datos son gestionados por el dueño/gerente. |
| **Equipo de desarrollo** | Externo | Construye y mantiene el sistema. | Diseña, implementa, prueba y despliega el sistema. |

### 5.2 Entorno de operación

El sistema operará en el siguiente entorno tecnológico:

**Dispositivos e infraestructura por sucursal:**

| Dispositivo | Función en el sistema | Cantidad total (5 sucursales) |
| --- | --- | --- |
| PC de escritorio | Punto de venta principal, corte de caja, reportes, administración | 5 (1 por sucursal) |
| Tablets | Toma de órdenes por meseros, consulta de menú | 10-14 total |
| Pantallas TV | Vista de órdenes pendientes para cocina/barra | 5 (1 por sucursal) |
| Smartphones | Respaldo para meseros, consultas rápidas | Dispositivos personales de empleados |

**Conectividad por sucursal:**

| Sucursal | Calidad de Internet | Estrategia del sistema |
| --- | --- | --- |
| Iztapalapa | Buena | Operación en la nube, tiempo real |
| Chalco | Buena | Operación en la nube, tiempo real |
| Amecameca | Intermitente | **Modo offline con sincronización** periódica (cada 5-10 min) |
| Yecapixtla | Intermitente | **Modo offline con sincronización** periódica (cada 5-10 min) |
| Cuautla | Intermitente | **Modo offline con sincronización** periódica (cada 5-10 min) |

**Usuarios concurrentes estimados:**

| Tipo de sucursal | Usuarios concurrentes máx. | Sucursales |
| --- | --- | --- |
| Grande | 10-12 | Iztapalapa, Chalco |
| Mediana/Pequeña | 4-5 | Amecameca, Yecapixtla, Cuautla |
| **Total franquicia** | **~35-40** | — |

### 5.3 Información adicional

**Restricciones técnicas:**

- El sistema **debe** funcionar sin conexión a internet y sincronizar datos automáticamente cuando se restablezca la conectividad (requisito crítico para 3 de las 5 sucursales).
- El sistema debe soportar hasta **40 usuarios concurrentes** distribuidos en las 5 sucursales.
- La interfaz debe ser **responsive** y funcional en PC, tablets y smartphones.

**Restricciones de negocio:**

- Horario de operación: lunes a sábado, 8:00 AM a 10:00 PM. Los domingos no se opera (antes se usaban para corte de caja manual; con el sistema, quedan libres).
- El sistema debe respetar los roles y permisos diferenciados por tipo de usuario (dueño, gerente, cajero, mesero, barista, cocinero).
- La información financiera solo debe ser accesible para el dueño, gerentes y contador.

**Restricciones de calendario:**

- Fecha límite de liberación: **antes del 1 de abril de 2026**.