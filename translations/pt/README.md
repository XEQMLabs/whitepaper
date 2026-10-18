# XEQM Labs - Plataforma EXIOM
## Whitepaper de Tokenomics
### Rascunho v12 | 09/27/2026

---

## O Que Está Ativo Hoje vs. O Que Está Planejado

| Componente | Status |
|---|---|
| Mainnet EXIOM | Ativa, operacional desde 6 de maio de 2026 |
| Rede de service nodes | Ativa — 943 service nodes ativos em 27 de setembro de 2026 |
| Lokinet (LLARP) | Lançado em uma versão não impositiva antes do HF23 (transporte ativo, clustering por proximidade observável); o HF23 ativa a imposição. A implementação começa no Q4 de 2026 |
| Armazenamento light-node em SQLite | Em desenvolvimento; lançado com a versão do Lokinet pré-HF23, para menor uso de memória e disco dos nós, com light nodes de janela recente opcionais |
| Troca de moeda XEQ para XEQM | Entregue e encerrada, execução em produção de 35 dias, livro-razão público auditável |
| Carteira GUI | Ativa, github.com/XEQMLabs/XEQMLabs-GUI |
| Explorador de nós | Ativo, monitoramento ativo de service nodes |
| EXIOM Oracle | Ativo na mainnet (Robinhood Chain, chainId 4663); comitê de operadores de 12 membros em 28 de setembro de 2026 |
| API para desenvolvedores EXIOM | Ativa em beta — chaves self-serve, declarações de conformidade assinadas e um motor de verificação, OpenAPI em /docs; grátis para desenvolver com uso pré-pago por chamada em implantação (27 de setembro de 2026) |
| EXIOM Privacy Oracle (TLSNotary / ZK) | Fundamentos ativos (motor de verificação, sessões de oracle); oracle completo de dados privados da web na Fase 3 |
| Plataforma de trading RFQ EXIOM | Em desenvolvimento, Fase 2/3, par XEQM/BTC primeiro |
| HF22, dedup de quórum por chave de carteira, unificação de unbonding, recuperação de travamento do Pulse | Ativado no bloco 219120 da mainnet. A revisão de recuperação de travamento do Pulse (snode_revision 1, fallback baseado em assinatura) foi ativada no bloco 236920 em 18 de outubro de 2026 |
| HF23, limite de cluster por proximidade e modificador de recompensa (imposição) | Em projeto; ativa os limites de concentração assim que a versão não impositiva do Lokinet + light-node tiver amadurecido; previsto para o Q4 de 2026 |
| Governança formal on-chain | Planejada, Fase 6 |

---

## 1. O Que É a XEQM Labs

A XEQM Labs é uma empresa de tecnologia de privacidade. Seu produto principal, o EXIOM, é uma rede Layer 1 Proof-of-Stake preservadora de privacidade e uma plataforma comercial para desenvolvedores operada por um conjunto global de service nodes. XEQM é a moeda de acesso e uso da plataforma. Os desenvolvedores constroem gratuitamente e pagam pelo uso em produção em XEQM, consumido à medida que chamam a API. Os operadores de service node ganham XEQM por protegerem a rede, e os mesmos operadores podem ganhar receita adicional executando um sidecar de oracle que serve os produtos de oracle da plataforma.

O projeto traz consigo uma história comunitária e operacional que remonta a mais de sete anos. A mainnet EXIOM foi construída para dar a essa comunidade uma rede com oferta verificável, um cronograma de emissão previsível, consenso Proof-of-Stake puro sem nenhum componente de Proof-of-Work, e mecânicas de service node que respeitam o tempo e o capital do operador.

XEQM é uma moeda Layer 1 nativa, não tokenizada em nenhuma outra chain, não é um ERC-20 nem um ativo wrapped, e não é bridgeada. Os detentores interagem diretamente com a mainnet EXIOM.

### A Família de Produtos EXIOM

**Rede de Service Nodes EXIOM.** Ativa na mainnet. Um conjunto global de service nodes protege a chain, ganha recompensas de bloco e forma a camada de infraestrutura sobre a qual todos os outros produtos EXIOM são executados. 943 service nodes ativos em 27 de setembro de 2026.

**Troca de Moeda EXIOM.** Um produto comercial que permite a projetos migrar sua comunidade de detentores de uma chain legada para uma nova chain com total auditabilidade criptográfica. O piloto foi a migração de detentores de XEQ para XEQM na mainnet EXIOM, executada por 35 dias, com cada submissão processada por meio de um livro-razão criptograficamente verificado portando uma impressão digital SHA256 pública. O produto está disponível para outros projetos que exijam uma migração de chain verificável.

**EXIOM Oracle.** Ativo na mainnet. O primeiro produto de oracle da plataforma: um comitê de operadores de service node XEQM — cada um executando um sidecar de oracle leve — que produz atestações de conformidade BLS-agregadas e assinadas em EIP-712 (por exemplo, que um endereço é elegível para uma determinada jurisdição) que as aplicações consomem através da API para desenvolvedores. Está implantado na Robinhood Chain (chainId 4663) e opera um comitê de operadores de 12 membros em 28 de setembro de 2026. Executar o sidecar é como um operador de service node ganha receita adicional baseada em uso, além das recompensas de bloco.

