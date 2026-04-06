## Business case
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

## System requirements

### Primary funcitionality

| ID | Historia de Usuario | Prioridad |
|---|---|---|
| HU-01 | Como **mesero**, quiero registrar las órdenes de los comensales desde una tablet seleccionando productos del catálogo digital, para que las órdenes queden registradas con trazabilidad completa y se eliminen errores u omisiones. | 🔴 Alta |
| HU-02 | Como **mesero**, quiero que la orden se envíe automáticamente a la pantalla de barra o cocina al confirmarla, para que no tenga que llevar comandas en papel y se agilice la comunicación. | 🔴 Alta |
| HU-03 | Como **mesero**, quiero recibir una notificación cuando un pedido esté listo en barra o cocina, para que pueda entregarlo al comensal sin demoras innecesarias. | 🟡 Media |
| HU-04 | Como **cajero**, quiero consultar las órdenes activas de cada mesa con los totales calculados automáticamente, para que el cobro sea rápido, preciso y sin errores de cálculo manual. | 🔴 Alta |
| HU-05 | Como **cajero**, quiero registrar el método de pago (efectivo o tarjeta) y generar un comprobante de venta, para que cada transacción quede documentada correctamente. | 🔴 Alta |
| HU-06 | Como **cajero**, quiero registrar ventas directamente en el sistema, para que esas ventas no se pierdan ni queden fuera del registro financiero. | 🔴 Alta |
| HU-07 | Como **barista/cocinero**, quiero visualizar en una pantalla las órdenes pendientes organizadas por prioridad, para que pueda preparar los productos en el orden correcto sin depender de comandas en papel. | 🟡 Media |
| HU-08 | Como **barista/cocinero**, quiero consultar la receta estandarizada de cada producto en el sistema, para que la preparación sea uniforme y consistente entre todos los turnos y sucursales. | 🟠 Baja |
| HU-09 | Como **barista/cocinero**, quiero marcar productos como "listos" en la pantalla, para que el mesero sea notificado automáticamente y el flujo de entrega no dependa de comunicación verbal. | 🟡 Media |
| HU-10 | Como **gerente de sucursal**, quiero realizar el corte de caja con ventas totales calculadas automáticamente por el sistema, para que el cierre financiero diario no requiera suma manual y se eliminen las 8 horas semanales dedicadas a esta tarea. | 🔴 Alta |
| HU-11 | Como **gerente de sucursal**, quiero comparar el efectivo físico contado contra el total esperado por el sistema, para que se identifiquen inmediatamente faltantes o sobrantes con su origen. | 🔴 Alta |
| HU-12 | Como **gerente de sucursal**, quiero consultar las existencias de insumos en tiempo real, para que pueda tomar decisiones de reabastecimiento oportunas y reducir desperdicios. | 🔴 Alta |
| HU-13 | Como **gerente de sucursal**, quiero recibir alertas automáticas cuando un insumo alcance su nivel mínimo de stock, para que pueda solicitar reabastecimiento antes de que se agoten los productos. | 🔴 Alta |
| HU-14 | Como **gerente de sucursal**, quiero registrar mermas y ajustes de inventario con justificación, para que haya un control documentado de las pérdidas y se puedan analizar sus causas. | 🔴 Alta |
| HU-15 | Como **dueño**, quiero consultar un dashboard con indicadores clave de ventas, inventario y finanzas de todas las sucursales, para que pueda tomar decisiones estratégicas basadas en datos confiables y no en reportes verbales. | 🟡 Media |
| HU-16 | Como **dueño**, quiero filtrar reportes por sucursal, rango de fechas y categoría de producto, para que pueda comparar el desempeño entre sucursales y periodos específicos. | 🟡 Media |
| HU-17 | Como **dueño/contador**, quiero exportar reportes financieros en formato PDF y Excel, para que el contador pueda integrarlos a la contabilidad formal sin transcripción manual. | 🟡 Media |
| HU-18 | Como **dueño**, quiero administrar el catálogo de productos (altas, bajas, precios, descripciones, fotos) de forma centralizada, para que haya consistencia en la oferta y precios entre las cinco sucursales. | 🟡 Media |
| HU-19 | Como **dueño/gerente**, quiero mantener un catálogo de proveedores con datos de contacto, productos que suministran e historial de precios, para que las compras estén organizadas y sean rastreables. | 🟡 Media |
| HU-20 | Como **gerente**, quiero generar órdenes de compra desde el sistema y registrar la entrada de mercancía verificando cantidades, para que el inventario se actualice automáticamente y las compras queden vinculadas a facturas. | 🟡 Media |
| HU-21 | Como **dueño/gerente**, quiero registrar, consultar y actualizar recetas estandarizadas vinculando ingredientes con el inventario, para que el sistema descuente insumos automáticamente por cada venta y se controle el consumo real. | 🟠 Baja |
| HU-22 | Como **comensal**, quiero consultar el menú digital actualizado escaneando un código QR desde mi celular, para que pueda ver productos disponibles con fotos, precios y descripciones sin depender de un menú impreso desactualizado. | 🟡 Media |
| HU-23 | Como **comensal**, quiero filtrar los productos del menú digital por categoría (bebidas, alimentos, postres, etc.), para que pueda encontrar rápidamente lo que me interesa. | 🟡 Media |
| HU-24 | Como **dueño/gerente**, quiero crear y programar promociones con vigencia desde el sistema, para que se apliquen automáticamente en el punto de venta y se reflejen en el menú digital sin intervención manual. | 🟠 Baja |
| HU-25 | Como **dueño**, quiero consultar el impacto de cada promoción (ventas generadas durante su vigencia), para que pueda evaluar la efectividad de las estrategias comerciales. | 🟠 Baja |
| HU-26 | Como **cajero**, quiero registrar datos básicos de clientes (nombre, contacto), para que la empresa cuente con una base de datos que soporte futuros programas de fidelización. | 🟠 Baja |
| HU-27 | Como **gerente/mesero**, quiero que el sistema funcione en modo offline y sincronice datos automáticamente al restablecerse la conexión, para que las sucursales con internet intermitente no interrumpan su operación. | 🔴 Alta |
| HU-28 | Como **dueño**, quiero que el sistema aplique roles y permisos diferenciados (dueño, gerente, cajero, mesero, barista, cocinero), para que cada usuario acceda solo a las funcionalidades que le corresponden y la información sensible esté protegida. | 🔴 Alta |

