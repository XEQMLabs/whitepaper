# Limites de Concentração de Nós - Imposição da Sobrevivência da Rede
## Companheiro Técnico do Whitepaper de Tokenomics do EXIOM
### 07/26/2026

> **Nota de escopo (atualizada em outubro de 2026).** A unidade imposta é o *cluster de proximidade* (um grupo de nós que compartilham infraestrutura física ou de roteamento, detectado via proximidade de roteamento do Lokinet, temporização de provas de uptime e ASN), **não o país**. Um país com várias instalações independentes não é afetado. Os números por país abaixo são um indicador geográfico grosseiro de onde a concentração atualmente se encontra, não aquilo que o protocolo limita. As contagens de nós neste companheiro são um retrato de julho de 2026 (~672 nós); veja o whitepaper para os totais atuais da rede (943 nós em 27 de setembro de 2026). O Lokinet é lançado em uma versão não impositiva antes do HF23, e o HF23 ativa a imposição.

Este documento é um companheiro do Whitepaper de Tokenomics do EXIOM e pressupõe que ele tenha sido lido. O whitepaper cobre quais são os controles de concentração e por que existem. Este documento cobre o detalhe mecânico de como cada controle funciona, os dados de validação de testnet por trás do HF22, a matemática econômica precisa por trás do modificador de recompensa zero, a questão da identidade do operador em uma chain de privacidade, e os riscos residuais que o protocolo não resolve totalmente.

---

## Os Dados Atuais de Concentração

| País | Nós ativos |
|---|---|
| France | 492 |
| Germany | 70 |
| United States | 55 |
| Canada | 18 |
| Poland | 13 |
| United Kingdom | 10 |
| Türkiye | 5 |
| Australia | 4 |
| Singapore | 2 |
| Lithuania | 2 |
| Serbia | 1 |

A França detém 492 dos 672 nós neste retrato (cerca de 73% da rede), e essa concentração é quase inteiramente uma única instalação Contabo em Grand Est que detém aproximadamente 426 nós (cerca de 63% da rede). O total do país não é o que o protocolo limita; o **cluster** de Grand Est é. O limiar de sobrevivência é 30% dos nós ativos por cluster de proximidade (cerca de 202 nós nos 672 deste retrato, e cerca de 283 nos 943 nós do whitepaper atual), recalculado continuamente à medida que a rede cresce. Grand Est, com aproximadamente 426 nós, é mais que o dobro desse cap.

---

## O Que Isso Significa para os Operadores de Nós

Esta seção responde à pergunta diretamente: como o HF23 afeta a forma como você executa seus nós?

**O HF23 não limita por país, e não exige um nó por IP, um nó por VPS ou um nó por carteira.** O cap é 30% da rede ativa por *cluster de proximidade* (nós que compartilham infraestrutura física ou de roteamento). Um operador executando 10, 50 ou mesmo 100 nós em infraestrutura compartilhada não é afetado de forma alguma pelo HF23, desde que seu cluster permaneça abaixo desse limiar. Você pode executar múltiplos nós em uma máquina, uma conta de VPS e uma carteira. Nada no HF23 muda isso.

**O modificador de recompensa zero se aplica apenas a nós acima do cap por cluster (30% dos nós ativos).** Os nós registrados mais antigos em um cluster ganham recompensas completas até esse limiar. Apenas os nós classificados acima dele em um cluster superconcentrado ganham zero, e apenas até serem migrados para um cluster menos concentrado.

**A deduplicação de quórum limita a influência no consenso por rodada, não a contagem de nós nem a renda.** Um operador executando 50 nós em um VPS ganha recompensas de bloco em todos os 50 e gerencia sua infraestrutura exatamente como faz hoje. Ele recebe um assento de quórum por cluster por rodada em vez de potencialmente muitos, que é o resultado pretendido.

**A abordagem correta para um novo operador** é verificar o explorador de nós, ver onde os clusters existentes estão concentrados, e implantar em um cluster pouco povoado. Dez nós em um servidor com seu próprio roteamento distinto funcionam perfeitamente bem sob o HF23 porque esse cluster está longe do limiar de 30%. Recompensas completas, participação plena no quórum, sem problemas.

