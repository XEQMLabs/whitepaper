# Límites de Concentración de Nodos - Aplicación de la Supervivencia de la Red
## Documento Técnico Complementario al Libro Blanco de Tokenomía EXIOM
### 26/07/2026

> *Esta traducción fue producida con herramientas de traducción de inteligencia artificial. Se proporciona únicamente por conveniencia informativa. En caso de conflicto o ambigüedad, la versión en inglés prevalece: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

---

## Qué Significa Esto para los Operadores de Nodos

HF23 **no** requiere un nodo por IP, un nodo por VPS ni un nodo por cartera. El límite es el 30% de la red activa por clúster de proximidad, actualmente aproximadamente 208 nodos. Un operador que ejecute 10, 50 o incluso 100 nodos en infraestructura compartida no se ve afectado por HF23 siempre que su clúster permanezca por debajo de ese umbral.

El modificador de recompensa cero se aplica únicamente a los nodos por encima del umbral de 208 nodos dentro de un clúster sobreconcentrado, clasificados por antigüedad de registro. La deduplicación de quórum limita la influencia de consenso por ronda, no el recuento de nodos ni los ingresos.

El enfoque correcto para un nuevo operador es verificar el explorador de nodos, ver dónde están concentrados los clústeres existentes e implementar en una región escasamente poblada. Diez nodos en un servidor en Brasil o Argentina funcionan perfectamente bajo HF23 porque esas regiones están muy lejos del umbral del 30%.

El problema específico que HF23 resuelve es que una instalación en Francia aloja actualmente aproximadamente 426 nodos, el 61% de la red. Si esa instalación queda fuera de línea, la red se detiene.

---

## Datos de Concentración Actuales

| País | Nodos activos |
|---|---|
| Francia | 492 |
| Alemania | 70 |
| Estados Unidos | 55 |
| Canadá | 18 |
| Polonia | 13 |
| Reino Unido | 10 |
| Turquía | 5 |
| Australia | 4 |
| Singapur | 2 |
| Lituania | 2 |
| Serbia | 1 |

---

## Por Qué Los Hard Forks Están Separados

HF22 se lanza después de pruebas exitosas. La deduplicación de quórum por clave de cartera y la unificación del período de desbloqueo no tienen dependencia de Lokinet. HF23 se lanza después de que se complete la evaluación de ingeniería de Lokinet.

---

## Controles HF22 (Entrando a Testnet, Validado)

**Deduplicación de quórum por clave de cartera del operador.** Como máximo un nodo por dirección de cartera del operador puede ocupar un asiento de validador por ronda. Validado en nueve ciclos de stall/recuperación con tasa de recuperación del 100% y cero intervención.

**Unificación del período de desbloqueo.** El período de desbloqueo por desregistro forzado se extiende de 7 días a 14 días, igualando el retiro voluntario.

---

## Controles HF23 (Fase de Diseño, Pendiente de Evaluación de Lokinet)

Una vez que Lokinet esté activo como transporte de red, el protocolo utilizará la proximidad de enrutamiento de Lokinet para determinar la agrupación física de nodos.

**Límite de registro de clúster.** Los nuevos registros de nodos rechazados cuando un clúster excede el 30% de los nodos activos.

**Modificador de recompensa cero.** Los nodos por encima del umbral del clúster ganan cero recompensas de bloque hasta que sean migrados. Los nodos más antiguos están protegidos hasta el umbral.

**Período de gracia.** 30 días de recompensas completas en la activación de HF23 antes de que el modificador entre en vigor.

**Regla de fallback de quórum.** El tamaño del quórum es de 12 asientos. Si hay menos de 12 clústeres distintos disponibles, el algoritmo permite asientos adicionales comenzando por los clústeres más pequeños primero, asegurando que la formación del quórum siempre sea posible.

---

*Para la especificación técnica completa, consulte la versión en inglés: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

*Este documento no constituye asesoramiento financiero ni legal. En caso de conflicto, la versión en inglés prevalece.*