### Quality attribute scenarios
| ID | Atributo de calidad | Escenario |
|---|---|---|
| QA-PERF-01 | Performance | Un mesero confirma una orden de 5 productos desde su tablet durante hora pico y el sistema la registra y la muestra en cocina/barra en ≤ 2 segundos. |
| QA-PERF-02 | Performance | El gerente solicita el corte de caja al cierre del día y el sistema calcula y presenta el resumen financiero en ≤ 5 segundos. |
| QA-PERF-03 | Performance | Un mesero busca un producto por nombre parcial en el catálogo durante la toma de orden y el sistema muestra resultados en ≤ 1 segundo por carácter ingresado. |
| QA-SEC-01 | Security | Un mesero intenta acceder al módulo de reportes financieros y el sistema bloquea el acceso, muestra permisos insuficientes y registra el intento en ≤ 1 segundo. |
| QA-SEC-02 | Security | Un cajero intenta modificar una orden ya cobrada y cerrada, y el sistema lo impide, exige autorización de gerente y deja trazabilidad completa. |
| QA-SEC-03 | Security | Un cajero deja el punto de venta sin cerrar sesión y el sistema cierra automáticamente la sesión tras ≤ 10 minutos de inactividad y exige reautenticación. |
| QA-USA-01 | Usability | Un mesero nuevo, sin capacitación previa, registra correctamente su primera orden en la tablet en ≤ 3 minutos sin ayuda externa. |
| QA-USA-02 | Usability | Un comensal escanea el QR del menú y puede localizar un producto y consultar su precio en ≤ 30 segundos, con satisfacción de usabilidad ≥ 4/5. |
| QA-USA-03 | Usability | Un cajero selecciona un método de pago incorrecto y puede corregirlo antes de cerrar la transacción en ≤ 2 pasos, sin perder datos de la orden. |
| QA-AVA-01 | Availability | Usuarios de las 5 sucursales acceden simultáneamente al sistema durante el horario operativo y este mantiene disponibilidad ≥ 99.5% mensual. |
| QA-AVA-02 | Availability | El servidor en la nube falla durante hora pico y las sucursales continúan offline; el servicio central se restablece en ≤ 15 minutos sin pérdida de datos. |
| QA-AVA-03 | Availability | El equipo despliega una actualización planificada y el sistema aplica el cambio sin interrupción percibida en horario operativo, con 0 minutos de indisponibilidad. |
| QA-REL-01 | Reliability | Una sucursal pierde internet durante 2 horas, registra 40 órdenes offline y luego sincroniza el 100% de las transacciones sin pérdidas ni duplicados. |
| QA-REL-02 | Reliability | Dos cajeros procesan transacciones concurrentes con promociones e inventario limitado y el sistema mantiene integridad referencial y consistencia de inventario. |
| QA-REL-03 | Reliability | Tres sucursales se reconectan en momentos distintos tras operar offline y el sistema consolida el 100% de las transacciones sin inconsistencias globales. |
| QA-MOD-01 | Modifiability | El dueño solicita un nuevo módulo de fidelización y el equipo lo implementa, prueba y despliega en ≤ 2 sprints sin regresiones en módulos existentes. |
| QA-MOD-02 | Modifiability | La franquicia abre una sexta sucursal y el sistema permite configurarla y dejarla operativa en ≤ 1 día hábil sin afectar a las sucursales actuales. |
| QA-MOD-03 | Modifiability | El dueño solicita nuevas reglas de promociones condicionadas y el equipo las implementa en ≤ 1 sprint sin modificar módulos no afectados ni introducir regresiones. |


