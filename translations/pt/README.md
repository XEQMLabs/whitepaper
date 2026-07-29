# XEQM Labs - Plataforma EXIOM
## Whitepaper de Tokenomia
### Rascunho v11 | 26/07/2026

> *Esta tradução foi produzida com ferramentas de tradução de inteligência artificial. É fornecida apenas para conveniência informativa. Em caso de conflito ou ambiguidade entre esta tradução e o original em inglês, a versão em inglês prevalece. A versão em inglês está em [github.com/XEQMLabs/whitepaper](https://github.com/XEQMLabs/whitepaper).*

---

## O Que Está Ativo Hoje vs. O Que Está Planejado

| Componente | Status |
|---|---|
| EXIOM mainnet | Ativo, operacional desde 6 de maio de 2026 |
| Rede de nós de serviço | Ativo, 693 nós ativos, 184 operadores (julho de 2026) |
| Lokinet (LLARP) | Presente no código-fonte, status de ativação em avaliação de engenharia |
| Troca de moedas XEQ para XEQM | Entregue e encerrado, execução de produção de 35 dias, livro-razão auditável público |
| Carteira GUI | Ativo, github.com/XEQMLabs/XEQMLabs-GUI |
| Explorador de nós | Ativo, monitoramento ativo de nós de serviço |
| API de desenvolvedor EXIOM | Em desenvolvimento, Fase 2 (ATIVO) |
| Oráculo de privacidade EXIOM | Projetado, pré-implementação, Fase 3 |
| Plataforma de trading RFQ EXIOM | Em desenvolvimento, Fase 2/3, primeiro par XEQM/BTC |
| HF22, deduplicação de quórum e unificação de desbloqueio | Entrando no testnet, validado, sem dependência de Lokinet |
| HF23, limite de cluster de proximidade, modificador de recompensa, transporte Lokinet | Fase de design, aguardando avaliação de engenharia Lokinet |
| Governança formal on-chain | Planejado, Fase 6 |

---

## 1. O Que É a XEQM Labs

A XEQM Labs é uma empresa de tecnologia de privacidade. Seu produto principal, EXIOM, é uma rede Layer 1 de Prova de Participação que preserva a privacidade e uma plataforma comercial para desenvolvedores operada por um conjunto global de nós de serviço. XEQM é a moeda de acesso e uso da plataforma.

O projeto carrega uma comunidade e histórico operacional de mais de sete anos. A mainnet EXIOM foi construída para dar a essa comunidade uma rede com oferta verificável, cronograma de emissão previsível e consenso puro de Prova de Participação sem componente de Prova de Trabalho.

XEQM é uma moeda nativa Layer 1, não tokenizada em nenhuma outra rede, não é um ERC-20 ou ativo embrulhado, e não tem bridge. Os detentores interagem diretamente com a mainnet EXIOM.

### A Família de Produtos EXIOM

**Rede de Nós de Serviço EXIOM.** Ativo na mainnet. 693 nós ativos em 184 operadores independentes em julho de 2026.

**Troca de Moedas EXIOM.** Um produto comercial que permite aos projetos migrar sua comunidade de detentores de uma rede legada para uma nova rede com total auditabilidade criptográfica. O piloto foi a migração de detentores de XEQ para XEQM, executada por 35 dias com cada envio processado através de um livro-razão verificado criptograficamente com impressão digital SHA256 pública.

**API de Desenvolvedor Privado EXIOM.** Em desenvolvimento. Uma plataforma de desenvolvedor que expõe as capacidades de privacidade da rede através de uma API estruturada. Fase 2, ativo.

**Oráculo de Privacidade EXIOM.** Projetado, pré-implementação. Um oráculo focado em privacidade que prova fatos sobre dados web privados sem expor a fonte subjacente. Fase 3.

**Plataforma de Trading RFQ EXIOM.** Em desenvolvimento. Uma plataforma de trading OTC peer-to-peer com atestações de liquidação criptográfica. O primeiro par de trading é XEQM/BTC. Fase 2/3.

A XEQM Labs não incentiva a compra de XEQM com base em apreciação especulativa de preço.

---

## 2. Proveniência da Oferta

A migração está completa. 276.917.604 XEQM foram emitidos na mainnet EXIOM em troca de ativos legados. Esse valor é a oferta inicial verificada no lançamento da mainnet em 6 de maio de 2026. Cada depósito legado foi registrado em um livro-razão público com impressão digital SHA256. As chaves de gasto de cada carteira envolvida na troca foram publicadas.

**Sem emissões discricionárias.** O protocolo não permite emissão ad-hoc ou cunhagens fora do cronograma.

**Sem queimas.** A arquitetura criptográfica desta rede não suporta queimas demonstráveis. Não representaremos nenhuma carteira como endereço de queima.

---

## 3. Modelo de Tokenomia

A rede produz um novo bloco a cada 60 segundos e concede 8,25 XEQM ao nó de serviço selecionado, gerando 11.880 XEQM por dia. Com 700 nós ativos, cada nó ganha aproximadamente 17,0 XEQM por dia, ou 516 XEQM por mês.

O tesouro recebe aproximadamente 17.857 XEQM por dia. Este é o orçamento operacional para a equipe ativa de desenvolvimento de software comercial durante a fase pré-receita.

### Alocação de Emissões

| Alocação | Participação | Propósito |
|---|---|---|
| Recompensas de Nós de Serviço | 40% | Recompensas de bloco pagas diretamente aos nós |
| Desenvolvimento do Protocolo Central | 25% | Blockchain, plataforma EXIOM e serviços de rede |
| Marketing e Conscientização | 15% | Visibilidade da rede e adoção |
| Ecossistema e Comunidade | 10% | Subsídios, recompensas, prêmios comunitários |
| Segurança e Auditorias | 5% | Auditorias e revisões de segurança |
| Reserva de Longo Prazo | 5% | Estabilidade e necessidades de emergência |

### Distribuição de Taxas da Plataforma EXIOM

| Destinatário | Participação |
|---|---|
| Operadores de Nós API | 35% |
| Tesouro XEQM Labs | 35% |
| Governança Comunitária | 30% |

---

## 4. Estrutura do Nó de Serviço

| Parâmetro | Valor |
|---|---|
| Requisito de nó completo | 200.000 XEQM |
| Participação mínima do operador | 100.000 XEQM (50%) |
| Taxa máxima do operador | 10% |
| Período de desbloqueio, retirada voluntária | 14 dias, recompensas continuam |
| Período de desbloqueio, desregistro forçado | 14 dias, sem recompensas (HF22) |
| Slots máximos de contribuidores | 11 (incluindo operador) |
| Contribuição mínima por slot | 10.000 XEQM |

### Economia do Nó

Um VPS pago por aproximadamente 5,28 USD por mês pode executar 10 nós de serviço, trazendo o custo por nó para aproximadamente 0,53 USD por mês. Hospedagem gerenciada via Pecunia disponível por 1,76 USD por nó por mês.

| Preço | Bruto/mês | Líquido: auto-hospedado ($0,53) | Líquido: Pecunia ($1,76) | APY sobre participação 200k |
|---|---|---|---|---|
| $0,01547 (hoje) | $0,008 | -$0,52 | -$1,75 | 3,1% |
| $0,05 | $0,026 | -$0,50 | -$1,73 | 3,1% |
| $0,10 | $0,052 | -$0,48 | -$1,71 | 3,1% |
| $0,25 | $0,129 | -$0,40 | -$1,63 | 3,1% |
| $0,50 | $0,258 | -$0,27 | -$1,50 | 3,1% |
| $1,00 | $0,516 | -$0,01 | -$1,24 | 3,1% |
| $2,00 | $1,032 | +$0,50 | -$0,73 | 3,1% |
| $5,00 | $2,580 | +$2,05 | +$0,82 | 3,1% |

---

## 6. XEQM como Moeda Utilitária

| Nível | Participação Necessária | Chamadas Incluídas |
|---|---|---|
| Gratuito | Nenhuma | 10.000 chamadas testnet por mês |
| Builder | 1.000 XEQM | 100.000 chamadas mainnet por mês |
| Produção | 10.000 XEQM | 1.000.000 chamadas por mês, webhooks, suporte prioritário |
| Enterprise | 50.000 XEQM | Chamadas ilimitadas, limites de taxa personalizados, SLA |

---

## 8. Resumo de Parâmetros

| Parâmetro | Valor |
|---|---|
| Mecanismo de consenso | 100% Prova de Participação |
| Tempo de bloco | 60 segundos |
| Recompensa de bloco | 8,25 XEQM por bloco |
| Emissões de bloco diárias | 11.880 XEQM |
| Emissão de governança | ~17.857 XEQM por dia |
| Requisito de nó completo | 200.000 XEQM |
| Tamanho do quórum | 12 assentos por rodada |
| Coeficiente de Nakamoto (julho 2026) | 7 (objetivo: 8) |
| Repositórios centrais | github.com/XEQMLabs |

---

## Idiomas Disponíveis

| Idioma | Whitepaper |
|---|---|
| English | [README.md](../../README.md) |
| Español | [../es/README.md](../es/README.md) |
| Français | [../fr/README.md](../fr/README.md) |
| Deutsch | [../de/README.md](../de/README.md) |
| 中文 | [../zh/README.md](../zh/README.md) |
| Türkçe | [../tr/README.md](../tr/README.md) |
| Polski | [../pl/README.md](../pl/README.md) |
| Bahasa Indonesia | [../id/README.md](../id/README.md) |

---

*Este é um documento rascunho. Os parâmetros, cronogramas de emissão e fases do roteiro aqui descritos são o design pretendido.*

*Este documento não constitui aconselhamento financeiro ou jurídico. XEQM é uma moeda utilitária para a plataforma EXIOM, não um produto de investimento. A classificação de tokens, o status de valores mobiliários e os regulamentos aplicáveis variam por jurisdição. Os participantes devem consultar seu arcabouço jurídico e regulatório local antes de adquirir ou operar com XEQM. A XEQM Labs não incentiva a compra de XEQM com base em apreciação especulativa de preço.*
