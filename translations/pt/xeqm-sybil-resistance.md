# Risco de Sybil e o Modelo de Mitigação do EXIOM
## Companheiro Técnico do Whitepaper de Tokenomics do EXIOM
### 07/26/2026

> **Nota (atualizada em outubro de 2026).** A concentração é imposta por *cluster de proximidade* (infraestrutura física ou de roteamento compartilhada), **não por país**. Os números de nós aqui são um retrato de julho de 2026; veja o whitepaper para os totais atuais. O Lokinet é lançado em uma versão não impositiva antes do HF23, e o HF23 ativa a imposição.

Este documento é um companheiro do Whitepaper de Tokenomics do EXIOM e da proposta de Limites de Concentração de Nós, e pressupõe que ambos tenham sido lidos. O whitepaper cobre quais são os controles. A concentration-limits-proposal cobre a mecânica de como cada controle funciona. Este documento cobre o modelo de ameaça: como é de fato um ataque Sybil em uma chain de privacidade, o que torna a arquitetura do EXIOM especificamente resistente ou vulnerável, e como a metodologia de monitoramento contínuo identifica a concentração na prática.

---

## A Ameaça Sybil em uma Chain de Privacidade

Um ataque Sybil em uma rede de service nodes significa um único ator operando muitos nós sob identidades aparentes distintas para ganhar influência desproporcional. Em uma blockchain transparente, a análise de grafo de carteiras muitas vezes pode revelar que múltiplos endereços de operadores de nós são financiados a partir de uma fonte comum, expondo o Sybil. Em uma chain de privacidade, essa ferramenta é indisponível por projeto. A garantia de privacidade que protege as transações dos usuários também remove o método mais comum de detecção de Sybil.

A superfície Sybil do EXIOM, portanto, difere de uma chain transparente de uma maneira específica: um operador que usa corretamente os recursos de privacidade pode apresentar múltiplos endereços de carteira que parecem não relacionados no nível do protocolo, independentemente de quanto capital controle. Isso não é uma falha no projeto de privacidade. É uma propriedade inerente de qualquer chain de privacidade que deve ser endereçada por mecanismos que não a análise de grafo de transações.

As duas superfícies de ataque Sybil no EXIOM são distintas e requerem controles separados:

**Ataque de influência no consenso.** Um operador acumula nós suficientes, por meio de qualquer estrutura de carteiras, para ocupar simultaneamente um número desproporcional de assentos de quórum. Isso permite que ele influencie os resultados de sessões de oracle, rodadas do Pulse e quóruns de obrigações além do que sua proporção individual de stake sugeriria ser justo. O dano é à integridade do consenso, não necessariamente ao uptime da rede.

**Ataque ao domínio de falha.** Um operador concentra nós em uma única instalação física. Isso pode ou não ser intencional como ataque; pode resultar de otimização de custos. O dano é à sobrevivência da rede: uma falha de instalação coloca os nós do operador offline simultaneamente, potencialmente travando a produção de blocos se a concentração for grande o bastante.

---

## O Que Torna o EXIOM Estruturalmente Resistente

**Custo de capital por identidade.** Diferentemente de ataques Sybil puros, em que as identidades são gratuitas, cada service node EXIOM requer 200,000 XEQM em stake, com o operador pessoalmente fazendo stake de pelo menos 100,000 XEQM. Um operador executando 100 nós tem 10,000,000 XEQM de capital em stake e bloqueado. Criar identidades aparentes adicionais por meio da divisão de carteiras não reduz esse custo -- cada nó ainda requer 100,000 XEQM de stake do operador. O ataque Sybil é caro em toda escala.

**Atrito de unbonding.** Um período de unbonding de 14 dias tanto na retirada voluntária quanto no desregistro forçado significa que o capital comprometido com nós Sybil não pode ser extraído rapidamente. Um atacante que decide sair não pode fazê-lo mais rápido que qualquer outro operador.

**Registro público de nós.** A chave de registro e o endereço de carteira do operador de cada service node são públicos. Um nó não pode participar do consenso anonimamente. Embora a identidade humana por trás de um endereço de carteira seja privada, a impressão digital operacional do nó se acumula ao longo do tempo por meio de padrões de registro, temporização de provas de uptime e comportamento de roteamento.

---

## Como a Concentração É Identificada Sem Análise de Grafo de Transações

Como a análise no nível das transações é indisponível, a detecção de concentração do EXIOM se apoia em quatro sinais que são observáveis a partir do comportamento dos nós em vez do histórico de financiamento.

**Clustering por chave de registro.** Nós registrados sob a mesma chave de carteira de operador são definitivamente o mesmo operador. Isso é determinístico a partir de dados on-chain. Um grande operador que não divide carteiras é totalmente visível por meio apenas desse sinal. As atuais maiores implantações na rede, incluindo nós executando 58 e 51 nós respectivamente a partir de endereços IP únicos, são cada uma operadores únicos confirmados por meio de análise de chave de registro.

**Clustering por endereço IP e sub-rede.** Atualmente o principal sinal de co-localização física. Múltiplos nós do mesmo endereço IP estão quase certamente no mesmo servidor. Múltiplos nós da mesma sub-rede sugerem a mesma conta de hospedagem ou bloco de datacenter. Esse sinal está disponível hoje sem quaisquer alterações no daemon e permanecerá como um sinal complementar após a ativação do Lokinet.

