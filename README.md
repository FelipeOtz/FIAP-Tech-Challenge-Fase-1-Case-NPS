# Tech Challenge Fase 1: Case NPS Preditivo no E-commerce

## 1. Objetivo do Projeto

O objetivo principal deste projeto é transformar dados operacionais em insights acionáveis para o negócio. Buscamos compreender quais fatores operacionais (como logística, atendimento e pedidos) influenciam a satisfação do cliente, identificar os perfis de promotores e detratores, e propor recomendações estratégicas de melhoria. Adicionalmente, exploramos a criação de um modelo preditivo capaz de estimar o NPS antes da aplicação da pesquisa, permitindo que a empresa atue de forma preventiva.

O crescimento acelerado do e-commerce nacional trouxe ganhos de escala, mas também desafios na experiência do cliente, refletidos na alta variabilidade do Net Promoter Score (NPS). Atualmente, o NPS é coletado apenas após a jornada de compra, limitando a proatividade da empresa.

---

## 2. Escopo Adotado no Projeto

Conforme os requisitos oficiais do Tech Challenge Fase 1, a proposta de desenvolvimento de um modelo preditivo para estimativa do NPS foi apresentada como uma etapa opcional, com objetivo de ampliar a maturidade analítica e técnica dos participantes, sem impacto negativo para aqueles que optassem por não implementá-la.

Diante desse direcionamento, este projeto concentrou seus esforços nas etapas obrigatórias do desafio, priorizando:

- Entendimento do negócio;
- Definição da variável alvo (target);
- Análise Exploratória dos Dados (EDA) com foco em negócio;
- Identificação de padrões operacionais relacionados à satisfação do cliente;
- Construção de recomendações estratégicas orientadas por dados.

A decisão de não implementar modelos preditivos nesta fase foi intencional e alinhada ao escopo proposto pelo desafio, permitindo aprofundar a análise estratégica, o pensamento analítico e o storytelling com dados, que representam os principais objetivos de aprendizagem desta etapa.

Como preparação para fases futuras, ao longo do documento também são apresentadas reflexões sobre possíveis abordagens preditivas que poderiam ser exploradas em uma evolução natural deste trabalho.

## 3. Descrição da Base de Dados

A base de dados utilizada consiste em um histórico de pedidos, entregas e interações com o atendimento ao cliente. As variáveis disponíveis (Dicionário de Dados) são:

- customer_id: Identificador único do cliente.
- order_id: Identificador único do pedido.
- customer_age: Idade do cliente.
- customer_region: Região geográfica do cliente.
- customer_tenure_months: Tempo de relacionamento do cliente com a empresa (em meses).
- order_value: Valor total do pedido.
- items_quantity: Quantidade de itens no pedido.
- discount_value: Valor de desconto aplicado ao pedido.
- payment_installments: Número de parcelas do pagamento.
- delivery_time_days: Tempo total de entrega (em dias).
- delivery_delay_days: Quantidade de dias de atraso na entrega.
- freight_value: Valor do frete.
- delivery_attempts: Número de tentativas de entrega.
- customer_service_contacts: Número de contatos do cliente com o atendimento.
- resolution_time_days: Tempo para resolução de problemas (em dias).
- complaints_count: Número de reclamações registradas pelo cliente.
- repeat_purchase_30d: Indica se houve recompra em até 30 dias após o pedido (0 = não, 1 = sim).
- csat_internal_score: Score interno de satisfação do cliente.
- nps_score: Nota de satisfação do cliente (NPS), variando de 0 a 10, coletada após a experiência de compra (Variável Alvo).

---

## 4. Estrutura do Repositório

Para garantir as boas práticas de organização do código, o projeto está estruturado da seguinte maneira:

```text
├── data/               # Diretório contendo os arquivos CSV (dados brutos e processados)
├── notebooks/          # Jupyter Notebooks com os códigos de EDA e modelagem, documentados e comentados
├── reports/            # Material de apresentação gerencial (Slides em PPTX) e link para o vídeo
├── README.md           # Documentação principal do projeto
└── requirements.txt    # Arquivo de requisitos para reproduzir o ambiente de análise.
```

---

## 5. Metodologia Utilizada

A resolução do desafio foi dividida nas seguintes etapas, focando no pensamento analítico e no storytelling com dados:

### 5.1 Entendimento do Negócio: A Transição do NPS Reativo para o Preditivo

