# Decifrando a Caixa Preta: Tornando Modelos de IA Explicáveis com LIME

## 1. Contextualização do Problema
A utilização crescente de modelos preditivos no setor bancário, especialmente para análise de risco de crédito, tem revelado um desafio crítico: a necessidade de interpretar e justificar decisões automatizadas. Modelos com alta precisão podem ser considerados 'caixas-pretas', dificultando a transparência exigida por clientes, gestores e órgãos reguladores.

## 2. Objetivos
Este projeto visa desenvolver um modelo preditivo de classificação de risco de crédito e aplicar a técnica Explainable AI (XAI) por meio da biblioteca LIME para gerar explicações locais das decisões do modelo, aumentando a confiança e a transparência.

## 3. Metodologia
- Dataset utilizado: Statlog (German Credit Data), disponível na UCI Machine Learning Repository.
- Modelo preditivo: Random Forest Classifier treinado para classificar clientes em bom ou mau risco de crédito.
- Técnica de interpretabilidade: LIME para gerar explicações locais, evidenciando os atributos que influenciam a decisão para cada instância.

## 4. Resultados
O modelo atingiu uma acurácia satisfatória, com capacidade de discriminação entre classes. As explicações geradas pelo LIME permitiram identificar os principais fatores que influenciaram cada decisão individual, facilitando a análise e comunicação dos resultados.

## 5. Discussão
A aplicação do LIME mostrou-se útil para compreender decisões específicas, porém apresenta limitações, como sua natureza local e possíveis distorções. É recomendado utilizar múltiplas técnicas de interpretabilidade para garantir maior robustez.

## 6. Instruções para Execução
1. Crie um ambiente virtual e ative-o.
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute o script principal: `python main.py`
4. As imagens com as explicações locais estarão na pasta `outputs/`.

## 7. Referências
- Ribeiro, M.T., Singh, S., & Guestrin, C. (2016). "Why Should I Trust You? Explaining the Predictions of Any Classifier". arXiv preprint arXiv:1602.04938.
- Documentação oficial do LIME: https://marcotcr.github.io/lime/tutorials.html
- UCI Machine Learning Repository: Statlog (German Credit Data)
