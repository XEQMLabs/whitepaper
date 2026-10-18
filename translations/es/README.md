# XEQM Labs - Plataforma EXIOM
## Whitepaper de Tokenómica
### Borrador v12 | 09/27/2026

---

## Lo que está activo hoy frente a lo que está planificado

| Componente | Estado |
|---|---|
| Mainnet de EXIOM | Activa, operativa desde el 6 de mayo de 2026 |
| Red de nodos de servicio | Activa — 943 nodos de servicio activos al 27 de septiembre de 2026 |
| Lokinet (LLARP) | Se publica en una versión sin aplicación obligatoria antes de HF23 (transporte activo, agrupamiento por proximidad observable); HF23 activa la aplicación obligatoria. La implementación comienza en el Q4 2026 |
| Almacenamiento de nodos ligeros SQLite | En desarrollo; se publica con la versión de Lokinet previa a HF23, para reducir la memoria y el disco de los nodos, con nodos ligeros opcionales de ventana reciente |
| Canje de monedas XEQ a XEQM | Entregado y cerrado, ejecución en producción de 35 días, libro mayor público auditable |
| Monedero GUI | Activo, github.com/XEQMLabs/XEQMLabs-GUI |
| Explorador de nodos | Activo, monitoreo activo de nodos de servicio |
| EXIOM Oracle | Activo en mainnet (Robinhood Chain, chainId 4663); comité de operadores de 12 miembros al 28 de septiembre de 2026 |
| API para desarrolladores de EXIOM | Activa en beta — claves de autoservicio, reclamaciones de cumplimiento firmadas y un motor de verificación, OpenAPI en /docs; gratis para construir con uso prepagado por llamada desplegándose progresivamente (27 de septiembre de 2026) |
| EXIOM Privacy Oracle (TLSNotary / ZK) | Fundamentos activos (motor de verificación, sesiones de oráculo); oráculo completo de datos web privados en la Fase 3 |
| Plataforma de trading RFQ de EXIOM | En desarrollo, Fase 2/3, XEQM/BTC como primer par |
| HF22, deduplicación de quórum por clave de monedero, unificación de desvinculación, recuperación de estancamiento de Pulse | Activado en el bloque 219120 de mainnet. La revisión de recuperación de estancamiento de Pulse (snode_revision 1, reserva basada en firmas) se activó en el bloque 236920 el 18 de octubre de 2026 |
| HF23, límite de clúster por proximidad y modificador de recompensa (aplicación obligatoria) | En diseño; activa los límites de concentración una vez que la versión sin aplicación obligatoria de Lokinet + nodos ligeros se haya asentado; previsto para el Q4 2026 |
| Gobernanza formal en cadena | Planificado, Fase 6 |

---

## 1. Qué es XEQM Labs

XEQM Labs es una empresa de tecnología de privacidad. Su producto insignia, EXIOM, es una red Layer 1 de Prueba de Participación que preserva la privacidad y una plataforma comercial para desarrolladores, operada por un conjunto global de nodos de servicio. XEQM es la moneda de acceso y uso de la plataforma. Los desarrolladores construyen gratis y pagan por el uso en producción en XEQM, que se consume a medida que llaman a la API. Los operadores de nodos de servicio ganan XEQM por asegurar la red, y los mismos operadores pueden ganar ingresos adicionales ejecutando un sidecar de oráculo que sirve a los productos de oráculo de la plataforma.

El proyecto arrastra una historia comunitaria y operativa que se remonta a más de siete años. La mainnet de EXIOM se construyó para dar a esa comunidad una red con un suministro verificable, un calendario de emisión predecible, consenso puro de Prueba de Participación sin ningún componente de Prueba de Trabajo, y una mecánica de nodos de servicio que respeta el tiempo y el capital de los operadores.

XEQM es una moneda nativa Layer 1, no tokenizada en ninguna otra cadena, no es un ERC-20 ni un activo envuelto, y no está puenteada. Los poseedores interactúan directamente con la mainnet de EXIOM.

### La familia de productos EXIOM

**Red de nodos de servicio de EXIOM.** Activa en mainnet. Un conjunto global de nodos de servicio asegura la cadena, gana recompensas de bloque y forma la capa de infraestructura sobre la que se ejecutan todos los demás productos de EXIOM. 943 nodos de servicio activos al 27 de septiembre de 2026.

**Canje de monedas de EXIOM.** Un producto comercial que permite a los proyectos migrar su comunidad de poseedores de una cadena heredada a una nueva cadena con auditabilidad criptográfica completa. El piloto fue la migración de los poseedores de XEQ a XEQM en la mainnet de EXIOM, que se ejecutó durante 35 días con cada envío procesado a través de un libro mayor verificado criptográficamente que lleva una huella pública SHA256. El producto está disponible para otros proyectos que requieran una migración de cadena verificable.

**EXIOM Oracle.** Activo en mainnet. El primer producto de oráculo de la plataforma: un comité de operadores de nodos de servicio de XEQM — cada uno ejecutando un sidecar de oráculo ligero — que produce atestaciones de cumplimiento con agregación BLS y firmadas con EIP-712 (por ejemplo, que una dirección es elegible para una jurisdicción dada) que las aplicaciones consumen a través de la API para desarrolladores. Está desplegado en Robinhood Chain (chainId 4663) y ejecuta un comité de operadores de 12 miembros al 28 de septiembre de 2026. Ejecutar el sidecar es la forma en que un operador de nodo de servicio gana ingresos adicionales basados en uso por encima de las recompensas de bloque.

**API para desarrolladores de EXIOM.** Activa en beta. Una API estructurada que expone las capacidades de cumplimiento y verificación de la plataforma — reclamaciones de cumplimiento firmadas y un motor de verificación (reclamaciones firmadas, TLSNotary y mecanismos de conocimiento cero) — con acceso de autoservicio (un DID más una clave de API), una especificación OpenAPI 3.1, webhooks y solicitudes idempotentes. Los desarrolladores construyen gratis con una generosa asignación mensual y pagan por el uso en producción en XEQM, consumido por llamada. Fase 2, activa.

