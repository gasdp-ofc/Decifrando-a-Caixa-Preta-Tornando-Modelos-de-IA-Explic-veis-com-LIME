# Decifrando a Caixa Preta: LIME aplicado ao German Credit (Statlog)

## Resumo executivo
Este projeto demonstra como gerar **explicações locais** para decisões de um modelo de crédito usando **LIME** (Local Interpretable Model-agnostic Explanations). O objetivo é fornecer transparência em decisões automáticas — especialmente negações de crédito — para clientes, gestores e órgãos regulatórios.

O dataset utilizado é o **Statlog (German Credit)** (UCI) — 1.000 amostras com ~20 atributos que descrevem informações sociodemográficas e financeiras dos solicitantes.

---

## Estrutura do repositório
- `Projeto_XAI_LIME_GermanCredit.py` — script principal (treino do modelo, avaliação, geração de explicações LIME e salvamento de outputs).
- `tune_and_compare.py` — script para busca de hiperparâmetros e comparação entre modelos (RandomForest, HistGradientBoosting, LogisticRegression).
- `notebook_for_video.ipynb` — notebook indicado para apresentação e gravação do vídeo (contém células prontas).
- `requirements.txt` — dependências do projeto.
- `outputs/` — diretório onde são salvas matrizes de confusão, relatórios, imagens e arquivos HTML com explicações do LIME.

---

## Objetivos do trabalho
1. Treinar um classificador para prever risco de crédito (bom vs mau).
2. Gerar **explicações locais** (com LIME) que mostrem quais features influenciaram cada previsão.
3. Interpretar e discutir as explicações, ressaltando uso prático e limitações.
4. Preparar material (código, README e roteiro) para apresentação (vídeo de até 4 minutos).

---

## Abordagem técnica (resumo)
1. **Pré-processamento**
   - Separar colunas numéricas e categóricas.
   - Aplicar `OneHotEncoder` para variáveis categóricas (handle_unknown='ignore').
   - Pipeline do scikit-learn com `ColumnTransformer` para garantir reprodutibilidade.
2. **Modelagem**
   - Modelo principal: `RandomForestClassifier` (boa baseline para dados tabulares).
   - Alternativas testadas no `tune_and_compare.py`: `HistGradientBoostingClassifier` e `LogisticRegression`.
   - Validação: `train_test_split` estratificado e métricas como accuracy, precision, recall, f1-score e matriz de confusão.
3. **Interpretabilidade**
   - `lime.lime_tabular.LimeTabularExplainer`: explica decisões **localmente** ao gerar um modelo linear sobre uma vizinhança sintetizada da instância.
   - Gerar explicações para casos específicos (ex.: cliente negado) e salvar HTML/PNG para apresentação.
4. **Entrega**
   - Salvamos explicações como HTML (visual interativo) e imagens PNG para inclusão no relatório/vídeo.

---

