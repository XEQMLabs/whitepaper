# Limites de Concentração de Nós - Aplicação da Capacidade de Sobrevivência da Rede
## Documento Técnico Complementar ao Whitepaper de Tokenomics da EXIOM
### 07/26/2026

> **Nota de escopo (atualizada em 19 de outubro de 2026).** A unidade sujeita à aplicação é o *cluster de proximidade* (um grupo de nós que compartilham infraestrutura física ou de roteamento, detectado por meio da proximidade de roteamento do Lokinet, da sincronização das provas de disponibilidade e do ASN), **não o país** e nem o país de registro de um provedor. Um país ou provedor com várias instalações genuinamente independentes representa menos risco do que uma única instalação detendo uma grande parcela. Os dados de concentração abaixo são um instantâneo de 19 de outubro de 2026 (893 nós ativos) agrupados por provedor de hospedagem, o melhor indicador disponível antes do Lokinet. O Lokinet é lançado em uma versão não impositiva antes do HF23, e o HF23 ativa a aplicação.

Este documento é complementar ao Whitepaper de Tokenomics da EXIOM e pressupõe que ele já tenha sido lido. O whitepaper aborda quais são os controles de concentração e por que existem. Este documento aborda o detalhe mecânico de como cada controle funciona, os dados de validação de testnet por trás do HF22, a matemática econômica precisa por trás do modificador de recompensa zero, a questão da identidade do operador em uma blockchain de privacidade e os riscos residuais que o protocolo não resolve totalmente.

---

## Os Dados Atuais de Concentração

Medidos em 19 de outubro de 2026 com 893 nós ativos, agrupados por provedor de hospedagem (ASN), que é o sinal de concentração disponível hoje antes do Lokinet. O provedor é um indicador muito melhor de um domínio de falha compartilhado do que uma bandeira de país, porque a rede e as instalações de uma mesma empresa tendem a falhar, ou a serem ordenadas a sair do ar, em conjunto.

| Provedor (ASN) | Nós ativos | Parcela |
|---|---|---|
| NodeHub (AS214083) | 444 | 49.7% |
| Contabo (AS51167, mais AS40021 e Contabo Asia AS141995) | ~303 | ~34% |
| OVH (AS16276) | 62 | 6.9% |
| Oracle (AS31898) | 22 | 2.5% |
| WebNX (AS18450) | 12 | 1.3% |
| todos os outros provedores combinados (mais 12 ASNs) | ~50 | ~5.6% |

Sozinha, a NodeHub detém 49.7% da rede, bem acima do limite de sobrevivência de 30% (267 nós com 893 ativos), e uma única sub-rede /24 detém 41.2%. Este único provedor é a concentração que o HF23 foi construído para quebrar.

Como se chegou aqui. A Pecunia, um serviço de hospedagem que se ofereceu para operar nós XEQM em nome dos operadores, colocou a maioria de seus nós na Contabo. O desempenho da Pecunia tem sido ruim, e muitos operadores migraram desde então para a NodeHub. Portanto, o domínio de falha dominante mudou da Contabo, que ainda detém cerca de um terço da rede (grande parte na instalação de Grand Est), para a NodeHub, agora o maior cluster isolado da rede.

Uma nota sobre os números por país. O país de registro de um provedor não é onde ficam seus servidores. A NodeHub é registrada nos US e a Contabo é registrada na DE, portanto uma visão por país marca seus nós como US e DE independentemente do data center físico (a maior instalação XEQM da Contabo fica em Grand Est, na França). O protocolo não limita nem o país nem o registro do provedor. Ele limita o cluster de proximidade, o conjunto de nós que de fato compartilham infraestrutura física ou de roteamento. O ASN e a sub-rede são o indicador disso hoje, e o HF23 os substitui pela proximidade de roteamento do Lokinet, que também consegue separar instalações distintas dentro de um mesmo provedor. O limite é 30% dos nós ativos por cluster (267 com os 893 atuais), recalculado continuamente à medida que a rede cresce.