**A dinâmica funciona a seu favor se você implantar em regiões esparsas.** Se uma região eventualmente lotar, o explorador de nós mostra isso e os operadores têm um incentivo financeiro para se mover antes de o cap afetá-los. Os operadores que chegaram primeiro mantêm recompensas completas em seus nós mais antigos até o limiar. Novos registros em um cluster superconcentrado não ganham nada imediatamente, então a economia naturalmente empurra as novas implantações para as regiões mais leves.

**O problema específico que o HF23 resolve** é uma instalação na França (o cluster Contabo de Grand Est) hospedando aproximadamente 426 nós, cerca de 63% da rede neste retrato. Se essa instalação ficar offline, a rede trava. O objetivo é colocar esse cluster abaixo do cap de 30%. Todo outro operador que executa uma configuração responsável de múltiplos nós em um cluster não concentrado é exatamente aquilo de que a rede precisa de mais.

---

## Por Que os Hard Forks São Separados

O HF22 é lançado após testes bem-sucedidos. A deduplicação de quórum por chave de carteira e a unificação do período de unbonding não têm dependência do Lokinet. Ambas foram validadas na testnet, e retê-las enquanto a avaliação do Lokinet está pendente é um atraso injustificado. Um ator sofisticado que leia o whitepaper antes de o HF22 ser lançado poderia tentar a divisão de carteiras para antecipar-se ao controle de quórum, mas fazê-lo é detectável por meio da correlação de temporização de provas de uptime e da análise de IP/ASN e cria um registro documentado para ação de governança.

O Lokinet é lançado primeiro em sua própria versão não impositiva (junto com a mudança de armazenamento light-node em SQLite), de modo que o novo transporte não é tornado crítico para o consenso no momento em que é introduzido. Durante essa versão, o clustering por proximidade roda ativo e observável, sem consequências de recompensa, que é quando a contagem real de clusters é medida e o limiar e o fallback do HF23 são ajustados. O HF23 então segue e ativa a imposição. Separar as versões também proporciona domínios de falha limpos: se algo der errado após a ativação do HF23, há menos variáveis a isolar. Até que a imposição do HF23 esteja ativa, Grand Est permanece exposto a todo o risco de sobrevivência além da dedup de quórum do HF22.

---

## Mecânica do HF22

### Deduplicação de Quórum por Chave de Carteira

O algoritmo de seleção de quórum executa uma passagem de deduplicação sobre cada conjunto de candidatos antes de finalizar. Quando o sorteio seleciona um nó candidato, o algoritmo verifica o endereço da carteira de seu operador contra todos os nós já selecionados para a rodada. Se uma correspondência for encontrada, o candidato é substituído por um novo sorteio a partir do pool elegível restante, excluindo todos os endereços já representados.

O sorteio de substituição não retorna aos candidatos já rejeitados. Ele sorteia do pool restante não selecionado na mesma ordem ponderada por probabilidade usada no sorteio inicial. Isso preserva as propriedades estatísticas da seleção de quórum sem introduzir um viés determinístico em direção a qualquer conjunto particular de nós restantes.

**Resultados da validação de testnet:**
- 20 ciclos de travamento/recuperação concluídos (20/20)
- Taxa de recuperação de 100% em todos os ciclos
- Zero intervenção manual necessária em qualquer ciclo (pior intervalo de bloco de 83 segundos)
- Baseline da mainnet pré-HF22: 1,000 blocos, 100% Pulse, zero blocos GOV_SIGNED
- Análise de timeout R0: nenhum timeout R0 introduzido em condições de produção. A análise de densidade da mainnet atual confirma que todo cluster de IP de alta densidade é um único operador, significando que a dedup por chave de carteira já fornece proteção total contra as atuais implantações whale. As duas maiores implantações de IP único (58 nós e 51 nós respectivamente) são cada uma um operador e estão limitadas a um assento de quórum por rodada sob o HF22.

**O que um assento de quórum significa na prática:** O tamanho do quórum e a frequência de rotação determinam com que frequência um nó participa. No tamanho atual da rede, um cap de assento único significa que a influência de um operador concentrado em sessões de oracle, rodadas do Pulse e quóruns de obrigações é idêntica à de um operador com um único nó. Sua renda de recompensas de bloco permanece inalterada.

