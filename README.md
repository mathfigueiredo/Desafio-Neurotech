# Respostas
## a) Quais dados você removeria da tabela única? Por quê?
Colunas que eu removeria:
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

## b) Quais técnicas foram utilizadas para avaliar a qualidade dos dados?

Devido ao tamanho total do dataset (em torno de 40 milhões de linhas), utilizei PySpark em um notebook do Databricks para fazer a análise. Chequei por valores nulos, problemas de formatação e de valores que poderiam não fazer sentido. Por falar nisso, eu gostaria de deixar uma sugestão: Talvez a necessidade de juntar tudo em um só dataset tenha sido parte crucial do desafio para fins de avaliação, mas eu não recomendaria que os datasets do tipo 'CONS' e 'DET' fossem unidos. Isso porque, segundo o dicionário de variáveis disponível no próprio site dos dados abertos, as tabelas do tipo 'CONS' não são de preenchimento obrigatório. Isso faz com que tenhamos muito mais observações nas tabelas do tipo DET e na hora de ajuntá-las com um JOIN, teremos várias chaves ID_EVENTO_ATENCAO_SAUDE das tabelas DET para apenas uma ou poucas observações de mesma identificação das tabelas CONS, o que pode fazer com que o modelo preditivo aprenda erroneamente a correlação entre os dados. [Neste notebook](https://github.com/mathfigueiredo/Desafio-Neurotech/blob/main/Desafio%20Neurotech.ipynb), eu criei a função **build_initial_df**, que leva como parâmetro **df_type**= 'cons' ou 'det'. Essa função vai criar um DataFrame único englobando todos os csvs CONS ou DET. Posteriormente, eu apliquei umn JOIN nos dois para que chegássemos a uma solução de um único DF, porém, sigo não recomendando que se utilize desta junção para treianr modelos preditivos.<br>

## c) Quais dados brutos podem ter maior potencial de informação para a empresa?
- Variáveis de localização (UF e Município): Alto valor para gerar conclusões específicas em relação à localidade das ações;
- TEMPO_DE_PERMANÊNCIA: Útil para estimar o valor total da internação e para organizar a logística de rotatividade dos hospitais;
- ANO_MES_EVENTO: Útil para fazer análises de forecast e acompanhar outras variáveis ao longo do tempo
- CD_PROCEDIMENTO e variáveis relacionadas aos Itens utilizados: São variáveis categórica e numéricas bastante úteis para a previsão dos valores financeiros das internações
- FAIXA_ETARIA: Também muito importante para previsão do tempo de permanência e dos gastos totais.
- ID_PLANO: Importante para tomar decisões empresariais, firmar parcerias...

## d) Que estratégia você sugeriria para ingerir e manter os dados atualizados na nuvem?
Como já citado, em primeiro lugar, manter os dois tipos de dataframes separados. Além disso, seria interessante criar um DAGs específicos no Airflow, provavelmente que rode mensalmente, para fazer os trabalhos de extração dos dados .zip, tratamento automático por meio das funções de juntar dataframes e limpar dados e, por fim, gerar visualizações e insights via dashboards que poderiam ser automaticamente enviados por email para gestores, stakeholders etc.
<br><br>
Eu gostaria de agradecer pela oportunidade de realizar esse desafio. Foi muito importante e de bastante aprendizado para mim. Também gostaria de me desculpar, de antemão, por não ter podido terminar o projeto da maneira que eu queria, com visualizações ou mesmo modelos de Machine Learning. Tive um final de semana bastante corrido por questões familiares e só pude iniciar de fato o desafio na noite do dia 17. Virei a madrugada tentando entregar o melhor possível, mas devo entregar o desafio ainda que incompleto, pois já são 07:25 da manhã do dia 18 e o prazo se encerra daqui há uma hora e meia. Sabemos que o tratamento de dados com PySpark e databricks de um dataset tão extenso leva muito tempo para realizar quase todas as ações, e por isso decidi finalizar o projeto da maneira que está para escrever minhas respostas aqui no GitHub. Se puderem me dar outra oportunidade de terminar este projeto, eu adoraria. Espero que gostem da minha resolução e muito obrigado mais uma vez!