---

## O Que Isso Significa para os Operadores de Nós

Esta seção responde à pergunta diretamente: como o HF23 afeta a forma como você opera seus nós?

**O HF23 não limita por país e não exige um nó por IP, um nó por VPS, nem um nó por carteira.** O limite é 30% da rede ativa por *cluster de proximidade* (nós que compartilham infraestrutura física ou de roteamento). Um operador que execute 10, 50 ou até 100 nós em infraestrutura compartilhada não é afetado de forma alguma pelo HF23, desde que seu cluster permaneça abaixo desse limite. Você pode executar vários nós em uma máquina, em uma conta VPS e em uma carteira. Nada no HF23 muda isso.

**O modificador de recompensa zero se aplica apenas aos nós acima do limite por cluster (30% dos nós ativos).** Os nós registrados há mais tempo em um cluster ganham recompensas integrais até esse limite. Somente os nós classificados acima dele em um cluster superconcentrado ganham zero, e apenas até que sejam migrados para um cluster menos concentrado.

**A deduplicação de quórum limita a influência no consenso por rodada, não a contagem de nós nem a renda.** Um operador que execute 50 nós em um único VPS ganha recompensas de bloco em todos os 50 e gerencia sua infraestrutura exatamente como faz hoje. Ele recebe uma vaga de quórum por cluster por rodada, em vez de potencialmente muitas, que é o resultado pretendido.

**A abordagem correta para um novo operador** é consultar o explorador de nós, ver onde os clusters existentes estão concentrados e fazer a implantação em um cluster pouco povoado. Dez nós em um servidor com seu próprio roteamento distinto funcionam perfeitamente bem sob o HF23, porque esse cluster está longe do limite de 30%. Recompensas integrais, participação total em quórum, sem problemas.

**A dinâmica joga a seu favor se você fizer a implantação em regiões esparsas.** Se uma região eventualmente lotar, o explorador de nós mostra isso e os operadores têm incentivo financeiro para se mudar antes que o limite os afete. Os operadores que chegaram primeiro mantêm as recompensas integrais em seus nós mais antigos até o limite. Novos registros em um cluster superconcentrado ganham nada imediatamente, de modo que a economia naturalmente empurra as novas implantações para regiões mais leves.

**O problema específico que o HF23 resolve** é um único provedor, a NodeHub, hospedando agora cerca de metade da rede (444 nós, 49.7%), com a Contabo em segundo lugar com aproximadamente um terço. Se a infraestrutura da NodeHub sair do ar ou for ordenada a parar, a rede trava. O objetivo é levar qualquer cluster isolado para abaixo do limite de 30%. Todo operador que executa uma configuração responsável de múltiplos nós em um provedor ou instalação diferente e não concentrado é exatamente o que a rede precisa em maior quantidade.

---

## Por Que os Hard Forks São Separados

O HF22 é lançado após testes bem-sucedidos. A deduplicação de quórum por chave de carteira e a unificação do período de desvinculação não têm dependência do Lokinet. Ambas foram validadas em testnet, e mantê-las retidas enquanto a avaliação do Lokinet está pendente é um atraso injustificado. Um ator sofisticado que leia o whitepaper antes do lançamento do HF22 poderia tentar a divisão de carteiras para se antecipar ao controle de quórum, mas fazer isso é detectável por meio da correlação de sincronização das provas de disponibilidade e da análise de IP/ASN e cria um registro documentado para ação de governança.

O Lokinet é lançado primeiro em sua própria versão não impositiva (junto com a mudança de armazenamento de nó leve em SQLite), de modo que o novo transporte não se torna crítico para o consenso no momento em que é introduzido. Durante essa versão, o clustering de proximidade roda ao vivo e de forma observável, sem consequências de recompensa, que é quando a contagem real de clusters é medida e o limite e o fallback do HF23 são ajustados. O HF23 então vem em seguida e ativa a aplicação. Separar as versões também proporciona domínios de falha limpos: se algo der errado após a ativação do HF23, há menos variáveis a isolar. Até que a aplicação do HF23 esteja ativa, Grand Est permanece exposta a todo o risco de sobrevivência além da deduplicação de quórum do HF22.