**A lacuna da divisão de carteiras e sua detecção interina:** Um operador que divide 426 nós em 10 carteiras obtém até 10 assentos de quórum por rodada em vez de um. Esta é a lacuna conhecida que o HF23 fecha. Nesse ínterim, a divisão de carteiras é detectável por meio de dois sinais já disponíveis sem alterações no daemon. Primeiro, a temporização de provas de uptime: nós no mesmo host físico ou hypervisor submetem provas em milissegundos uns dos outros, independentemente da chave de carteira. Um cluster de provas que chegam em janelas sub-10ms de nós registrados em carteiras diferentes é um forte sinal de infraestrutura compartilhada. Segundo, a correlação de IP e ASN: nós em carteiras diferentes que compartilham um IP, sub-rede ou ASN são registrados e sinalizados para revisão de governança. Um operador que divide carteiras mas mantém todos os nós na mesma instalação Contabo é identificável por meio de ambos os sinais e sujeito a ação de governança sob a política de lista de bloqueio.

### Unificação do Período de Unbonding

O período de unbonding do desregistro forçado muda de 10,080 blocos (aproximadamente 7 dias) para 20,160 blocos (aproximadamente 14 dias), igualando o período de retirada voluntária. Esta é uma mudança de constante de consenso.

O período forçado original de 7 dias foi uma escolha deliberada durante a estabilização da rede para limitar a penalidade sobre operadores que enfrentam eventos de infraestrutura fora de seu controle. Essa justificativa não se aplica mais. A rede está estável, o sistema de crédito de descomissionamento fornece o buffer para interrupções curtas, e um período unificado de 14 dias remove uma assimetria que não tem justificativa remanescente.

As moedas XEQM ficam bloqueadas on-chain durante o período de unbonding por meio da transação de registro. Não há mecanismo para liberar o bloqueio antecipadamente sem uma mudança de protocolo. Para falhas de infraestrutura documentadas, a governança pode compensar recompensas perdidas a partir da carteira de governança como uma transferência de XEQM, mas o bloqueio on-chain cumpre sua duração completa independentemente.

---

## Mecânica do HF23

### Clustering por Proximidade do Lokinet

O Lokinet (Low Latency Anonymous Routing Protocol, LLARP) roteia tráfego pela rede de service nodes na camada 3, suportando TCP, UDP e ICMP. Todo service node participa como relay. O grafo de roteamento que emerge reflete a topologia física da rede: nós na mesma instalação roteiam pelo mesmo switch upstream e pelo mesmo backbone de datacenter, produzindo seleções de caminho correlacionadas e latência inter-nós sub-milissegundo. Nós em instalações diferentes roteiam por caminhos diferentes com latência mensuravelmente mais alta.

O algoritmo de clustering ingere medições pareadas de latência de roteamento do Lokinet e de sobreposição de caminhos em todos os nós ativos e os agrupa em clusters usando essas medições como o sinal de proximidade. Um cluster não é uma região geográfica fixa; é um agrupamento dinâmico de nós cujo comportamento de roteamento indica infraestrutura física compartilhada. Dois nós em instalações Contabo diferentes em países diferentes podem rotear por infraestrutura de backbone Contabo compartilhada suficiente para aparecerem no mesmo cluster se sua sobreposição de caminhos for alta o bastante. Dois nós no mesmo datacenter, mas em máquinas físicas diferentes com conexões upstream diferentes, aparecerão em clusters diferentes se sua sobreposição de caminhos for baixa.

Sinais complementares usados junto à proximidade do Lokinet:

**Correlação de temporização de provas de uptime.** A rede já recebe provas de uptime de todos os nós ativos em um cronograma regular. A distribuição de timestamp das chegadas de provas de cada nó é registrada pelos nós receptores. Nós no mesmo host físico ou hypervisor de VM submetem provas dentro de uma janela estreita característica, tipicamente abaixo de 10 milissegundos. Agrupar essa distribuição de temporização de chegada fornece um sinal de co-localização física que não requer alterações no daemon e funciona antes de o Lokinet estar ativo.

