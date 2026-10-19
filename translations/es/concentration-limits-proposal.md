# Límites de Concentración de Nodos - Aplicación de la Supervivencia de la Red
## Complemento Técnico del Libro Blanco de Tokenómica de EXIOM
### 07/26/2026

> **Nota sobre el alcance (actualizada el 19 de octubre de 2026).** La unidad sujeta a aplicación es el *clúster de proximidad* (un grupo de nodos que comparten infraestructura física o de enrutamiento, detectado mediante la proximidad de enrutamiento de Lokinet, la sincronización de las pruebas de tiempo de actividad y el ASN), **no el país** ni el país de registro de un proveedor. Un país o proveedor con varias instalaciones genuinamente independientes representa menos riesgo que una sola instalación que concentre una gran cuota. Los datos de concentración que figuran a continuación son una instantánea del 19 de octubre de 2026 (893 nodos activos) agrupados por proveedor de alojamiento, el mejor sustituto disponible antes de Lokinet. Lokinet se distribuye en una versión no aplicativa antes de HF23, y HF23 activa la aplicación.

Este documento es un complemento del Libro Blanco de Tokenómica de EXIOM y presupone que este ya se ha leído. El libro blanco explica cuáles son los controles de concentración y por qué existen. Este documento aborda el detalle mecánico de cómo funciona cada control, los datos de validación en testnet detrás de HF22, las matemáticas económicas precisas que sustentan el modificador de recompensa cero, la cuestión de la identidad del operador en una cadena de privacidad y los riesgos residuales que el protocolo no resuelve por completo.

---

## Los Datos Actuales de Concentración

Medidos el 19 de octubre de 2026 con 893 nodos activos, agrupados por proveedor de alojamiento (ASN), que es la señal de concentración disponible hoy antes de Lokinet. El proveedor es un sustituto mucho mejor de un dominio de fallo compartido que la bandera de un país, porque la red e instalaciones de una misma empresa tienden a fallar, o a recibir la orden de desconexión, en conjunto.

| Proveedor (ASN) | Nodos activos | Cuota |
|---|---|---|
| NodeHub (AS214083) | 444 | 49.7% |
| Contabo (AS51167, más AS40021 y Contabo Asia AS141995) | ~303 | ~34% |
| OVH (AS16276) | 62 | 6.9% |
| Oracle (AS31898) | 22 | 2.5% |
| WebNX (AS18450) | 12 | 1.3% |
| todos los demás proveedores combinados (12 ASN más) | ~50 | ~5.6% |

NodeHub por sí solo concentra el 49.7% de la red, muy por encima del tope de supervivencia del 30% (267 nodos sobre 893 activos), y una sola subred /24 concentra el 41.2%. Este único proveedor es la concentración que HF23 está diseñado para romper.

Cómo se llegó a esto. Pecunia, un servicio de alojamiento que ofrecía ejecutar nodos XEQM para los operadores, ubicó la mayoría de sus nodos en Contabo. El rendimiento de Pecunia ha sido deficiente, y muchos operadores han migrado desde entonces a NodeHub. Así, el dominio de fallo dominante se ha desplazado de Contabo, que todavía concentra alrededor de un tercio de la red (gran parte de ella en la instalación de Grand Est), a NodeHub, ahora el mayor clúster individual de la red.

Una nota sobre las cifras por país. El país de registro de un proveedor no es donde se encuentran sus servidores. NodeHub está registrada en US y Contabo en DE, de modo que una vista por país etiqueta sus nodos como US y DE independientemente del centro de datos físico (la mayor instalación XEQM de Contabo está en Grand Est, FR). El protocolo no limita ni el país ni el registro del proveedor. Limita el clúster de proximidad, el conjunto de nodos que realmente comparten infraestructura física o de enrutamiento. El ASN y la subred son el sustituto actual de ello, y HF23 los reemplaza por la proximidad de enrutamiento de Lokinet, que también puede separar instalaciones distintas dentro de un mismo proveedor. El umbral es del 30% de los nodos activos por clúster (267 con los 893 actuales), recalculado de forma continua a medida que crece la red.