## Exemplo de uso (resumo rápido)
1. Criar ambiente virtual e instalar dependências:
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
```
2. Baixar dataset `german.data` (UCI Statlog) e colocá-lo na raiz do projeto (ou usar a função `download_dataset()` presente no notebook/script).
3. Executar:
```bash
python Projeto_XAI_LIME_GermanCredit.py
```
4. Verificar `outputs/` (classification_report, confusion_matrix.png, lime_explanation_idxX.html, etc).

---

## Interpretação prática das explicações (como usar com stakeholders)
- **Para um cliente:** mostrar as 3–5 features que mais influenciaram a decisão e traduzir tecnicamente (ex.: "histórico de crédito: ruim" => alto peso para negar).
- **Para compliance:** manter registro das explicações por decisão, demonstrando que cada negação foi baseada em variáveis mensuráveis.
- **Para time de produto/negócios:** agregar explicações (contar features recorrentes) para detectar vieses ou problemas de dados.

---

## Limitações e cuidados
- **Localidade:** LIME explica uma vizinhança local — explicações não garantem comportamento global do modelo.
- **Instabilidade:** pequenas mudanças no seed, no pré-processamento ou nas amostras sintéticas podem alterar explicações.
- **Correlações entre features:** LIME assume independência local ao perturbar features; se há fortes correlações, as explicações podem ser enganosas.
- **Dados sensíveis:** certifique-se de não usar features legalmente protegidas na decisão sem controle (ex.: gênero/raça), e registre justificativas de uso.
- **Auditoria:** use LIME como parte de um processo maior (logs, avaliações globais como SHAP, fairness checks, testes com contrafactuals).

---

## Sugestões de melhorias futuras
- Comparar LIME com SHAP (explicação local vs. explicação baseada em valores SHAP).
- Implementar análise global: feature importance, partial dependence plots e análise de equidade (fairness).
- Pipeline de monitoramento de explicações em produção (salvar explicação por transação, monitorar drift).
- Testes de estabilidade: rodar LIME múltiplas vezes e medir variância nas importâncias.

---

## Referências
- Ribeiro, M.T., Singh, S., & Guestrin, C. (2016). *"Why Should I Trust You? Explaining the Predictions of Any Classifier"*. arXiv:1602.04938.
- LIME documentation: https://marcotcr.github.io/lime/tutorials.html
- UCI Machine Learning Repository — Statlog (German Credit Data): https://archive.ics.uci.edu/
- Blog: *Explainable AI with LIME and SHAP* (Towards Data Science)

---




## 📊 Estrutura do Projeto

O repositório foi organizado da seguinte forma:

```
.
├── data/
│   └── german_credit_data.csv       # Dataset original
├── images/
│   ├── lime_example_1.png           # Exemplo de explicação LIME
│   ├── lime_example_2.png           # Outro exemplo visual
├── Projeto_XAI_LIME_Notebook.ipynb  # Notebook principal com código e análise
├── requirements.txt                 # Dependências do projeto
└── README.md                        # Documentação do projeto
```

---

## 🛠️ Passo a Passo do Projeto

1. **Coleta de Dados**  
   Utilizamos o dataset Statlog (German Credit Data) disponibilizado pela UCI Machine Learning Repository.

2. **Pré-processamento**  
   - Tratamento de valores nulos (quando necessário)
   - Codificação de variáveis categóricas com *OneHotEncoder*
   - Normalização de atributos numéricos

3. **Treinamento do Modelo**  
   Foi utilizada uma **Random Forest Classifier** para prever se um cliente é "bom" ou "mau" pagador.

4. **Aplicação do LIME**  
   - Escolha de instâncias individuais para explicar
   - Geração de explicações locais
   - Visualização dos pesos atribuídos a cada feature

5. **Análise dos Resultados**  
   - Interpretação das features mais relevantes
   - Comparação entre diferentes previsões
   - Discussão de limitações

---

## 📌 Exemplo de Saída do LIME

Abaixo, um exemplo fictício de explicação LIME:

![Exemplo LIME](images/lime_example_1.png)

**Interpretação:**  
- **Idade > 40 anos** → aumentou a probabilidade de bom crédito (+0.18)  
- **Histórico de inadimplência recente** → reduziu a probabilidade (-0.25)  
- **Renda acima da média** → impacto positivo (+0.12)

---

## ⚠️ Limitações do Estudo

- O LIME fornece explicações **locais**, ou seja, válidas apenas para a instância analisada.  
- A escolha do número de features exibidas pode afetar a interpretação.  
- Modelos muito complexos podem gerar explicações menos consistentes.

---

## 📚 Referências

- Ribeiro, M. T., Singh, S., & Guestrin, C. (2016). *"Why Should I Trust You?": Explaining the Predictions of Any Classifier*. arXiv preprint arXiv:1602.04938.  
- Documentação oficial do LIME: https://marcotcr.github.io/lime/tutorials.html  
- Dataset: UCI Machine Learning Repository - Statlog (German Credit Data)  
- Blog *Towards Data Science*: https://towardsdatascience.com/explainable-ai-with-lime-shap-7e8d3bfaac8e

---

## ✅ Conclusão

Este projeto demonstrou como é possível combinar **modelos preditivos de Machine Learning** com **técnicas de interpretabilidade** para oferecer explicações claras e úteis sobre decisões algorítmicas.  
O uso do LIME permitiu identificar quais variáveis tiveram maior impacto em cada decisão, oferecendo **transparência** e **confiança** tanto para usuários quanto para órgãos regulatórios.

A aplicação prática desse tipo de abordagem é fundamental em setores como:
- **Bancos e Finanças** (crédito e empréstimos)
- **Saúde** (diagnóstico assistido por IA)
- **Seguros** (avaliação de risco)

Com isso, reforçamos que a **IA explicável** é um passo essencial para adoção segura e responsável de algoritmos na sociedade.