**API para Desenvolvedores EXIOM.** Ativa em beta. Uma API estruturada que expõe as capacidades de conformidade e verificação da plataforma — declarações de conformidade assinadas e um motor de verificação (mecanismos de signed-claims, TLSNotary e zero-knowledge) — com acesso self-serve (um DID mais chave de API), uma especificação OpenAPI 3.1, webhooks e requisições idempotentes. Os desenvolvedores constroem gratuitamente com uma generosa franquia mensal e pagam pelo uso em produção em XEQM, consumido por chamada. Fase 2, ativa.

**EXIOM Privacy Oracle.** Projetado, fundamentos no lugar. A evolução mais ampla do oracle: provar fatos sobre dados privados da web (via TLSNotary e técnicas de zero-knowledge) sem expor a fonte subjacente. O motor de verificação e os endpoints de sessão de oracle que o sustentam já estão ativos; o oracle completo de dados privados da web é um entregável da Fase 3. Tanto a plataforma RFQ EXIOM quanto aplicações de terceiros podem consumir as saídas do oracle.

**Plataforma de Trading RFQ EXIOM.** Em desenvolvimento. Uma plataforma de trading peer-to-peer de balcão (over-the-counter) com atestações de liquidação criptográficas, construída sobre a API EXIOM. O primeiro par de trading é XEQM/BTC, ambos ativos Layer 1 nativos, sem tokenização, sem wrapping e sem risco de bridge. O oracle fornece atestações de preço privadas para a camada de precificação. Fase 2/3.

A XEQM Labs opera o EXIOM como uma plataforma de software comercial. O objetivo é uma receita de plataforma sustentável que reduza, ao longo do tempo, a dependência das emissões de governança. A XEQM Labs não incentiva a compra de XEQM com base em valorização especulativa de preço.

---

## 2. Proveniência da Oferta

A migração está completa. 276,917,604 XEQM foram emitidos na mainnet EXIOM em troca de participações legadas. Esse número é a oferta inicial verificada no lançamento da mainnet em 6 de maio de 2026. Cada depósito legado foi registrado em um livro-razão público com uma impressão digital SHA256. A nova chain foi cunhada uma única vez na conclusão da troca para corresponder exatamente a esse total verificado. As spend keys de cada carteira envolvida na troca foram publicadas, e qualquer pessoa pode verificar o histórico completo de transações, do depósito ao pagamento.

Além da oferta inicial, novo XEQM entra em circulação por meio de dois fluxos de emissão a nível de protocolo: recompensas de bloco dos service nodes e emissões de governança. Ambos operam em cronogramas fixos e previsíveis escritos no protocolo, que qualquer pessoa pode computar a partir de parâmetros públicos. As taxas e os detalhes operacionais estão na Seção 3. A oferta total cresce ao longo do tempo. XEQM é uma chain de oferta não limitada, no mesmo modelo da tail emission do Monero. A disciplina de oferta fixa com a qual o projeto se compromete refere-se à ausência de emissão discricionária, não a um teto rígido para as emissões impulsionadas pelo protocolo.

**Nenhuma cunhagem discricionária.** O protocolo não permite emissão ad-hoc, ajustes manuais de oferta ou cunhagens fora do cronograma. Cada novo XEQM que entra em circulação o faz por meio dos dois fluxos de emissão programados acima.

**Nenhuma queima.** A arquitetura criptográfica sobre a qual esta rede é construída não suporta queimas comprováveis da forma como esse termo costuma ser usado. Qualquer endereço para o qual uma moeda é enviada é apenas tão inutilizável quanto a chave for comprovadamente destruída. Não representaremos nenhuma carteira como um endereço de queima. Moedas não trocadas durante a janela de migração permanecem na chain legada inativa e não fazem parte da oferta de XEQM.

---

## 3. Modelo de Tokenomics

### Emissões de Bloco

A rede produz um novo bloco a cada 60 segundos e concede 8.25 XEQM ao service node selecionado, gerando 11,880 XEQM por dia. Com 943 nós ativos (27 de setembro de 2026), cada nó ganha aproximadamente 12.6 XEQM por dia, ou cerca de 380 XEQM por mês.

A partir do HF21, as recompensas de bloco são distribuídas em um cronograma de batching semanal. Antes do HF21, as recompensas eram emitidas a cada 20 blocos. As recompensas agora se acumulam ao longo de cada janela de 10,080 blocos (aproximadamente 7 dias) e são pagas ao final de cada janela. A taxa total de emissão permanece inalterada; apenas a cadência de pagamento mudou.

### Emissão de Governança

A tesouraria recebe aproximadamente 17,857 XEQM por dia, ou cerca de 124,999 XEQM por semana. Este é o orçamento operacional de uma equipe ativa de desenvolvimento de software comercial. Engenheiros, revisores de segurança, operadores de infraestrutura e colaboradores do ecossistema são remunerados a partir dessa emissão enquanto a plataforma está pré-receita. À medida que cada produto EXIOM atinge o status de geração de receita, a emissão de governança é revisada e reduzida de acordo. O objetivo de longo prazo é que a receita da plataforma substitua a emissão de governança como o principal mecanismo de financiamento.

### Alocação de Emissão

| Alocação | Participação | Finalidade |
|---|---|---|
| Recompensas de Service Node | 40% | Recompensas de bloco pagas diretamente aos service nodes |
| Desenvolvimento do Protocolo Central | 25% | Blockchain, plataforma EXIOM e serviços centrais da rede |
| Marketing e Divulgação | 15% | Visibilidade e adoção da rede |
| Ecossistema e Comunidade | 10% | Grants, bounties, recompensas comunitárias, suporte à integração |
| Segurança e Auditorias | 5% | Auditorias, revisões de segurança, testes de confiabilidade |
| Reserva de Longo Prazo | 5% | Estabilidade, necessidades emergenciais, operações de longo prazo |