### Constraints
| ID | Restricción | Tipo |
|----|-------------|------|
| RES-01 | El sistema **debe operar en modo offline** y sincronizar datos automáticamente cuando se resta   blezca la conexión a internet, dado que 3 de las 5 sucursales (Amecameca, Yecapixtla, Cuautla) presentan conectividad intermitente. | 🔧 Técnica |
| RES-02 | El sistema debe soportar hasta **40 usuarios concurrentes** distribuidos en las 5 sucursales, con picos de 10-12 usuarios simultáneos por sucursal grande. | 🔧 Técnica |
| RES-03 | La interfaz debe ser **responsive** y completamente funcional en tres tipos de dispositivos: PC de escritorio, tablets y smartphones. | 🔧 Técnica |
| RES-04 | El sistema debe ser compatible con **pantallas de TV** para la vista de preparación en cocina/barra, funcionando como un display de solo lectura con interacción mínima (marcar como "listo"). | 🔧 Técnica |
| RES-05 | El menú digital para clientes debe ser una **aplicación web accesible por código QR** (no una app nativa), sin requerir instalación por parte del comensal. | 🔧 Técnica |
| RES-06 | El sistema debe implementar un **modelo de roles y permisos diferenciados** para al menos 6 roles distintos (dueño, gerente, cajero, mesero, barista, cocinero), restringiendo el acceso a funcionalidades e información según el perfil. | 🔧 Técnica |
| RES-07 | La sincronización offline debe resolverse con una **estrategia de conflictos de datos** confiable, ya que múltiples dispositivos por sucursal pueden generar datos simultáneamente sin conexión (ej. varias tablets de meseros tomando órdenes). | 🔧 Técnica |
| RES-08 | El sistema debe procesar un volumen de entre **700 y 1,100 órdenes diarias** a nivel franquicia (~18,200-28,600 mensuales), garantizando rendimiento adecuado en operaciones de lectura/escritura. | 🔧 Técnica |
| RES-09 | El sistema debe operar correctamente sobre la **infraestructura existente** (5 PCs, 10-14 tablets, 5 TVs, smartphones personales), sin requerir inversión adicional en hardware especializado. | 🔧 Técnica |