**Análise de ASN.** O endereço IP de cada nó mapeia para um Autonomous System Number via dados BGP públicos. Nós que compartilham um ASN compartilham infraestrutura de roteamento de nível de provedor e exposição legal de nível de provedor. Um provedor que recebe uma ordem de nível jurisdicional afetando toda a sua infraestrutura derruba todos os seus nós de ASN simultaneamente, independentemente de em quantos clusters Lokinet eles apareçam. A concentração de ASN é rastreada como um sinal complementar e contribui para a revisão de governança de operadores próximos ao limiar de cluster.

### Limite de Registro de Cluster

No momento do registro, o protocolo executa uma avaliação de proximidade contra todos os clusters existentes. As características de roteamento Lokinet do nó que se registra são medidas contra o centroide de cada cluster existente. Se o cluster mais próximo já contém 30% ou mais dos nós ativos, o registro é rejeitado com um código de erro específico indicando a capacidade do cluster e a contagem de nós do cluster mais próximo.

A rejeição é determinística: qualquer nó que roteie de forma suficientemente similar a um cluster superconcentrado para ser atribuído a ele é rejeitado, independentemente da chave de carteira do operador, do histórico de registro ou do montante de stake. O operador não pode recorrer da rejeição por meio da governança. O único caminho adiante é registrar-se em infraestrutura que roteie para um cluster diferente.

O limiar é avaliado contra a contagem de nós ativos no momento do registro. À medida que a rede cresce, o limiar de 30% em termos absolutos cresce com ela. Um operador no cap hoje pode registrar nós adicionais em um cluster anteriormente limitado à medida que a rede cresce e o cap absoluto sobe, sem migrar nenhum nó existente.

### Modificador de Recompensa Zero

O modificador de recompensa zero é aplicado no momento do cálculo da recompensa de bloco. O cálculo de recompensa para um nó selecionado inclui uma verificação de elegibilidade de cluster. Se o cluster do nó contém mais nós do que o limiar de cap, e o rank de registro do nó dentro desse cluster está acima do limiar (classificado do mais antigo ao mais novo), o cálculo de recompensa retorna zero.

O ranking é computado a partir da altura do bloco de registro do nó dentro de sua atribuição de cluster. O nó registrado mais antigo no cluster recebe rank 1, o registrado mais recentemente recebe rank N. Nós com rank maior que o limiar de cap ganham zero. Nós com rank igual ou abaixo do limiar de cap ganham a recompensa padrão completa. O ranking é recomputado cada vez que a atribuição de cluster muda, o que ocorre quando nós migram para fora do cluster, quando novos nós entram, ou quando a fronteira do cluster se desloca devido a mudanças na topologia da rede.

**A matemática econômica para Grand Est:** Com 426 nós e um cap de 208 nós, 218 nós ganham zero recompensas de bloco. Com o preço auto-hospedado de $0.53 por nó por mês, esses 218 nós custam $115.54 por mês com renda zero. Com o preço da Pecunia de $1.76 por nó por mês, o custo é de $383.68 por mês. O operador tem duas respostas racionais: migrar os nós em excesso para clusters não concentrados, restaurando suas recompensas imediatamente após o novo registro ser aceito, ou desregistrar os nós em excesso e recuperar o XEQM em stake por meio do processo de unbonding. Qualquer resposta reduz a concentração. Não há base racional para manter os nós em excesso com recompensa zero.

**Mecânica do período de carência:** No bloco de ativação do HF23, o protocolo tira um retrato de todos os clusters ativos e suas contagens de nós. Qualquer cluster que exceda o limiar de 30% é marcado como superconcentrado. Por 30 dias após o bloco de ativação, o modificador de recompensa zero é suspenso para todos os nós, incluindo aqueles acima do limiar de cap. Durante o período de carência, os donos de nós podem observar as atribuições de cluster do explorador de nós, planejar migrações e começar a executá-las. No bloco de vencimento do período de carência, o modificador é ativado. Os nós que tiverem migrado para fora do cluster superconcentrado até esse bloco ganham recompensas completas desse bloco em diante. Os nós ainda acima do limiar ganham zero desse bloco em diante até migrarem.

### Deduplicação de Quórum por Cluster de Proximidade

