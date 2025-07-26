# Decifrando a Caixa Preta: Tornando Modelos de IA Explicáveis com LIME

## Contextualização do Problema
Modelos preditivos são amplamente utilizados em análise de crédito para avaliar o risco de clientes. No entanto, apesar de alcançarem alta precisão, muitos desses modelos são "caixas-pretas", tornando difícil entender como chegam às suas decisões. Essa falta de transparência gera desconfiança em clientes, gestores e órgãos regulatórios, especialmente em casos de **negação de crédito**.

Para atender às demandas de **compliance** e confiança, este projeto aplica **técnicas de Explainable AI (XAI)** utilizando a biblioteca **LIME (Local Interpretable Model-Agnostic Explanations)**, que fornece explicações locais sobre como cada variável (como idade, renda, histórico de crédito, etc.) influenciou a decisão para cada cliente.

## Objetivo
- Treinar um modelo preditivo de classificação de risco de crédito usando o dataset **Statlog (German Credit Data)**.
- Aplicar **LIME** para explicar previsões individuais.
- Mostrar visualmente quais características mais impactaram as decisões do modelo.
- Discutir **limitações, distorções e benefícios** do uso de LIME na prática.

## Modelo Preditivo
O modelo escolhido foi um **Random Forest Classifier**, pois:
- Tem bom desempenho em problemas de classificação binária.
- Captura relações não lineares entre variáveis.
- É robusto contra overfitting, especialmente com tuning de hiperparâmetros.

## Dataset
- **Fonte**: [UCI Machine Learning Repository – Statlog (German Credit Data)](https://archive.ics.uci.edu/ml/datasets/statlog+(german+credit+data))
- **Tamanho**: 1.000 amostras e 20 atributos (numéricos e categóricos).
- **Tarefa**: Classificação binária (bom vs. mau risco de crédito).

## Como o LIME Foi Aplicado
- Utilizamos `lime.lime_tabular.LimeTabularExplainer`.
- Para cada previsão (ex.: negação de crédito), o LIME gera uma explicação mostrando:
  - Variáveis que mais aumentaram a probabilidade de aprovação ou reprovação.
  - Gráficos destacando o impacto local de cada variável.

Exemplo de saída (cliente analisado):
- Renda baixa (+0.20 na probabilidade de reprovação)
- Idade < 30 anos (+0.15)
- Bom histórico de crédito (-0.25)

Esses pesos ajudam a entender **por que o modelo negou ou aprovou crédito**.

## Reflexões e Limitações
- **Importância**: Explicações permitem que o banco justifique decisões, evitando desconfiança e ajudando em auditorias.
- **Limitações**:
  - O LIME cria explicações locais baseadas em aproximações lineares, o que pode distorcer a lógica global do modelo.
  - As explicações podem variar dependendo dos parâmetros do LIME (número de amostras, vizinhança simulada).
  - Exige cuidado para não induzir interpretações equivocadas.

## Como Executar o Projeto
1. Clone o repositório:
   ```bash
   git clone https://github.com/gasdp-ofc/credit-xai-lime.git
   cd credit-xai-lime
