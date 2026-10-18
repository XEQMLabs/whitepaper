# Riesgo Sybil y el modelo de mitigación de EXIOM
## Complemento técnico del Whitepaper de Tokenómica de EXIOM
### 07/26/2026

> **Nota (actualizada en octubre de 2026).** La concentración se aplica por *clúster de proximidad* (infraestructura física o de enrutamiento compartida), **no por país**. Las cifras de nodos aquí son una instantánea de julio de 2026; consulte el whitepaper para los totales actuales. Lokinet se publica en una versión sin aplicación obligatoria antes de HF23, y HF23 activa la aplicación obligatoria.

Este documento es un complemento del Whitepaper de Tokenómica de EXIOM y de la propuesta de Límites de concentración de nodos, y asume que ambos han sido leídos. El whitepaper cubre cuáles son los controles. La concentration-limits-proposal cubre la mecánica de cómo funciona cada control. Este documento cubre el modelo de amenaza: cómo se ve realmente un ataque Sybil en una cadena de privacidad, qué hace que la arquitectura de EXIOM sea específicamente resistente o vulnerable, y cómo la metodología de monitoreo continuo identifica la concentración en la práctica.

---

## La amenaza Sybil en una cadena de privacidad

Un ataque Sybil en una red de nodos de servicio significa que un solo actor opera muchos nodos bajo identidades aparentemente distintas para obtener una influencia desproporcionada. En una blockchain transparente, el análisis del grafo de monederos a menudo puede revelar que múltiples direcciones de operador de nodos se financian desde una fuente común, exponiendo al Sybil. En una cadena de privacidad, esa herramienta no está disponible por diseño. La garantía de privacidad que protege las transacciones de los usuarios también elimina el método de detección de Sybil más común.

La superficie Sybil de EXIOM, por tanto, difiere de una cadena transparente de una manera específica: un operador que usa correctamente las funciones de privacidad puede presentar múltiples direcciones de monedero que parecen no relacionadas a nivel de protocolo, independientemente de cuánto capital controlen. Esto no es un fallo en el diseño de privacidad. Es una propiedad inherente de cualquier cadena de privacidad que debe abordarse mediante mecanismos distintos del análisis del grafo de transacciones.

Las dos superficies de ataque Sybil en EXIOM son distintas y requieren controles separados:

**Ataque de influencia de consenso.** Un operador acumula suficientes nodos, a través de cualquier estructura de monederos, para ocupar un número desproporcionado de plazas de quórum simultáneamente. Esto les permite influir en los resultados de las sesiones de oráculo, las rondas de Pulse y los quórums de obligaciones más allá de lo que su proporción de stake individual sugeriría que es justo. El daño es a la integridad del consenso, no necesariamente al tiempo de actividad de la red.

**Ataque de dominio de fallo.** Un operador concentra nodos en una sola instalación física. Esto puede ser o no intencional como ataque; puede resultar de la optimización de costos. El daño es a la supervivencia de la red: una interrupción de la instalación deja los nodos del operador fuera de línea simultáneamente, lo que puede estancar la producción de bloques si la concentración es suficientemente grande.

---

## Qué hace a EXIOM estructuralmente resistente

**Costo de capital por identidad.** A diferencia de los ataques Sybil puros donde las identidades son gratuitas, cada nodo de servicio de EXIOM requiere 200,000 XEQM en stake, con el operador aportando personalmente al menos 100,000 XEQM. Un operador que ejecuta 100 nodos tiene 10,000,000 XEQM de capital en stake y bloqueado. Crear identidades aparentes adicionales mediante la división de monederos no reduce este costo -- cada nodo todavía requiere 100,000 XEQM de stake del operador. El ataque Sybil es caro a cualquier escala.

**Fricción de desvinculación.** Un período de desvinculación de 14 días tanto en el retiro voluntario como en el desregistro forzado significa que el capital comprometido en nodos Sybil no puede extraerse rápidamente. Un atacante que decide salir no puede hacerlo más rápido que cualquier otro operador.

**Registro público de nodos.** La clave de registro y la dirección de monedero del operador de cada nodo de servicio son públicas. Un nodo no puede participar en el consenso de forma anónima. Si bien la identidad humana detrás de una dirección de monedero es privada, la huella operativa del nodo se acumula con el tiempo a través de los patrones de registro, la temporización de las pruebas de tiempo de actividad y el comportamiento de enrutamiento.

---

## Cómo se identifica la concentración sin análisis del grafo de transacciones

Debido a que el análisis a nivel de transacción no está disponible, la detección de concentración de EXIOM se basa en cuatro señales que son observables a partir del comportamiento del nodo en lugar del historial de financiación.

**Agrupamiento por clave de registro.** Los nodos registrados bajo la misma clave de monedero del operador son definitivamente el mismo operador. Esto es determinista a partir de los datos en cadena. Un operador grande que no divide monederos es completamente visible solo a través de esta señal. Los despliegues más grandes actuales en la red, incluidos nodos que ejecutan 58 y 51 nodos respectivamente desde direcciones IP únicas, son cada uno operadores individuales confirmados mediante el análisis de la clave de registro.

**Agrupamiento por dirección IP y subred.** Actualmente la señal principal de colocación física conjunta. Múltiples nodos desde la misma dirección IP están casi con certeza en el mismo servidor. Múltiples nodos desde la misma subred sugieren la misma cuenta de alojamiento o bloque de centro de datos. Esta señal está disponible hoy sin ningún cambio en el daemon y permanecerá como señal suplementaria después de la activación de Lokinet.