A incapacidade de agir preventivamente é a dor central identificada. No modelo tradicional de e-commerce, o monitoramento da satisfação ocorre via pesquisas pós-venda, o que cria um atraso informacional crítico. Quando um cliente responde à pesquisa de NPS demonstrando insatisfação por um atraso logístico ou um erro no pedido, ele já percorreu toda a jornada de frustração. O dano ao Customer Lifetime Value (LTV) já está em curso.

### A Importância Estratégica do NPS no E-commerce

No contexto competitivo do varejo digital, o NPS atua como um indicador antecedente de saúde financeira. A lealdade do consumidor correlaciona-se diretamente com a redução do Custo de Aquisição de Cliente (CAC).

Clientes satisfeitos não apenas retornam com maior frequência, mas também atuam como embaixadores da marca, gerando o marketing "boca a boca" que é o motor de crescimento mais eficiente do setor. A detração interrompe o ciclo de receita por cliente.

A análise estratégica revela que a detração interrompe o ciclo de receita por cliente de forma abrupta. Um detrator custa significativamente mais para ser reconquistado do que um promotor para ser mantido.

No Brasil, onde o faturamento do e-commerce atingiu R$ 160 bilhões no primeiro semestre de 2024, a capacidade de reter clientes por meio de um NPS alto permite que a empresa capture fatias de mercado (market share) de concorrentes com operações menos eficientes e menos centradas no cliente.

---

### 5.2 Áreas Beneficiadas pela Visão Preditiva

A transformação do NPS em um modelo preditivo gera benefícios transversais em toda a organização, permitindo que diferentes departamentos ajam de forma coordenada:

#### Logística

O departamento pode realizar o ajuste dinâmico de rotas e prazos prometidos baseados em "pontos de ruptura" de atraso identificados pelo modelo. Se os dados mostram que um atraso superior a dois dias em uma região específica invariavelmente gera detratores, a logística pode priorizar esses envios ou renegociar SLAs com transportadoras locais.

#### Atendimento ao Cliente (Customer Service)

A identificação precoce de clientes com alto risco de detração permite um contato preventivo. O time de suporte pode oferecer soluções proativas, como descontos ou estornos parciais do frete, antes que o cliente sinta a necessidade de abrir uma reclamação formal.

#### Produto e Pricing

O modelo auxilia na avaliação se a qualidade percebida do item ou o valor do frete compensam eventuais falhas logísticas. Em categorias de alto valor agregado, como eletrônicos, a tolerância a falhas na entrega é sensivelmente menor, exigindo uma precificação que suporte uma logística de excelência.

---

### 5.3 Metas de Negócio vs. Metas Analíticas: Definindo a Régua do Sucesso

Uma das distinções mais críticas em um projeto de ciência de dados é a separação entre o que o negócio deseja alcançar e como a equipe técnica medirá o progresso.

### Metas de Negócio e KPIs Estratégicos

As metas de negócio são formuladas em termos de indicadores estratégicos (Key Performance Indicators - KPIs) que impactam diretamente o lucro e a vantagem competitiva da empresa.

As principais metas incluem:

- Redução da Taxa de Detração: Diminuir a proporção de clientes que atribuem notas de 0 a 6 para Y% ao ano.
- Aumento do Customer Lifetime Value (LTV): Elevar o valor total gerado pelo cliente ao longo do relacionamento com a marca, através da fidelização.
- Otimização do ROI de Retenção: Garantir que o custo das ações preventivas seja inferior ao custo de perda desses clientes.

---

### 5.4 Definição da Target

No âmago da construção de uma solução de dados completa está a definição precisa da variável alvo (target). O target representa o fenômeno que o modelo tentará prever e deve refletir fielmente a dor de negócio original. No projeto em questão, a variável alvo é o nps_score.

### A Variável NPS_Score e seu Momento de Coleta

O nps_score foi escolhido por ser a métrica padrão para medir a lealdade do consumidor, correlacionando-se diretamente com o comportamento de compra futura. Ele funciona como o principal KPI de sucesso para a área de Experiência do Cliente. A coleta ocorre por meio da pergunta: "Em uma escala de 0 a 10, o quanto você recomendaria nossa empresa para um amigo ou colega?".

Os clientes são categorizados em três grupos fundamentais:

- Promotores (9-10): Clientes leais e entusiastas que impulsionam o crescimento orgânico através de recomendações.
- Neutros (7-8): Clientes satisfeitos, mas sem engajamento emocional, vulneráveis a ofertas da concorrência.
- Detratores (0-6): Clientes insatisfeitos que podem prejudicar a reputação da marca através de comentários negativos.