### Architectural concerns
| ID | Concern |
| --- | --- |
| C001.1.1 | Políticas de retención de datos. Definir cuánto tiempo se conservan órdenes históricas, cortes de caja, registros de inventario y logs de auditoría. |
| C001.1.2 | Estrategia de archivado. Definir cómo se archivan datos históricos de ventas, inventario y cortes de caja sin afectar el rendimiento operativo diario. |
| C001.1.3 | Limpieza de datos transitorios. Definir procedimientos para limpiar órdenes abandonadas, sesiones expiradas y datos temporales generados durante operación offline. |
| C001.2.1 | Estrategia de sincronización offline-online. Garantizar la consistencia de datos cuando sucursales operan con conectividad intermitente y múltiples dispositivos generan datos simultáneamente sin conexión. |
| C001.2.2 | Persistencia local de datos. Definir dónde y cómo se almacenarán los datos localmente en cada dispositivo mientras opera en modo offline. |
| C001.2.3 | Validación de datos post-sincronización. Definir mecanismos para validar la integridad de los datos después de cada sincronización. |
| C001.3.1 | Frecuencia y retención de respaldos. Definir la frecuencia de respaldos y periodos de retención considerando el volumen de transacciones de la franquicia. |
| C001.3.2 | Objetivos RPO y RTO. Definir máximo de pérdida de datos tolerable y tiempo máximo de recuperación. |
| C001.3.3 | Respaldo en entorno offline. Definir cómo se respaldan los datos locales antes de sincronizar con el servidor central. |
| C001.4.1 | Migración de datos iniciales. Definir estrategia para migrar catálogos, proveedores, recetas e inventario desde registros manuales y hojas de cálculo. |
| C001.4.2 | Compatibilidad hacia atrás en esquema. Definir cómo manejar cambios de esquema sin perder datos ni interrumpir la operación. |
| C002.1.1 | Integración entre módulos interdependientes. Definir una arquitectura interna con módulos cohesivos y bajo acoplamiento. |
| C002.1.2 | Atomicidad de operaciones cross-module. Garantizar consistencia entre venta y descuento de inventario, especialmente en modo offline. |
| C002.1.3 | Dependencias entre historias de usuario. Gestionar dependencias técnicas entre historias basadas en datos o capacidades previas. |
| C002.2.1 | Mecanismo de comunicación en tiempo real. Definir cómo reflejar órdenes y notificaciones de manera inmediata en cocina, barra y meseros. |
| C002.2.2 | Cola de mensajes en modo offline. Definir estrategia de encolamiento y entrega garantizada de mensajes sin conexión. |
| C002.3.1 | Integración con sistemas de pago. Definir cómo registrar pagos con tarjeta y el fallback en modo offline. |
| C002.3.2 | Integración con impresoras de comprobantes. Definir compatibilidad con impresoras térmicas de tickets. |
| C003.1.1 | Implementación de RBAC. Diseñar autenticación y autorización robustas para roles diferenciados sin fricción operativa. |
| C003.1.2 | Granularidad de permisos. Definir matriz de permisos por rol. |
| C003.1.3 | Gestión de sesiones. Definir expiración, cierre automático y concurrencia en dispositivos compartidos. |
| C003.1.4 | Autenticación en modo offline. Definir cómo validar identidad sin conexión al servidor central. |
| C003.2.1 | Protección de datos financieros. Definir cifrado en tránsito y en reposo para ventas, cortes de caja y reportes. |
| C003.2.2 | Almacenamiento seguro local. Proteger los datos almacenados localmente en caso de pérdida o robo del dispositivo. |
| C003.3.1 | Trazabilidad completa de operaciones. Registrar quién realizó qué acción y cuándo en órdenes, cobros, inventario y cortes de caja. |
| C003.3.2 | Detección de anomalías financieras. Implementar detección automática de faltantes y su posible origen. |
| C004.1.1 | Estrategia de despliegue multi-sucursal. Definir cómo desplegar actualizaciones sin interrumpir la operación diaria. |
| C004.1.2 | Versionamiento y rollback. Definir cómo revertir actualizaciones problemáticas en sucursales con conectividad variable. |
| C004.1.3 | Consistencia de versiones entre sucursales. Garantizar que todas operen con la misma versión del sistema. |
| C004.2.1 | Monitoreo remoto de sucursales. Definir cómo monitorear estado, caídas, errores y problemas de sincronización. |
| C004.2.2 | Estándares de logging. Definir niveles, formato, rotación y retención de logs. |
| C004.2.3 | Métricas de operación. Definir qué métricas recolectar y cómo analizarlas. |
| C004.3.1 | Continuidad operativa ante caída del servidor central. Garantizar que las sucursales sigan operando en funciones críticas. |
| C004.3.2 | Estrategia de recuperación ante desastres. Definir plan de recuperación ante pérdida de datos, fallos de hardware y desastres naturales. |
| C004.3.3 | Redundancia de datos críticos. Mantener copias redundantes de datos financieros y de inventario. |
| C005.1.1 | Definición de límites de módulos. Delimitar responsabilidades de cada módulo para permitir desarrollo paralelo. |
| C005.1.2 | Gestión de dependencias compartidas. Manejar código compartido sin crear acoplamiento excesivo. |
| C005.1.3 | Estrategia de reutilización de código. Reutilizar componentes entre apps e interfaces del sistema. |
| C005.2.1 | Pipeline de integración continua. Diseñar CI/CD para despliegues incrementales en múltiples puntos. |
| C005.2.2 | Gestión de ambientes. Definir estrategia de desarrollo, staging y producción considerando sucursales con conectividad distinta. |
| C005.3.1 | Gestión de deuda técnica. Rastrear y priorizar deuda técnica durante el desarrollo incremental. |
| C005.3.2 | Documentación técnica. Definir requisitos de documentación para APIs, esquemas y sincronización. |
| C006.1.1 | Heterogeneidad de dispositivos. Diseñar frontend adaptable a PCs, tablets, smartphones y TVs sin duplicar código. |
| C006.1.2 | Rendimiento en dispositivos limitados. Garantizar una aplicación ligera y rápida en tablets y smartphones. |
| C006.1.3 | Experiencia offline. Comunicar al usuario el estado de conexión, errores y sincronización pendiente. |
| C006.2.1 | Usabilidad bajo presión operativa. Diseñar interfaces que minimicen pasos para tareas frecuentes. |
| C006.2.2 | Capacitación y curva de aprendizaje. Lograr que el sistema sea intuitivo y requiera mínima capacitación. |
| C006.3.1 | Experiencia del menú QR. Garantizar una experiencia rápida, atractiva y funcional sin descarga de app. |
| C007.1.1 | Estructura de datos multi-sucursal. Soportar múltiples sucursales, usuarios concurrentes y volumen diario de órdenes sin degradación. |
| C007.1.2 | Aislamiento vs. datos compartidos. Definir qué datos se comparten y cuáles se aíslan por sucursal. |
| C007.1.3 | Crecimiento futuro. Permitir agregar nuevas sucursales sin rediseño significativo. |
| C007.2.1 | Tiempos de respuesta objetivo. Definir tiempos aceptables para operaciones críticas. |
| C007.2.2 | Pruebas de carga. Diseñar estrategia de pruebas para picos operativos simultáneos. |
| C008.1.1 | Identificación de procesos críticos. Determinar qué procesos no pueden detenerse y cuáles toleran interrupciones. |
| C008.1.2 | SLAs internos. Definir niveles de servicio internos para disponibilidad del sistema. |
| C008.2.1 | Costos de infraestructura. Definir presupuesto sostenible para hosting, licencias y mantenimiento. |
| C008.2.2 | Análisis costo-beneficio. Evaluar si el costo del sistema justifica la reducción de pérdidas proyectada. |
| C009.1.1 | Cumplimiento fiscal mexicano (SAT). Definir si el sistema debe generar CFDI o solo comprobantes internos. |
| C009.1.2 | Regulaciones de protección de datos. Cumplir con la LFPDPPP para datos de clientes y empleados. |
| C009.1.3 | Regulaciones de transacciones financieras. Identificar requisitos regulatorios aplicables al registro de transacciones. |
| C009.2.1 | Términos de uso del menú digital. Definir aviso de privacidad y términos de uso para el menú QR. |
| C010.1.1 | Pruebas en entorno offline. Diseñar pruebas reproducibles para sincronización y operación sin conectividad. |
| C010.1.2 | Gestión de datos de prueba. Generar datos de prueba realistas según el volumen operativo. |
| C010.1.3 | Pruebas multi-dispositivo. Validar funcionamiento correcto en PCs, tablets, smartphones y TVs. |
| C010.1.4 | Pruebas de rendimiento. Validar tiempos de respuesta y comportamiento bajo carga. |
| C010.2.1 | Quality gates por sprint. Definir criterios técnicos mínimos antes de desplegar a producción. |
| C010.2.2 | Validación de integridad financiera. Verificar consistencia de cálculos financieros entre módulos. |

