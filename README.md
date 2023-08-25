# 💻> Prompts para Analista de Dados
Abaixo, alguns prompts que podem ajudar no dia a dia de um analista de dados.


# No Excel / Sheets 📊📄

## Explicação de comando
```
Você pode me explicar como o comando PROCV funciona no Excel?
```
```
Agora poderia explicar como se estivesse descrevendo para uma criança?
```
```
Você pode fornecer um exemplo usando alguns dados de amostra e mostrar a sintaxe da fórmula?
```

## Erro em fórmula ❌🔢
```
Estou usando a fórmula do Excel abaixo para contar o número de palavras na célula D2, mas está retornando um #VALUE! erro no Excel. Você pode me dizer como consertar isso?

=LEN(TRIM(D2))-LEN(SUBSTITUTE(TRIM(D2),"","")+1)
```

## Montando um passo a passo...
```
Tenho uma tabela Excel contendo os seguintes campos: Order ID Product Quantity Retail Price Revenue Order Size.
Preciso criar uma Tabela Dinâmica mostrando a receita média (average revenue) para cada tamanho de pedido(Order Size), formatada como moeda (USD). Forneça instruções claras e passo a passo para criar a Tabela Dinâmica usando o Excel para Office 365 em um PC.

Aqui esta um exemplo das primeiras 15 linhas de dados...

Order ID Product Quantity Retail Price Revenue Order Size
44016 WORLD WAR 2 GLIDERS ASSTD DESIGNS 5 $0.32 $1.60 Small
24854 JUMBO BAG RED RETROSPOT 25 $247 $6176 Medium
37210 ASSORTED COLOUR BIRD ORNAMENT 75 $1.72 $129.15 Large
14622 POPCORN HOLDER 6 $1.01 $6.07 Small 36868 PACK OF 72 RETROSPOT CAKE CASES 10 $0.76 $7.56 Small
37375 WHITE HANGING HEART T-LIGHT HOLDER 5 $3.20 $16.02 Small
45660 RABBIT NIGHT LIGHT 100 $2.38 $237.54 Large
27305 MINI PAINT SET VINTAGE 15 $0.78 $11.72 Medium
17826 PACK OF 12 LONDON TISSUES 1 $0.45 $0.45 Small
31194 PACK OF 60 PINK PAISLEY CAKE CASES 75 $0.74 $55.59 Large
48711 VICTORIAN GLASS HANGING T-LIGHT 15 $1.65 $24.77 Medium
20858 ASSORTED COLOURS SILK FAN 2 $1.07 $2.13 Small
21517 BROCADE RING PURSE 2 $1.06 $2.13 Small
31271 RED HARMONICA IN BOX 250 Medium
```


# Requisitos ✅📋

## Enquiquecer documentação
```
Fórum Data Lake
- Cultura baseada em dados (data-driven)
- Quanto tempo para consumir dados (Contábil, Receitas)
- Dores
	- Marketing
		- Campanhas
			- Vips
			- Clientes recorrentes
		- perfil de clientes por loja
		- campanha dificuldades
		- análise por produto X, por exemplo
		- Por canal
		- ML?
	- Vendas
		- B2B
			- Falta de acompanhamento
			- Sugerir antes do cliente precisar
Sistemas
- A caminho do Lake
	- Shopify
	- Protheus
- Outros
	- Sellbie

Enriquecer essa especificação de requisitos e colocar num formato padrão de especificação (gerar em formato .md)
```

# KPIS 📊📈🔑
```
Você atuará como um especialista em Análise de Dados. Você estará me treinando, como um colega de trabalho júnior que está aprendendo Análise de Dados. Você pode explicar a diferença entre um KPI e uma métrica?
```

```
Explique como se fosse para uma criança
```

**KPI de RH**
```
Você como um grande analista de dados do ramo de rh, monte uma pequena base de dados de pessoa em SQL Server, e informe os principais indicadores (KPI´s) de rh e a formula para calcular cada um deles (pode ser um select para cada uns dos KPIs)
```