A atualização de deduplicação de quórum do HF23 substitui a verificação de endereço de carteira por uma verificação de pertencimento a cluster. Quando o sorteio seleciona um nó candidato, o algoritmo verifica sua atribuição de cluster contra todos os nós já selecionados para a rodada. Se dois nós compartilham uma atribuição de cluster, o segundo é substituído por um sorteio do pool restante, excluindo todos os clusters já representados.

O efeito prático sobre um operador que divide carteiras: 10 endereços de carteira em 426 nós, todos na mesma instalação Contabo, aparecem no mesmo cluster de proximidade. A verificação de cluster captura todos eles como uma única unidade. Um nó desse cluster ocupa um assento. Os outros 425 nós desse cluster não, independentemente de sob quantos endereços de carteira distintos estejam registrados.

### Requisito de Contagem Mínima de Clusters e Regra de Fallback

O tamanho do quórum da rede EXIOM é de 12 assentos por rodada. A deduplicação por cluster de proximidade, portanto, requer pelo menos 12 clusters de proximidade distintos no conjunto de nós ativos para garantir a formação de quórum. Se a rede produz menos de 12 clusters distintos, o algoritmo não consegue satisfazer a restrição de um-assento-por-cluster e a formação de quórum falha.

A distribuição atual da rede, uma vez aplicado o clustering por proximidade do Lokinet, é estimada em produzir entre 12 e 18 clusters distintos. Isso está desconfortavelmente próximo do mínimo de 12 assentos. A infraestrutura de backbone de provedor compartilhada entre instalações nominalmente separadas pode fazer com que duas localizações de IP distintas se fundam em um cluster de proximidade no grafo de roteamento do Lokinet. Qualquer fusão desse tipo que reduza a contagem de clusters abaixo de 12 quebra a formação de quórum inteiramente.

O algoritmo, portanto, implementa uma regra de fallback obrigatória:

1. O algoritmo tenta preencher todos os 12 assentos com um nó por cluster distinto, percorrendo os clusters disponíveis em ordem aleatória.
2. Se todos os clusters distintos se esgotarem antes de os 12 assentos serem preenchidos, o algoritmo entra em uma passagem de fallback.
3. Na passagem de fallback, ele permite um segundo nó de cada cluster, começando primeiro pelos clusters menores. Os clusters menos concentrados recebem um segundo assento antes dos mais concentrados.
4. O algoritmo continua as passagens de fallback, incrementando o máximo de assentos por cluster em um a cada passagem, até que os 12 assentos sejam preenchidos.
5. O cluster mais concentrado, como Grand Est nas condições atuais, recebe assentos adicionais somente depois que todos os clusters menores tiverem recebido sua alocação de fallback.

Toda rodada que aciona o fallback é registrada com a contagem de clusters que a causou. A governança monitora a frequência de fallback como um indicador direto de risco de concentração. Uma rede com 12 ou mais clusters distintos nunca aciona o fallback. Uma rede que aciona o fallback de forma consistente está sinalizando que a imposição de concentração do HF23 ainda não está alcançando diversidade física adequada e que o cap de cluster ou a imposição do período de carência requer atenção da governança.

O log de fallback é publicado no explorador de nós junto às atribuições de cluster para que a comunidade de operadores possa observar o risco de concentração em tempo real.

---

## Identidade do Operador em uma Chain de Privacidade

O protocolo não precisa identificar qual operador humano é dono de quais nós para impor o cap de cluster e o modificador de recompensa zero. Ambos os controles operam no nível do cluster. O que pode e o que não pode ser determinado é contexto útil para o monitoramento de governança, mas não é exigido para a imposição do protocolo.

**O que é determinístico a partir de dados on-chain:** nós registrados sob a mesma chave de carteira de operador são definitivamente o mesmo operador. Esta é informação pública na transação de registro.

**O que é inferível com alta confiança a partir de dados do Lokinet e de temporização:** o número de hosts físicos distintos subjacentes a um cluster de nós, independentemente de quantas chaves de carteira usem. Cinco chaves de carteira, cada uma executando 85 nós, todos nos mesmos dois servidores físicos, produzem duas assinaturas de temporização distintas e dois centroides de proximidade Lokinet, não cinco.