---

## Mecânica do HF22

### Deduplicação de Quórum por Chave de Carteira

O algoritmo de seleção de quórum executa uma passagem de deduplicação sobre cada conjunto de candidatos antes de finalizar. Quando o sorteio seleciona um nó candidato, o algoritmo verifica o endereço da carteira de seu operador contra todos os nós já selecionados para a rodada. Se uma correspondência for encontrada, o candidato é substituído por meio de um novo sorteio no restante do conjunto elegível, excluindo todos os endereços já representados.

O sorteio de substituição não retorna ciclicamente aos candidatos já rejeitados. Ele sorteia no conjunto restante não selecionado na mesma ordem ponderada por probabilidade usada no sorteio inicial. Isso preserva as propriedades estatísticas da seleção de quórum sem introduzir um viés determinístico em favor de qualquer conjunto específico de nós restantes.

**Resultados da validação de testnet:**
- 20 ciclos de travamento/recuperação concluídos (20/20)
- 100% de taxa de recuperação em todos os ciclos
- Zero intervenção manual necessária em qualquer ciclo (maior intervalo entre blocos de 83 segundos)
- Linha de base da mainnet pré-HF22: 1,000 blocos, 100% Pulse, zero blocos GOV_SIGNED
- Análise de timeout de R0: nenhum timeout de R0 introduzido em condições de produção. A análise de densidade da mainnet atual confirma que cada cluster de IP de alta densidade é um único operador, significando que a deduplicação por chave de carteira já fornece proteção total contra as atuais implantações de baleias. As duas maiores implantações de IP único (58 nós e 51 nós, respectivamente) são cada uma de um único operador e estão limitadas a uma vaga de quórum por rodada sob o HF22.

**O que uma vaga de quórum significa na prática:** O tamanho do quórum e a frequência de rotação determinam com que frequência um nó participa. No tamanho atual da rede, um limite de vaga única significa que a influência de um operador concentrado nas sessões do oráculo, nas rodadas Pulse e nos quóruns de obrigações é idêntica à de um operador com um único nó. Sua renda de recompensa de bloco permanece inalterada.

**A lacuna da divisão de carteiras e sua detecção provisória:** Um operador que divida 426 nós entre 10 carteiras obtém até 10 vagas de quórum por rodada, em vez de uma. Esta é a lacuna conhecida que o HF23 fecha. Nesse ínterim, a divisão de carteiras é detectável por meio de dois sinais já disponíveis sem alterações no daemon. Primeiro, a sincronização das provas de disponibilidade: nós no mesmo host físico ou hipervisor enviam provas dentro de milissegundos uns dos outros, independentemente da chave de carteira. Um cluster de provas chegando em janelas abaixo de 10ms a partir de nós registrados em carteiras diferentes é um forte sinal de infraestrutura compartilhada. Segundo, a correlação de IP e ASN: nós em carteiras diferentes compartilhando um IP, uma sub-rede ou um ASN são registrados e sinalizados para revisão de governança. Um operador que divide carteiras mas mantém todos os nós na mesma instalação da Contabo é identificável por ambos os sinais e sujeito à ação de governança sob a política de lista de bloqueio.

### Unificação do Período de Desvinculação

O período de desvinculação por cancelamento forçado de registro muda de 10,080 blocos (aproximadamente 7 dias) para 20,160 blocos (aproximadamente 14 dias), igualando o período de retirada voluntária. Esta é uma mudança de constante de consenso.