**Correlación de temporización de pruebas de tiempo de actividad.** La red recibe pruebas de tiempo de actividad de cada nodo activo en un calendario regular. La distribución de marcas de tiempo de llegada de estas pruebas es registrada por los nodos receptores. Los nodos que se ejecutan en el mismo host físico o hipervisor de VM envían pruebas dentro de una ventana estrecha característica, típicamente por debajo de 10 milisegundos, porque comparten el mismo reloj del sistema y la misma interfaz de red. Un clúster de nodos de diferentes claves de monedero cuyas pruebas llegan de forma constante dentro de esta ventana es una señal fuerte de infraestructura física compartida, detectable sin ningún cambio en el daemon y sin que Lokinet esté activo.

Esta señal es específicamente útil para identificar operadores que dividen monederos pero mantienen sus nodos en infraestructura compartida. Las claves de monedero difieren; la temporización de las pruebas no.

**Proximidad de enrutamiento de Lokinet (se publica sin aplicación obligatoria antes de HF23; se aplica en HF23).** Una vez que Lokinet esté activo como transporte de red, el grafo de enrutamiento proporciona un mapa continuo de la topología física de la red de nodos. Los nodos en la misma instalación enrutan a través de la misma infraestructura upstream, produciendo selecciones de ruta correlacionadas y latencia entre nodos de menos de un milisegundo independientemente de sus claves de monedero o direcciones IP anunciadas. Esta es la señal más robusta porque refleja la realidad física de la red que no puede cambiarse mediante configuración de software sin mover realmente la infraestructura.

---

## El ataque de división de monederos en detalle

El enfoque Sybil más sofisticado disponible en EXIOM es la división de monederos: registrar nodos bajo múltiples direcciones de monedero financiadas a través de la capa de transacciones de la cadena de privacidad de modo que la fuente de financiación común no sea visible. Esto derrota la señal de agrupamiento por clave de registro pero no las demás.

Un operador que ejecuta 426 nodos a través de 10 monederos, todos alojados en la misma instalación de Contabo, queda expuesto por:

- Temporización de pruebas de tiempo de actividad: las pruebas de los 426 nodos llegan en la ventana característica de menos de 10ms de la infraestructura compartida
- Análisis de IP y subred: incluso con múltiples IP, la asignación del bloque del centro de datos y el ASN son compartidos
- Proximidad de Lokinet (post-HF23): los 426 nodos enrutan a través de la misma red troncal de Contabo independientemente de la clave de monedero

Un operador que ejecuta 426 nodos a través de 10 monederos, genuinamente distribuidos entre 10 proveedores diferentes en 10 países diferentes, no queda significativamente expuesto por ninguna señal actual. Las claves de registro difieren, la temporización de las pruebas difiere porque la infraestructura difiere, los ASN difieren, y las rutas de Lokinet difieren. A nivel de protocolo, esto parece 10 operadores diferentes.

Este es el riesgo Sybil residual en EXIOM después de aplicar todos los controles. Está acotado en sus consecuencias: la deduplicación de quórum de HF23 limita cada clúster de proximidad a una plaza de quórum por ronda independientemente de la estructura de monederos, de modo que incluso un operador distribuido que divide monederos no gana una influencia de consenso ilimitada. Sus ingresos por recompensa de bloque escalan con su número de nodos, lo cual es justo porque han aportado capital proporcional. Su influencia de consenso por ronda está limitada por la deduplicación de clúster independientemente de cuántos monederos usen.

---

## Metodología de monitoreo continuo

**Lista de bloqueo de gobernanza.** Una lista de bloqueo de claves públicas gestionada por gobernanza impide que las claves de registro bloqueadas registren nuevos nodos. Un operador que se muda a una nueva clave de monedero mientras la original está bloqueada crea un registro documentado de evasión, y la temporización de las pruebas y el comportamiento de enrutamiento de la nueva clave se correlacionan contra el perfil histórico de la clave bloqueada.

**Análisis del grafo de plazas de contribuyentes.** Las plazas de contribuyentes de los nodos de servicio son una señal de identidad secundaria. Un operador que financia plazas de contribuyentes a través de múltiples de sus propias claves de monedero crea un grafo de relaciones observable incluso en una cadena de privacidad, porque las transacciones de registro de contribuyentes llevan datos observables sobre a qué nodos contribuyen. Un operador que contribuye de forma constante a nodos registrados bajo el monedero A desde los monederos B y C, mientras esos mismos monederos B y C registran sus propios nodos, crea un grafo de correlación que complementa la señal directa de agrupamiento por clave de registro.

**Monitoreo de ASN.** La IP de cada nodo activo se asigna a un Autonomous System Number mediante datos públicos de BGP. La red rastrea la concentración de ASN a través del conjunto de nodos activos. Los nodos que comparten un ASN comparten infraestructura a nivel de proveedor y exposición legal. Una alta concentración de ASN se marca para revisión de gobernanza incluso cuando los registros de nodos individuales parecen no relacionados. La señal de ASN no identifica a un operador humano, pero identifica un dominio de fallo.

El estado actual de implementación de todos los controles descritos en este documento se mantiene en la [propuesta de Límites de concentración de nodos](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md).

---

*Este documento no constituye asesoramiento financiero ni legal. XEQM es una moneda de utilidad para la plataforma EXIOM, no un producto de inversión. La clasificación de tokens, el estatus de valores y las regulaciones aplicables varían según la jurisdicción. Los participantes deben consultar su marco legal y regulatorio local antes de adquirir u operar con XEQM. XEQM Labs no fomenta la compra de XEQM sobre la base de una apreciación especulativa del precio.*