## Priorities
### User Stories
La priorización se basa en: (1) impacto directo en reducción de pérdidas económicas ($33,000-$58,000 MXN/mes), (2) alineación con necesidades del negocio (NEC-01 a NEC-09), (3) posición en el plan de sprints y (4) dependencias técnicas entre módulos.

| ID_HU | Prioridad | Justificación |
|---|---|---|
| HU-01 | 🔴 Alta | Núcleo operativo del negocio (EP-01). Elimina órdenes no registradas o modificadas sin control, que generan pérdidas de $4,800-$8,000/mes (NEC-04). |
| HU-02 | 🔴 Alta | Complemento esencial de HU-01 (EP-01/EP-03). Elimina dependencia de comandas en papel y errores de comunicación verbal con cocina/barra (PROC-01F). |
| HU-03 | 🟡 Media | Mejora la eficiencia del flujo de entrega (EP-03), pero no bloquea la operación: el mesero puede verificar visualmente la pantalla o recibir aviso verbal como alternativa. |
| HU-04 | 🔴 Alta | Pilar del punto de venta (EP-02). Elimina el cálculo manual de cuentas que genera errores en los cobros y pérdidas directas (NEC-03, NEC-04). |
| HU-05 | 🔴 Alta | Trazabilidad financiera obligatoria (EP-02). Cada transacción debe quedar documentada para alimentar el corte de caja automatizado (NEC-03). |
| HU-06 | 🔴 Alta | Las ventas para llevar representan un canal de ingreso que actualmente se registra de forma inconsistente (PROC-04). Integrarlas al sistema evita pérdida de registro financiero (EP-02). |
| HU-07 | 🟡 Media | Vista de preparación (EP-03). Mejora significativamente la operación de cocina/barra, pero es funcional después de que el registro de órdenes esté operando. |
| HU-08 | 🟠 Baja | Gestión de recetas (EP-08). Importante para estandarización, pero el personal de barra/cocina actualmente prepara por conocimiento propio y puede seguir haciéndolo temporalmente. |
| HU-09 | 🟡 Media | Complementa HU-07 y HU-03 (EP-03). Cierra el ciclo de comunicación cocina→mesero, pero requiere que la vista de preparación ya esté implementada. |
| HU-10 | 🔴 Alta | Ataca directamente las 32 horas/mes (8 h × 4 semanas) dedicadas al corte de caja manual en cada sucursal (EP-04). Impacto operativo inmediato. |
| HU-11 | 🔴 Alta | Complemento inseparable de HU-10 (EP-04). Sin la comparación automática efectivo vs. sistema, el corte de caja pierde su valor de control financiero (NEC-03). |
| HU-12 | 🔴 Alta | Control de inventario en tiempo real (EP-05). El desperdicio actual representa 10-15% del costo de insumos, una de las pérdidas más significativas de la franquicia (NEC-01). |
| HU-13 | 🔴 Alta | Las alertas de stock mínimo previenen desabasto y pérdida de ventas (EP-05). Directamente ligada a NEC-01 y a la reducción de desperdicios. |
| HU-14 | 🔴 Alta | El registro documentado de mermas es clave para identificar causas de pérdida de inventario (EP-05). Sin esta trazabilidad, no se pueden tomar medidas correctivas (NEC-01). |
| HU-15 | 🟡 Media | Dashboard de reportes (EP-09). Esencial para la toma de decisiones del dueño (NEC-07), pero depende de que los módulos de órdenes, cobro, inventario y corte ya generen datos. |
| HU-16 | 🟡 Media | Filtros de reportes (EP-09). Complementa HU-15 para análisis comparativo entre sucursales. Valor alto para el dueño pero funciona solo con datos acumulados (NEC-07). |
| HU-17 | 🟡 Media | Exportación de reportes (EP-09). Necesidad del contador para integración contable formal (NEC-07). Depende de que los reportes ya estén generados. |
| HU-18 | 🟡 Media | Catálogo centralizado (EP-07). Prerequisito del menú digital y necesario para consistencia de precios entre sucursales (NEC-05), pero puede operar con datos precargados inicialmente. |
| HU-19 | 🟡 Media | Catálogo de proveedores (EP-06). Organiza la cadena de abastecimiento (NEC-02), pero actualmente el dueño/gerente gestiona proveedores de forma funcional aunque manual. |
| HU-20 | 🟡 Media | Órdenes de compra y entrada de mercancía (EP-06). Cierra el ciclo de aprovisionamiento y actualiza inventario (NEC-02). Depende de que el inventario ya esté operando. |
| HU-21 | 🟠 Baja | Recetas estandarizadas (EP-08). Vincula ingredientes con inventario para descuento automático (NEC-06). Importante pero el descuento puede operarse de forma simplificada inicialmente. |
| HU-22 | 🟡 Media | Menú digital QR (EP-10). Valor visible para el cliente final y cumple NEC-08, pero no impacta directamente en la reducción de pérdidas económicas de la franquicia. |
| HU-23 | 🟡 Media | Filtros del menú digital (EP-10). Mejora la experiencia del comensal en el menú QR. Complemento de HU-22, no es crítico para la operación interna. |
| HU-24 | 🟠 Baja | Gestión de promociones (EP-11). Funcionalidad de valor agregado que depende del catálogo y menú digital ya operativos. No resuelve pérdidas actuales. |
| HU-25 | 🟠 Baja | Análisis de impacto de promociones (EP-11). Solo tiene sentido después de que existan promociones activas. Es una funcionalidad de optimización comercial futura. |
| HU-26 | 🟠 Baja | Registro de clientes (EP-12). Base para programas futuros de fidelización. No tiene impacto operativo inmediato ni reduce pérdidas actuales (NEC-09). |
| HU-27 | 🔴 Alta | Requisito crítico de infraestructura. 3 de 5 sucursales (60%) tienen conectividad intermitente. Sin modo offline, el sistema es inutilizable en Amecameca, Yecapixtla y Cuautla (RES-01). |
| HU-28 | 🔴 Alta | Requisito transversal de seguridad. La información financiera debe estar restringida a dueño, gerentes y contador (NEC-03, RES-06). Fundamento para toda la arquitectura de permisos. |

