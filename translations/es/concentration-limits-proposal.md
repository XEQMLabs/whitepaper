# Límites de concentración de nodos - Aplicación de la supervivencia de la red
## Complemento técnico del Whitepaper de Tokenómica de EXIOM
### 07/26/2026

> **Nota de alcance (actualizada en octubre de 2026).** La unidad que se aplica es el *clúster de proximidad* (un grupo de nodos que comparten infraestructura física o de enrutamiento, detectado mediante la proximidad de enrutamiento de Lokinet, la temporización de pruebas de tiempo de actividad y el ASN), **no el país**. Un país con varias instalaciones independientes no se ve afectado. Las cifras por país que figuran a continuación son un indicador geográfico aproximado de dónde se sitúa actualmente la concentración, no lo que el protocolo limita. Los recuentos de nodos en este complemento son una instantánea de julio de 2026 (~672 nodos); consulte el whitepaper para los totales actuales de la red (943 nodos al 27 de septiembre de 2026). Lokinet se publica en una versión sin aplicación obligatoria antes de HF23, y HF23 activa la aplicación obligatoria.

Este documento es un complemento del Whitepaper de Tokenómica de EXIOM y asume que este ha sido leído. El whitepaper cubre cuáles son los controles de concentración y por qué existen. Este documento cubre el detalle mecánico de cómo funciona cada control, los datos de validación de testnet detrás de HF22, la matemática económica precisa detrás del modificador de recompensa cero, la cuestión de la identidad del operador en una cadena de privacidad, y los riesgos residuales que el protocolo no resuelve por completo.

---

## Los datos actuales de concentración

| País | Nodos activos |
|---|---|
| Francia | 492 |
| Alemania | 70 |
| Estados Unidos | 55 |
| Canadá | 18 |
| Polonia | 13 |
| Reino Unido | 10 |
| Türkiye | 5 |
| Australia | 4 |
| Singapur | 2 |
| Lituania | 2 |
| Serbia | 1 |

Francia alberga 492 de los 672 nodos de esta instantánea (alrededor del 73% de la red), y esa concentración es casi en su totalidad una sola instalación de Contabo en Grand Est que alberga aproximadamente 426 nodos (alrededor del 63% de la red). El total del país no es lo que el protocolo limita; el **clúster** de Grand Est sí lo es. El umbral de supervivencia es el 30% de los nodos activos por clúster de proximidad (alrededor de 202 nodos en los 672 de esta instantánea, y alrededor de 283 en los 943 nodos del whitepaper actual), recalculado continuamente a medida que la red crece. Grand Est, con aproximadamente 426 nodos, es más del doble de ese límite.

---

## Qué significa esto para los operadores de nodos

Esta sección responde la pregunta directamente: ¿cómo afecta HF23 la forma en que ejecuta sus nodos?

**HF23 no limita por país, y no requiere un nodo por IP, un nodo por VPS, ni un nodo por monedero.** El límite es el 30% de la red activa por *clúster de proximidad* (nodos que comparten infraestructura física o de enrutamiento). Un operador que ejecuta 10, 50 o incluso 100 nodos en infraestructura compartida no se ve afectado en absoluto por HF23 mientras su clúster se mantenga por debajo de ese umbral. Puede ejecutar múltiples nodos en una máquina, una cuenta de VPS y un monedero. Nada en HF23 cambia eso.

**El modificador de recompensa cero se aplica solo a los nodos por encima del límite por clúster (30% de los nodos activos).** Los nodos registrados más antiguos en un clúster ganan recompensas completas hasta ese umbral. Solo los nodos clasificados por encima de él en un clúster sobreconcentrado ganan cero, y solo hasta que se migran a un clúster menos concentrado.

**La deduplicación de quórum limita la influencia de consenso por ronda, no el número de nodos ni los ingresos.** Un operador que ejecuta 50 nodos en un VPS gana recompensas de bloque en los 50 y gestiona su infraestructura exactamente como lo hace hoy. Reciben una plaza de quórum por clúster por ronda en lugar de potencialmente muchas, que es el resultado previsto.