### Receita e Distribuição da Plataforma EXIOM

Além das recompensas de bloco, a plataforma gera receita a partir do uso pelos desenvolvedores. O acesso é pré-pago: um desenvolvedor financia sua conta depositando XEQM (não reembolsável), e esse saldo é consumido à medida que utiliza a API de produção, precificada por chamada. Desenvolvimento e avaliação na franquia gratuita não são cobrados.

O XEQM consumido é reconhecido como receita da plataforma e distribuído entre os operadores que servem o oracle e as operações da plataforma:

| Destinatário | Participação | Finalidade |
|---|---|---|
| Operadores de sidecar de oracle | 70% | Operadores de service node que executam o sidecar de oracle, recompensados na proporção das obrigações de oracle que ajudam a servir |
| Operações e desenvolvimento da plataforma | 30% | Financia operações e desenvolvimento contínuos, reduzindo ao longo do tempo a dependência da emissão de governança |

Os operadores recebem a maioria porque executam a infraestrutura que serve o oracle. A proporção 70/30 é o valor inicial e é ajustável por governança. A receita é reconhecida e distribuída na mesma cadência semanal das recompensas de bloco — cada janela de 10,080 blocos (aproximadamente 7 dias), alinhada ao batching de recompensas do HF21 — de modo que um operador recebe as recompensas de bloco e a participação na receita de uso em um único ritmo. Essa participação na receita é o mecanismo pelo qual a recompensa de sidecar do operador descrita na Seção 4 é financiada por uso real em vez de por emissão.

Hardware de referência para executar um service node (e seu sidecar de oracle): 4 núcleos de CPU, 8 GB de RAM, 100 GB de SSD, conexão de 100 Mbps. Cargas de trabalho mais pesadas do privacy-oracle exigem especificações mais altas, abordadas na Seção 10.

---

## 4. Estrutura do Service Node

### Parâmetros de Staking

| Parâmetro | Valor |
|---|---|
| Requisito de nó completo | 200,000 XEQM |
| Stake mínimo do operador | 100,000 XEQM (50% do requisito completo) |
| Taxa máxima do operador | 10% |
| Período de unbonding, retirada voluntária | 14 dias, recompensas continuam |
| Período de unbonding, desregistro forçado | 14 dias, sem recompensas (unificado no HF22) |
| Máximo de slots de contribuidores | 11 (incluindo o operador) |
| Contribuição comunitária mínima por slot | 10,000 XEQM |
| Janela de staker comunitário por nó | Até 100,000 XEQM em até 10 slots de contribuidores |

### Economia do Nó

Muitos provedores de VPS em nuvem oferecem um nível de serviço gratuito que pode suportar a operação de um service node a custo mensal zero. Um VPS pago a aproximadamente $5.28 por mês pode executar 10 service nodes, levando o custo de hospedagem por nó a cerca de $0.53 por mês. Hospedagem gerenciada através da Pecunia está disponível a $1.76 por nó por mês.

As recompensas de bloco por nó escalam inversamente com a contagem de nós ativos: com 943 service nodes ativos (27 de setembro de 2026), a emissão diária de 11,880 XEQM da rede resulta em aproximadamente 12.6 XEQM por nó por dia, cerca de 380 XEQM por mês. Como tanto a recompensa quanto o stake são denominados em XEQM, o APY das recompensas de bloco é de aproximadamente 2.3% independentemente do preço; a hospedagem é o único custo recorrente material, a cerca de $0.53 por nó por mês auto-hospedado ou $1.76 através da Pecunia. Executar o sidecar de oracle (Seção 10) adiciona um segundo fluxo de renda baseado em receita que escala com o uso real da plataforma, financiado pelo consumo dos desenvolvedores em vez de por emissão.

### Economia do Contribuidor

Operadores que não podem ou optam por não executar infraestrutura podem contribuir com stake para um nó existente em até 10 slots de contribuidores. O operador pode cobrar de 0% a 10% da recompensa de bloco antes de o restante ser dividido proporcionalmente entre os contribuidores. Os contribuidores não têm custo de hospedagem, portanto, em todo ponto de preço, o rendimento líquido de um contribuidor supera o de um operador auto-hospedado ou hospedado pela Pecunia.

### Ciclo de Vida do Nó

Os nós permanecem ativos indefinidamente com a manutenção do colateral e dos requisitos de desempenho. Um nó que fica fora de conformidade pode ser remediado sem penalidade. Se não for remediado, o desregistro forçado dispara um período de unbonding de 14 dias sem recompensas. A saída voluntária acarreta um período de unbonding de 14 dias com as recompensas continuando durante todo o período.

---

## 5. Sobrevivência da Rede e Vetores de Ataque

### Requisito de Sobrevivência

A rede EXIOM assume compromissos de confiabilidade com os desenvolvedores. Uma rede que pode ser colocada offline por uma única falha de datacenter não pode assumir esses compromissos. O protocolo impõe um tamanho máximo de domínio de falha: nenhuma instalação física, datacenter ou cluster de roteamento único pode hospedar mais de 30% dos nós ativos.

Com 943 nós (27 de setembro de 2026), 30% é aproximadamente 283 nós. Perder qualquer instalação única pode colocar no máximo 283 nós offline simultaneamente, deixando pelo menos 660 nós operacionais, suficientes para manter a produção de blocos e a formação de quórum sem descomissionamentos em cascata. Este é um requisito de engenharia, não uma preferência de descentralização.

