# DesafioTelecom_X2_br.ipynb
DesafioTelecom_X2_br.ipynb
Análise e Previsão de Churn de Clientes de Telecomunicações
Visão Geral do Projeto
Este projeto tem como objetivo analisar e prever o churn (evasão) de clientes de uma empresa de telecomunicações. Através da exploração de um conjunto de dados abrangente, pré-processamento, análise exploratória de dados (EDA) e treinamento de modelos de aprendizado de máquina, buscamos identificar os fatores que contribuem para o churn e desenvolver um modelo capaz de prever quais clientes estão em maior risco de evasão.

Estrutura do Conjunto de Dados
O conjunto de dados inicial (dados_tratados.csv) é composto por 7043 linhas e 22 colunas, sem valores nulos. As colunas contêm informações detalhadas sobre os clientes, incluindo:

Informações Demográficas: Gênero, se é idoso (SeniorCitizen), se tem parceiro (Partner), se tem dependentes (Dependents).
Serviços Contratados: Serviço de telefone (PhoneService), múltiplas linhas (MultipleLines), tipo de serviço de internet (InternetService), serviços adicionais de internet (segurança online, backup, proteção de dispositivo, suporte técnico, streaming de TV e filmes).
Informações de Contrato e Pagamento: Tempo de contrato em meses (Tenure), tipo de contrato (Contract), faturamento sem papel (PaperlessBilling), método de pagamento (PaymentMethod), cobranças mensais (ChargesMonthly) e totais (ChargesTotal).
Variável Alvo: Churn (indica se o cliente cancelou o serviço).
Metodologia
O projeto seguiu as seguintes etapas:

1. Pré-processamento dos Dados
Remoção de Colunas Irrelevantes: CustomerID (identificador único), ChargesDaily, ChargesTotal (altamente correlacionadas com ChargesMonthly), Gender e PhoneService (não significativas para o churn no teste Qui-quadrado) foram removidas.
Tratamento de Valores: Os valores 'No internet service' em colunas relacionadas a serviços foram padronizados para 'No' para consistência.
Verificação de Nulos: Confirmado que não havia valores nulos.
2. Análise Exploratória de Dados (EDA)
Correlação Numérica: Clientes com maior Tenure (tempo de contrato) tendem a churnar menos (correlação negativa de -0.35). ChargesMonthly apresentou uma baixa correlação positiva (0.19) com o churn.
Análise Categórica: Variáveis como Contract (mês a mês tem maior risco), OnlineSecurity e TechSupport (ausência aumenta o risco), InternetService (fibra óptica com maior churn), SeniorCitizen (idosos com maior propensão), PaperlessBilling e PaymentMethod (cheque eletrônico com maior churn) foram identificadas como principais indicadores de churn.
3. Seleção de Variáveis
O Teste Qui-quadrado foi aplicado para identificar variáveis categóricas com associação estatisticamente significativa ao churn (p-value < 0.05). Todas as variáveis, exceto Gender e PhoneService, foram consideradas significativas e mantidas para a modelagem.
4. Divisão e Codificação dos Dados
Os dados foram divididos em conjuntos de treino (80%) e teste (20%) com estratificação (stratify=y) para manter a proporção da variável alvo Churn.
One-Hot Encoding foi aplicado às variáveis categóricas para convertê-las em formato numérico, com drop_first=True para evitar multicolinearidade. Os conjuntos de treino e teste foram alinhados para garantir consistência nas colunas.
5. Modelagem e Avaliação
Foram treinados e avaliados dois modelos de classificação:

Regressão Logística (Modelo Normal):

Precisão (Churn 'Yes'): 0.65
Recall (Churn 'Yes'): 0.52
F1-Score (Churn 'Yes'): 0.58
Acurácia Geral: 0.80
Random Forest:

Precisão (Churn 'Yes'): 0.62
Recall (Churn 'Yes'): 0.48
F1-Score (Churn 'Yes'): 0.54
Acurácia Geral: 0.78
Regressão Logística (Modelo Balanceado com class_weight='balanced'):

Precisão (Churn 'Yes'): 0.51
Recall (Churn 'Yes'): 0.79 (Aumento significativo)
F1-Score (Churn 'Yes'): 0.62
Acurácia Geral: 0.74
O balanceamento de classes foi crucial, pois o recall para a classe 'Yes' (churn) aumentou significativamente de 0.52 para 0.79 no modelo de Regressão Logística. Embora a precisão tenha diminuído, a capacidade de identificar mais clientes que realmente irão churnar é mais valiosa neste contexto.

Principais Insights e Recomendações
Contratos Mês a Mês: Clientes com este tipo de contrato representam o maior risco de churn. Estratégias de retenção devem focar em oferecer incentivos para contratos de longo prazo.
Serviços de Segurança e Suporte: A ausência de OnlineSecurity e TechSupport é um forte indicador de churn. Promover esses serviços ou incluí-los como parte de pacotes básicos pode reduzir a evasão.
Clientes Idosos e Sem Dependentes: SeniorCitizen e Dependents (clientes sem dependentes) são grupos com maior propensão a churnar. Campanhas direcionadas e personalizadas podem ser eficazes.
Método de Pagamento: O Electronic check está associado a altas taxas de churn. Investigar insatisfações ou fricções com este método e oferecer alternativas atraentes.
Serviço de Internet Fibra Óptica: A maior taxa de churn entre usuários de fibra óptica pode indicar problemas de serviço ou expectativas não atendidas. A qualidade do serviço e o suporte devem ser aprimorados para este segmento.
Clientes de Alto Risco de Churn
Com base no modelo de Regressão Logística balanceado, os 10 clientes com maior risco de evasão foram identificados, com suas respectivas probabilidades de churn:

CustomerID	Churn_Probability
9497-QCMMS	0.948357
9300-AGZNL	0.947937
4424-TKOPW	0.946475
7024-OHCCK	0.946475
2720-WGKHP	0.946331
5178-LMXOP	0.943828
5150-ITWWB	0.943827
7216-EWTRS	0.942768
1374-DMZUI	0.942670
8098-LLAZX	0.941477
Próximos Passos: Recomenda-se que ações proativas de retenção sejam desenvolvidas e aplicadas imediatamente a esses clientes de alto risco. Isso pode incluir ofertas personalizadas, contato direto da equipe de suporte ou programas de fidelidade específicos.

