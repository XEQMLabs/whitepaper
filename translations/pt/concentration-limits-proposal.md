# Limites de Concentração de Nós - Aplicação da Sobrevivência da Rede
## Documento Técnico Complementar ao Whitepaper de Tokenomia EXIOM
### 26/07/2026

> *Esta tradução foi produzida com ferramentas de tradução AI. Em caso de conflito, a versão em inglês prevalece: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

---

## O Que Isso Significa para Operadores de Nós

HF23 **não exige** um nó por IP, um nó por VPS ou um nó por carteira. O limite é 30% da rede ativa por cluster de proximidade, atualmente cerca de 208 nós. Um operador executando 10, 50 ou 100 nós em infraestrutura compartilhada não é afetado pelo HF23, desde que seu cluster permaneça abaixo desse limite.

O problema específico que o HF23 resolve: uma instalação na França atualmente hospeda cerca de 426 nós, 61% da rede. Se essa instalação ficar offline, a rede para.

---

## Dados de Concentração Atuais

| País | Nós ativos |
|---|---|
| França | 492 |
| Alemanha | 70 |
| Estados Unidos | 55 |
| Canadá | 18 |
| Polônia | 13 |
| Reino Unido | 10 |
| Turquia | 5 |
| Austrália | 4 |
| Singapura | 2 |
| Lituânia | 2 |
| Sérvia | 1 |

---

## Controles HF22 (Entrando no Testnet, Validado)

**Deduplicação de quórum por chave de carteira do operador.** No máximo um nó por endereço de carteira por rodada. Validado em nove ciclos com taxa de recuperação de 100%.

**Unificação do período de desbloqueio.** Período de desregistro forçado estendido de 7 para 14 dias.

---

## Controles HF23 (Fase de Design)

**Limite de registro de cluster.** Novos registros rejeitados quando um cluster excede 30% dos nós ativos.

**Modificador de recompensa zero.** Nós acima do limite do cluster ganham zero recompensas até migração.

**Regra de fallback do quórum.** Tamanho do quórum: 12 assentos. Se menos de 12 clusters distintos existirem, o algoritmo concede assentos adicionais começando pelos menores clusters.

---

*Para a especificação técnica completa, consulte a versão em inglês: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

*Este documento não constitui aconselhamento financeiro ou jurídico. Em caso de conflito, a versão em inglês prevalece.*