### Dois Hard Forks

A imposição da sobrevivência é entregue em dois estágios, separados para reduzir risco e lançar imediatamente trabalho validado.

**HF22, ativado:** Deduplicação de quórum por chave de carteira do operador e unificação do período de unbonding, mais uma revisão de recuperação de travamento do Pulse (snode_revision 1) que substitui o fallback de recuperação Proof-of-Work anterior por um baseado em assinatura. Sem dependência do Lokinet. Validado por meio de 20 ciclos de travamento/recuperação com uma taxa de recuperação de 100%, zero intervenção, e um pior intervalo de bloco de 83 segundos. O HF22 foi ativado no bloco 219120 da mainnet; a revisão de recuperação de travamento foi ativada no bloco 236920 em 18 de outubro de 2026.

**HF23, em projeto, previsto para o Q4 de 2026:** Limite de registro de cluster por proximidade, modificador de recompensa zero para nós em excesso, e atualização da deduplicação de quórum de chave de carteira para cluster de proximidade. Todos os três dependem do grafo de roteamento do Lokinet como sinal de proximidade. Para evitar tornar um novo transporte crítico para o consenso no momento em que é introduzido, o Lokinet é lançado primeiro em uma versão separada não impositiva (junto com a mudança de armazenamento light-node em SQLite), onde o clustering por proximidade está ativo e observável, mas não tem consequências de recompensa. O HF23 então ativa a imposição, depois que essa versão tiver amadurecido e a contagem real de clusters tiver sido medida e o limite e o fallback tiverem sido ajustados.

### Controles do HF22

**Deduplicação de quórum por chave de carteira do operador.** No máximo um nó por endereço de carteira do operador pode ocupar um assento de validador em qualquer rodada do Pulse, sessão de oracle ou quórum de obrigações. Se um sorteio aleatório selecionar dois nós do mesmo endereço de operador, o segundo é substituído por um nó de um operador diferente. As recompensas de bloco não são afetadas; elas são atribuídas por ordenação de tempo de espera, independentemente da participação no quórum.

Limitação conhecida: contornada pela divisão de carteiras. Um operador usando múltiplos endereços de carteira apresenta múltiplas chaves de operador ao protocolo. O HF23 fecha essa lacuna por meio da deduplicação por cluster de proximidade.

**Unificação do período de unbonding.** O unbonding do desregistro forçado foi estendido de 7 dias para 14 dias, igualando a retirada voluntária. Ambos os casos agora são de 14 dias.

### Controles do HF23

Uma vez que o Lokinet esteja ativo como transporte da rede, nós que estão fisicamente co-localizados mostrarão assinaturas de roteamento características: latência mútua sub-milissegundo e alta sobreposição de caminhos pelo grafo de roteamento do Lokinet. Nós em instalações genuinamente diferentes mostrarão latência mais alta e menor sobreposição de caminhos. Esse sinal de clustering é derivado do comportamento observável da rede, sem exigir que os operadores divulguem seu provedor ou localização.

**Limite de registro de cluster.** Novos registros de nó são avaliados contra a proximidade de roteamento do Lokinet em relação aos clusters existentes. Se o cluster-alvo já contém 30% ou mais dos nós ativos, o registro é rejeitado pelo protocolo.

**Modificador de recompensa zero.** Nós acima do limite de cap do cluster ganham zero recompensas de bloco até serem migrados para um cluster não concentrado. Os nós são classificados dentro de cada cluster pela idade de registro; os nós mais antigos até o limite de cap ganham recompensas completas. Todo nó acima desse limite ganha zero. Uma taxa reduzida pode ser racionalizada frente aos custos de VPS; zero não pode.

Um período de carência de 30 dias se aplica na ativação do HF23. Todos os nós ganham recompensas completas durante o período de carência. No vencimento, o modificador de recompensa zero é ativado nos nós em excesso.

**Deduplicação de quórum por cluster de proximidade.** Atualiza a dedup por chave de carteira do HF22 para dedup por cluster de proximidade. No máximo um nó por cluster de proximidade por rodada, independentemente da estrutura de carteiras. Fecha a lacuna da divisão de carteiras.

O tamanho do quórum é de 12 assentos por rodada. A dedup, portanto, requer pelo menos 12 clusters de proximidade distintos para funcionar sem um fallback. Dada a topologia atual da rede, a contagem de clusters na ativação do HF23 pode estar próxima desse mínimo. O algoritmo implementa um fallback obrigatório: se todos os clusters distintos se esgotarem antes de os 12 assentos serem preenchidos, assentos adicionais são alocados começando pelos clusters menores (menos concentrados) primeiro, antes de o cluster mais concentrado receber um segundo assento. A frequência de fallback é registrada e publicada no explorador de nós como um indicador em tempo real de risco de concentração. Uma rede que nunca aciona o fallback atingiu diversidade física adequada.

### Controles Adicionais

**Barreira de custo de capital.** O stake mínimo de 100,000 XEQM do operador garante que todo operador comprometa capital real em cada nó. Executar N nós requer pelo menos N x 100,000 XEQM em stake.

**Proteção contra captura de taxa do operador.** O EXIOM não está sujeito ao ataque de captura de taxa do operador presente em algumas redes de service node, em que um operador registra um nó com capital mínimo e define uma taxa de 100% para capturar toda a recompensa de bloco independentemente do stake dos contribuidores. A taxa máxima é limitada a 10% e o stake mínimo de 50% do operador torna isso economicamente irracional.