**El enfoque correcto para un nuevo operador** es consultar el explorador de nodos, ver dónde están concentrados los clústeres existentes, y desplegar en un clúster poco poblado. Diez nodos en un servidor con su propio enrutamiento distinto funcionan perfectamente bien bajo HF23 porque ese clúster no está ni cerca del umbral del 30%. Recompensas completas, participación de quórum completa, sin problemas.

**La dinámica trabaja a su favor si despliega en regiones escasas.** Si una región acaba llenándose, el explorador de nodos lo muestra y los operadores tienen un incentivo financiero para mudarse antes de que el límite les afecte. Los operadores que llegaron primero mantienen las recompensas completas en sus nodos más antiguos hasta el umbral. Los nuevos registros en un clúster sobreconcentrado no ganan nada de inmediato, por lo que la economía empuja naturalmente los nuevos despliegues hacia regiones más ligeras.

**El problema específico que HF23 resuelve** es una instalación en Francia (el clúster de Contabo en Grand Est) que aloja aproximadamente 426 nodos, alrededor del 63% de la red en esta instantánea. Si esa instalación queda fuera de línea la red se estanca. El objetivo es llevar ese clúster por debajo del límite del 30%. Cada otro operador que ejecuta una configuración responsable de múltiples nodos en un clúster no concentrado es exactamente lo que la red necesita más.

---

## Por qué los hard forks están separados

HF22 se publica tras pruebas exitosas. La deduplicación de quórum por clave de monedero y la unificación del período de desvinculación no tienen dependencia de Lokinet. Ambas han sido validadas en testnet y retenerlas mientras la evaluación de Lokinet está pendiente es un retraso injustificado. Un actor sofisticado que lea el whitepaper antes de que se publique HF22 podría intentar la división de monederos para anticiparse al control de quórum, pero hacerlo es detectable mediante la correlación de temporización de pruebas de tiempo de actividad y el análisis de IP/ASN, y crea un registro documentado para la acción de gobernanza.

Lokinet se publica primero en su propia versión sin aplicación obligatoria (junto con el cambio de almacenamiento de nodos ligeros SQLite), de modo que el nuevo transporte no se hace crítico para el consenso en el momento en que se introduce. Durante esa versión el agrupamiento por proximidad se ejecuta activo y observable sin consecuencias en las recompensas, que es cuando se mide el número real de clústeres y se ajustan el umbral y la reserva de HF23. HF23 luego sigue y activa la aplicación obligatoria. Separar las versiones también da dominios de fallo limpios: si algo sale mal tras la activación de HF23 hay menos variables que aislar. Hasta que la aplicación obligatoria de HF23 esté activa, Grand Est permanece expuesto al riesgo completo de supervivencia más allá de la deduplicación de quórum de HF22.

---

## Mecánica de HF22

### Deduplicación de quórum por clave de monedero

El algoritmo de selección de quórum ejecuta una pasada de deduplicación sobre cada conjunto de candidatos antes de finalizar. Cuando el sorteo selecciona un nodo candidato, el algoritmo comprueba su dirección de monedero del operador contra todos los nodos ya seleccionados para la ronda. Si se encuentra una coincidencia, el candidato es reemplazado sorteando de nuevo del grupo elegible restante, excluyendo todas las direcciones ya representadas.

El sorteo de reemplazo no recicla candidatos ya rechazados. Sortea del grupo no seleccionado restante en el mismo orden ponderado por probabilidad usado para el sorteo inicial. Esto preserva las propiedades estadísticas de la selección de quórum sin introducir un sesgo determinista hacia ningún conjunto particular de nodos restantes.

