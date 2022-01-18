# Respostas
### a) Quais dados você removeria da tabela única? Por quê?
R: Colunas que eu removeria:
- CD_TABELA_REFERENCIA
- IND_PACOTE
- IND_TABELA_PROPRIA
- NM_MODALIDADE
- CD_MOTIVO_SAIDA
- CID_1, CID_2, CID_3, CID_4
- LG_VALOR_PREESTABELECIDO
<br>
O motivo de remover estas colunas é que elas contém informações que condizem mais com as funções internas dos funcionários da saúde do que com a função de um Cientista de Dados na construção de um modelo preditivo, pois são variáveis de controle interno, e não variáveis que podem influenciar no resultado de outras variáveis que, por ventura, possamos querer prever.
<br>
### b) Quais técnicas foram utilizadas para avaliar a qualidade dos dados?
Devido ao tamanho total do dataset (em torno de 40 milhões de linhas), utilizei PySpark em um notebook do Databricks para fazer a análise. Chequei por valores nulos, problemas de formatação e de valores que poderiam não fazer sentido. Por falar nisso, eu gostaria de deixar uma sugestão: Talvez a necessidade de juntar tudo em um só dataset tenha sido parte crucial do desafio para fins de avaliação, mas eu não recomendaria que os datasets do tipo 'CONS' e 'DET' fossem unidos. Isso porque, segundo o dicionário de variáveis disponível no próprio site dos dados abertos, as tabelas do tipo 'CONS' não são de preenchimento obrigatório. Isso faz com que tenhamos muito mais observações nas tabelas do tipo DET e na hora de ajuntá-las com um JOIN, teremos várias chaves ID_EVENTO_ATENCAO_SAUDE das tabelas DET para apenas uma ou poucas observações de mesma identificação das tabelas CONS, o que pode fazer com que o modelo preditivo aprenda erroneamente a correlação entre os dados. [Neste notebook](https://github.com/mathfigueiredo/Desafio-Neurotech/blob/main/Desafio%20Neurotech.ipynb)
### c) Quais dados brutos podem ter maior potencial de informação para a empresa?

### d) Que estratégia você sugeriria para ingerir e manter os dados atualizados na nuvem?