---

## Qué Significa Esto para los Operadores de Nodos

Esta sección responde la pregunta directamente: ¿cómo afecta HF23 a la forma en que ejecutas tus nodos?

**HF23 no limita por país, y no exige un nodo por IP, un nodo por VPS, ni un nodo por monedero.** El tope es del 30% de la red activa por *clúster de proximidad* (nodos que comparten infraestructura física o de enrutamiento). Un operador que ejecute 10, 50 o incluso 100 nodos en infraestructura compartida no se ve afectado en absoluto por HF23 siempre que su clúster se mantenga por debajo de ese umbral. Puedes ejecutar varios nodos en una sola máquina, una sola cuenta VPS y un solo monedero. Nada en HF23 cambia eso.

**El modificador de recompensa cero se aplica únicamente a los nodos que superan el tope por clúster (30% de los nodos activos).** Los nodos registrados más antiguamente en un clúster ganan recompensas completas hasta ese umbral. Solo los nodos situados por encima de él en un clúster sobreconcentrado ganan cero, y solo hasta que se migran a un clúster menos concentrado.

**La deduplicación de quórum limita la influencia en el consenso por ronda, no el número de nodos ni los ingresos.** Un operador que ejecute 50 nodos en un solo VPS gana recompensas de bloque en los 50 y gestiona su infraestructura exactamente como lo hace hoy. Recibe un asiento de quórum por clúster por ronda en lugar de potencialmente muchos, que es el resultado buscado.

**El enfoque correcto para un nuevo operador** es consultar el explorador de nodos, ver dónde están concentrados los clústeres existentes y desplegar en un clúster poco poblado. Diez nodos en un solo servidor con su propio enrutamiento distinto funcionan perfectamente bien bajo HF23 porque ese clúster está muy lejos del umbral del 30%. Recompensas completas, participación plena en el quórum, sin problemas.

**La dinámica juega a tu favor si despliegas en regiones poco pobladas.** Si una región acaba por llenarse, el explorador de nodos lo muestra y los operadores tienen un incentivo financiero para moverse antes de que el tope los afecte. Los operadores que llegaron primero conservan las recompensas completas en sus nodos más antiguos hasta el umbral. Los nuevos registros en un clúster sobreconcentrado no ganan nada de inmediato, por lo que la economía empuja de forma natural los nuevos despliegues hacia regiones más ligeras.

**El problema concreto que HF23 resuelve** es que un solo proveedor, NodeHub, aloja ahora alrededor de la mitad de la red (444 nodos, 49.7%), con Contabo en segundo lugar con aproximadamente un tercio. Si la infraestructura de NodeHub se desconecta o recibe la orden de desconexión, la red se detiene. El objetivo es llevar cualquier clúster individual por debajo del tope del 30%. Cada operador que ejecute una configuración responsable de varios nodos en un proveedor o instalación distinto y no concentrado es exactamente de lo que la red necesita más.

---

## Por Qué los Hard Forks Están Separados

HF22 se distribuye tras pruebas exitosas. La deduplicación de quórum por clave de monedero y la unificación del periodo de desvinculación no dependen de Lokinet. Ambas se han validado en testnet y retenerlas mientras está pendiente la evaluación de Lokinet es una demora injustificada. Un actor sofisticado que lea el libro blanco antes de que se distribuya HF22 podría intentar dividir monederos para anticiparse al control de quórum, pero hacerlo es detectable mediante la correlación de la sincronización de las pruebas de tiempo de actividad y el análisis de IP/ASN, y crea un registro documentado para la acción de gobernanza.

Lokinet se distribuye primero en su propia versión no aplicativa (junto con el cambio de almacenamiento de nodo ligero SQLite), de modo que el nuevo transporte no se vuelve crítico para el consenso en el momento en que se introduce. Durante esa versión, la agrupación por proximidad funciona en vivo y de forma observable sin consecuencias en las recompensas, que es cuando se mide el recuento real de clústeres y se ajustan el umbral de HF23 y la regla de reserva. HF23 viene después y activa la aplicación. Separar las versiones también proporciona dominios de fallo limpios: si algo sale mal tras la activación de HF23, hay menos variables que aislar. Hasta que la aplicación de HF23 esté activa, Grand Est permanece expuesta al riesgo completo de supervivencia más allá de la deduplicación de quórum de HF22.