O período forçado original de 7 dias foi uma escolha deliberada durante a estabilização da rede para limitar a penalidade sobre operadores que enfrentavam eventos de infraestrutura fora de seu controle. Essa justificativa não se aplica mais. A rede está estável, o sistema de crédito de desativação fornece a margem para interrupções curtas, e um período unificado de 14 dias remove uma assimetria que não tem justificativa remanescente.

As moedas XEQM ficam bloqueadas on-chain durante o período de desvinculação por meio da transação de registro. Não há mecanismo para liberar o bloqueio antecipadamente sem uma mudança de protocolo. Para falhas de infraestrutura documentadas, a governança pode compensar as recompensas perdidas a partir da carteira de governança como uma transferência de XEQM, mas o bloqueio on-chain cumpre sua duração integral independentemente disso.

---

## Mecânica do HF23

### Clustering de Proximidade do Lokinet

O Lokinet (Low Latency Anonymous Routing Protocol, LLARP) roteia o tráfego através da rede de nós de serviço na camada 3, suportando TCP, UDP e ICMP. Cada nó de serviço participa como um relay. O grafo de roteamento que emerge reflete a topologia física da rede: nós na mesma instalação roteiam através do mesmo switch upstream e do mesmo backbone do data center, produzindo seleções de caminho correlacionadas e latência inter-nós abaixo de um milissegundo. Nós em instalações diferentes roteiam através de caminhos diferentes com latência mensuravelmente maior.

O algoritmo de clustering ingere medições pareadas de latência de roteamento do Lokinet e de sobreposição de caminhos entre todos os nós ativos e os agrupa em clusters usando essas medições como o sinal de proximidade. Um cluster não é uma região geográfica fixa; é um agrupamento dinâmico de nós cujo comportamento de roteamento indica infraestrutura física compartilhada. Dois nós em instalações diferentes da Contabo em países diferentes podem rotear através de infraestrutura de backbone da Contabo compartilhada o suficiente para aparecerem no mesmo cluster se sua sobreposição de caminhos for alta o bastante. Dois nós no mesmo data center, mas em máquinas físicas diferentes com conexões upstream diferentes, aparecerão em clusters diferentes se sua sobreposição de caminhos for baixa.

Sinais complementares usados em conjunto com a proximidade do Lokinet:

**Correlação de sincronização das provas de disponibilidade.** A rede já recebe provas de disponibilidade de todos os nós ativos em um cronograma regular. A distribuição de timestamps das chegadas de provas de cada nó é registrada pelos nós receptores. Nós no mesmo host físico ou hipervisor de VM enviam provas dentro de uma janela característica estreita, tipicamente abaixo de 10 milissegundos. Agrupar essa distribuição de sincronização de chegada fornece um sinal de colocalização física que não requer alterações no daemon e funciona antes de o Lokinet estar ativo.

**Análise de ASN.** O endereço IP de cada nó mapeia para um Autonomous System Number via dados BGP públicos. Nós que compartilham um ASN compartilham infraestrutura de roteamento em nível de provedor e exposição legal em nível de provedor. Um provedor que recebe uma ordem em nível de jurisdição afetando toda a sua infraestrutura derruba todos os seus nós de ASN simultaneamente, independentemente de em quantos clusters do Lokinet eles apareçam. A concentração de ASN é rastreada como um sinal complementar e contribui para a revisão de governança de operadores próximos ao limite de cluster.

### Limite de Registro por Cluster

No momento do registro, o protocolo executa uma avaliação de proximidade contra todos os clusters existentes. As características de roteamento do Lokinet do nó em registro são medidas contra o centroide de cada cluster existente. Se o cluster mais próximo já contiver 30% ou mais dos nós ativos, o registro é rejeitado com um código de erro específico indicando a capacidade do cluster e a contagem de nós do cluster mais próximo.

A rejeição é determinística: qualquer nó que roteie de forma suficientemente semelhante a um cluster superconcentrado a ponto de ser atribuído a ele é rejeitado, independentemente da chave de carteira do operador, do histórico de registro ou do valor em stake. O operador não pode recorrer da rejeição por meio da governança. O único caminho adiante é registrar em infraestrutura que roteie para um cluster diferente.