**Resultados de validación de testnet:**
- 20 ciclos de estancamiento/recuperación completados (20/20)
- Tasa de recuperación del 100% en todos los ciclos
- Cero intervención manual requerida en ningún ciclo (peor intervalo de bloque 83 segundos)
- Línea base de mainnet pre-HF22: 1,000 bloques, 100% Pulse, cero bloques GOV_SIGNED
- Análisis de tiempos de espera de R0: ningún tiempo de espera de R0 introducido en condiciones de producción. El análisis de densidad de la mainnet actual confirma que cada clúster de IP de alta densidad es un solo operador, lo que significa que la deduplicación por clave de monedero ya proporciona protección completa contra los despliegues de ballenas actuales. Los dos despliegues de IP única más grandes (58 nodos y 51 nodos respectivamente) son cada uno un solo operador y están limitados a una plaza de quórum por ronda bajo HF22.

**Qué significa una plaza de quórum en la práctica:** El tamaño del quórum y la frecuencia de rotación determinan con qué frecuencia participa un nodo. Al tamaño actual de la red, un límite de una sola plaza significa que la influencia de un operador concentrado en las sesiones de oráculo, las rondas de Pulse y los quórums de obligaciones es idéntica a la de un operador con un solo nodo. Sus ingresos por recompensa de bloque no cambian.

**La brecha de división de monederos y su detección provisional:** Un operador que divide 426 nodos en 10 monederos obtiene hasta 10 plazas de quórum por ronda en lugar de una. Esta es la brecha conocida que HF23 cierra. Mientras tanto, la división de monederos es detectable mediante dos señales ya disponibles sin cambios en el daemon. Primero, la temporización de pruebas de tiempo de actividad: los nodos en el mismo host físico o hipervisor envían pruebas con milisegundos de diferencia entre sí, independientemente de la clave de monedero. Un clúster de pruebas que llega en ventanas de menos de 10ms desde nodos registrados en diferentes monederos es una señal fuerte de infraestructura compartida. Segundo, la correlación de IP y ASN: los nodos en diferentes monederos que comparten una IP, subred o ASN se registran y marcan para revisión de gobernanza. Un operador que divide monederos pero mantiene todos los nodos en la misma instalación de Contabo es identificable mediante ambas señales y está sujeto a acción de gobernanza bajo la política de lista de bloqueo.

### Unificación del período de desvinculación

El período de desvinculación por desregistro forzado cambia de 10,080 bloques (aproximadamente 7 días) a 20,160 bloques (aproximadamente 14 días), coincidiendo con el período de retiro voluntario. Este es un cambio de constante de consenso.

El período forzado original de 7 días fue una elección deliberada durante la estabilización de la red para limitar la penalización a los operadores que experimentaban eventos de infraestructura fuera de su control. Esa justificación ya no se aplica. La red es estable, el sistema de crédito de desmantelamiento proporciona el amortiguador para interrupciones breves, y un período unificado de 14 días elimina una asimetría que no tiene justificación restante.

Las monedas XEQM están bloqueadas en cadena durante el período de desvinculación mediante la transacción de registro. No hay mecanismo para liberar el bloqueo anticipadamente sin un cambio de protocolo. Para fallos de infraestructura documentados, la gobernanza puede compensar las recompensas perdidas desde el monedero de gobernanza como una transferencia de XEQM, pero el bloqueo en cadena cumple su duración completa independientemente.

---

## Mecánica de HF23

### Agrupamiento por proximidad de Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) enruta tráfico a través de la red de nodos de servicio en la capa 3, admitiendo TCP, UDP e ICMP. Cada nodo de servicio participa como un relé. El grafo de enrutamiento que emerge refleja la topología física de la red: los nodos en la misma instalación enrutan a través del mismo switch upstream y la misma red troncal del centro de datos, produciendo selecciones de ruta correlacionadas y latencia entre nodos de menos de un milisegundo. Los nodos en diferentes instalaciones enrutan a través de diferentes rutas con una latencia mensurablemente más alta.