**EXIOM Privacy Oracle.** Diseñado, con los fundamentos ya establecidos. La evolución más amplia del oráculo: demostrar hechos sobre datos web privados (mediante TLSNotary y técnicas de conocimiento cero) sin exponer la fuente subyacente. El motor de verificación y los endpoints de sesión de oráculo que lo sustentan ya están activos; el oráculo completo de datos web privados es un entregable de la Fase 3. Tanto la plataforma RFQ de EXIOM como las aplicaciones de terceros pueden consumir las salidas del oráculo.

**Plataforma de trading RFQ de EXIOM.** En desarrollo. Una plataforma de trading extrabursátil de persona a persona con atestaciones de liquidación criptográficas, construida sobre la API de EXIOM. El primer par de trading es XEQM/BTC, ambos activos nativos Layer 1 sin tokenización, sin envoltura y sin riesgo de puente. El oráculo proporciona atestaciones de precio privadas para la capa de precios. Fase 2/3.

XEQM Labs opera EXIOM como una plataforma de software comercial. El objetivo es un ingreso sostenible de la plataforma que reduzca la dependencia de las emisiones de gobernanza con el tiempo. XEQM Labs no fomenta la compra de XEQM sobre la base de una apreciación especulativa del precio.

---

## 2. Procedencia del suministro

La migración está completa. Se emitieron 276,917,604 XEQM en la mainnet de EXIOM a cambio de tenencias heredadas. Esa cifra es el suministro inicial verificado en el lanzamiento de la mainnet el 6 de mayo de 2026. Cada depósito heredado se registró en un libro mayor público con una huella SHA256. La nueva cadena se acuñó una sola vez al concluir el canje para igualar ese total verificado exacto. Las claves de gasto de cada monedero involucrado en el canje se han publicado, y cualquiera puede verificar el historial de transacciones completo desde el depósito hasta el pago.

Más allá del suministro inicial, nuevos XEQM entran en circulación a través de dos flujos de emisión a nivel de protocolo: recompensas de bloque de nodos de servicio y emisiones de gobernanza. Ambos se ejecutan en calendarios fijos y predecibles escritos en el protocolo que cualquiera puede calcular a partir de parámetros públicos. Las tasas y el detalle operativo están en la Sección 3. El suministro total crece con el tiempo. XEQM es una cadena de suministro no limitado bajo el mismo modelo que la emisión de cola de Monero. La disciplina de suministro fijo a la que el proyecto se compromete se refiere a la ausencia de emisión discrecional, no a un tope estricto sobre las emisiones impulsadas por el protocolo.

**Sin acuñaciones discrecionales.** El protocolo no permite emisión ad-hoc, ajustes manuales de suministro ni acuñaciones fuera de calendario. Cada nuevo XEQM que entra en circulación lo hace a través de los dos flujos de emisión programados anteriores.

**Sin quemas.** La arquitectura criptográfica sobre la que se construye esta red no admite quemas demostrables en la forma en que ese término se usa típicamente. Cualquier dirección a la que se envíe una moneda es tan ingastable solo en la medida en que la clave esté demostrablemente destruida. No representaremos ningún monedero como una dirección de quema. Las monedas no canjeadas durante la ventana de migración permanecen en la cadena heredada inactiva y no forman parte del suministro de XEQM.

---

## 3. Modelo de tokenómica

### Emisiones de bloque

La red produce un nuevo bloque cada 60 segundos y otorga 8.25 XEQM al nodo de servicio seleccionado, generando 11,880 XEQM por día. Con 943 nodos activos (27 de septiembre de 2026), cada nodo gana aproximadamente 12.6 XEQM por día, o alrededor de 380 XEQM por mes.

A partir de HF21, las recompensas de bloque se distribuyen en un calendario de agrupación semanal. Antes de HF21, las recompensas se emitían cada 20 bloques. Las recompensas ahora se acumulan a lo largo de cada ventana de 10,080 bloques (aproximadamente 7 días) y se pagan al final de cada ventana. La tasa de emisión total no ha cambiado; solo ha cambiado la cadencia de pago.

### Emisión de gobernanza

El tesoro recibe aproximadamente 17,857 XEQM por día, o alrededor de 124,999 XEQM por semana. Este es el presupuesto operativo para un equipo activo de desarrollo de software comercial. Los ingenieros, revisores de seguridad, operadores de infraestructura y colaboradores del ecosistema se compensan con esta emisión mientras la plataforma está pre-ingresos. A medida que cada producto de EXIOM alcanza un estado generador de ingresos, la emisión de gobernanza se revisa y reduce en consecuencia. El objetivo a largo plazo es que los ingresos de la plataforma reemplacen la emisión de gobernanza como mecanismo de financiación principal.

### Asignación de la emisión

| Asignación | Porción | Propósito |
|---|---|---|
| Recompensas de nodos de servicio | 40% | Recompensas de bloque pagadas directamente a los nodos de servicio |
| Desarrollo del protocolo central | 25% | Blockchain, plataforma EXIOM y servicios de red centrales |
| Marketing y sensibilización | 15% | Visibilidad y adopción de la red |
| Ecosistema y comunidad | 10% | Subvenciones, recompensas, premios comunitarios, soporte de integración |
| Seguridad y auditorías | 5% | Auditorías, revisiones de seguridad, pruebas de fiabilidad |
| Reserva a largo plazo | 5% | Estabilidad, necesidades de emergencia, operaciones a largo plazo |

### Ingresos y distribución de la plataforma EXIOM