O limite é avaliado contra a contagem de nós ativos no momento do registro. À medida que a rede cresce, o limite de 30% em termos absolutos cresce com ela. Um operador no limite hoje pode registrar nós adicionais em um cluster anteriormente limitado à medida que a rede cresce e o limite absoluto sobe, sem migrar nenhum nó existente.

### Modificador de Recompensa Zero

O modificador de recompensa zero é aplicado no momento do cálculo da recompensa de bloco. O cálculo da recompensa para um nó selecionado inclui uma verificação de elegibilidade de cluster. Se o cluster do nó contiver mais nós do que o limite estabelecido, e a classificação de registro do nó dentro daquele cluster estiver acima do limite (classificado do mais antigo para o mais novo), o cálculo da recompensa retorna zero.

A classificação é computada a partir da altura do bloco de registro do nó dentro de sua atribuição de cluster. O nó registrado há mais tempo no cluster recebe a classificação 1, o registrado mais recentemente recebe a classificação N. Nós com classificação maior que o limite estabelecido ganham zero. Nós com classificação igual ou abaixo do limite ganham a recompensa padrão integral. A classificação é recomputada toda vez que a atribuição de cluster muda, o que ocorre quando nós migram para fora do cluster, quando novos nós entram, ou quando a fronteira do cluster se desloca devido a mudanças na topologia da rede.

**A matemática econômica para Grand Est:** Com 426 nós e um limite de 208 nós, 218 nós ganham zero de recompensa de bloco. Ao preço de auto-hospedagem de $0.53 por nó por mês, esses 218 nós custam $115.54 por mês com renda zero. Ao preço da Pecunia de $1.76 por nó por mês, o custo é de $383.68 por mês. O operador tem duas respostas racionais: migrar os nós excedentes para clusters não concentrados, restaurando suas recompensas imediatamente após o novo registro ser aceito, ou cancelar o registro dos nós excedentes e recuperar o XEQM em stake por meio do processo de desvinculação. Qualquer resposta reduz a concentração. Não há base racional para manter os nós excedentes com recompensa zero.

**Mecânica do período de carência:** No bloco de ativação do HF23, o protocolo tira um instantâneo de todos os clusters ativos e suas contagens de nós. Qualquer cluster que exceda o limite de 30% é marcado como superconcentrado. Durante 30 dias após o bloco de ativação, o modificador de recompensa zero fica suspenso para todos os nós, incluindo aqueles acima do limite. Durante o período de carência, os proprietários de nós podem observar as atribuições de cluster do explorador de nós, planejar migrações e começar a executá-las. No bloco de expiração do período de carência, o modificador é ativado. Os nós que migraram para fora do cluster superconcentrado até aquele bloco ganham recompensas integrais daquele bloco em diante. Os nós que ainda estiverem acima do limite ganham zero daquele bloco em diante até migrarem.

### Deduplicação de Quórum por Cluster de Proximidade

A atualização de deduplicação de quórum do HF23 substitui a verificação de endereço de carteira por uma verificação de pertencimento a cluster. Quando o sorteio seleciona um nó candidato, o algoritmo verifica sua atribuição de cluster contra todos os nós já selecionados para a rodada. Se dois nós compartilharem uma atribuição de cluster, o segundo é substituído por um sorteio no conjunto restante, excluindo todos os clusters já representados.

O efeito prático sobre um operador que divide carteiras: 10 endereços de carteira distribuídos entre 426 nós, todos na mesma instalação da Contabo, aparecem no mesmo cluster de proximidade. A verificação de cluster captura todos eles como uma única unidade. Um nó daquele cluster ocupa uma vaga. Os outros 425 nós daquele cluster não ocupam, independentemente de sob quantos endereços de carteira distintos estejam registrados.

### Requisito de Contagem Mínima de Clusters e Regra de Fallback