[mais informações](https://medium.com/blog-do-zouza/decifrando-kpis-a-f%C3%B3rmula-do-sucesso-para-seu-neg%C3%B3cio-d6a34e52ea9)


# SQL 🗃️🔍

## Conceitos
```
Você atuará como um especialista em SQL. Você estará me treinando, como um colega de trabalho júnior que está aprendendo SQL e precisa de ajuda. Você pode explicar a diferença entre um LEFT JOIN e um INNER JOIN no SQL?
```

```
Explique a diferença entre os tipos de dados int e smallint
```

## Explicação de Comandos
```sql
Você atuará como um Analista Sênior especialista em SQL. Você estará me ajudando, um analista júnior de sua equipe, a entender as consultas SQL que usaremos juntos no trabalho.

Você pode me explicar a seguinte instrução SQL?

SELECT
  sa.attribution_clean,
  COUNT(s.id) AS students,
  SUM(r.dollars) AS total spend, SUM(r.dollars)/COUNT(s.id) AS spend_per_student
FROM Students s
LEFT JOIN StudentAttribution sa ON sa student_id = s.id
LEFT JOIN Revenue r ON r.student_id = s.id
GROUP BY 1
ORDER BY 2 DESC
```

## Documentação 📚📑
```sql 
Documente detalhadamento o que esta sendo feito no SQL abaixo:

SELECT c.estadocliente                   AS Estado,
       p.nomeproduto                     AS nomeproduto,
       ROUND(AVG(v.quantidadevendas), 4) AS quantidade_media
  FROM dw.dim_cliente c
  JOIN dw.fato_vendas v ON v.codigocliente = c.codigocliente
  JOIN dw.dim_produto p ON p.codigoproduto = v.codigoproduto
 WHERE 1 = 1
   AND v.codigostatusvenda = 1 -- Concluído
 GROUP BY c.estadocliente, p.nomeproduto
 ORDER BY c.estadocliente, p.nomeproduto;
```

## Identação e Comentários ✍️🗂️

```sql
Você atuará como um Analista Sênior especialista em SQL. Você estará me ajudando, um analista júnior em sua equipe. entender consultas SQL que usaremos juntos no trabalho.

Você poderia adicionar identação, comentários à consulta a seguir para facilitar o entendimento de outros analistas?

CREATE TEMPORARY TABLE tmp_students AS SELECT id, name FROM students;
CREATE TEMPORARY TABLE tmp_scores AS SELECT student_id, score FROM exam_scores;

WITH score_avg AS (SELECT student_id, AVG(score) OVER (PARTITION BY student_id) AS avg_score FROM tmp_scores)
SELECT s.name, ts.score, sa.attribution, sa.attribution_clean, score_avg.avg_score
FROM tmp_students s
LEFT JOIN tmp_scores ts ON s.id = ts.student_id
LEFT JOIN (SELECT student_id, MAX(attribution) AS attribution, MAX(attribution_clean) AS attribution_clean FROM student_attributions GROUP BY student_id) sa ON s.id = sa.student_id
JOIN score_avg ON ts.student_id = score_avg.student_id
ORDER BY score_avg.avg_score DESC;
```

## Identificação de Erros ❌🔢
```sql
Você atuará como um Analista Sênior especialista em SQL. Você estará me ajudando, um analista júnior de sua equipe, a entender as consultas SQL que usaremos juntos no trabalho.

Estou com um erro na minha consulta sql. Você pode me ajudar a dizer o que pode estar errado?

SELECT s.name,  -- Nome do estudante
       ts.score,  -- Pontuação da nota
       sa.attribution,  -- Atribuição do estudante
       sa.attribution_clean,  -- Atribuição limpa do estudante
       score_avg.avg_score  -- Média de pontuação das notas do estudante
FROM tmp_students s
-- Combinação à esquerda dos estudantes com suas notas
LEFT JOIM tmp_scores ts ON s.id = ts.student_id
-- Combinação à esquerda das atribuições dos estudantes, usando a subconsulta para obter a atribuição máxima
LEFT JOIN (
    SELECT student_id,
           MAX(attribution) AS attribution,
           MAX(attribution_clean) AS attribution_clean
    FROM student_attributions
    GROUP BY student_id
) sa ON s.id_a = sa.student_id
-- Combinação interna (INNER JOIN) com a subconsulta que calcula as médias de pontuação
JOIN score_avg ON ts.student_id = score_avg.student_id
-- Ordena os resultados pela média de pontuação das notas em ordem decrescente
ORDER BY score_avg.avg_score DESC;
```


# Python 🐍

## Conceitos e Definições
```
Você pode comparar e contrastar as bibliotecas matplotlib, seaborn e plotly express em Python?
```

## Explicação de Código
```python
Você pode explicar o que o código a seguir está fazendo em alto nível? Certifique-se de incluir também uma saída de amostra. 

import pandas as pd
import numpy as np

students_data = {
    'student_id': [1000001, 1000002, 1000003, 1000004],
    'first_name': ['John', 'Jane', 'Alice', 'Bob'],
    'last_name': ['Doe', 'Smith', 'Johnson', 'Williams']
}

student_attribution_data = {
    'student_id': [1000001, 1000002, 1000003, 1000005],
    'attribution_clean': ['youtube', 'youtube', 'youtube', 'facebook']
}

revenue_data = {
    'student_id': [1000001, 1000002, 1000003],
    'dollars': [50, 100, 75]
}

students_df = pd.DataFrame(students_data)
student_attribution_df = pd.DataFrame(student_attribution_data)
revenue_df = pd.DataFrame(revenue_data)

merged_df = student_attribution_df.merge(students_df, on=['first_name', 'last_name', 'student_id'], how='left')
merged_df = merged_df.merge(revenue_df, on='student_id', how='left')

filtered_df = merged_df[(merged_df['attribution_clean'] == 'youtube') &
                        (merged_df['student_id'].between(1000000, 2000000))]

grouped_df = filtered_df.groupby('attribution_clean').agg(
    students=('student_id', lambda x: np.count_nonzero(x)),
    total_revenue=('dollars', 'sum')
)

grouped_df['revenue_per_student'] = grouped_df['total_revenue'] / grouped_df['students']

result_df = grouped_df.sort_values(by='students', ascending=False)

print(result_df)
```

```
Você poderia comentar o código acima?
```

```
Alguma dica de melhores práticas para o código acima? E com exemplo
```

## Interpretação de Resultados
```
Você pode interpretar a seguinte saída de regressão linear de statsmodels? 

OLS Regression Results                            
        ==============================================================================
        Dep. Variable:                      y   R-squared:                       0.669
        Model:                            OLS   Adj. R-squared:                  0.667
        Method:                 Least Squares   F-statistic:                     299.2
        Date:                Mon, 01 Mar 2021   Prob (F-statistic):           2.33e-37
        Time:                        16:19:34   Log-Likelihood:                -88.686
        No. Observations:                 150   AIC:                             181.4
        Df Residuals:                     148   BIC:                             187.4
        Df Model:                           1                                         
        Covariance Type:            nonrobust                                         
        ==============================================================================
                         coef    std err          t      P>|t|      [0.025      0.975]
        ------------------------------------------------------------------------------
        const         -3.2002      0.257    -12.458      0.000      -3.708      -2.693
        x1             0.7529      0.044     17.296      0.000       0.667       0.839
        ==============================================================================
        Omnibus:                        3.538   Durbin-Watson:                   1.279
        Prob(Omnibus):                  0.171   Jarque-Bera (JB):                3.589
        Skew:                           0.357   Prob(JB):                        0.166
        Kurtosis:                       2.744   Cond. No.                         43.4
        ==============================================================================
```		

# Power BI 💼📊

## Entendimentos
```
Sou novo no Power BI, como faço para começar?
```
```
Sou novo no Tableau, como faço para começar?
```
```
Sou novo no Google Looker, como faço para começar?
```
```
Sou novo no AWS Quicksight, como faço para começar?
```

## Conceitos
```
Poderia explicar a diferença entre medidas x colunas calculadas no Power BI?
```
```
Sou um usuário relativamente novo do Power BI. Você pode fornecer um exemplo de uma coluna calculada e uma medida e descrever quando usar cada uma?
```

## Dúvidas - Conexão com BD
```
Acabei de ser contratado como analista de dados da Zouza Factory e preciso importar dados do banco de dados MySQL para o Power Bl. Eu tenho acesso ao MySQL, mas não tenho certeza de como conectar. Pode me ajudar?
```

## DAX - Explicar
```
Você pode explicar o que esse código DAX está fazendo e adicionar comentários em linha para que outros usuários possam entender o que está acontecendo?

Taxa de Crescimento Mensal = 
VAR MaxData = MAX('Tabela de Vendas'[Data])
VAR MaxDataAnterior = CALCULATE(MAX('Tabela de Vendas'[Data]), PREVIOUSMONTH('Tabela de Vendas'[Data]))
VAR VendasAtual = CALCULATE(SUM('Tabela de Vendas'[Total Vendas]), 'Tabela de Vendas'[Data] = MaxData)
VAR VendasAnterior = CALCULATE(SUM('Tabela de Vendas'[Total Vendas]), 'Tabela de Vendas'[Data] = MaxDataAnterior)
RETURN IF(ISBLANK(VendasAnterior) || VendasAnterior = 0, BLANK(), (VendasAtual - VendasAnterior) / VendasAnterior)
```

## DAX - Criar
```
Estou usando o Power BI, você poderia me ajudar a escrever uma fórmula DAX para calcular a receita total?
```

## DAX - Correção
```
Poderia me ajudar na correção da seguinte medida DAX?

Total Revenue (GPT) =
SUMX(
    'Sales Data',
    'Sales Data'[Order Quantity] Product Lookup'[ProductPrice]
```

## Visual - Sugestão
```
Estou usando o Power BI e preciso mostrar a tendência total de pedidos de clientes nos últimos 3 anos. Você pode sugerir um visual e descrever como construí-lo?
```

## Visual - Dicas
```
Quais são as práticas recomendadas ao usar um gráfico de pizza?
```

---
## Mais informações
- [Visão Geral - ChatGPT](https://medium.com/blog-do-zouza/chatgpt-vis%C3%A3o-geral-f68ed1d1cf54)
- [ChatGPT - Criando Medidas DAX com ChatGPT](https://www.youtube.com/watch?v=vo9uo6aFLME)