El algoritmo de agrupamiento ingiere mediciones de latencia de enrutamiento de Lokinet por pares y de solapamiento de rutas a través de todos los nodos activos y los agrupa en clústeres usando estas mediciones como señal de proximidad. Un clúster no es una región geográfica fija; es una agrupación dinámica de nodos cuyo comportamiento de enrutamiento indica infraestructura física compartida. Dos nodos en diferentes instalaciones de Contabo en diferentes países pueden enrutar a través de suficiente infraestructura troncal compartida de Contabo como para aparecer en el mismo clúster si su solapamiento de rutas es suficientemente alto. Dos nodos en el mismo centro de datos pero en diferentes máquinas físicas con diferentes conexiones upstream aparecerán en diferentes clústeres si su solapamiento de rutas es bajo.

Señales suplementarias usadas junto con la proximidad de Lokinet:

**Correlación de temporización de pruebas de tiempo de actividad.** La red ya recibe pruebas de tiempo de actividad de todos los nodos activos en un calendario regular. La distribución de marcas de tiempo de las llegadas de pruebas desde cada nodo es registrada por los nodos receptores. Los nodos en el mismo host físico o hipervisor de VM envían pruebas dentro de una ventana estrecha característica, típicamente por debajo de 10 milisegundos. Agrupar esta distribución de temporización de llegada proporciona una señal de colocación física conjunta que no requiere cambios en el daemon y funciona antes de que Lokinet esté activo.

**Análisis de ASN.** La dirección IP de cada nodo se asigna a un Autonomous System Number mediante datos públicos de BGP. Los nodos que comparten un ASN comparten infraestructura de enrutamiento a nivel de proveedor y exposición legal a nivel de proveedor. Un proveedor que recibe una orden a nivel de jurisdicción que afecta a toda su infraestructura derriba todos sus nodos de ASN simultáneamente, independientemente de en cuántos clústeres de Lokinet aparezcan. La concentración de ASN se rastrea como una señal suplementaria y contribuye a la revisión de gobernanza de los operadores cercanos al umbral del clúster.

### Límite de registro de clúster

En el momento del registro, el protocolo ejecuta una evaluación de proximidad contra todos los clústeres existentes. Las características de enrutamiento de Lokinet del nodo que se registra se miden contra el centroide de cada clúster existente. Si el clúster más cercano ya contiene el 30% o más de los nodos activos, el registro se rechaza con un código de error específico que indica la capacidad del clúster y el número de nodos del clúster más cercano.

El rechazo es determinista: cualquier nodo que enrute de forma suficientemente similar a un clúster sobreconcentrado como para ser asignado a él es rechazado, independientemente de la clave de monedero del operador, el historial de registro o la cantidad de stake. El operador no puede apelar el rechazo mediante gobernanza. El único camino a seguir es registrarse en una infraestructura que enrute a un clúster diferente.

El umbral se evalúa contra el número de nodos activos en el momento del registro. A medida que la red crece, el umbral del 30% en términos absolutos crece con ella. Un operador en el límite hoy puede registrar nodos adicionales en un clúster previamente limitado a medida que la red crece y el límite absoluto aumenta, sin migrar ningún nodo existente.

### Modificador de recompensa cero

El modificador de recompensa cero se aplica en el momento del cálculo de la recompensa de bloque. El cálculo de la recompensa para un nodo seleccionado incluye una comprobación de elegibilidad del clúster. Si el clúster del nodo contiene más nodos que el umbral del límite, y el rango de registro del nodo dentro de ese clúster está por encima del umbral (clasificado del más antiguo al más nuevo), el cálculo de la recompensa devuelve cero.

El ranking se calcula a partir de la altura de bloque de registro del nodo dentro de su asignación de clúster. El nodo registrado más antiguo en el clúster obtiene el rango 1, el registrado más recientemente obtiene el rango N. Los nodos con rango mayor que el umbral del límite ganan cero. Los nodos con rango igual o inferior al umbral del límite ganan la recompensa estándar completa. El ranking se recalcula cada vez que cambia la asignación del clúster, lo que ocurre cuando los nodos migran fuera del clúster, cuando se unen nuevos nodos, o cuando el límite del clúster se desplaza debido a cambios en la topología de la red.