---

## Mecánica de HF22

### Deduplicación de Quórum por Clave de Monedero

El algoritmo de selección de quórum ejecuta una pasada de deduplicación sobre cada conjunto de candidatos antes de finalizarlo. Cuando el sorteo selecciona un nodo candidato, el algoritmo compara la dirección del monedero de su operador con la de todos los nodos ya seleccionados para la ronda. Si se encuentra una coincidencia, el candidato se reemplaza sacando de nuevo del grupo restante de nodos elegibles, excluyendo todas las direcciones ya representadas.

El sorteo de reemplazo no vuelve a recorrer los candidatos ya rechazados. Saca del grupo restante no seleccionado en el mismo orden ponderado por probabilidad usado para el sorteo inicial. Esto preserva las propiedades estadísticas de la selección de quórum sin introducir un sesgo determinista hacia ningún conjunto concreto de nodos restantes.

**Resultados de validación en testnet:**
- 20 ciclos de detención/recuperación completados (20/20)
- Tasa de recuperación del 100% en todos los ciclos
- Cero intervención manual requerida en cualquier ciclo (peor intervalo entre bloques de 83 segundos)
- Línea base de mainnet previa a HF22: 1,000 bloques, 100% Pulse, cero bloques GOV_SIGNED
- Análisis de tiempo de espera R0: no se introdujeron tiempos de espera R0 en condiciones de producción. El análisis de densidad de la mainnet actual confirma que cada clúster de IP de alta densidad es un solo operador, lo que significa que la deduplicación por clave de monedero ya proporciona protección completa contra los despliegues de ballenas actuales. Los dos mayores despliegues de IP única (58 nodos y 51 nodos respectivamente) son cada uno un solo operador y están limitados a un asiento de quórum por ronda bajo HF22.

**Qué significa un asiento de quórum en la práctica:** El tamaño del quórum y la frecuencia de rotación determinan con qué frecuencia participa un nodo. Al tamaño de red actual, un tope de un solo asiento significa que la influencia de un operador concentrado en las sesiones de oráculo, las rondas de Pulse y los quórums de obligaciones es idéntica a la de un operador con un solo nodo. Sus ingresos por recompensa de bloque no cambian.

**La brecha de división de monederos y su detección provisional:** Un operador que divide 426 nodos entre 10 monederos obtiene hasta 10 asientos de quórum por ronda en lugar de uno. Esta es la brecha conocida que HF23 cierra. Mientras tanto, la división de monederos es detectable mediante dos señales ya disponibles sin cambios en el daemon. Primero, la sincronización de las pruebas de tiempo de actividad: los nodos en el mismo host físico o hipervisor envían pruebas con milisegundos de diferencia entre sí, independientemente de la clave del monedero. Un grupo de pruebas que llegan en ventanas de menos de 10 ms desde nodos registrados en distintos monederos es una señal fuerte de infraestructura compartida. Segundo, la correlación de IP y ASN: los nodos en distintos monederos que comparten una IP, subred o ASN quedan registrados y marcados para revisión de gobernanza. Un operador que divide monederos pero mantiene todos los nodos en la misma instalación de Contabo es identificable a través de ambas señales y queda sujeto a acción de gobernanza bajo la política de lista de bloqueo.

### Unificación del Periodo de Desvinculación

El periodo de desvinculación por baja forzosa cambia de 10,080 bloques (aproximadamente 7 días) a 20,160 bloques (aproximadamente 14 días), igualando el periodo de retiro voluntario. Este es un cambio de constante de consenso.