**O que não pode ser determinado em uma chain de privacidade:** se duas chaves de carteira diferentes com infraestrutura distinta pertencem ao mesmo operador humano. A fonte de financiamento de cada chave de carteira é privada por projeto. Um operador sofisticado usando cinco carteiras financiadas a partir de cinco fontes diferentes por meio da camada de transações da chain de privacidade apresenta cinco identidades distintas no nível do protocolo.

Para a imposição de sobrevivência, isso não importa. O cluster contém 426 nós. Os 208 mais antigos ganham recompensas. Os 218 mais novos ganham zero. A identidade do operador é irrelevante para esse cálculo.

---

## Status de Implementação

| Controle | Status |
|---|---|
| Dedup de quórum por chave de carteira do operador | HF22, ativado no bloco 219120 |
| Unificação do período de unbonding, 7 para 14 dias | HF22, ativado |
| Recuperação de travamento do Pulse (fallback por assinatura, snode_revision 1) | Ativado no bloco 236920, 18 de outubro de 2026 |
| Ativação do Lokinet como transporte da rede | Em desenvolvimento; lançado em uma versão não impositiva antes do HF23 |
| Armazenamento light-node em SQLite | Em desenvolvimento; lançado com a versão do Lokinet pré-HF23 |
| Algoritmo de clustering por proximidade | Fase de projeto, pendente de avaliação do Lokinet |
| Limite de registro de cluster, limiar de 30% | HF23, fase de projeto |
| Modificador de recompensa zero para nós em excesso | HF23, fase de projeto |
| Mecanismo de período de carência | HF23, fase de projeto |
| Dedup de quórum por cluster de proximidade com regra de fallback | HF23, fase de projeto |
| Monitoramento de contagem mínima de clusters e logging de fallback | HF23, fase de projeto |
| Ferramental de correlação de temporização de provas de uptime | Sem alterações de daemon necessárias, ferramental em desenvolvimento |
| Complemento de clustering por ASN | Sem alterações de daemon necessárias, ferramental em desenvolvimento |

---

## O Que Estes Controles Não Resolvem

**Concentração legal de nível de provedor.** Um provedor que recebe uma ordem legal de nível jurisdicional afetando toda a sua infraestrutura global derruba todos os seus nós simultaneamente, mesmo que esses nós apareçam em múltiplos clusters de proximidade Lokinet. A análise de ASN traz esse risco à superfície, mas o protocolo não pode impor diversidade de provedores sem exigir a divulgação, pelo operador, da identidade de seu provedor. A dispersão geográfica naturalmente produzida pelo cap de cluster mitiga substancialmente esse risco na prática, uma vez que operadores forçados a se distribuir entre clusters, na prática, usarão múltiplos provedores.

**Determinação da identidade do operador humano através de divisões de carteira em chain de privacidade.** Conforme descrito acima, um operador sofisticado usando múltiplas carteiras financiadas por meio da chain de privacidade não pode ser identificado no nível do protocolo. O cap de cluster e o modificador de recompensa zero endereçam o risco de domínio de falha independentemente da identidade. A dedup de quórum fecha a lacuna de influência no consenso no HF23. O risco residual é que um operador sofisticado execute muitos nós em muitos clusters genuinamente distintos, acumulando renda de recompensa de bloco proporcional à sua contagem de nós enquanto contribui proporcionalmente para a saúde da rede. Este é o resultado aceitável: a influência concentrada no consenso é limitada; a participação de capital distribuída é recompensada.

Operadores com dúvidas sobre atribuição de cluster, planejamento de migração ou o cronograma HF22/HF23 são encorajados a postar no canal do Telegram de Operadores de Nós ou abrir uma issue neste repositório.

---

## Available Languages

Traduções comunitárias deste documento são mantidas no repositório do whitepaper. Na eventualidade de qualquer conflito entre uma tradução e a versão em inglês, a versão em inglês prevalece.

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

*Este documento não constitui aconselhamento financeiro ou jurídico. XEQM é uma moeda de utilidade para a plataforma EXIOM, não um produto de investimento. A classificação de tokens, o status de valores mobiliários e as regulamentações aplicáveis variam por jurisdição. Os participantes devem consultar seu arcabouço legal e regulatório local antes de adquirir ou operar com XEQM. A XEQM Labs não incentiva a compra de XEQM com base em valorização especulativa de preço.*
