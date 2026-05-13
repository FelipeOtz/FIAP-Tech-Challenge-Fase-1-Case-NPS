# Resumo Geral do Notebook: Análise Exploratória dos Dados (EDA) para NPS

Este notebook realiza uma **Análise Exploratória de Dados (EDA)** abrangente para um projeto de Net Promoter Score (NPS) em um contexto de e-commerce. O foco principal é transformar dados operacionais em insights acionáveis sobre a satisfação do cliente, identificando fatores que influenciam o NPS, perfis de promotores e detratores, pontos de ruptura na experiência e recomendações estratégicas. O notebook foi executado com sucesso, gerando estatísticas, visualizações interativas (usando Plotly) e interpretações gerenciais.

## Estrutura e Metodologia
- **Setup Inicial**: Importação de bibliotecas (Pandas, NumPy, Plotly, Seaborn, Matplotlib) e configuração de estilos visuais limpos para apresentações executivas.
- **Carregamento de Dados**: Base de dados carregada de `../data/desafio_nps_fase_1.csv`, com inspeção inicial (shape: linhas e colunas, tipos de dados, valores nulos e duplicados). Não há duplicados significativos.
- **Engenharia de Recursos**: Criação de colunas derivadas, como `nps_class` (categorização em Promotor, Neutro, Detrator) e faixas etárias/regionais para análises segmentadas.
- **Análises Realizadas**:
  - Estatísticas descritivas do NPS (média, mediana, desvio padrão, distribuição).
  - Correlações entre variáveis numéricas e NPS.
  - Visualizações focadas em fatores operacionais, pontos de ruptura e perfis de clientes.
  - Matriz de cascata para interações entre atrasos e reclamações.

## Principais Descobertas e Resultados
1. **Visão Geral do NPS**:
   - **Distribuição**: Média do NPS ≈ 4.38.
   - **Categorização**: Clientes classificados em Promotor (nota ≥9), Neutro (7-8) e Detrator (<7). Ordem visual priorizada para gráficos.

2. **Fatores Críticos para a Satisfação**:
   - **Correlações Gerais**: Fatores que pioram o NPS incluem atraso na entrega (`delivery_delay_days`) e volume de reclamações (`complaints_count`). Fatores que melhoram incluem pontuação interna de satisfação (CSAT, `csat_internal_score`).
   - **Foco Operacional**: Após remover variáveis de "efeito" (como recompra), a logística emerge como gargalo principal. Atraso na entrega é o maior vilão; CSAT interno é o maior impulsionador.
   - **Interpretação**: Correlação ≠ causalidade; foco em causas controláveis pela empresa.

3. **Pontos de Ruptura na Experiência do Cliente**:
   - **Atraso na Entrega**: Mesmo sem atraso (0 dias), NPS médio = 6.86 (Neutro/Detrator). Ruptura imediata no dia 1 (cai para 5.55), piorando ~1 ponto por dia extra. Aos 8 dias, NPS = 0.
   - **Reclamações**: Sem reclamações, NPS = 8.52 (Promotor). 1 reclamação = 7.77 (Neutro). 2 reclamações = 6.05 (fronteira Detrator). 3+ = 4.91 ou menos (Detrator consolidado).
   - **Efeito Cascata (Matriz de Risco)**: Heatmap interativo mostra interação entre atraso e reclamações. Tolerância alta se não houver SAC (até 2 dias de atraso com 0-1 reclamação mantém NPS ~7.6). Mas 6+ reclamações levam a detração (NPS ~4.8) mesmo sem atraso. Ponto de ruptura real: quando falha logística força múltiplas reclamações.

4. **Perfis de Clientes (NPS Alto vs. Baixo)**:
   - **Por Região**: NPS médio consistente e baixo (~4.1-4.5) em todas as regiões (ex.: Sudeste, Nordeste, etc.). Problema sistêmico, não localizado.
   - **Por Idade**: Semelhante, NPS baixo em todas as faixas (18-25, 26-35, etc.). Não há perfil etário mais satisfeito.
   - **Perfil de Promotores**: Associado a alto CSAT interno (9-10), com NPS médio elevado. Gráfico de barras confirma impacto direto: baixo CSAT → baixo NPS; alto CSAT → alto NPS.

## Interpretações e Insights Gerenciais
- **Problema Sistêmico**: A base está comprometida; entregar no prazo não cria promotores. Logística e SAC são os maiores gargalos. A experiência básica (produto, navegação) não encanta.
- **Tolerância Zero a Atritos**: Clientes perdoam atrasos curtos se não precisarem reclamar, mas burocracia no SAC destrói a lealdade mais que atrasos.
- **Recomendações Implícitas**: Priorizar redução de atrasos e reclamações; investir em CSAT interno para gerar promotores. Foco em resolução rápida no SAC para evitar cascata de detração.

## Limitações e Próximos Passos
- Análise correlacional; sugere causalidade, mas não prova (recomenda testes A/B ou modelagem preditiva).
- Dados parecem limpos, mas sem outliers tratados explicitamente.
- Próximos passos sugeridos: Modelagem preditiva (regressão para NPS), segmentação avançada ou dashboards interativos.