Más allá de las recompensas de bloque, la plataforma obtiene ingresos del uso de los desarrolladores. El acceso es prepagado: un desarrollador financia su cuenta depositando XEQM (no reembolsable), y ese saldo se reduce a medida que consume la API de producción, con precio por llamada. El desarrollo y la evaluación sobre la asignación gratuita no se cobran.

El XEQM consumido se reconoce como ingreso de la plataforma y se distribuye entre los operadores que sirven el oráculo y las operaciones de la plataforma:

| Receptor | Porción | Propósito |
|---|---|---|
| Operadores de sidecar de oráculo | 70% | Operadores de nodos de servicio que ejecutan el sidecar de oráculo, recompensados en proporción a las tareas de oráculo que ayudan a servir |
| Operaciones y desarrollo de la plataforma | 30% | Financia las operaciones y el desarrollo continuos, reduciendo con el tiempo la dependencia de la emisión de gobernanza |

Los operadores se llevan la mayoría porque ejecutan la infraestructura que sirve el oráculo. La proporción 70/30 es el valor inicial y es ajustable mediante gobernanza. Los ingresos se reconocen y distribuyen en la misma cadencia semanal que las recompensas de bloque — cada ventana de 10,080 bloques (aproximadamente 7 días), alineada con la agrupación de recompensas de HF21 — de modo que un operador recibe las recompensas de bloque y la porción de ingresos por uso en un solo ritmo. Esta porción de ingresos es el mecanismo por el cual la recompensa de sidecar del operador descrita en la Sección 4 se financia con uso real en lugar de emisión.

Hardware de referencia para ejecutar un nodo de servicio (y su sidecar de oráculo): 4 núcleos de CPU, 8 GB de RAM, 100 GB de SSD, conexión de 100 Mbps. Las cargas de trabajo más pesadas de oráculo de privacidad requieren especificaciones más altas, cubiertas en la Sección 10.

---

## 4. Estructura de los nodos de servicio

### Parámetros de staking

| Parámetro | Valor |
|---|---|
| Requisito de nodo completo | 200,000 XEQM |
| Stake mínimo del operador | 100,000 XEQM (50% del requisito completo) |
| Comisión máxima del operador | 10% |
| Período de desvinculación, retiro voluntario | 14 días, las recompensas continúan |
| Período de desvinculación, desregistro forzado | 14 días, sin recompensas (unificado en HF22) |
| Número máximo de plazas de contribuyentes | 11 (incluido el operador) |
| Contribución comunitaria mínima por plaza | 10,000 XEQM |
| Ventana de participantes comunitarios por nodo | Hasta 100,000 XEQM en hasta 10 plazas de contribuyentes |

### Economía de los nodos

Muchos proveedores de VPS en la nube ofrecen un nivel de servicio gratuito que puede sostener la operación de un nodo de servicio sin costo mensual. Un VPS de pago a aproximadamente $5.28 por mes puede ejecutar 10 nodos de servicio, llevando el costo de alojamiento por nodo a aproximadamente $0.53 por mes. El alojamiento gestionado a través de Pecunia está disponible a $1.76 por nodo por mes.

Las recompensas de bloque por nodo escalan de forma inversa con el número de nodos activos: con 943 nodos de servicio activos (27 de septiembre de 2026), la emisión diaria de 11,880 XEQM de la red equivale a aproximadamente 12.6 XEQM por nodo por día, alrededor de 380 XEQM por mes. Debido a que tanto la recompensa como el stake están denominados en XEQM, el APY de recompensa de bloque es de aproximadamente 2.3% independientemente del precio; el alojamiento es el único costo recurrente material, a aproximadamente $0.53 por nodo por mes autoalojado o $1.76 a través de Pecunia. Ejecutar el sidecar de oráculo (Sección 10) añade un segundo flujo de ingresos que se basa en ingresos y escala con el uso real de la plataforma, financiado por el consumo de los desarrolladores en lugar de la emisión.

### Economía de los contribuyentes

Los operadores que no pueden o eligen no ejecutar infraestructura pueden contribuir stake a un nodo existente a través de hasta 10 plazas de contribuyentes. El operador puede cobrar del 0% al 10% de la recompensa de bloque antes de que el resto se divida proporcionalmente entre los contribuyentes. Los contribuyentes no soportan ningún costo de alojamiento, por lo que en cada punto de precio el rendimiento neto de un contribuyente supera al de un operador autoalojado o alojado en Pecunia.

### Ciclo de vida del nodo

Los nodos permanecen activos indefinidamente con los requisitos de colateral y rendimiento mantenidos. Un nodo que incumple los requisitos puede ser remediado sin penalización. Si no se remedia, el desregistro forzado desencadena un período de desvinculación de 14 días sin recompensas. La salida voluntaria conlleva un período de desvinculación de 14 días con las recompensas continuando durante todo el período.

---

## 5. Supervivencia de la red y vectores de ataque

### Requisito de supervivencia

La red EXIOM hace compromisos de fiabilidad con los desarrolladores. Una red que puede quedar fuera de línea por una sola interrupción de centro de datos no puede hacer esos compromisos. El protocolo impone un tamaño máximo de dominio de fallo: ninguna instalación física, centro de datos o clúster de enrutamiento individual puede alojar más del 30% de los nodos activos.

Con 943 nodos (27 de septiembre de 2026), el 30% es aproximadamente 283 nodos. La pérdida de cualquier instalación individual puede dejar fuera de línea como máximo 283 nodos simultáneamente, dejando al menos 660 nodos operativos, suficientes para mantener la producción de bloques y la formación de quórum sin desregistros en cascada. Este es un requisito de ingeniería, no una preferencia de descentralización.

### Dos hard forks

La aplicación de la supervivencia se entrega en dos etapas, separadas para reducir el riesgo y enviar el trabajo validado de inmediato.