El periodo forzoso original de 7 días fue una elección deliberada durante la estabilización de la red para limitar la penalización a operadores que experimentaban eventos de infraestructura fuera de su control. Esa justificación ya no se aplica. La red es estable, el sistema de crédito por retirada de servicio proporciona el margen para cortes breves, y un periodo unificado de 14 días elimina una asimetría que ya no tiene justificación.

Las monedas XEQM quedan bloqueadas en la cadena durante el periodo de desvinculación mediante la transacción de registro. No existe mecanismo para liberar el bloqueo de forma anticipada sin un cambio de protocolo. En caso de fallos de infraestructura documentados, la gobernanza puede compensar las recompensas perdidas desde el monedero de gobernanza como una transferencia XEQM, pero el bloqueo en la cadena cumple toda su duración de todos modos.

---

## Mecánica de HF23

### Agrupación por Proximidad de Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) enruta el tráfico a través de la red de nodos de servicio en la capa 3, con soporte para TCP, UDP e ICMP. Cada nodo de servicio participa como relé. El grafo de enrutamiento que surge refleja la topología física de la red: los nodos en la misma instalación enrutan a través del mismo conmutador ascendente y la misma red troncal del centro de datos, produciendo selecciones de ruta correlacionadas y latencia entre nodos de menos de un milisegundo. Los nodos en instalaciones distintas enrutan por rutas diferentes con una latencia medible más alta.

El algoritmo de agrupación ingiere mediciones por pares de la latencia de enrutamiento de Lokinet y del solapamiento de rutas entre todos los nodos activos y los agrupa en clústeres usando estas mediciones como señal de proximidad. Un clúster no es una región geográfica fija; es una agrupación dinámica de nodos cuyo comportamiento de enrutamiento indica infraestructura física compartida. Dos nodos en distintas instalaciones de Contabo en distintos países pueden enrutar a través de suficiente infraestructura troncal compartida de Contabo como para aparecer en el mismo clúster si su solapamiento de rutas es lo bastante alto. Dos nodos en el mismo centro de datos pero en máquinas físicas distintas con conexiones ascendentes diferentes aparecerán en clústeres distintos si su solapamiento de rutas es bajo.

Señales complementarias usadas junto con la proximidad de Lokinet:

**Correlación de la sincronización de las pruebas de tiempo de actividad.** La red ya recibe pruebas de tiempo de actividad de todos los nodos activos según un calendario regular. La distribución de marcas de tiempo de las llegadas de pruebas de cada nodo es registrada por los nodos receptores. Los nodos en el mismo host físico o hipervisor de VM envían pruebas dentro de una ventana estrecha característica, típicamente por debajo de 10 milisegundos. Agrupar esta distribución de sincronización de llegadas proporciona una señal de colocalización física que no requiere cambios en el daemon y funciona antes de que Lokinet esté activo.

**Análisis de ASN.** La dirección IP de cada nodo se asigna a un Número de Sistema Autónomo mediante datos públicos de BGP. Los nodos que comparten un ASN comparten infraestructura de enrutamiento a nivel de proveedor y exposición legal a nivel de proveedor. Un proveedor que reciba una orden a nivel jurisdiccional que afecte a toda su infraestructura desconecta simultáneamente todos sus nodos del ASN, sin importar en cuántos clústeres de Lokinet aparezcan. La concentración de ASN se rastrea como señal complementaria y contribuye a la revisión de gobernanza de operadores cercanos al umbral del clúster.

### Tope de Registro por Clúster

En el momento del registro, el protocolo ejecuta una evaluación de proximidad contra todos los clústeres existentes. Las características de enrutamiento de Lokinet del nodo que se registra se miden contra el centroide de cada clúster existente. Si el clúster más cercano ya contiene el 30% o más de los nodos activos, el registro se rechaza con un código de error específico que indica la capacidad del clúster y el recuento de nodos del clúster más cercano.

El rechazo es determinista: cualquier nodo que enrute de forma lo bastante similar a un clúster sobreconcentrado como para ser asignado a él es rechazado, sin importar la clave del monedero del operador, su historial de registro ni el monto apostado. El operador no puede apelar el rechazo a través de la gobernanza. El único camino a seguir es registrarse en infraestructura que enrute hacia un clúster diferente.