**Análise de temporização de provas de uptime.** Nós no mesmo host físico submetem provas de uptime em clusters estreitamente correlacionados, detectáveis a partir dos dados de recibo de prova existentes sem alterações no daemon.

**Análise de ASN.** Nós por trás do mesmo Autonomous System Number compartilham infraestrutura de nível de provedor e exposição legal. A concentração de ASN contribui para a atribuição de cluster e a revisão de governança.

**Lista de bloqueio de governança.** Uma lista de bloqueio de chaves públicas gerenciada por governança impede que chaves de registro bloqueadas registrem novos nós.

**Meta de coeficiente de Nakamoto.** A rede tem como meta um coeficiente de operador de pelo menos 8. Em 27 de setembro de 2026, entre 943 service nodes ativos e 204 operadores, o coeficiente de Nakamoto de operador — o número mínimo de operadores que controlam a maioria dos nós ativos — é 9, atingindo a meta (acima de 7 entre 184 operadores em julho de 2026). A concentração de instalações físicas é um problema separado e mais agudo: uma única região de datacenter ainda hospeda a maioria dos nós, que é exatamente a concentração que o limite de cluster por proximidade do HF23 foi projetado para quebrar.

A proposta completa de limites de concentração está em [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). A metodologia de resistência a sybil está em [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Lokinet Como o Transporte Futuro da Rede

A infraestrutura de endereçamento da rede EXIOM migrará de endereços IP anunciados publicamente para endereçamento Lokinet. O Lokinet é lançado primeiro em uma versão não impositiva antes do HF23 (previsto para o Q4 de 2026); o HF23 então adiciona a imposição de concentração que usa o grafo de roteamento do Lokinet. O Lokinet (Low Latency Anonymous Routing Protocol, LLARP) é um protocolo de roteamento onion de camada 3 que roteia qualquer tráfego baseado em IP por meio de múltiplos service nodes via roteamento onion multi-hop, sem que nenhum nó único no caminho conheça tanto a origem quanto o destino.

Uma vez que o Lokinet esteja ativo:

- Os service nodes serão endereçados por seu identificador criptográfico Lokinet em vez de um endereço IP anunciado publicamente
- A API para desenvolvedores EXIOM será acessível como um serviço oculto em um endereço `.loki`, ocultando o IP de origem do desenvolvedor do nó da API
- A plataforma de trading RFQ será acessível como um serviço oculto, ocultando os endereços IP do solicitante e do LP da plataforma
- A comunicação da sessão de oracle entre o prover e o quórum de verificadores será roteada pelo Lokinet, eliminando a premissa de confiança no coordenador centralizado

O Lokinet é lançado em uma versão não impositiva antes do HF23, prevista para o Q4 de 2026, com o HF23 seguindo assim que tiver amadurecido. A base de código LLARP está presente no repositório EXIOM; a implementação do Lokinet como transporte principal da rede começa no Q4 de 2026.

---

## 6. XEQM Como Moeda de Utilidade

A demanda por XEQM vem de três fontes. O staking de nós bloqueia a maior parte da oferta, aproximadamente 68% nos atuais 943 nós ativos (27 de setembro de 2026). O consumo pelos desenvolvedores cria uma camada contínua de velocidade: as aplicações pagam pelo uso da API de produção em XEQM, de modo que a adoção da plataforma se converte diretamente em demanda recorrente pela moeda. O acesso ao oracle adiciona uma terceira camada para consumidores de maior volume.

O acesso segue um modelo pré-pago baseado em uso em vez de um gate de stake-to-unlock — os desenvolvedores não precisam adquirir e bloquear um stake fixo para construir:

| Nível | Modelo de acesso |
|---|---|
| Grátis | Construa e avalie sem custo: uma generosa franquia mensal de chamadas, sem depósito exigido |
| Produção | Uso pré-pago: deposite XEQM e pague por chamada; webhooks e limites mais altos |
| Enterprise | Limites personalizados, SLA e suporte; termos por volume |

O uso em produção é medido por chamada de API e debitado do saldo pré-pago de XEQM do desenvolvedor. Os depósitos são não reembolsáveis e são reconhecidos como receita da plataforma à medida que são consumidos (ver Seção 3). Um projeto anterior condicionava os níveis a um stake fixo de XEQM; isso foi substituído por este modelo pré-pago, que é mais simples para os desenvolvedores e padrão para APIs comerciais.

---

## 7. Governança e Tesouraria

O endereço da carteira de governança e a view key são publicados. Qualquer pessoa pode verificar o saldo a qualquer momento. A governança atualmente opera por meio da equipe fundadora, com participação da comunidade por meio de canais abertos no Telegram e discussões no GitHub.

Alocações da tesouraria, provenientes da emissão de governança descrita na Seção 3:

- Desenvolvimento central (25%): engenharia para a API EXIOM, o oracle e a plataforma RFQ
- Marketing e divulgação (15%): listagens em exchanges, conteúdo, crescimento da comunidade
- Ecossistema e comunidade (10%): grants, bounties, suporte à integração
- Segurança e auditorias (5%): auditorias de código, revisões de segurança, testes de penetração
- Reserva de longo prazo (5%): estabilidade operacional e reservas de emergência

A Fase 3 introduz um processo formal de propostas e comentários. A Fase 6 introduz votação ponderada em que operadores de service node e de nós de API detêm direitos formais proporcionais ao stake e à antiguidade.

---

## 8. Resumo de Parâmetros

| Parâmetro | Valor |
|---|---|
| Mecanismo de consenso | 100% Proof-of-Stake |
| Tempo de bloco | 60 segundos |
| Recompensa de bloco | 8.25 XEQM por bloco |
| Emissões diárias de bloco | 11,880 XEQM |
| Emissão de governança | ~17,857 XEQM por dia |
| Requisito de nó completo | 200,000 XEQM |
| Stake mínimo do operador | 100,000 XEQM (50%) |
| Taxa máxima do operador | 10% |
| Máximo de slots de contribuidores | 11 (incluindo o operador) |
| Contribuição comunitária mínima | 10,000 XEQM por slot |
| Janela de staker comunitário por nó | Até 100,000 XEQM em 10 slots |
| Período de unbonding, retirada voluntária | 14 dias, recompensas continuam |
| Período de unbonding, desregistro forçado | 14 dias, sem recompensas (HF22) |
| Oferta total | 276,917,604 XEQM no lançamento, crescendo por emissões programadas |
| Oferta bloqueada com 943 nós (Sep 27, 2026) | ~188,600,000 XEQM (~68% da oferta inicial) |
| Em livre circulação com 943 nós | ~88,300,000 XEQM na oferta inicial, crescendo com as emissões |
| APY de operador solo com 943 nós | ~2.3% (apenas recompensas de bloco, pagas semanalmente via HF21) |
| Custo auto-hospedado por nó | ~$0.53/mês (VPS de $5.28/mo, 10 nós) |
| Custo de hospedagem gerenciada (Pecunia) | $1.76/nó/mês |
| Service nodes ativos (27 de setembro de 2026) | 943 |
| Coeficiente de Nakamoto de operador (Sep 27, 2026) | 9 — controle majoritário; meta >= 8; 943 nós, 204 operadores |
| Ativação externa do oracle | Nakamoto >= 6 atingido; condicionado à conclusão da Fase 3 |
| Tamanho do quórum | 12 assentos por rodada |
| Dedup de quórum, HF22 | Um endereço de carteira de operador por assento de quórum por rodada |
| Dedup de quórum, HF23 | Um cluster de proximidade por assento de quórum por rodada (requer Lokinet) |
| Fallback de dedup de quórum, HF23 | Se existirem menos de 12 clusters distintos, os clusters menores recebem assentos adicionais primeiro, antes dos clusters mais concentrados; frequência de fallback registrada e publicada |
| Limite de sobrevivência da rede, HF23 | 30% dos nós ativos por cluster de proximidade (~283 nós na contagem atual) |
| Modificador de recompensa zero, HF23 | Zero recompensas de bloco para nós acima do cap do cluster, classificados por idade de registro |
| Repositórios centrais | github.com/XEQMLabs |

---

## 9. Roadmap

**Fase 1, Estabilização da rede. CONCLUÍDA.** A rede de service nodes cresceu para 943 service nodes ativos em 27 de setembro de 2026 (de 693 entre 184 operadores em julho de 2026, coeficiente de Nakamoto 7). A troca de moeda XEQ para XEQM foi executada e encerrada com sucesso.

**Fase 2, API para desenvolvedores EXIOM e EXIOM Oracle. ATIVA.** O EXIOM Oracle está ativo na mainnet com um comitê de operadores, e a API para desenvolvedores está ativa em beta (credenciais self-serve, endpoints de conformidade e verificação, OpenAPI). Trabalho restante da Fase 2: cobrança por consumo pré-pago, a participação dos operadores na receita, e as primeiras integrações em produção. O desenvolvimento da plataforma de trading RFQ EXIOM prossegue em paralelo, com XEQM/BTC como o primeiro par de trading.

**Fase 3, EXIOM Privacy Oracle e plataforma RFQ.** O oracle é implantado em fases: prova de conceito interna, testnet federada, depois mainnet com consumidores internos. A plataforma de trading RFQ atinge produção nesta fase, usando o oracle para atestação de preço privada no par XEQM/BTC. Ambos são construídos sobre a API EXIOM.

**Fase 4, Acesso de consumidores externos ao oracle.** As saídas do oracle ficam disponíveis para desenvolvedores dos níveis Produção e Enterprise e consumidores externos. Limiar do coeficiente de Nakamoto de 6 já atingido; ativação condicionada à conclusão da Fase 3.

**HF22, ativado (bloco 219120 da mainnet).** Duas mudanças de consenso sem dependência do Lokinet, deduplicação de quórum por chave de carteira do operador (um endereço de operador por assento de quórum por rodada) e unificação do período de unbonding (desregistro forçado estendido de 7 para 14 dias), mais uma revisão de recuperação de travamento do Pulse (snode_revision 1) que foi ativada no bloco 236920 em 18 de outubro de 2026, substituindo a recuperação Proof-of-Work por um fallback baseado em assinatura. Validada em 20 ciclos de travamento/recuperação (100% de recuperação, pior intervalo de bloco de 83 segundos).

**Versão do Lokinet e light-node, antes do HF23.** Uma versão não impositiva que coloca o Lokinet online como transporte da rede (clustering por proximidade ativo e observável no explorador de nós, sem consequências de recompensa) e introduz o armazenamento light-node em SQLite (menor memória e disco por nó, com light nodes de janela recente opcionais). Essa versão amadurece para que a contagem real de clusters de proximidade possa ser medida e o limite e o fallback do HF23 ajustados antes de qualquer imposição entrar em vigor.

**HF23, em projeto, previsto para o Q4 de 2026.** Ativa a imposição assim que a versão não impositiva do Lokinet e do light-node acima tiver amadurecido: limite de registro de cluster por proximidade (registros rejeitados quando um cluster excede 30% dos nós ativos); modificador de recompensa zero para nós acima do limite de cap, classificados por idade de registro; atualização da deduplicação de quórum de chave de carteira para cluster de proximidade, com uma regra de fallback obrigatória garantindo que a formação de quórum seja sempre possível mesmo quando existem menos de 12 clusters distintos (os clusters menores recebem assentos adicionais primeiro, antes dos clusters mais concentrados, com a frequência de fallback registrada e publicada como um indicador de risco de concentração). Um período de carência de 30 dias se aplica na ativação antes de o modificador de recompensa zero entrar em vigor.

**Fase 6, Governança formal.** Processo estruturado de propostas, votação ponderada para operadores, transição de longo prazo para longe da governança da equipe fundadora.

---

## 10. EXIOM Oracle

### O primeiro oracle ativo: EXIOM Oracle

O primeiro produto de oracle da plataforma está ativo na mainnet. O EXIOM Oracle é um comitê de operadores de service node XEQM — cada um executando um sidecar de oracle leve junto a seu nó — que coletivamente produzem atestações BLS-agregadas e assinadas em EIP-712 sobre fatos de conformidade, mais diretamente se um determinado endereço é elegível para uma determinada jurisdição. As aplicações consomem essas atestações através da API para desenvolvedores e podem submeter o resultado assinado on-chain. O comitê está implantado na Robinhood Chain (chainId 4663) e opera um comitê de operadores de 12 membros em 28 de setembro de 2026, com um limiar de assinatura de dois terços (8-de-12).

**Modelo de segurança: conjunto registrado versus limiar.** O EXIOM Oracle não faz amostragem de um comitê por rodada. Como um agregado BLS custa ao gate o mesmo para verificar quer tenham assinado oito membros ou oitocentos, todo membro registrado assina todas as rodadas; amostrar um subconjunto não traria nada e reintroduziria o risco de um sorteio azarado conter membros coludidos em número suficiente para forjar. A segurança, portanto, reduz-se a duas propriedades do conjunto de membros registrados de tamanho N, no limiar de dois terços k = ceil(2N/3) que o gate impõe:

- **Forjamento** requer que um adversário controle pelo menos k membros registrados — uma coluso, e portanto uma questão de concentração de **operadores**.
- **Travamento** (uma falha de liveness) requer que pelo menos N - k + 1 = floor(N/3) + 1 membros registrados fiquem offline de uma só vez — uma falha correlacionada, e portanto uma questão de concentração de **infraestrutura**.

Estes são os dois coeficientes de Nakamoto, e são propriedades do conjunto registrado, não da frota mais ampla de service nodes: a distribuição da frota limita o consenso, enquanto a resistência do oracle a forjamento e a sua liveness dependem apenas de quem detém os assentos registrados.

**Realização atual.** Em 28 de setembro de 2026, os membros registrados são todos operados pelo operador do projeto, de modo que o coeficiente de operador do oracle é 1: hoje sua resistência a forjamento repousa na confiança em um único operador, não em criptografia distribuída. Este é o estado inicial honesto. O modelo de segurança é k-de-N entre operadores independentes; a realização se fortalece à medida que independentes se inscrevem, que é o propósito de integrar operadores adicionais de service node como membros do sidecar. A contagem de nós por si só não ajuda — membros adicionais elevam ambos os coeficientes apenas na medida em que sejam operadores independentes em instalações distintas.

**Como a diversidade é imposta.** Como não há seleção por rodada, a diversidade é decidida na **admissão**: um membro só é registrado se mantiver a participação de todo operador abaixo de k e a participação de toda instalação em ou abaixo de floor(N/3), e k é elevado para acompanhar ceil(2N/3) à medida que o conjunto cresce. A concentração do conjunto registrado é monitorada continuamente e publicada como uma margem de forjamento (k menos a participação do maior operador) e uma margem de liveness (floor(N/3) + 1 menos a participação da maior instalação); uma margem não positiva é um alarme. O sinal de instalação é o ASN e a temporização de chegada das provas de uptime hoje, aguçado no HF23 para a proximidade de roteamento do Lokinet, que detecta co-localização física mesmo entre ASNs distintos. Esses fatos de distribuição são, eles próprios, atestáveis por meio da interface de fatos tipados do oracle, de modo que a métrica de concentração é um valor assinado pelo comitê em vez da saída de um único script confiável.

O sidecar é deliberadamente leve: ele detém apenas sua própria chave de assinatura, lê a identidade de seu nó localmente e nunca manipula as spend keys do operador. Executá-lo é o mecanismo pelo qual um operador de service node ganha a receita adicional, financiada por uso, descrita nas Seções 3 e 4.

### A visão mais ampla: EXIOM Privacy Oracle

O EXIOM Privacy Oracle permite que aplicações consumam feeds de dados privados autenticados sem expor os dados-fonte subjacentes. Ele usa técnicas de prova de zero-knowledge para provar a proveniência de dados a partir de endpoints HTTPS padrão, sem exigir cooperação do lado do servidor nem hardware confiável. É um entregável da Fase 3, seguindo a estabilização da plataforma de API da Fase 2 e uma consultoria de criptografia antes de a construção completa começar.

O oracle não é um feed de dados de propósito geral. É um oracle privacy-first para casos de uso em que os próprios dados devem permanecer confidenciais: limiares de preço sem revelar os preços exatos, saldos de conta sem expor credenciais, atestações de conformidade sem divulgar o registro subjacente. A plataforma RFQ EXIOM é o primeiro consumidor interno, usando-o para provar que uma execução XEQM/BTC ocorreu a um preço de referência ou melhor, sem revelar o preço exato à plataforma ou à outra parte.

Uma vez que o Lokinet esteja ativo como transporte da rede, a comunicação da sessão de oracle entre o prover e o quórum de verificadores será roteada por onion através da rede de service nodes. Nem a origem do prover nem os endereços de rede dos nós do quórum serão visíveis para qualquer nó relay único, eliminando a premissa de confiança no coordenador centralizado.

### Arquitetura

**Camada do prover.** A aplicação ou usuário que detém acesso à fonte de dados privada participa de um protocolo criptográfico que se compromete com a resposta TLS sem revelá-la. Credenciais e dados brutos nunca deixam o controle do prover.

**Camada do verificador.** Um quórum rotativo de service nodes verifica que os dados comprometidos satisfazem a condição solicitada. Os nós verificadores aprendem apenas o resultado (verdadeiro ou falso, acima ou abaixo de um limiar) e nunca veem os dados subjacentes ou as credenciais.

**Camada do consumidor.** Os consumidores recebem apenas a saída mínima: um resultado booleano, uma comparação de limiar, uma atestação assinada ou um pequeno valor derivado. Os dados-fonte brutos nunca são publicados.

### Plano de Construção em Fases

**Fase 1, Prova de conceito interna.** A equipe fundadora valida o protocolo criptográfico completo de ponta a ponta contra um pequeno conjunto de fontes na whitelist, sem consumidores externos ou participação de service nodes.

**Fase 2, Testnet federada do oracle.** Operadores voluntários de service node com forte histórico de uptime juntam-se ao pool de verificadores na testnet. Testes adversariais da integridade das atestações antes de qualquer implantação na mainnet.

**Fase 3, Oracle na mainnet com consumidores internos.** A obrigação de verificador do oracle é aberta a nós qualificados da mainnet. As saídas alimentam contratos internos EXIOM e a plataforma RFQ. As taxas do oracle começam a fluir para os nós verificadores participantes.

**Fase 4, Acesso de consumidores externos.** As saídas do oracle ficam disponíveis para desenvolvedores dos níveis Produção e Enterprise e consumidores externos. Condicionada à conclusão da Fase 3.

### Requisitos de Hardware do Verificador

Requisitos indicativos: 8 núcleos de CPU, 16 GB de RAM, 200 GB de SSD, 500 Mbps com baixa latência. O hardware de referência padrão de um nó de API não é suficiente para a obrigação de verificador do oracle.

### Recompensas do Verificador

| Fonte de Receita | Descrição |
|---|---|
| Recompensas de bloco | Recompensa de bloco padrão do service node, inalterada |
| Participação na receita da plataforma | Participação proporcional na receita de consumo dos desenvolvedores para operadores que executam o sidecar de oracle |
| Taxas de sessão do oracle | Taxa por sessão dos consumidores do oracle, distribuída ao quórum de verificadores |
| Bônus de obrigação do oracle | Emissão de governança suplementar durante períodos de baixo volume, reduzida à medida que as taxas de sessão se autossustentam |

---

## 11. Plataforma de Trading RFQ EXIOM

A plataforma RFQ EXIOM é um sistema de trading peer-to-peer de balcão (over-the-counter) com atestações de liquidação criptográficas, construído sobre a API EXIOM. O primeiro par de trading é XEQM/BTC, ambos ativos Layer 1 nativos, sem tokenização, sem wrapping e sem risco de bridge.

Uma vez que o Lokinet esteja ativo, a plataforma RFQ será acessível como um serviço oculto Lokinet. Nem o endereço IP do solicitante nem o do LP serão visíveis para a plataforma. A camada de precificação do oracle permite que uma contraparte prove que uma execução ocorreu a um preço de referência ou melhor, a partir de uma fonte na whitelist, sem revelar o preço exato de execução à plataforma ou à outra parte.

A especificação da aplicação RFQ e o modelo de dados estão completos. O desenvolvimento ativo prossegue na Fase 2 na camada de API. A produção completa da plataforma de trading é um entregável da Fase 3, dependente de a API EXIOM atingir produção e de o MVP do oracle concluir sua prova de conceito interna.

---

---

## Available Languages

Traduções comunitárias deste whitepaper são mantidas na pasta de traduções por conveniência. **A versão em inglês é o único documento autoritativo em todos os momentos.** As traduções podem ficar atrasadas em relação à revisão atual em inglês e não têm garantia de estarem atualizadas; na eventualidade de qualquer conflito, ambiguidade ou diferença de qualquer tipo, a versão em inglês prevalece.

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

*Este é um documento em rascunho. Parâmetros, cronogramas de emissão e fases do roadmap aqui descritos são o projeto pretendido. Atualizações serão publicadas à medida que a rede e a plataforma evoluírem.*

*Este documento não constitui aconselhamento financeiro ou jurídico. XEQM é uma moeda de utilidade para a plataforma EXIOM, não um produto de investimento. A classificação de tokens, o status de valores mobiliários e as regulamentações aplicáveis variam por jurisdição. Os participantes devem consultar seu arcabouço legal e regulatório local antes de adquirir ou operar com XEQM. A XEQM Labs não incentiva a compra de XEQM com base em valorização especulativa de preço.*