**HF22, activado:** Deduplicación de quórum por clave de monedero del operador y unificación del período de desvinculación, más una revisión de recuperación de estancamiento de Pulse (snode_revision 1) que reemplaza la anterior reserva de recuperación de Prueba de Trabajo por una basada en firmas. Sin dependencia de Lokinet. Validado a través de 20 ciclos de estancamiento/recuperación con una tasa de recuperación del 100%, cero intervención, y un peor intervalo de bloque de 83 segundos. HF22 se activó en el bloque 219120 de mainnet; la revisión de recuperación de estancamiento se activó en el bloque 236920 el 18 de octubre de 2026.

**HF23, en diseño, previsto para el Q4 2026:** Límite de registro de clúster por proximidad, modificador de recompensa cero para nodos excedentes, y actualización de la deduplicación de quórum de clave de monedero a clúster por proximidad. Los tres dependen del grafo de enrutamiento de Lokinet como señal de proximidad. Para evitar hacer que un nuevo transporte sea crítico para el consenso en el momento en que se introduce, Lokinet se publica primero en una versión separada sin aplicación obligatoria (junto con el cambio de almacenamiento de nodos ligeros SQLite), donde el agrupamiento por proximidad está activo y es observable pero no tiene consecuencias en las recompensas. HF23 luego activa la aplicación obligatoria, después de que esa versión se haya asentado y se haya medido el número real de clústeres y se hayan ajustado el umbral y la reserva.

### Controles de HF22

**Deduplicación de quórum por clave de monedero del operador.** Como máximo un nodo por dirección de monedero del operador puede ocupar una plaza de validador en cualquier ronda de Pulse, sesión de oráculo o quórum de obligaciones dado. Si un sorteo aleatorio selecciona dos nodos de la misma dirección de operador, el segundo es reemplazado por un nodo de un operador diferente. Las recompensas de bloque no se ven afectadas; se asignan por orden de tiempo de espera independientemente de la participación en el quórum.

Limitación conocida: derrotada por la división de monederos. Un operador que usa múltiples direcciones de monedero presenta múltiples claves de operador al protocolo. HF23 cierra esta brecha mediante la deduplicación por clúster de proximidad.

**Unificación del período de desvinculación.** La desvinculación por desregistro forzado se amplió de 7 días a 14 días, coincidiendo con el retiro voluntario. Ambos casos son ahora de 14 días.

### Controles de HF23

Una vez que Lokinet esté activo como transporte de red, los nodos que estén físicamente colocados juntos mostrarán firmas de enrutamiento características: latencia mutua de menos de un milisegundo y alto solapamiento de rutas a través del grafo de enrutamiento de Lokinet. Los nodos en instalaciones genuinamente diferentes mostrarán mayor latencia y menor solapamiento de rutas. Esta señal de agrupamiento se deriva del comportamiento de red observable, sin ningún requisito de que los operadores divulguen su proveedor o ubicación.

**Límite de registro de clúster.** Los nuevos registros de nodos se evalúan contra la proximidad de enrutamiento de Lokinet a los clústeres existentes. Si el clúster objetivo ya contiene el 30% o más de los nodos activos, el registro es rechazado por el protocolo.

**Modificador de recompensa cero.** Los nodos por encima del umbral del límite de clúster ganan cero recompensas de bloque hasta que se migren a un clúster no concentrado. Los nodos se clasifican dentro de cada clúster por antigüedad de registro; los nodos más antiguos hasta el umbral del límite ganan recompensas completas. Cada nodo por encima de ese umbral gana cero. Una tasa reducida puede justificarse frente a los costos de VPS; cero no puede.

Se aplica un período de gracia de 30 días en la activación de HF23. Todos los nodos ganan recompensas completas durante el período de gracia. Al vencimiento, el modificador de recompensa cero se activa sobre los nodos excedentes.

**Deduplicación de quórum por clúster de proximidad.** Actualiza la deduplicación por clave de monedero de HF22 a deduplicación por clúster de proximidad. Como máximo un nodo por clúster de proximidad por ronda, independientemente de la estructura de monederos. Cierra la brecha de división de monederos.

El tamaño del quórum es de 12 plazas por ronda. La deduplicación, por tanto, requiere al menos 12 clústeres de proximidad distintos para funcionar sin una reserva. Dada la topología de red actual, el número de clústeres en la activación de HF23 puede estar cerca de este mínimo. El algoritmo implementa una reserva obligatoria: si todos los clústeres distintos se agotan antes de que se llenen las 12 plazas, se asignan plazas adicionales comenzando por los clústeres más pequeños (menos concentrados) primero, antes de que el clúster más concentrado reciba una segunda plaza. La frecuencia de la reserva se registra y publica en el explorador de nodos como un indicador de riesgo de concentración en tiempo real. Una red que nunca activa la reserva ha logrado una diversidad física adecuada.

### Controles adicionales

**Barrera del costo de capital.** El stake mínimo del operador de 100,000 XEQM asegura que cada operador comprometa capital real en cada nodo. Ejecutar N nodos requiere al menos N x 100,000 XEQM en stake.

**Protección contra la captura de comisiones del operador.** EXIOM no está sujeto al ataque de captura de comisiones del operador presente en algunas redes de nodos de servicio, donde un operador registra un nodo con capital mínimo y fija una comisión del 100% para capturar toda la recompensa de bloque independientemente del stake de los contribuyentes. La comisión máxima está limitada al 10% y el stake mínimo del operador del 50% hace que esto sea económicamente irracional.

**Análisis de temporización de pruebas de tiempo de actividad.** Los nodos en el mismo host físico envían pruebas de tiempo de actividad en clústeres estrechamente correlacionados, detectables a partir de los datos de recepción de pruebas existentes sin cambios en el daemon.