El umbral se evalúa contra el recuento de nodos activos en el momento del registro. A medida que la red crece, el umbral del 30% en términos absolutos crece con ella. Un operador en el tope hoy puede registrar nodos adicionales en un clúster previamente topado a medida que la red crece y el tope absoluto sube, sin migrar ninguno de los nodos existentes.

### Modificador de Recompensa Cero

El modificador de recompensa cero se aplica en el momento del cálculo de la recompensa de bloque. El cálculo de recompensa para un nodo seleccionado incluye una comprobación de elegibilidad del clúster. Si el clúster del nodo contiene más nodos que el umbral del tope, y el rango de registro del nodo dentro de ese clúster está por encima del umbral (ordenados del más antiguo al más nuevo), el cálculo de recompensa devuelve cero.

El rango se calcula a partir de la altura del bloque de registro del nodo dentro de su asignación de clúster. El nodo registrado más antiguamente en el clúster recibe el rango 1, el registrado más recientemente recibe el rango N. Los nodos con rango mayor que el umbral del tope ganan cero. Los nodos con rango igual o inferior al umbral del tope ganan la recompensa estándar completa. El rango se recalcula cada vez que cambia la asignación de clúster, lo que ocurre cuando los nodos migran fuera del clúster, cuando se unen nuevos nodos, o cuando la frontera del clúster se desplaza debido a cambios en la topología de la red.

**Las matemáticas económicas para Grand Est:** Con 426 nodos y un tope de 208 nodos, 218 nodos ganan cero recompensas de bloque. Con un precio de autoalojamiento de $0.53 por nodo al mes, esos 218 nodos cuestan $115.54 al mes sin ingresos. Con el precio de Pecunia de $1.76 por nodo al mes, el coste es de $383.68 al mes. El operador tiene dos respuestas racionales: migrar los nodos excedentes a clústeres no concentrados, restaurando sus recompensas de inmediato en cuanto se acepte el nuevo registro, o dar de baja los nodos excedentes y recuperar el XEQM apostado a través del proceso de desvinculación. Cualquiera de las dos respuestas reduce la concentración. No hay base racional para mantener los nodos excedentes con recompensa cero.

**Mecánica del periodo de gracia:** En el bloque de activación de HF23, el protocolo toma una instantánea de todos los clústeres activos y sus recuentos de nodos. Todo clúster que supere el umbral del 30% se marca como sobreconcentrado. Durante los 30 días posteriores al bloque de activación, el modificador de recompensa cero queda suspendido para todos los nodos, incluidos los que están por encima del umbral del tope. Durante el periodo de gracia, los propietarios de nodos pueden observar las asignaciones de clúster del explorador de nodos, planificar migraciones y comenzar a ejecutarlas. En el bloque de expiración del periodo de gracia, el modificador se activa. Los nodos que hayan migrado fuera del clúster sobreconcentrado para ese bloque ganan recompensas completas a partir de ese bloque. Los nodos que sigan por encima del umbral ganan cero a partir de ese bloque hasta que migren.

### Deduplicación de Quórum por Clúster de Proximidad

La mejora de deduplicación de quórum de HF23 reemplaza la comprobación de la dirección del monedero por una comprobación de pertenencia a un clúster. Cuando el sorteo selecciona un nodo candidato, el algoritmo comprueba su asignación de clúster contra la de todos los nodos ya seleccionados para la ronda. Si dos nodos comparten una asignación de clúster, el segundo se reemplaza con un sorteo del grupo restante, excluyendo todos los clústeres ya representados.

El efecto práctico sobre un operador que divide monederos: 10 direcciones de monedero repartidas entre 426 nodos, todos en la misma instalación de Contabo, aparecen en el mismo clúster de proximidad. La comprobación de clúster los captura a todos como una sola unidad. Un nodo de ese clúster ocupa un asiento. Los otros 425 nodos de ese clúster no, sin importar bajo cuántas direcciones de monedero distintas estén registrados.

