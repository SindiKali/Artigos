# Por que vulnerabilidades web clássicas continuam relevantes na era da IA

![image](https://cdn-images-1.medium.com/max/800/0*FsmHhwl-FbbxBpgt)

Este artigo adota uma abordagem de **revisão de literatura e análise empírica baseada em relatórios da indústria de software e segurança cibernética.** 
A investigação cruza dados de telemetria de desenvolvimento (como os estudos do GitClear sobre 211 milhões de linhas de código e métricas do Google DevOps Research and Assessment - DORA), 
relatórios de segurança de Large Language Models (LLMs) e padrões de vulnerabilidades mapeados pelo OWASP Top 10. O objetivo é examinar como a automação 
de código por inteligência artificial impacta a estabilidade de entrega e a persistência de falhas clássicas em ambientes de produção.

## 1. Velocidade ou Defesa

A área de desenvolvimento web passou por uma transformação drástica nos últimos anos. Com a proliferação de frameworks de alta produtividade, arquiteturas de microsserviços e a adoção massiva de assistentes de inteligência artificial (LLMs, copilots e ferramentas de geração de código), construir aplicações web tornou-se mais veloz do que nunca.

Porém, há um efeito colateral mensurável nessa dinâmica. De acordo com métricas de entrega do Google DORA, observa-se um impacto na estabilidade de entregas corporativas sob alta automação, enquanto levantamentos e discussões publicados pela **Cloud Security Alliance em julho de 2025** apontam que até **62% das soluções de código geradas por modelos de linguagem** podem carregar falhas de design ou vulnerabilidades conhecidas se não forem rigorosamente auditadas.

Vulnerabilidades clássicas - como Cross-Site Scripting (XSS), Insecure Direct Object References (IDOR) e SQL Injection - continuam assolando APIs, sites e sistemas em produção justamente devido a essa pressa automatizada.

## 2. O Impacto da Automação na Geração de Código

Historicamente, falhas de segurança surgiam por limitações técnicas ou desconhecimento pontual dos desenvolvedores. No cenário atual, o problema mudou de forma: com o uso intensivo de IAs para gerar rotas de API, componentes e funções em segundos, o desenvolvedor muitas vezes é rebaixado ao papel de um mero "revisor de código passivo".

As IAs são treinadas em datasets públicos que misturam código limpo com padrões legados e inseguros. Quando solicitadas a resolver uma demanda complexa, as ferramentas priorizam a sintaxe e a funcionalidade imediata, ignorando o contexto de ameaças do sistema. O resultado é a reintrodução de falhas mapeadas no CWE Top 25 (como falta de validação de entrada).

## 3. Radiografia de Vulnerabilidades no Ecossistema Atual

### XSS (Cross-Site Scripting) em Arquiteturas Modernas

Muitos desenvolvedores acreditam que frameworks modernos (como React ou Svelte) eliminam o XSS devido ao escape automático de variáveis no JSX. Contudo, as falhas ressurgem em pontos cegos corporativos, como o uso irresponsável de renderizadores diretos (```dangerouslySetInnerHTML```) e lógicas de DOM-based XSS manipulando parâmetros de URL sem sanitização prévia.

### IDOR/BOLA e controle de acesso em APIs RESTful

Com a explosão de arquiteturas de microsserviços e APIs consumidas por aplicações mobile e web, o IDOR tornou-se uma das falhas lógicas mais lucrativas e recorrentes em programas de Bug Bounty. Como a IA tende a gerar lógicas de rotas baseadas em IDs sequenciais ou objetos diretos do banco sem implementar camadas robustas de controle de acesso baseado em papéis (RBAC), a falha passa invisível pelos testes unitários básicos.

### SQL Injection e Armadilhas de ORMs

Embora o uso de ORMs (*Object-Relational Mappers*) tenha mitigado grande parte das injeções SQL tradicionais, o problema migrou para duas frentes na era da IA:

**Consultas cruas geradas por IA**: Quando o ORM padrão falha em resolver uma query complexa, a IA prontamente sugere o uso de métodos de execução de SQL cru (raw queries), concatenando variáveis diretamente na string de forma insegura.

**Filtros dinâmicos inseguros**: Construção de cláusulas WHERE dinâmicas baseadas em inputs de usuários não tratados.

## 4. O Fator IA e a Ilusão da Segurança Automatizada

O cerne da questão reside na forma como o código gerado por máquina é consumido pelas equipes de engenharia:

**A Falácia da Sintaxe Correta**: Como o código compila, roda perfeitamente e resolve a *issue* do Jira, assume-se que ele é robusto. A ausência de erros visíveis mascara falhas lógicas de segurança.

**Falta de Revisão Humana Profunda (_Code Review_)**: Sob pressão de prazos agressivos, equipes aceitam *Pull Requests* (PRs) gigantescos contendo código gerado por IA sem auditar o tratamento de erros e o saneamento de entradas.

**Ausência de Contexto de Negócio**: Modelos de IA não conhecem o modelo de ameaças específico do produto ou a sensibilidade dos dados da empresa, aplicando soluções genéricas que violam o princípio do privilégio mínimo.

## 5. Conclusão

A inteligência artificial e os frameworks modernos não são o problema em si, mas ferramentas que amplificam tanto a produtividade quanto os erros estruturais humanos. Para mitigar a onda de vulnerabilidades clássicas impulsionadas pela automação desregrada, recomenda-se:

1. **Tratar a IA como um estagiário sênior**: Excelente para gerar código repetitivo (*boilerplate*), mas sob supervisão estrita de segurança.

2. **Integrar SAST (_Static Application Security Testing_) no pipeline CI/CD**: Automatizar a detecção de padrões inseguros antes que o código chegue ao repositório principal.

3. **Resgatar a cultura de revisão de código**: Questionar ativamente não apenas se o código funciona, mas de que forma ele pode ser manipulado por um atacante mal-intencionado.

## <ins> Referências e Leituras Recomendadas </ins>

* **GitClear (2025)**: Pesquisa longitudinal sobre qualidade de código, duplicação e impacto de assistentes de IA em repositórios corporativos.

* **Google DevOps Research and Assessment (DORA) Report**: Análise sobre estabilidade de entrega e taxas de defeito correlacionadas à automação de desenvolvimento.

* **Cloud Security Alliance (CSA) & arXiv (2025)**: Estudos empíricos sobre a incidência de vulnerabilidades mapeadas pelo CWE Top 25 em código gerado por *Large Language Models* (LLMs).

* **OWASP Top 10**: Referência padrão para riscos de segurança em aplicações web e APIs.