### Quality Attributes
| ID Escenario | Atributo | Descripción corta | Importancia de negocio | Dificultad técnica | Prioridad |
|---|---|---|---|---|---|
| QA-PERF-01 | Performance | Latencia orden → cocina/barra ≤ 2s | Alta | Media | **Media** |
| QA-PERF-02 | Performance | Generación de corte de caja ≤ 5s | Media | Alta | **Media** |
| QA-PERF-03 | Performance | Búsqueda en catálogo ≤ 1s | Media | Baja | **Baja** |
| QA-SEC-01 | Security | Bloqueo acceso financiero por rol | Alta | Baja | **Media** |
| QA-SEC-02 | Security | Protección de órdenes cerradas | Alta | Media | **Media** |
| QA-SEC-03 | Security | Caducidad de sesión por inactividad | Media | Media | **Media** |
| QA-USA-01 | Usability | Mesero nuevo registra orden ≤ 3 min | Alta | Media | **Media** |
| QA-USA-02 | Usability | Comensal consulta menú QR ≤ 30s | Media | Baja | **Baja** |
| QA-USA-03 | Usability | Recuperación de error en cobro | Alta | Baja | **Media** |
| QA-AVA-01 | Availability | Uptime ≥ 99.5% en horario operativo | Alta | Media | **Media** |
| QA-AVA-02 | Availability | Recuperación ante fallo servidor ≤ 15 min | Alta | Alta | **Alta** |
| QA-AVA-03 | Availability | Despliegue sin interrupción (rolling update) | Baja | Alta | **Baja** |
| QA-REL-01 | Reliability | Sincronización offline 0 pérdidas | Alta | Alta | **Alta** |
| QA-REL-02 | Reliability | Integridad en transacciones concurrentes | Alta | Media | **Media** |
| QA-REL-03 | Reliability | Consistencia multi-sucursal post-sync | Alta | Alta | **Alta** |
| QA-MOD-01 | Modifiability | Nuevo módulo ≤ 2 sprints, 0 regresiones | Media | Media | **Media** |
| QA-MOD-02 | Modifiability | Nueva sucursal operativa ≤ 1 día | Media | Baja | **Baja** |
| QA-MOD-03 | Modifiability | Cambio reglas de promociones ≤ 1 sprint | Baja | Media | **Baja** |