O tamanho do quórum da rede EXIOM é de 12 vagas por rodada. A deduplicação por cluster de proximidade, portanto, requer pelo menos 12 clusters de proximidade distintos no conjunto de nós ativos para garantir a formação de quórum. Se a rede produzir menos de 12 clusters distintos, o algoritmo não consegue satisfazer a restrição de uma vaga por cluster e a formação de quórum falha.

Estima-se que a distribuição atual da rede, uma vez aplicado o clustering de proximidade do Lokinet, produza entre 12 e 18 clusters distintos. Isso é desconfortavelmente próximo do mínimo de 12 vagas. A infraestrutura de backbone compartilhada de um provedor entre instalações nominalmente separadas pode fazer com que dois locais de IP distintos se fundam em um único cluster de proximidade no grafo de roteamento do Lokinet. Qualquer fusão desse tipo que reduza a contagem de clusters abaixo de 12 quebra totalmente a formação de quórum.

O algoritmo, portanto, implementa uma regra de fallback obrigatória:

1. O algoritmo tenta preencher todas as 12 vagas com um nó por cluster distinto, percorrendo os clusters disponíveis em ordem aleatória.
2. Se todos os clusters distintos se esgotarem antes de as 12 vagas serem preenchidas, o algoritmo entra em uma passagem de fallback.
3. Na passagem de fallback, ele permite um segundo nó de cada cluster, começando primeiro pelos menores clusters. Os clusters menos concentrados recebem uma segunda vaga antes dos mais concentrados.
4. O algoritmo continua as passagens de fallback, incrementando em um o máximo de vagas por cluster a cada passagem, até que as 12 vagas sejam preenchidas.
5. O cluster mais concentrado, como Grand Est nas condições atuais, recebe vagas adicionais somente depois que todos os clusters menores tiverem recebido sua alocação de fallback.

Toda rodada que aciona o fallback é registrada com a contagem de clusters que a causou. A governança monitora a frequência de fallback como um indicador direto de risco de concentração. Uma rede com 12 ou mais clusters distintos nunca aciona o fallback. Uma rede que aciona o fallback de forma consistente está sinalizando que a aplicação de concentração do HF23 ainda não está alcançando diversidade física adequada e que o limite de cluster ou a aplicação do período de carência requer atenção da governança.

O log de fallback é publicado no explorador de nós junto com as atribuições de cluster, para que a comunidade de operadores possa observar o risco de concentração em tempo real.

---

## Identidade do Operador em uma Blockchain de Privacidade

O protocolo não precisa identificar qual operador humano é dono de quais nós para aplicar o limite de cluster e o modificador de recompensa zero. Ambos os controles operam no nível do cluster. O que pode e o que não pode ser determinado é um contexto útil para o monitoramento de governança, mas não é necessário para a aplicação do protocolo.

**O que é determinístico a partir dos dados on-chain:** nós registrados sob a mesma chave de carteira de operador são definitivamente do mesmo operador. Esta é uma informação pública na transação de registro.

**O que é inferível com alta confiança a partir dos dados do Lokinet e de sincronização:** o número de hosts físicos distintos subjacentes a um cluster de nós, independentemente de quantas chaves de carteira eles usem. Cinco chaves de carteira executando cada uma 85 nós, todos nos mesmos dois servidores físicos, produzem duas assinaturas de sincronização distintas e dois centroides de proximidade do Lokinet, não cinco.

**O que não pode ser determinado em uma blockchain de privacidade:** se duas chaves de carteira diferentes com infraestrutura distinta pertencem ao mesmo operador humano. A fonte de financiamento de cada chave de carteira é privada por design. Um operador sofisticado usando cinco carteiras financiadas por cinco fontes diferentes através da camada de transações da blockchain de privacidade apresenta cinco identidades distintas no nível do protocolo.