### Requisito de Recuento Mínimo de Clústeres y Regla de Reserva

El tamaño del quórum de la red EXIOM es de 12 asientos por ronda. La deduplicación por clúster de proximidad requiere, por tanto, al menos 12 clústeres de proximidad distintos en el conjunto de nodos activos para garantizar la formación del quórum. Si la red produce menos de 12 clústeres distintos, el algoritmo no puede satisfacer la restricción de un asiento por clúster y la formación del quórum falla.

Se estima que la distribución actual de la red, una vez aplicada la agrupación por proximidad de Lokinet, produce entre 12 y 18 clústeres distintos. Esto está incómodamente cerca del mínimo de 12 asientos. La infraestructura troncal compartida de un proveedor entre instalaciones nominalmente separadas puede hacer que dos ubicaciones IP distintas se fusionen en un solo clúster de proximidad en el grafo de enrutamiento de Lokinet. Cualquier fusión de ese tipo que reduzca el recuento de clústeres por debajo de 12 rompe por completo la formación del quórum.

Por ello, el algoritmo implementa una regla de reserva obligatoria:

1. El algoritmo intenta ocupar los 12 asientos con un nodo por cada clúster distinto, recorriendo los clústeres disponibles en orden aleatorio.
2. Si todos los clústeres distintos se agotan antes de ocupar los 12 asientos, el algoritmo entra en una pasada de reserva.
3. En la pasada de reserva, permite un segundo nodo de cada clúster, empezando primero por los clústeres más pequeños. Los clústeres menos concentrados reciben un segundo asiento antes que los más concentrados.
4. El algoritmo continúa las pasadas de reserva, incrementando en uno el máximo de asientos por clúster en cada pasada, hasta ocupar los 12 asientos.
5. El clúster más concentrado, como Grand Est en las condiciones actuales, recibe asientos adicionales solo después de que todos los clústeres más pequeños hayan recibido su asignación de reserva.

Cada ronda que activa la reserva se registra con el recuento de clústeres que la provocó. La gobernanza supervisa la frecuencia de la reserva como indicador directo de riesgo de concentración. Una red con 12 o más clústeres distintos nunca activa la reserva. Una red que activa la reserva de forma consistente está señalando que la aplicación de concentración de HF23 aún no está logrando una diversidad física adecuada y que el tope de clúster o la aplicación del periodo de gracia requieren atención de la gobernanza.

El registro de reserva se publica en el explorador de nodos junto a las asignaciones de clúster, de modo que la comunidad de operadores pueda observar el riesgo de concentración en tiempo real.

---

## Identidad del Operador en una Cadena de Privacidad

El protocolo no necesita identificar qué operador humano posee qué nodos para aplicar el tope de clúster y el modificador de recompensa cero. Ambos controles operan a nivel de clúster. Lo que puede y no puede determinarse es un contexto útil para la supervisión de la gobernanza, pero no es necesario para la aplicación del protocolo.

**Qué es determinista a partir de los datos en la cadena:** los nodos registrados bajo la misma clave de monedero de operador son definitivamente el mismo operador. Esta es información pública en la transacción de registro.

**Qué es inferible con alta confianza a partir de los datos de Lokinet y de sincronización:** el número de hosts físicos distintos que subyacen a un clúster de nodos, sin importar cuántas claves de monedero usen. Cinco claves de monedero ejecutando 85 nodos cada una, todas en los mismos dos servidores físicos, producen dos firmas de sincronización distintas y dos centroides de proximidad de Lokinet, no cinco.

**Qué no puede determinarse en una cadena de privacidad:** si dos claves de monedero diferentes con infraestructura distinta pertenecen al mismo operador humano. La fuente de financiación de cada clave de monedero es privada por diseño. Un operador sofisticado que use cinco monederos financiados desde cinco fuentes diferentes a través de la capa de transacciones de la cadena de privacidad presenta cinco identidades distintas a nivel de protocolo.

