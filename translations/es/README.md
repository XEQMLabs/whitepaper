# XEQM Labs - Plataforma EXIOM
## Libro Blanco de Tokenomía
### Borrador v11 | 26/07/2026

> *Esta traducción fue producida con herramientas de traducción de inteligencia artificial. Se proporciona únicamente por conveniencia informativa. En caso de conflicto o ambigüedad entre esta traducción y el original en inglés, prevalece la versión en inglés. La versión en inglés está en [github.com/XEQMLabs/whitepaper](https://github.com/XEQMLabs/whitepaper).*

---

## Qué Está Activo Hoy vs. Qué Está Planificado

| Componente | Estado |
|---|---|
| EXIOM mainnet | Activo, operativo desde el 6 de mayo de 2026 |
| Red de nodos de servicio | Activo, 693 nodos activos, 184 operadores (julio 2026) |
| Lokinet (LLARP) | Presente en el código base, estado de activación en evaluación de ingeniería |
| Intercambio de monedas XEQ a XEQM | Entregado y cerrado, ejecución de producción de 35 días, registro auditable público |
| Cartera GUI | Activo, github.com/XEQMLabs/XEQMLabs-GUI |
| Explorador de nodos | Activo, monitoreo activo de nodos de servicio |
| API de desarrollador EXIOM | En desarrollo, Fase 2 (ACTIVO) |
| Oráculo de privacidad EXIOM | Diseñado, pre-implementación, Fase 3 |
| Plataforma de trading RFQ EXIOM | En desarrollo, Fase 2/3, primer par XEQM/BTC |
| HF22, deduplicación de quórum y unificación de desbloqueo | Ingresando a testnet, validado, sin dependencia de Lokinet |
| HF23, límite de clúster de proximidad, modificador de recompensa, transporte Lokinet | Fase de diseño, pendiente de evaluación de ingeniería de Lokinet |
| Gobernanza formal en cadena | Planificado, Fase 6 |

---

## 1. Qué Es XEQM Labs

XEQM Labs es una empresa de tecnología de privacidad. Su producto insignia, EXIOM, es una red Layer 1 de Prueba de Participación que preserva la privacidad y una plataforma comercial para desarrolladores operada por un conjunto global de nodos de servicio. XEQM es la moneda de acceso y uso de la plataforma. Los desarrolladores apuestan XEQM para desbloquear niveles de API. Las aplicaciones consumen XEQM cuando realizan llamadas. Los operadores de nodos de servicio ganan XEQM por asegurar la red. Los operadores de nodos API ganan XEQM por servir tráfico de desarrolladores.

El proyecto lleva adelante una comunidad e historia operativa de más de siete años. La mainnet de EXIOM fue construida para dar a esa comunidad una red con un suministro verificable, un cronograma de emisión predecible, consenso puro de Prueba de Participación sin componente de Prueba de Trabajo, y mecánicas de nodos de servicio que respetan el tiempo y el capital del operador.

XEQM es una moneda nativa Layer 1, no tokenizada en ninguna otra cadena, no es un ERC-20 ni un activo envuelto, y no tiene puente. Los titulares interactúan directamente con la mainnet de EXIOM.

### La Familia de Productos EXIOM

**Red de Nodos de Servicio EXIOM.** Activo en mainnet. 693 nodos activos en 184 operadores independientes a julio de 2026.

**Intercambio de Monedas EXIOM.** Un producto comercial que permite a los proyectos migrar su comunidad de titulares de una cadena heredada a una nueva cadena con total auditabilidad criptográfica. El piloto fue la migración de titulares de XEQ a XEQM, ejecutándose durante 35 días con cada envío procesado a través de un libro mayor verificado criptográficamente con una huella SHA256 pública.

**API de Desarrollador Privado EXIOM.** En desarrollo. Una plataforma de desarrolladores que expone las capacidades de privacidad de la red a través de una API estructurada. Fase 2, activo.

**Oráculo de Privacidad EXIOM.** Diseñado, pre-implementación. Un oráculo centrado en la privacidad que prueba hechos sobre datos web privados sin exponer la fuente subyacente. Fase 3.

**Plataforma de Trading RFQ EXIOM.** En desarrollo. Una plataforma de trading over-the-counter peer-to-peer con attestaciones de liquidación criptográfica. El primer par de trading es XEQM/BTC. Fase 2/3.

XEQM Labs no fomenta la compra de XEQM sobre la base de apreciación de precio especulativa.

---

## 2. Procedencia del Suministro

La migración está completa. Se emitieron 276.917.604 XEQM en la mainnet de EXIOM a cambio de tenencias heredadas. Esa cifra es el suministro inicial verificado al lanzamiento el 6 de mayo de 2026. Cada depósito heredado fue registrado en un libro mayor público con una huella SHA256. Las claves de gasto de cada cartera involucrada en el intercambio han sido publicadas.

**Sin acuñaciones discrecionales.** El protocolo no permite emisión ad-hoc ni acuñaciones fuera de calendario.

**Sin quemas.** La arquitectura criptográfica de esta red no admite quemas demostrables. No representaremos ninguna cartera como dirección de quema.

---

## 3. Modelo de Tokenomía

La red produce un nuevo bloque cada 60 segundos y otorga 8,25 XEQM al nodo de servicio seleccionado, generando 11.880 XEQM por día. Con 700 nodos activos, cada nodo gana aproximadamente 17,0 XEQM por día, o 516 XEQM por mes.

El tesoro recibe aproximadamente 17.857 XEQM por día. Este es el presupuesto operativo para el equipo de desarrollo activo mientras la plataforma es pre-ingresos.

### Asignación de Emisiones

| Asignación | Participación | Propósito |
|---|---|---|
| Recompensas de Nodos de Servicio | 40% | Recompensas de bloque pagadas directamente a los nodos |
| Desarrollo del Protocolo Central | 25% | Blockchain, plataforma EXIOM y servicios de red |
| Marketing y Concienciación | 15% | Visibilidad de la red y adopción |
| Ecosistema y Comunidad | 10% | Subvenciones, recompensas, soporte de integración |
| Seguridad y Auditorías | 5% | Auditorías y revisiones de seguridad |
| Reserva a Largo Plazo | 5% | Estabilidad y necesidades de emergencia |

### Distribución de Tarifas de la Plataforma EXIOM

| Destinatario | Participación |
|---|---|
| Operadores de Nodos API | 35% |
| Tesoro de XEQM Labs | 35% |
| Gobernanza Comunitaria | 30% |

---

## 4. Estructura del Nodo de Servicio

| Parámetro | Valor |
|---|---|
| Requisito de nodo completo | 200.000 XEQM |
| Participación mínima del operador | 100.000 XEQM (50%) |
| Tarifa máxima del operador | 10% |
| Período de desbloqueo, retiro voluntario | 14 días, las recompensas continúan |
| Período de desbloqueo, desregistro forzado | 14 días, sin recompensas (HF22) |
| Ranuras máximas de contribuyentes | 11 (incluido el operador) |
| Contribución mínima por ranura | 10.000 XEQM |

### Economía del Nodo

Muchos proveedores de VPS en la nube ofrecen un nivel de servicio gratuito. Un VPS de pago a aproximadamente 5,28 USD por mes puede ejecutar 10 nodos de servicio, con un costo por nodo de aproximadamente 0,53 USD por mes. El alojamiento gestionado a través de Pecunia está disponible a 1,76 USD por nodo por mes.

| Precio | Bruto/mes | Neto: autoalojado ($0,53) | Neto: Pecunia ($1,76) | APY sobre participación de 200k |
|---|---|---|---|---|
| $0,01547 (hoy) | $0,008 | -$0,52 | -$1,75 | 3,1% |
| $0,05 | $0,026 | -$0,50 | -$1,73 | 3,1% |
| $0,10 | $0,052 | -$0,48 | -$1,71 | 3,1% |
| $0,25 | $0,129 | -$0,40 | -$1,63 | 3,1% |
| $0,50 | $0,258 | -$0,27 | -$1,50 | 3,1% |
| $1,00 | $0,516 | -$0,01 | -$1,24 | 3,1% |
| $2,00 | $1,032 | +$0,50 | -$0,73 | 3,1% |
| $5,00 | $2,580 | +$2,05 | +$0,82 | 3,1% |

---

## 5. Supervivencia de la Red y Vectores de Ataque

El protocolo aplica un tamaño máximo de dominio de fallo: ningún clúster de instalación, datacenter o enrutamiento puede alojar más del 30% de los nodos activos. Con 693 nodos, el 30% es aproximadamente 208 nodos.

**HF22, entrando a testnet:** Deduplicación de quórum por clave de cartera del operador y unificación del período de desbloqueo. Validado a través de nueve ciclos de stall/recuperación con tasa de recuperación del 100% y cero intervención.

**HF23, fase de diseño:** Límite de registro de clúster de proximidad, modificador de recompensa cero para nodos excedentes, y actualización de deduplicación de quórum de clave de cartera a clúster de proximidad. Todos dependen de la activación de Lokinet.

---

## 6. XEQM como Moneda de Utilidad

| Nivel | Participación Requerida | Llamadas Incluidas |
|---|---|---|
| Gratuito | Ninguna | 10.000 llamadas de testnet por mes |
| Constructor | 1.000 XEQM | 100.000 llamadas de mainnet por mes |
| Producción | 10.000 XEQM | 1.000.000 llamadas por mes, webhooks, soporte prioritario |
| Empresa | 50.000 XEQM | Llamadas ilimitadas, límites de tasa personalizados, SLA |

---

## 8. Resumen de Parámetros

| Parámetro | Valor |
|---|---|
| Mecanismo de consenso | 100% Prueba de Participación |
| Tiempo de bloque | 60 segundos |
| Recompensa de bloque | 8,25 XEQM por bloque |
| Emisiones de bloque diarias | 11.880 XEQM |
| Emisión de gobernanza | ~17.857 XEQM por día |
| Requisito de nodo completo | 200.000 XEQM |
| Participación mínima del operador | 100.000 XEQM (50%) |
| Tarifa máxima del operador | 10% |
| Tamaño del quórum | 12 asientos por ronda |
| Coeficiente de Nakamoto (julio 2026) | 7 (objetivo: 8) |
| Repositorios centrales | github.com/XEQMLabs |

---

## Idiomas Disponibles

| Idioma | Libro Blanco |
|---|---|
| English | [README.md](../../README.md) |
| Français | [../fr/README.md](../fr/README.md) |
| Deutsch | [../de/README.md](../de/README.md) |
| 中文 | [../zh/README.md](../zh/README.md) |
| Português | [../pt/README.md](../pt/README.md) |
| Türkçe | [../tr/README.md](../tr/README.md) |
| Polski | [../pl/README.md](../pl/README.md) |

---

*Este es un documento borrador. Los parámetros, cronogramas de emisión y fases del plan de trabajo descritos aquí son el diseño previsto.*

*Este documento no constituye asesoramiento financiero ni legal. XEQM es una moneda de utilidad para la plataforma EXIOM, no un producto de inversión. La clasificación de tokens, el estado de valores y las regulaciones aplicables varían según la jurisdicción. Los participantes deben consultar su marco legal y regulatorio local antes de adquirir u operar con XEQM. XEQM Labs no fomenta la compra de XEQM sobre la base de apreciación de precio especulativa.*