Para a aplicação da capacidade de sobrevivência, isso não importa. O cluster contém 426 nós. Os 208 mais antigos ganham recompensas. Os 218 mais novos ganham zero. A identidade do operador é irrelevante para esse cálculo.

---

## Status de Implementação

| Controle | Status |
|---|---|
| Deduplicação de quórum por chave de carteira do operador | HF22, ativado no bloco 219120 |
| Unificação do período de desvinculação, de 7 para 14 dias | HF22, ativado |
| Recuperação de travamento Pulse (fallback de assinatura, snode_revision 1) | Ativado no bloco 236920, 18 de outubro de 2026 |
| Ativação do Lokinet como transporte de rede | Em desenvolvimento; lançado em uma versão não impositiva antes do HF23 |
| Armazenamento de nó leve em SQLite | Em desenvolvimento; lançado com a versão pré-HF23 do Lokinet |
| Algoritmo de clustering de proximidade | Fase de design, pendente de avaliação do Lokinet |
| Limite de registro por cluster, limite de 30% | HF23, fase de design |
| Modificador de recompensa zero para nós excedentes | HF23, fase de design |
| Mecanismo de período de carência | HF23, fase de design |
| Deduplicação de quórum por cluster de proximidade com regra de fallback | HF23, fase de design |
| Monitoramento de contagem mínima de clusters e registro de fallback | HF23, fase de design |
| Ferramental de correlação de sincronização das provas de disponibilidade | Nenhuma alteração de daemon necessária, ferramental em desenvolvimento |
| Complemento de clustering por ASN | Nenhuma alteração de daemon necessária, ferramental em desenvolvimento |

---

## O Que Estes Controles Não Resolvem

**Concentração legal em nível de provedor.** Um provedor que recebe uma ordem legal em nível de jurisdição afetando toda a sua infraestrutura global derruba todos os seus nós simultaneamente, mesmo que esses nós apareçam em múltiplos clusters de proximidade do Lokinet. A análise de ASN traz esse risco à tona, mas o protocolo não consegue aplicar a diversidade de provedores sem exigir a divulgação, por parte do operador, da identidade de seu provedor. A dispersão geográfica produzida naturalmente pelo limite de cluster mitiga substancialmente esse risco na prática, uma vez que operadores forçados a se distribuir entre clusters usarão, na prática, múltiplos provedores.

**Determinação da identidade do operador humano através de divisões de carteira em blockchain de privacidade.** Como descrito acima, um operador sofisticado usando múltiplas carteiras financiadas através da blockchain de privacidade não pode ser identificado no nível do protocolo. O limite de cluster e o modificador de recompensa zero abordam o risco de domínio de falha independentemente da identidade. A deduplicação de quórum fecha a lacuna de influência no consenso no HF23. O risco residual é que um operador sofisticado execute muitos nós distribuídos por muitos clusters genuinamente distintos, acumulando renda de recompensa de bloco proporcional à sua contagem de nós, ao mesmo tempo em que contribui proporcionalmente para a saúde da rede. Este é o resultado aceitável: a influência concentrada no consenso é limitada; a participação distribuída de capital é recompensada.

Operadores com dúvidas sobre atribuição de cluster, planejamento de migração ou o cronograma do HF22/HF23 são incentivados a postar no canal do Telegram dos Operadores de Nós ou abrir uma issue neste repositório.

---

## Idiomas Disponíveis

Traduções comunitárias deste documento são mantidas no repositório do whitepaper. Em caso de qualquer conflito entre uma tradução e a versão em inglês, a versão em inglês prevalece.

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

*Este documento não constitui aconselhamento financeiro ou jurídico. XEQM é uma moeda utilitária para a plataforma EXIOM, não um produto de investimento. A classificação de tokens, o status de valores mobiliários e as regulamentações aplicáveis variam conforme a jurisdição. Os participantes devem consultar seu arcabouço legal e regulatório local antes de adquirir ou operar com XEQM. A XEQM Labs não incentiva a compra de XEQM com base em valorização especulativa de preço.*
