# Tech Challenge Fase 1: Case NPS Preditivo no E-commerce

## 1. Objetivo do Projeto

O crescimento acelerado do e-commerce nacional trouxe ganhos de escala, mas também desafios na experiência do cliente, refletidos na alta variabilidade do Net Promoter Score (NPS). Atualmente, o NPS é coletado apenas após a jornada de compra, limitando a proatividade da empresa.

O objetivo principal deste projeto é transformar dados operacionais em insights acionáveis para o negócio. Buscamos compreender quais fatores operacionais (como logística, atendimento e pedidos) influenciam a satisfação do cliente, identificar os perfis de promotores e detratores, e propor recomendações estratégicas de melhoria. Adicionalmente, exploramos a criação de um modelo preditivo capaz de estimar o NPS antes da aplicação da pesquisa, permitindo que a empresa atue de forma preventiva.

---

## 2. Descrição da Base de Dados

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

## 3. Estrutura do Repositório

Para garantir as boas práticas de organização do código, o projeto está estruturado da seguinte maneira:

```text
├── data/               # Diretório contendo os arquivos CSV (dados brutos e processados)
├── notebooks/          # Jupyter Notebooks com os códigos de EDA e modelagem, documentados e comentados
├── reports/            # Material de apresentação gerencial (Slides em PDF/PPTX) e link para o vídeo
├── README.md           # Documentação principal do projeto
└── requirements.txt    # The requirements file for reproducing the analysis environment
```

---

## 4. Metodologia Utilizada

A resolução do desafio foi dividida nas seguintes etapas, focando no pensamento analítico e no storytelling com dados.

---

### Entendimento do Negócio: A Transição do NPS Reativo para o Preditivo

A incapacidade de agir preventivamente é a dor central identificada. No modelo tradicional de e-commerce, o monitoramento da satisfação ocorre via pesquisas pós-venda, o que cria um atraso informacional crítico. Quando um cliente responde à pesquisa de NPS demonstrando insatisfação por um atraso logístico ou um erro no pedido, ele já percorreu toda a jornada de frustração. O dano ao Customer Lifetime Value (LTV) já está em curso.

---

### A Importância Estratégica do NPS no E-commerce

No contexto competitivo do varejo digital, o NPS atua como um indicador antecedente de saúde financeira. A lealdade do consumidor correlaciona-se diretamente com a redução do Custo de Aquisição de Cliente (CAC).

Clientes satisfeitos não apenas retornam com maior frequência, mas também atuam como embaixadores da marca, gerando o marketing "boca a boca" que é o motor de crescimento mais eficiente do setor.

Clientes promotores possuem maior recorrência. A detração interrompe o ciclo de receita por cliente.

A análise estratégica revela que a detração interrompe o ciclo de receita por cliente de forma abrupta. Um detrator custa significativamente mais para ser reconquistado do que um promotor para ser mantido.

No Brasil, onde o faturamento do e-commerce atingiu R$ 160 bilhões no primeiro semestre de 2024, a capacidade de reter clientes por meio de um NPS alto permite que a empresa capture fatias de mercado (market share) de concorrentes com operações menos eficientes e menos centradas no cliente.

---

### Áreas Beneficiadas pela Visão Preditiva

A transformação do NPS em um modelo preditivo gera benefícios transversais em toda a organização, permitindo que diferentes departamentos ajam de forma coordenada:

#### Logística

O departamento pode realizar o ajuste dinâmico de rotas e prazos prometidos baseados em "pontos de ruptura" de atraso identificados pelo modelo.

#### Atendimento ao Cliente (Customer Service)

A identificação precoce de clientes com alto risco de detração permite um contato preventivo.

#### Produto e Pricing

O modelo auxilia na avaliação se a qualidade percebida do item ou o valor do frete compensam eventuais falhas logísticas.

Para contextualizar o desempenho interno, a organização deve utilizar indicadores complementares de mercado.

---

### Metas de Negócio vs. Metas Analíticas: Definindo a Régua do Sucesso

Uma das distinções mais críticas em um projeto de ciência de dados é a separação entre o que o negócio deseja alcançar e como a equipe técnica medirá o progresso.

---

### Metas de Negócio e KPIs Estratégicos

As metas de negócio são formuladas em termos de indicadores estratégicos (Key Performance Indicators - KPIs) que impactam diretamente o lucro e a vantagem competitiva da empresa.

As principais metas incluem:

- Redução da Taxa de Detração: Diminuir a proporção de clientes que atribuem notas de 0 a 6 para Y% ao ano.
- Aumento do Customer Lifetime Value (LTV): Elevar o valor total gerado pelo cliente ao longo do relacionamento com a marca, através da fidelização.
- Otimização do ROI de Retenção: Garantir que o custo das ações preventivas seja inferior ao custo de perda desses clientes.

---

### Definição da Target

No âmago da construção de uma solução de dados completa está a definição precisa da variável alvo (target). No projeto em questão, a variável alvo é o nps_score.

---

### A Variável NPS_Score e seu Momento de Coleta

O nps_score foi escolhido por ser a métrica padrão para medir a lealdade do consumidor.

Os clientes são categorizados em três grupos fundamentais:

- Promotores (9-10): Clientes leais e entusiastas que impulsionam o crescimento orgânico através de recomendações.
- Neutros (7-8): Clientes satisfeitos, mas sem engajamento emocional, vulneráveis a ofertas da concorrência.
- Detratores (0-6): Clientes insatisfeitos que podem prejudicar a reputação da marca através de comentários negativos.

A informação é coletada após o encerramento da jornada de compra, geralmente via e-mail ou SMS após a confirmação da entrega (last-mile delivery).

---

### Riscos de Uso Inadequado e Armadilhas Estatísticas

- Lagging Indicator e Ação Tardia
- Viés de Seleção (Selection Bias)
- Leakage (Vazamento de Informação)
- Target Drift

---

### Análise Exploratória (EDA): Decifrando os Direcionadores da Detração

A análise exploratória conduzida via Python focou em identificar as raízes operacionais da insatisfação.

---

### Fatores Críticos e Pontos de Ruptura

| Variável Operacional      | Relação com o NPS_Score     | Insight de Negócio                                                                                   |
| ------------------------- | --------------------------- | ---------------------------------------------------------------------------------------------------- |
| delivery_delay_days       | Correlação Negativa Forte   | O atraso é o principal gatilho de detração. A incerteza incomoda mais que o prazo longo.             |
| delivery_attempts         | Impacto Exponencial         | Múltiplas tentativas frustradas geram fricção elevada na última milha e aumentam o custo de suporte. |
| customer_service_contacts | Indicador de Atrito         | Cada contato adicional com o SAC correlaciona-se com uma queda média na nota de satisfação.          |
| resolution_time_days      | Determinante de Recuperação | Prazos de resolução superiores a 48 horas tornam a recuperação de um detrator quase impossível.      |

---

## 5. Requisitos de Execução

1. Clonar o repositório.
2. Instalar dependências: pandas, seaborn, matplotlib.
3. Executar o notebook principal em notebooks/.

---

## 6. Referencias

- https://www.medallia.com/br/puntuacion-neta-del-promotor/
- https://www.adtail.ag/post/estatisticas-ecommerce-webshoppers-2024-2025
- https://paymentscmi.com/insights/brazil-e-commerce-market/