A informação é coletada após o encerramento da jornada de compra, geralmente via e-mail ou SMS após a confirmação da entrega (last-mile delivery). Essa janela temporal é crítica: se coletada muito cedo, ignora falhas na entrega; se coletada muito tarde, o sentimento do cliente pode ter sido diluído por outras experiências.

### Riscos de Uso Inadequado e Armadilhas Estatísticas

- Lagging Indicator e Ação Tardia: Tratar o NPS como um indicador de tempo real é o principal risco. Como ele é coletado após o fato, o uso isolado pode levar a decisões tardias. O modelo preditivo deve atuar como uma antecipação deste sinal.

- Viés de Seleção (Selection Bias): Existe uma tendência natural onde apenas os clientes nos extremos da experiência (muito satisfeitos ou muito irritados) respondem à pesquisa. Isso pode levar o modelo a otimizar para padrões extremos, ignorando a "maioria silenciosa" de clientes neutros ou passivos.

- Leakage (Vazamento de Informação): O uso de dados que não estariam disponíveis no momento da previsão. Por exemplo, incluir no treinamento do modelo se o cliente já respondeu à pesquisa ou se já recebeu um cupom de desculpas invalida a capacidade preditiva em produção, pois o modelo estaria "olhando o futuro".

- Target Drift: A distribuição da satisfação pode mudar devido a fatores macroeconômicos ou mudanças na concorrência, sem que a definição da variável mude. Se o mercado brasileiro se tornar mais exigente em relação ao frete, o mesmo serviço que gerava nota 9 em 2023 pode gerar nota 7 em 2025

### Estratégia de Categorização do NPS

Embora a variável `nps_score` represente a nota de satisfação do cliente em uma escala de 0 a 10, durante a análise exploratória foi identificado que os valores estavam armazenados em formato contínuo (`float`), permitindo a existência de valores decimais, como por exemplo 8.7 ou 9.3.

Para garantir consistência metodológica na classificação dos clientes e evitar perdas de informação decorrentes de arredondamentos artificiais, optou-se por não realizar qualquer arredondamento das notas.

A categorização foi realizada respeitando os intervalos clássicos do Net Promoter Score (NPS), aplicados diretamente sobre os valores contínuos:

- **Detrator:** notas menores que 7.0
- **Neutro/Passivo:** notas maiores ou iguais a 7.0 e menores que 9.0
- **Promotor:** notas maiores ou iguais a 9.0

Dessa forma, exemplos como:

- Nota **6.9** → Detrator
- Nota **8.7** → Neutro/Passivo
- Nota **9.1** → Promotor

---

### 5.5 Análise Exploratória (EDA): Decifrando os Direcionadores da Detração

A análise exploratória conduzida via Python focou em identificar as raízes operacionais da insatisfação. No contexto do e-commerce, os dados sugerem que a satisfação não é apenas uma função do produto, mas sim do cumprimento da promessa logística e da facilidade de resolução de problemas

---

### Fatores Críticos e Pontos de Ruptura

Os dados operacionais revelam que o atraso na entrega é o fator mais corrosivo para a lealdade. Cerca de 69% dos consumidores são menos propensos a comprar novamente de um varejista se o item não chegar no prazo prometido. No entanto, a análise identifica "pontos de ruptura" específicos. Um atraso de um dia pode ser tolerado por um promotor antigo, mas o impacto na probabilidade de detração aumenta drasticamente a partir do terceiro dia de atraso, especialmente para novos clientes.

| Variável Operacional      | Relação com o NPS_Score     | Insight de Negócio                                                                                   |
| ------------------------- | --------------------------- | ---------------------------------------------------------------------------------------------------- |
| delivery_delay_days       | Correlação Negativa Forte   | O atraso é o principal gatilho de detração. A incerteza incomoda mais que o prazo longo.             |
| delivery_attempts         | Impacto Exponencial         | Múltiplas tentativas frustradas geram fricção elevada na última milha e aumentam o custo de suporte. |
| customer_service_contacts | Indicador de Atrito         | Cada contato adicional com o SAC correlaciona-se com uma queda média na nota de satisfação.          |
| resolution_time_days      | Determinante de Recuperação | Prazos de resolução superiores a 48 horas tornam a recuperação de um detrator quase impossível.      |

---

## 6. Requisitos de Execução

1. Clonar o repositório.
2. Instalar dependências:
```pip install -r requirements.txt```
3. Executar o notebook principal em notebooks/.

---

## 7. Referencias

- https://www.medallia.com/br/puntuacion-neta-del-promotor/
- https://www.adtail.ag/post/estatisticas-ecommerce-webshoppers-2024-2025
- https://paymentscmi.com/insights/brazil-e-commerce-market/