**La matemática económica para Grand Est:** Con 426 nodos y un límite de 208 nodos, 218 nodos ganan cero recompensas de bloque. Al precio autoalojado de $0.53 por nodo por mes, esos 218 nodos cuestan $115.54 por mes con cero ingresos. Al precio de Pecunia de $1.76 por nodo por mes, el costo es de $383.68 por mes. El operador tiene dos respuestas racionales: migrar los nodos excedentes a clústeres no concentrados, restaurando sus recompensas de inmediato al aceptarse el nuevo registro, o desregistrar los nodos excedentes y recuperar el XEQM en stake mediante el proceso de desvinculación. Cualquiera de las respuestas reduce la concentración. No hay base racional para mantener los nodos excedentes con recompensa cero.

**Mecánica del período de gracia:** En el bloque de activación de HF23, el protocolo toma una instantánea de todos los clústeres activos y sus recuentos de nodos. Cualquier clúster que supere el umbral del 30% se marca como sobreconcentrado. Durante los 30 días posteriores al bloque de activación, el modificador de recompensa cero se suspende para todos los nodos, incluidos los que están por encima del umbral del límite. Durante el período de gracia, los propietarios de nodos pueden observar las asignaciones de clúster del explorador de nodos, planificar migraciones y comenzar a ejecutarlas. En el bloque de vencimiento del período de gracia, el modificador se activa. Los nodos que han migrado fuera del clúster sobreconcentrado para ese bloque ganan recompensas completas a partir de ese bloque. Los nodos que aún están por encima del umbral ganan cero a partir de ese bloque hasta que migren.

### Deduplicación de quórum por clúster de proximidad

La actualización de deduplicación de quórum de HF23 reemplaza la comprobación de dirección de monedero por una comprobación de pertenencia a clúster. Cuando el sorteo selecciona un nodo candidato, el algoritmo comprueba su asignación de clúster contra todos los nodos ya seleccionados para la ronda. Si dos nodos comparten una asignación de clúster, el segundo es reemplazado por un sorteo del grupo restante, excluyendo todos los clústeres ya representados.

El efecto práctico sobre un operador que divide monederos: 10 direcciones de monedero a través de 426 nodos, todos en la misma instalación de Contabo, aparecen en el mismo clúster de proximidad. La comprobación de clúster los captura a todos como una sola unidad. Un nodo de ese clúster ocupa una plaza. Los otros 425 nodos de ese clúster no, independientemente de bajo cuántas direcciones de monedero distintas estén registrados.

### Requisito de número mínimo de clústeres y regla de reserva

El tamaño del quórum de la red EXIOM es de 12 plazas por ronda. La deduplicación por clúster de proximidad, por tanto, requiere al menos 12 clústeres de proximidad distintos en el conjunto de nodos activos para garantizar la formación de quórum. Si la red produce menos de 12 clústeres distintos, el algoritmo no puede satisfacer la restricción de una plaza por clúster y la formación de quórum falla.

Se estima que la distribución actual de la red, una vez aplicado el agrupamiento por proximidad de Lokinet, produce entre 12 y 18 clústeres distintos. Esto está incómodamente cerca del mínimo de 12 plazas. La infraestructura troncal compartida del proveedor entre instalaciones nominalmente separadas puede hacer que dos ubicaciones de IP distintas se fusionen en un solo clúster de proximidad en el grafo de enrutamiento de Lokinet. Cualquier fusión de ese tipo que reduzca el número de clústeres por debajo de 12 rompe la formación de quórum por completo.

El algoritmo, por tanto, implementa una regla de reserva obligatoria:

1. El algoritmo intenta llenar las 12 plazas con un nodo por clúster distinto, recorriendo los clústeres disponibles en orden aleatorio.
2. Si todos los clústeres distintos se agotan antes de que se llenen las 12 plazas, el algoritmo entra en una pasada de reserva.
3. En la pasada de reserva, permite un segundo nodo de cada clúster, comenzando primero con los clústeres más pequeños. Los clústeres menos concentrados reciben una segunda plaza antes que los más concentrados.
4. El algoritmo continúa con pasadas de reserva, incrementando el número máximo de plazas por clúster en uno en cada pasada, hasta que se llenen las 12 plazas.
5. El clúster más concentrado, como Grand Est bajo las condiciones actuales, recibe plazas adicionales solo después de que todos los clústeres más pequeños hayan recibido su asignación de reserva.

Cada ronda que activa la reserva se registra con el número de clústeres que la causó. La gobernanza monitorea la frecuencia de la reserva como un indicador directo de riesgo de concentración. Una red con 12 o más clústeres distintos nunca activa la reserva. Una red que activa la reserva de forma constante está señalando que la aplicación de concentración de HF23 aún no está logrando una diversidad física adecuada y que el límite de clúster o la aplicación del período de gracia requieren atención de gobernanza.

El registro de la reserva se publica en el explorador de nodos junto con las asignaciones de clúster para que la comunidad de operadores pueda observar el riesgo de concentración en tiempo real.

---

## Identidad del operador en una cadena de privacidad

El protocolo no necesita identificar qué operador humano posee qué nodos para aplicar el límite de clúster y el modificador de recompensa cero. Ambos controles operan a nivel de clúster. Lo que puede y no puede determinarse es un contexto útil para el monitoreo de gobernanza pero no es necesario para la aplicación del protocolo.

**Qué es determinista a partir de los datos en cadena:** los nodos registrados bajo la misma clave de monedero del operador son definitivamente el mismo operador. Esta es información pública en la transacción de registro.

**Qué es inferible con alta confianza a partir de los datos de Lokinet y de temporización:** el número de hosts físicos distintos que subyacen a un clúster de nodos, independientemente de cuántas claves de monedero usen. Cinco claves de monedero ejecutando cada una 85 nodos, todos en los mismos dos servidores físicos, producen dos firmas de temporización distintas y dos centroides de proximidad de Lokinet, no cinco.

**Qué no puede determinarse en una cadena de privacidad:** si dos claves de monedero diferentes con infraestructura distinta pertenecen al mismo operador humano. La fuente de financiación de cada clave de monedero es privada por diseño. Un operador sofisticado que usa cinco monederos financiados desde cinco fuentes diferentes a través de la capa de transacciones de la cadena de privacidad presenta cinco identidades distintas a nivel de protocolo.

Para la aplicación de la supervivencia, esto no importa. El clúster contiene 426 nodos. Los 208 más antiguos ganan recompensas. Los 218 más nuevos ganan cero. La identidad del operador es irrelevante para ese cálculo.

---

## Estado de implementación

| Control | Estado |
|---|---|
| Deduplicación de quórum por clave de monedero del operador | HF22, activado en el bloque 219120 |
| Unificación del período de desvinculación, de 7 a 14 días | HF22, activado |
| Recuperación de estancamiento de Pulse (reserva por firma, snode_revision 1) | Activado en el bloque 236920, 18 de octubre de 2026 |
| Activación de Lokinet como transporte de red | En desarrollo; se publica en una versión sin aplicación obligatoria antes de HF23 |
| Almacenamiento de nodos ligeros SQLite | En desarrollo; se publica con la versión de Lokinet previa a HF23 |
| Algoritmo de agrupamiento por proximidad | Fase de diseño, pendiente de la evaluación de Lokinet |
| Límite de registro de clúster, umbral del 30% | HF23, fase de diseño |
| Modificador de recompensa cero para nodos excedentes | HF23, fase de diseño |
| Mecanismo del período de gracia | HF23, fase de diseño |
| Deduplicación de quórum por clúster de proximidad con regla de reserva | HF23, fase de diseño |
| Monitoreo del número mínimo de clústeres y registro de la reserva | HF23, fase de diseño |
| Herramientas de correlación de temporización de pruebas de tiempo de actividad | Sin cambios en el daemon requeridos, herramientas en desarrollo |
| Suplemento de agrupamiento por ASN | Sin cambios en el daemon requeridos, herramientas en desarrollo |