**Correlação de temporização de provas de uptime.** A rede recebe provas de uptime de todo nó ativo em um cronograma regular. A distribuição de timestamp de chegada dessas provas é registrada pelos nós receptores. Nós executando no mesmo host físico ou hypervisor de VM submetem provas dentro de uma janela estreita característica, tipicamente abaixo de 10 milissegundos, porque compartilham o mesmo relógio de sistema e a mesma interface de rede. Um cluster de nós de chaves de carteira diferentes cujas provas chegam consistentemente dentro dessa janela é um forte sinal de infraestrutura física compartilhada, detectável sem quaisquer alterações no daemon e sem o Lokinet estar ativo.

Esse sinal é especificamente útil para identificar operadores que dividem carteiras mas mantêm seus nós em infraestrutura compartilhada. As chaves de carteira diferem; a temporização das provas não.

**Proximidade de roteamento do Lokinet (lançada não impositiva antes do HF23; imposta no HF23).** Uma vez que o Lokinet esteja ativo como transporte da rede, o grafo de roteamento fornece um mapa contínuo de topologia física da rede de nós. Nós na mesma instalação roteiam pela mesma infraestrutura upstream, produzindo seleções de caminho correlacionadas e latência inter-nós sub-milissegundo independentemente de suas chaves de carteira ou endereços IP anunciados. Este é o sinal mais robusto porque reflete a realidade física da rede que não pode ser alterada por configuração de software sem de fato mover infraestrutura.

---

## O Ataque de Divisão de Carteiras em Detalhe

A abordagem Sybil mais sofisticada disponível no EXIOM é a divisão de carteiras: registrar nós sob múltiplos endereços de carteira financiados por meio da camada de transações da chain de privacidade, de modo que a fonte de financiamento comum não seja visível. Isso derrota o sinal de clustering por chave de registro, mas não os demais.

Um operador executando 426 nós em 10 carteiras, todos hospedados na mesma instalação Contabo, é exposto por:

- Temporização de provas de uptime: provas de todos os 426 nós chegam na janela sub-10ms característica de infraestrutura compartilhada
- Análise de IP e sub-rede: mesmo com múltiplos IPs, a atribuição de bloco de datacenter e o ASN são compartilhados
- Proximidade do Lokinet (pós-HF23): todos os 426 nós roteiam pelo mesmo backbone Contabo independentemente da chave de carteira

Um operador executando 426 nós em 10 carteiras, genuinamente distribuídos entre 10 provedores diferentes em 10 países diferentes, não é significativamente exposto por nenhum sinal atual. As chaves de registro diferem, a temporização das provas difere porque a infraestrutura difere, os ASNs diferem, e os caminhos do Lokinet diferem. No nível do protocolo, isso parece 10 operadores diferentes.

Este é o risco Sybil residual no EXIOM depois de todos os controles aplicados. Ele é limitado em suas consequências: a deduplicação de quórum do HF23 limita cada cluster de proximidade a um assento de quórum por rodada independentemente da estrutura de carteiras, de modo que mesmo um operador distribuído que divide carteiras não ganha influência ilimitada no consenso. Sua renda de recompensa de bloco escala com sua contagem de nós, o que é justo porque ele fez stake de capital proporcional. Sua influência no consenso por rodada é limitada pela dedup de cluster independentemente de quantas carteiras use.

---

## Metodologia de Monitoramento Contínuo

**Lista de bloqueio de governança.** Uma lista de bloqueio de chaves públicas gerenciada por governança impede que chaves de registro bloqueadas registrem novos nós. Um operador que se muda para uma nova chave de carteira enquanto a original está bloqueada cria um registro documentado de evasão, e a temporização das provas e o comportamento de roteamento da nova chave são correlacionados contra o perfil histórico da chave bloqueada.

**Análise de grafo de slots de contribuidores.** Os slots de contribuidores de service node são um sinal de identidade secundário. Um operador que financia slots de contribuidores em múltiplas de suas próprias chaves de carteira cria um grafo de relacionamento observável mesmo em uma chain de privacidade, porque as transações de registro de contribuidores carregam dados observáveis sobre para quais nós contribuem. Um operador que consistentemente contribui para nós registrados sob a carteira A a partir das carteiras B e C, enquanto essas mesmas carteiras B e C registram seus próprios nós, cria um grafo de correlação que complementa o sinal direto de clustering por chave de registro.

**Monitoramento de ASN.** O IP de cada nó ativo mapeia para um Autonomous System Number por meio de dados BGP públicos. A rede rastreia a concentração de ASN no conjunto de nós ativos. Nós que compartilham um ASN compartilham infraestrutura de nível de provedor e exposição legal. Alta concentração de ASN é sinalizada para revisão de governança mesmo quando registros de nós individuais parecem não relacionados. O sinal de ASN não identifica um operador humano, mas identifica um domínio de falha.

O status atual de implementação de todos os controles descritos neste documento é mantido na [proposta de Limites de Concentração de Nós](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md).

---

*Este documento não constitui aconselhamento financeiro ou jurídico. XEQM é uma moeda de utilidade para a plataforma EXIOM, não um produto de investimento. A classificação de tokens, o status de valores mobiliários e as regulamentações aplicáveis variam por jurisdição. Os participantes devem consultar seu arcabouço legal e regulatório local antes de adquirir ou operar com XEQM. A XEQM Labs não incentiva a compra de XEQM com base em valorização especulativa de preço.*