**Análisis de ASN.** Los nodos detrás del mismo Autonomous System Number comparten infraestructura a nivel de proveedor y exposición legal. La concentración de ASN contribuye a la asignación de clústeres y a la revisión de gobernanza.

**Lista de bloqueo de gobernanza.** Una lista de bloqueo de claves públicas gestionada por gobernanza impide que las claves de registro bloqueadas registren nuevos nodos.

**Objetivo del coeficiente de Nakamoto.** La red apunta a un coeficiente de operadores de al menos 8. Al 27 de septiembre de 2026, a través de 943 nodos de servicio activos y 204 operadores, el coeficiente de Nakamoto de operadores — el número mínimo de operadores que controlan una mayoría de los nodos activos — es 9, cumpliendo el objetivo (frente a 7 a través de 184 operadores en julio de 2026). La concentración de instalaciones físicas es un problema separado y más agudo: una sola región de centro de datos todavía aloja una mayoría de los nodos, que es exactamente la concentración que el límite de clúster por proximidad de HF23 está diseñado para romper.

La propuesta completa de límites de concentración está en [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). La metodología de resistencia Sybil está en [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Lokinet como futuro transporte de red

La infraestructura de direccionamiento de la red EXIOM migrará de direcciones IP anunciadas públicamente al direccionamiento de Lokinet. Lokinet se publica primero en una versión sin aplicación obligatoria antes de HF23 (previsto para el Q4 2026); HF23 luego añade la aplicación de concentración que usa el grafo de enrutamiento de Lokinet. Lokinet (Low Latency Anonymous Routing Protocol, LLARP) es un protocolo de enrutamiento cebolla de capa 3 que enruta cualquier tráfico basado en IP a través de múltiples nodos de servicio mediante enrutamiento cebolla de múltiples saltos, sin que ningún nodo individual en la ruta conozca tanto el origen como el destino.

Una vez que Lokinet esté activo:

- Los nodos de servicio se direccionarán por su identificador criptográfico de Lokinet en lugar de una dirección IP anunciada públicamente
- La API para desarrolladores de EXIOM será accesible como un servicio oculto en una dirección `.loki`, ocultando la IP de origen del desarrollador al nodo de la API
- La plataforma de trading RFQ será accesible como un servicio oculto, ocultando las direcciones IP del solicitante y del LP a la plataforma
- La comunicación de sesión de oráculo entre el probador y el quórum verificador se enrutará a través de Lokinet, eliminando el supuesto de confianza en un coordinador centralizado

Lokinet se publica en una versión sin aplicación obligatoria antes de HF23, prevista para el Q4 2026, con HF23 siguiendo una vez que se haya asentado. El código base de LLARP está presente en el repositorio de EXIOM; la implementación de Lokinet como transporte de red principal comienza en el Q4 2026.

---

## 6. XEQM como moneda de utilidad

La demanda de XEQM proviene de tres fuentes. El staking de nodos bloquea la mayor parte del suministro, aproximadamente el 68% con los 943 nodos activos actuales (27 de septiembre de 2026). El consumo de los desarrolladores crea una capa de velocidad continua: las aplicaciones pagan por el uso de la API de producción en XEQM, de modo que la adopción de la plataforma se convierte directamente en demanda recurrente de la moneda. El acceso al oráculo añade una tercera capa para consumidores de mayor volumen.

El acceso sigue un modelo prepagado basado en uso en lugar de una barrera de stake-para-desbloquear — los desarrolladores no tienen que adquirir y bloquear un stake fijo para construir:

| Nivel | Modelo de acceso |
|---|---|
| Gratis | Construir y evaluar sin costo: una generosa asignación mensual de llamadas, sin depósito requerido |
| Producción | Uso prepagado: depositar XEQM y pagar por llamada; webhooks y límites más altos |
| Empresa | Límites personalizados, SLA y soporte; términos por volumen |

El uso en producción se mide por llamada a la API y se deduce del saldo prepagado de XEQM del desarrollador. Los depósitos son no reembolsables y se reconocen como ingresos de la plataforma a medida que se consumen (ver Sección 3). Un diseño anterior condicionaba los niveles a un stake fijo de XEQM; eso ha sido reemplazado por este modelo prepagado, que es más simple para los desarrolladores y estándar para las API comerciales.

---

## 7. Gobernanza y tesoro

La dirección del monedero de gobernanza y la clave de visualización están publicadas. Cualquiera puede verificar el saldo en cualquier momento. La gobernanza actualmente se ejecuta a través del equipo fundador con aportación de la comunidad mediante canales abiertos de Telegram y discusiones de GitHub.

Asignaciones del tesoro, extraídas de la emisión de gobernanza descrita en la Sección 3:

- Desarrollo central (25%): ingeniería para la API de EXIOM, el oráculo y la plataforma RFQ
- Marketing y sensibilización (15%): listados en exchanges, contenido, crecimiento de la comunidad
- Ecosistema y comunidad (10%): subvenciones, recompensas, soporte de integración
- Seguridad y auditorías (5%): auditorías de código, revisiones de seguridad, pruebas de penetración
- Reserva a largo plazo (5%): estabilidad operativa y reservas de emergencia

La Fase 3 introduce un proceso formal de propuestas y comentarios. La Fase 6 introduce la votación ponderada donde los operadores de nodos de servicio y nodos de API tienen derechos formales proporcionales al stake y la antigüedad.

---

## 8. Resumen de parámetros

| Parámetro | Valor |
|---|---|
| Mecanismo de consenso | 100% Prueba de Participación |
| Tiempo de bloque | 60 segundos |
| Recompensa de bloque | 8.25 XEQM por bloque |
| Emisiones de bloque diarias | 11,880 XEQM |
| Emisión de gobernanza | ~17,857 XEQM por día |
| Requisito de nodo completo | 200,000 XEQM |
| Stake mínimo del operador | 100,000 XEQM (50%) |
| Comisión máxima del operador | 10% |
| Número máximo de plazas de contribuyentes | 11 (incluido el operador) |
| Contribución comunitaria mínima | 10,000 XEQM por plaza |
| Ventana de participantes comunitarios por nodo | Hasta 100,000 XEQM en 10 plazas |
| Período de desvinculación, retiro voluntario | 14 días, las recompensas continúan |
| Período de desvinculación, desregistro forzado | 14 días, sin recompensas (HF22) |
| Suministro total | 276,917,604 XEQM en el lanzamiento, creciendo mediante emisiones programadas |
| Suministro bloqueado con 943 nodos (27 sep. 2026) | ~188,600,000 XEQM (~68% del suministro inicial) |
| En libre circulación con 943 nodos | ~88,300,000 XEQM al suministro inicial, creciendo con las emisiones |
| APY de operador en solitario con 943 nodos | ~2.3% (solo recompensas de bloque, pagadas semanalmente vía HF21) |
| Costo autoalojado por nodo | ~$0.53/mes ($5.28/mes VPS, 10 nodos) |
| Costo de alojamiento gestionado (Pecunia) | $1.76/nodo/mes |
| Nodos de servicio activos (27 de septiembre de 2026) | 943 |
| Coeficiente de Nakamoto de operadores (27 sep. 2026) | 9 — control mayoritario; objetivo >= 8; 943 nodos, 204 operadores |
| Activación externa del oráculo | Nakamoto >= 6 alcanzado; condicionado a la finalización de la Fase 3 |
| Tamaño del quórum | 12 plazas por ronda |
| Deduplicación de quórum, HF22 | Una dirección de monedero de operador por plaza de quórum por ronda |
| Deduplicación de quórum, HF23 | Un clúster de proximidad por plaza de quórum por ronda (requiere Lokinet) |
| Reserva de deduplicación de quórum, HF23 | Si existen menos de 12 clústeres distintos, los clústeres más pequeños reciben plazas adicionales primero antes que los clústeres más concentrados; la frecuencia de la reserva se registra y publica |
| Límite de supervivencia de red, HF23 | 30% de los nodos activos por clúster de proximidad (~283 nodos al número actual) |
| Modificador de recompensa cero, HF23 | Cero recompensas de bloque para los nodos por encima del límite de clúster, clasificados por antigüedad de registro |
| Repositorios centrales | github.com/XEQMLabs |

---

## 9. Hoja de ruta

**Fase 1, Estabilización de la red. COMPLETA.** La red de nodos de servicio creció hasta 943 nodos de servicio activos al 27 de septiembre de 2026 (desde 693 a través de 184 operadores en julio de 2026, coeficiente de Nakamoto 7). El canje de monedas XEQ a XEQM se ejecutó y cerró con éxito.

**Fase 2, API para desarrolladores de EXIOM y EXIOM Oracle. ACTIVA.** El EXIOM Oracle está activo en mainnet con un comité de operadores, y la API para desarrolladores está activa en beta (credenciales de autoservicio, endpoints de cumplimiento y verificación, OpenAPI). Trabajo restante de la Fase 2: facturación por consumo prepagado, la porción de ingresos del operador, y las primeras integraciones en producción. El desarrollo de la plataforma de trading RFQ de EXIOM procede en paralelo, con XEQM/BTC como primer par de trading.

**Fase 3, EXIOM Privacy Oracle y plataforma RFQ.** El oráculo se despliega por fases: prueba de concepto interna, testnet federada, luego mainnet con consumidores internos. La plataforma de trading RFQ alcanza producción en esta fase, usando el oráculo para la atestación de precio privada en el par XEQM/BTC. Ambas están construidas sobre la API de EXIOM.

**Fase 4, Acceso de consumidores externos al oráculo.** Las salidas del oráculo disponibles para desarrolladores de nivel Producción y Empresa y consumidores externos. Umbral del coeficiente de Nakamoto de 6 ya alcanzado; la activación está condicionada a la finalización de la Fase 3.

**HF22, activado (bloque 219120 de mainnet).** Dos cambios de consenso sin dependencia de Lokinet, la deduplicación de quórum por clave de monedero del operador (una dirección de operador por plaza de quórum por ronda) y la unificación del período de desvinculación (desregistro forzado ampliado de 7 a 14 días), más una revisión de recuperación de estancamiento de Pulse (snode_revision 1) que se activó en el bloque 236920 el 18 de octubre de 2026, reemplazando la recuperación de Prueba de Trabajo por una reserva basada en firmas. Validado a través de 20 ciclos de estancamiento/recuperación (100% de recuperación, peor intervalo de bloque 83 segundos).

**Versión de Lokinet y nodos ligeros, antes de HF23.** Una versión sin aplicación obligatoria que pone Lokinet en línea como transporte de red (agrupamiento por proximidad activo y observable en el explorador de nodos, sin consecuencias en las recompensas) e introduce el almacenamiento de nodos ligeros SQLite (menor memoria y disco por nodo, con nodos ligeros opcionales de ventana reciente). Esta versión se asienta para que se pueda medir el número real de clústeres de proximidad y se ajusten el umbral y la reserva de HF23 antes de que entre en vigor cualquier aplicación obligatoria.

**HF23, en diseño, previsto para el Q4 2026.** Activa la aplicación obligatoria una vez que la versión sin aplicación obligatoria de Lokinet y nodos ligeros anterior se haya asentado: límite de registro de clúster por proximidad (registros rechazados cuando un clúster supera el 30% de los nodos activos); modificador de recompensa cero para los nodos por encima del umbral del límite clasificados por antigüedad de registro; actualización de la deduplicación de quórum de clave de monedero a clúster de proximidad, con una regla de reserva obligatoria que asegura que la formación de quórum sea siempre posible incluso cuando existan menos de 12 clústeres distintos (los clústeres más pequeños reciben plazas adicionales primero antes que los clústeres más concentrados, con la frecuencia de la reserva registrada y publicada como un indicador de riesgo de concentración). Se aplica un período de gracia de 30 días en la activación antes de que el modificador de recompensa cero entre en vigor.

**Fase 6, Gobernanza formal.** Proceso estructurado de propuestas, votación ponderada para operadores, transición a largo plazo lejos de la gobernanza del equipo fundador.

---

## 10. EXIOM Oracle

### El primer oráculo activo: EXIOM Oracle

El primer producto de oráculo de la plataforma está activo en mainnet. El EXIOM Oracle es un comité de operadores de nodos de servicio de XEQM — cada uno ejecutando un sidecar de oráculo ligero junto a su nodo — que producen colectivamente atestaciones con agregación BLS y firmadas con EIP-712 sobre hechos de cumplimiento, más directamente si una dirección dada es elegible para una jurisdicción dada. Las aplicaciones consumen estas atestaciones a través de la API para desarrolladores y pueden enviar el resultado firmado en cadena. El comité está desplegado en Robinhood Chain (chainId 4663) y ejecuta un comité de operadores de 12 miembros al 28 de septiembre de 2026, con un umbral de firma de dos tercios (8 de 12).

**Modelo de seguridad: conjunto registrado frente a umbral.** El EXIOM Oracle no muestrea un comité por ronda. Debido a que una agregación BLS cuesta a la puerta lo mismo verificar si firmaron ocho miembros u ochocientos, cada miembro registrado firma cada ronda; muestrear un subconjunto no compraría nada y reintroduciría el riesgo de que un sorteo desafortunado resulte tener suficientes miembros coludidos para falsificar. La seguridad, por tanto, se reduce a dos propiedades del conjunto de miembros registrados de tamaño N, al umbral de dos tercios k = ceil(2N/3) que la puerta impone:

- **La falsificación** requiere que un adversario controle al menos k miembros registrados — una colusión, y por tanto una cuestión de concentración de **operadores**.
- **El paro** (un fallo de disponibilidad) requiere que al menos N - k + 1 = floor(N/3) + 1 miembros registrados se apaguen a la vez — una interrupción correlacionada, y por tanto una cuestión de concentración de **infraestructura**.

Estos son los dos coeficientes de Nakamoto, y son propiedades del conjunto registrado, no de la flota más amplia de nodos de servicio: la distribución de la flota acota el consenso, mientras que la resistencia a la falsificación y a los fallos de disponibilidad del oráculo dependen solo de quién ocupa las plazas registradas.

**Realización actual.** Al 28 de septiembre de 2026 los miembros registrados son todos operados por el operador del proyecto, por lo que el coeficiente de operadores del oráculo es 1: hoy su resistencia a la falsificación descansa en la confianza en un solo operador, no en criptografía distribuida. Este es el estado de partida honesto. El modelo de seguridad es k-de-N a través de operadores independientes; la realización se endurece a medida que se inscriben independientes, que es el propósito de incorporar operadores de nodos de servicio adicionales como miembros del sidecar. El número de nodos por sí solo no ayuda — los miembros adicionales elevan ambos coeficientes solo en la medida en que sean operadores independientes en instalaciones distintas.

**Cómo se impone la diversidad.** Debido a que no hay selección por ronda, la diversidad se decide en la **admisión**: un miembro se registra solo si mantiene la porción de cada operador por debajo de k y la porción de cada instalación en o por debajo de floor(N/3), y k se eleva para seguir ceil(2N/3) a medida que crece el conjunto. La concentración del conjunto registrado se monitorea continuamente y se publica como un margen de falsificación (k menos la porción del operador más grande) y un margen de disponibilidad (floor(N/3) + 1 menos la porción de la instalación más grande); un margen no positivo es una alarma. La señal de instalación es hoy el ASN y la temporización de llegada de las pruebas de tiempo de actividad, afinada en HF23 a la proximidad de enrutamiento de Lokinet, que detecta la colocación física conjunta incluso a través de ASN distintos. Esos hechos de distribución son ellos mismos atestables a través de la interfaz de hechos tipados del oráculo, de modo que la métrica de concentración es un valor firmado por el comité en lugar de la salida de un único script de confianza.

El sidecar es deliberadamente ligero: solo contiene su propia clave de firma, lee la identidad de su nodo localmente, y nunca maneja las claves de gasto del operador. Ejecutarlo es el mecanismo por el cual un operador de nodo de servicio gana los ingresos adicionales financiados por uso descritos en las Secciones 3 y 4.

### La visión más amplia: EXIOM Privacy Oracle

El EXIOM Privacy Oracle permite a las aplicaciones consumir fuentes de datos privados autenticadas sin exponer los datos de origen subyacentes. Utiliza técnicas de prueba de conocimiento cero para demostrar la procedencia de los datos desde endpoints HTTPS estándar, sin requerir cooperación del lado del servidor ni hardware de confianza. Es un entregable de la Fase 3, que sigue a la estabilización de la plataforma de API de la Fase 2 y a una consulta de criptografía antes de que comience la construcción completa.

El oráculo no es una fuente de datos de propósito general. Es un oráculo centrado en la privacidad para casos de uso donde los datos en sí deben permanecer confidenciales: umbrales de precio sin revelar los precios exactos, saldos de cuenta sin exponer credenciales, atestaciones de cumplimiento sin divulgar el registro subyacente. La plataforma RFQ de EXIOM es el primer consumidor interno, usándolo para demostrar que una ejecución de XEQM/BTC ocurrió a un precio de referencia o mejor sin revelar el precio exacto a la plataforma ni a la otra parte.

Una vez que Lokinet esté activo como transporte de red, la comunicación de sesión de oráculo entre el probador y el quórum verificador se enrutará mediante enrutamiento cebolla a través de la red de nodos de servicio. Ni el origen del probador ni las direcciones de red de los nodos del quórum serán visibles para ningún nodo de retransmisión individual, eliminando el supuesto de confianza en un coordinador centralizado.

### Arquitectura

**Capa del probador.** La aplicación o el usuario que posee acceso a la fuente de datos privada participa en un protocolo criptográfico que se compromete con la respuesta TLS sin revelarla. Las credenciales y los datos en bruto nunca salen del control del probador.

**Capa del verificador.** Un quórum rotativo de nodos de servicio verifica que los datos comprometidos satisfacen la condición solicitada. Los nodos verificadores solo conocen el resultado (verdadero o falso, por encima o por debajo de un umbral) y nunca ven los datos o las credenciales subyacentes.

**Capa del consumidor.** Los consumidores reciben solo la salida mínima: un resultado booleano, una comparación de umbral, una atestación firmada, o un pequeño valor derivado. Los datos de origen en bruto nunca se publican.

### Plan de construcción por fases

**Fase 1, Prueba de concepto interna.** El equipo fundador valida el protocolo criptográfico completo de extremo a extremo contra un pequeño conjunto de fuentes en lista blanca, sin consumidores externos ni participación de nodos de servicio.

**Fase 2, Testnet de oráculo federado.** Operadores voluntarios de nodos de servicio con un sólido historial de tiempo de actividad se unen al grupo de verificadores en testnet. Pruebas adversariales de la integridad de las atestaciones antes de cualquier despliegue en mainnet.

**Fase 3, Oráculo en mainnet con consumidores internos.** La tarea de verificador del oráculo se abre a nodos de mainnet cualificados. Las salidas alimentan los contratos internos de EXIOM y la plataforma RFQ. Las comisiones del oráculo comienzan a fluir a los nodos verificadores participantes.

**Fase 4, Acceso de consumidores externos.** Las salidas del oráculo disponibles para desarrolladores de nivel Producción y Empresa y consumidores externos. Condicionado a la finalización de la Fase 3.

### Requisitos de hardware del verificador

Requisitos indicativos: 8 núcleos de CPU, 16 GB de RAM, 200 GB de SSD, 500 Mbps con baja latencia. El hardware de referencia estándar de un nodo de API no es suficiente para la tarea de verificador del oráculo.

### Recompensas del verificador

| Fuente de ingresos | Descripción |
|---|---|
| Recompensas de bloque | Recompensa de bloque estándar de nodo de servicio, sin cambios |
| Porción de ingresos de la plataforma | Porción proporcional de los ingresos por consumo de desarrolladores para los operadores que ejecutan el sidecar de oráculo |
| Comisiones de sesión de oráculo | Comisión por sesión de los consumidores del oráculo, distribuida al quórum verificador |
| Bonificación por tarea de oráculo | Emisión de gobernanza suplementaria durante períodos de bajo volumen, reducida a medida que las comisiones de sesión se autosostienen |

---

## 11. Plataforma de trading RFQ de EXIOM

La plataforma RFQ de EXIOM es un sistema de trading extrabursátil de persona a persona con atestaciones de liquidación criptográficas, construido sobre la API de EXIOM. El primer par de trading es XEQM/BTC, ambos activos nativos Layer 1 sin tokenización, sin envoltura y sin riesgo de puente.

Una vez que Lokinet esté activo, la plataforma RFQ será accesible como un servicio oculto de Lokinet. Ni la dirección IP del solicitante ni la del LP serán visibles para la plataforma. La capa de precios del oráculo permite a una contraparte demostrar que una ejecución ocurrió a un precio de referencia o mejor desde una fuente en lista blanca, sin revelar el precio exacto de ejecución a la plataforma ni a la otra parte.

La especificación de la aplicación RFQ y el modelo de datos están completos. El desarrollo activo procede en la Fase 2 sobre la capa de API. La producción completa de la plataforma de trading es un entregable de la Fase 3, dependiente de que la API de EXIOM alcance producción y de que el MVP del oráculo complete su prueba de concepto interna.

---

---

## Idiomas disponibles

Las traducciones comunitarias de este whitepaper se mantienen en la carpeta de traducciones por conveniencia. **La versión en inglés es el único documento autoritativo en todo momento.** Las traducciones pueden quedar rezagadas respecto a la revisión actual en inglés y no se garantiza que estén actualizadas; en caso de cualquier conflicto, ambigüedad o diferencia de cualquier tipo, la versión en inglés prevalece.

| Language | Whitepaper |
|---|---|
| Español | [translations/es/README.md](./translations/es/README.md) |
| Français | [translations/fr/README.md](./translations/fr/README.md) |
| Deutsch | [translations/de/README.md](./translations/de/README.md) |
| 中文 | [translations/zh/README.md](./translations/zh/README.md) |
| Português | [translations/pt/README.md](./translations/pt/README.md) |
| Türkçe | [translations/tr/README.md](./translations/tr/README.md) |
| Polski | [translations/pl/README.md](./translations/pl/README.md) |
| Bahasa Indonesia | [translations/id/README.md](./translations/id/README.md)

---

*Este es un documento en borrador. Los parámetros, calendarios de emisión y fases de la hoja de ruta descritos aquí son el diseño previsto. Las actualizaciones se publicarán a medida que la red y la plataforma evolucionen.*

*Este documento no constituye asesoramiento financiero ni legal. XEQM es una moneda de utilidad para la plataforma EXIOM, no un producto de inversión. La clasificación de tokens, el estatus de valores y las regulaciones aplicables varían según la jurisdicción. Los participantes deben consultar su marco legal y regulatorio local antes de adquirir u operar con XEQM. XEQM Labs no fomenta la compra de XEQM sobre la base de una apreciación especulativa del precio.*