---

## Qué no resuelven estos controles

**Concentración legal a nivel de proveedor.** Un proveedor que recibe una orden legal a nivel de jurisdicción que afecta a toda su infraestructura global derriba todos sus nodos simultáneamente, incluso si esos nodos aparecen en múltiples clústeres de proximidad de Lokinet. El análisis de ASN expone este riesgo pero el protocolo no puede imponer la diversidad de proveedores sin requerir que el operador divulgue la identidad de su proveedor. La dispersión geográfica producida naturalmente por el límite de clúster mitiga sustancialmente este riesgo en la práctica, ya que los operadores obligados a distribuirse entre clústeres usarán en la práctica múltiples proveedores.

**Determinación de la identidad del operador humano a través de divisiones de monedero en una cadena de privacidad.** Como se describió anteriormente, un operador sofisticado que usa múltiples monederos financiados a través de la cadena de privacidad no puede ser identificado a nivel de protocolo. El límite de clúster y el modificador de recompensa cero abordan el riesgo de dominio de fallo independientemente de la identidad. La deduplicación de quórum cierra la brecha de influencia de consenso en HF23. El riesgo residual es que un operador sofisticado ejecute muchos nodos a través de muchos clústeres genuinamente distintos, acumulando ingresos por recompensa de bloque proporcionales a su número de nodos mientras contribuye proporcionalmente a la salud de la red. Este es el resultado aceptable: la influencia de consenso concentrada está acotada; la participación distribuida de capital es recompensada.

Se anima a los operadores con preguntas sobre la asignación de clústeres, la planificación de migraciones o el cronograma de HF22/HF23 a publicar en el canal de Telegram de Operadores de Nodos o a abrir un issue en este repositorio.

---

## Idiomas disponibles

Las traducciones comunitarias de este documento se mantienen en el repositorio del whitepaper. En caso de cualquier conflicto entre una traducción y la versión en inglés, la versión en inglés prevalece.

| Language | Document |
|---|---|
| Español | [translations/es/concentration-limits-proposal.md](./translations/es/concentration-limits-proposal.md) |
| Français | [translations/fr/concentration-limits-proposal.md](./translations/fr/concentration-limits-proposal.md) |
| Deutsch | [translations/de/concentration-limits-proposal.md](./translations/de/concentration-limits-proposal.md) |
| 中文 | [translations/zh/concentration-limits-proposal.md](./translations/zh/concentration-limits-proposal.md) |
| Português | [translations/pt/concentration-limits-proposal.md](./translations/pt/concentration-limits-proposal.md) |
| Türkçe | [translations/tr/concentration-limits-proposal.md](./translations/tr/concentration-limits-proposal.md) |
| Polski | [translations/pl/concentration-limits-proposal.md](./translations/pl/concentration-limits-proposal.md) |
| Bahasa Indonesia | [translations/id/concentration-limits-proposal.md](./translations/id/concentration-limits-proposal.md) |

---

*Este documento no constituye asesoramiento financiero ni legal. XEQM es una moneda de utilidad para la plataforma EXIOM, no un producto de inversión. La clasificación de tokens, el estatus de valores y las regulaciones aplicables varían según la jurisdicción. Los participantes deben consultar su marco legal y regulatorio local antes de adquirir u operar con XEQM. XEQM Labs no fomenta la compra de XEQM sobre la base de una apreciación especulativa del precio.*