Para la aplicación de la supervivencia, esto no importa. El clúster contiene 426 nodos. Los 208 más antiguos ganan recompensas. Los 218 más nuevos ganan cero. La identidad del operador es irrelevante para ese cálculo.

---

## Estado de Implementación

| Control | Estado |
|---|---|
| Deduplicación de quórum por clave de monedero del operador | HF22, activado en el bloque 219120 |
| Unificación del periodo de desvinculación, de 7 a 14 días | HF22, activado |
| Recuperación de detención de Pulse (reserva de firma, snode_revision 1) | Activado en el bloque 236920, 18 de octubre de 2026 |
| Activación de Lokinet como transporte de red | En desarrollo; se distribuye en una versión no aplicativa antes de HF23 |
| Almacenamiento de nodo ligero SQLite | En desarrollo; se distribuye con la versión de Lokinet previa a HF23 |
| Algoritmo de agrupación por proximidad | Fase de diseño, pendiente de la evaluación de Lokinet |
| Tope de registro por clúster, umbral del 30% | HF23, fase de diseño |
| Modificador de recompensa cero para nodos excedentes | HF23, fase de diseño |
| Mecanismo de periodo de gracia | HF23, fase de diseño |
| Deduplicación de quórum por clúster de proximidad con regla de reserva | HF23, fase de diseño |
| Monitoreo del recuento mínimo de clústeres y registro de reserva | HF23, fase de diseño |
| Herramientas de correlación de la sincronización de las pruebas de tiempo de actividad | No requiere cambios en el daemon, herramientas en desarrollo |
| Complemento de agrupación por ASN | No requiere cambios en el daemon, herramientas en desarrollo |

---

## Qué No Resuelven Estos Controles

**Concentración legal a nivel de proveedor.** Un proveedor que reciba una orden legal a nivel jurisdiccional que afecte a toda su infraestructura global desconecta todos sus nodos simultáneamente, incluso si esos nodos aparecen en varios clústeres de proximidad de Lokinet. El análisis de ASN pone de manifiesto este riesgo, pero el protocolo no puede imponer la diversidad de proveedores sin exigir que el operador revele la identidad de su proveedor. La dispersión geográfica que produce de forma natural el tope de clúster mitiga sustancialmente este riesgo en la práctica, ya que los operadores obligados a distribuirse entre clústeres usarán en la práctica varios proveedores.

**Determinación de la identidad del operador humano a través de divisiones de monedero en una cadena de privacidad.** Como se describió anteriormente, un operador sofisticado que use varios monederos financiados a través de la cadena de privacidad no puede ser identificado a nivel de protocolo. El tope de clúster y el modificador de recompensa cero abordan el riesgo del dominio de fallo independientemente de la identidad. La deduplicación de quórum cierra la brecha de influencia en el consenso en HF23. El riesgo residual es que un operador sofisticado ejecute muchos nodos en muchos clústeres genuinamente distintos, acumulando ingresos por recompensa de bloque proporcionales a su número de nodos a la vez que contribuye proporcionalmente a la salud de la red. Este es el resultado aceptable: la influencia concentrada en el consenso está acotada; la participación distribuida de capital es recompensada.

Se anima a los operadores con preguntas sobre la asignación de clúster, la planificación de migraciones o el calendario de HF22/HF23 a publicar en el canal de Telegram de Operadores de Nodos o a abrir un issue en este repositorio.

---

## Idiomas Disponibles

Las traducciones comunitarias de este documento se mantienen en el repositorio del libro blanco. En caso de cualquier conflicto entre una traducción y la versión en inglés, prevalece la versión en inglés.

| Idioma | Documento |
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

*Este documento no constituye asesoramiento financiero ni legal. XEQM es una moneda de utilidad para la plataforma EXIOM, no un producto de inversión. La clasificación del token, su estatus como valor y la normativa aplicable varían según la jurisdicción. Los participantes deben consultar su marco legal y regulatorio local antes de adquirir XEQM u operar con él. XEQM Labs no fomenta la compra de XEQM sobre la base de una apreciación especulativa del precio.*
