# regressao-linear-teste-e-prever-resultados

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

![Badge code size](https://img.shields.io/github/languages/code-size/fab-souza/regressao-linear-teste-e-prever-resultados)
<!---
![GitHub Org's stars](https://img.shields.io/github/stars/fab-souza/regressao-linear-teste-e-prever-resultados?style=social)
--> 


| :placard: Vitrine.Dev |    |
| -------------  | --- |
| :sparkles: Nome        | **Regressão Linear: testando relações e prevendo resultados**
| :label: Tecnologias | python
| :rocket: URL         | 
| :fire: Desafio     | Conteúdo do 5º [curso](https://www.alura.com.br/curso-online-data-science-modelo-regressao-linear) da formação [Data Science](https://www.alura.com.br/formacao-data-science)

![](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/ff56c32e-f5c1-4882-a49f-188f758c489c#vitrinedev)


# Sobre o curso 📚

Continuando a pôr em prática o que aprendi nos cursos da formação Data Science da [Alura](https://www.alura.com.br/), já passei pela análise e exploração dos dados, agora chegou a vez de falar sobre os modelos de previsão. Neste curso, também ministrado pelo instrutor [Rodrigo Dias](https://www.linkedin.com/in/rodrigo-fernando-dias-118181120/), aprendi:

- sobre a importância das visualizações para compreender a distribuição dos dados;

- a diferença entre variáveis dependentes e explicativas;

- a importância de separar os dados em conjuntos de treino e teste;

- a criar modelos que relacionam as variáveis dependentes e explicativas, permitindo previsões e análises estatísticas;

- compreender os erros em função dos resíduos e métricas, ou seja, identificar possíveis discrepâncias entre as previsões e os valores reais;

- finalizando com a comparação e salvamento dos melhores modelos. 

Desta vez, utilizamos dados disponíveis no [Kaggle](https://www.kaggle.com/datasets/dongeorge/beer-consumption-sao-paulo) sobre o consumo de cerveja em uma região na cidade de São Paulo.

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/6139fb64-2328-4665-a099-8c8d3e119696)

Ao longo do curso, desenvolvemos um modelo de Machine Learning capaz de fazer a previsão do consumo médio de cerveja, utilizando a Regressão Linear. 

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/7bf21f17-e69c-48f0-abc6-1c4ee2357b04)


# Minha prática 👩🏻‍💻

Para esta prática, pensei em utilizar um dataset sobre consumo de energia, também disponibilizado no [Kaggle](https://www.kaggle.com/datasets/fedesoriano/electric-power-consumption). 
Ele contém informações sobre os registros de temperatura, umidade, velocidade do vento e o consumo de energia de 3 regiões da cidade Tetouan, situada no norte do Marrocos. 
Os registros começaram em 1º de janeiro de 2017 e vão até o dia 30 de dezembro do mesmo ano, com um intervalo de 10 minutos entre eles.

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/82524c48-be9a-4d6c-9efe-4e3366e1bb81)

Na descrição do dataset, não é informado quais são as unidades de medida das variáveis, mas uma delas possui um exemplo em °C. Então, vou supor que as variáveis seguem as mesmas unidades de medidas usadas aqui no Brasil.

* Temperatura = °C
* Umidade = %

E aqui veio uma variável um pouco complicada de determinar. Para a velocidade do vento, eu encontrei páginas citando o uso de m/s, km/h e nós (kt). 
Ao fazer um *.describe()* do DataFrame, vi que o valor mínimo dela é **0,05** e seu máximo é de **6,48**. 

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/7c50d4b2-2dd3-4705-83ff-9d935ac86eab)

A página [Clima de Ensinar](https://www.climadeensinar.com/post/2016/09/08/como-%C3%A9-medida-a-velocidade-do-vento) possui uma tabela que ilustra como classificar o vento de acordo com sua velocidade nas três unidades de medida, m/s, km/h e nós.

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/e8e89a11-920a-4b59-b47e-02e96739d864)

Se a unidade de medida do dataset fosse em km/h, ou em nós, a cidade não teria ventos diferentes de *brisa leve*, pois este tipo de vento vai até 12km/h, ou 6 nós. Se estiver em m/s, os ventos podem ser classificados chegar até *brisa moderada*, que vão até 7,4m/s.

Fiz uma pesquisa no Google sobre a cidade, onde tive acesso ao clima da região, com registro da temperatura, umidade e velocidade do vento (em km/h). 

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/30c29072-1ae0-4515-a5b8-ac4b2540021d)

Para transformar km/h para m/s, divido por 3,6.  

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/21cb5c39-fac4-477e-9d5c-b927d46e021b)

Fonte: [Prepare Enem](https://www.preparaenem.com/fisica/como-passar-m-s-para-km-h.htm)

Fazendo 21 km/h para m/s, tenho 5,83 m/s, valor este que está dentro da faixa registrada no dataset. Portanto:

* Velocidade do vento = m/s
* Consumo de energia = kWh

---
Com as unidades de medida estabelecidas, iniciei a manipulação do dataset.
Diferente do dataset usado no curso, neste caso eu não tenho informações como temperatura mínima, média, máxima e se o dia está em um fim de semana ou não. Ao fazer um gráfico de correlação, vi que, com exceção dos **consumos** e **fluxos**, as demais variáveis não possuem correlação superior a 0,5 e decidi adicionar as colunas semelhantes do dataset usado no curso para ver se elas melhoravam.

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/48200778-7c96-45b8-8769-3754ab293c50)

Para criar as variáveis referentes a mínima, média e máxima de algumas colunas, eu poderia fazer igual ao dataset do curso e descobrir o quanto os valores variaram ao longo do dia, mas acho que perderia muitos dados ao fazer essa compactação. Dessa forma, achei melhor agrupar as informações por hora.

O Pandas tem um método que faz a reamostragem de séries temporais, o **resample**. Tive que definir uma regra, que é o intervalo da reamostragem, informar a coluna em forma de *datetime* e, fora do método, o que eu queria de retorno, se é o mínimo, o máximo, etc.

No caso dos **consumos**, eu precisava da soma do que foi registrado no intervalo de 1 hora e defini o retorno da reamostragem como **resultado_soma**. Nas demais colunas, este tipo de reamostragem não seria útil e as excluí.

Para descobrir as médias, também utilizei o **resample** e nomeie seu retorno como **resultado_media**. Neste caso, a reamostragem dos consumos não é relevante e retirei elas do DataFrame. Eu também fiz este procedimento para descobrir os mínimos e máximos destas colunas, para só então, unir todas elas em um dataset maior. 

Na reamostragem de mínimo e máximo, também excluí as 3 colunas do consumo e adicionei um sufixo nas colunas, para diferenciá-las umas das outras. Para evitar a repetição, criei uma função que remove as colunas e adiciona os sufixos.

Na hora de unir os DataFrame, por algum motivo 🤔, algumas colunas tiveram o sufixo retirado. Fiz a alteração dos nomes e terminei de unir os 4 DataFrame.

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/4baeee49-2203-4d15-b4d1-6cf5879d229c)

Para fazer classificação dos dias, se é no fim de semana ou não, primeiramente, tive que restaurar o índice, como o método **.reset_index**. Depois, utilizei o método **weekday**, do módulo *datetime*, que funciona da seguinte forma, para cada dia, ele retorna um inteiro, por exemplo, segunda-feira é ‘0’ e domingo é ‘6’. Criei uma função que preenche uma nova coluna no dataset com ‘0’ e ‘1’. Para os retornos do **weekday** maiores ou iguais a 5 (sábado e domingo) a coluna é preenchida com ‘1’, caso contrário, recebe ‘0’.

## Nova correlação:

Após todas as manipulações, fiz uma nova correlação e o resultado não foi muito diferente da primeira. Em todas as variáveis reajustadas, não houve grande mudança de valores. A **Temperatura** continua sendo a variável com maior correlação, a **Umidade** continua apresentando valores negativos e **Velocidade do vento**, **Fluxos gerais** e **Fluxos difusos** continuaram com seus valores baixos, próximos à 0. Já para a nova variável, **Fim de semana**, sua correlação com os consumos também fica próximo à 0 nas três subestações, valor positivo apenas para a Zona 3 e negativo nas outras duas.

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/a57c51e0-dc09-48d9-96a4-422ec312f460)

## Criando o modelo:

Para dar início a criação do modelo, importei a função **train_test_split**, da biblioteca *Scikit_learn*, que separa os dados em duas partes, *Treino* e *Teste*, um para treinar o modelo e o outro para testá-lo.

Defini o **Consumo_zona3** como **y**, **Temperatura**, **Umidade** e **Velocidade_vento** como **X**, passei ambas para a função **train_test_split**, também defini a porcentagem de dados usados para o teste e um valor para o **random_state**.

Importei métodos destinados à regressão, **linear_model**, **LinearRegression** e **metrics**. Iniciei um modelo de regressão linear vazio e o treinei com os dados de treinamento, **X_train** e **y_train**, com a função **.fit()**

Para avaliar o desempenho do modelo, calculei o coeficiente de determinação com o **.score()**. Ele é um método que retorna a precisão média do modelo ao comparar os valores previstos para *X_train* com os valores verdadeiros de *y_train*. Ou seja, representa a qualidade do ajuste do modelo aos dados e não obtive um bom resultado: **0,238**

Ele trabalha com valores entre 0 e 1, e quanto mais próximo de 1, melhor. Ou seja, não é um bom modelo. Eu já sabia que duas, das três, variáveis independentes não estavam fortemente correlacionadas ao **Consumo**, então, não deveria esperar um bom modelo como resultado.

Em uma forma de tentar melhorar o modelo, troquei a **Umidade** por **Fluxos_gerais**, criei um novo modelo e o coeficiente melhorou um pouco. De 0,238 passou para 0,271. 

Com esta pequena melhora, resolvi tentar usar o novo modelo para prever um consumo de energia. Criei uma variável, *y_previsto*, para receber as previsões de **X_test** e comparei seus resultados com os valores originais, **y_test**, através da função **metrics.r2_score()**. Seu valor também varia entre 0 e 1, ele mostra o quanto o modelo se ajustou aos dados e seu retorno foi de **0,282**. Ou seja, o modelo consegue explicar 28,2% das variações dos dados.

Para finalizar, eu quis ver o quão próximo o modelo chegou de um dado, através de uma previsão pontual. Atribuí a variável *entrada* o primeiro registro em **X_test**, coletando sua temperatura, velocidade do vento e fluxos gerais. Passei para o método **.predict()** a nova variável e ele retornou o valor de **20408.79**.

Ou seja, para um período com temperatura de 27,44 °C, ventos de 4,9 m/s e fluxos gerais de 818, a previsão de consumo é de 20.408,79 kWh.

No entanto, fiz um *.loc* do índice do primeiro registro de **X_test** e vi que o consumo de energia, nas condições registradas, foi de 27.986,61 kWh na Zona 3.

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/6f4bfdde-4215-4baa-80ff-1bb9b355f20e)


# Conclusão 🏁

Eu já tinha conhecimento de que o **Consumo** não tinha forte correlação com as demais variáveis, exceto **Temperatura**, e mesmo assim continuei trabalhando com este dataset. Como resultado, o modelo não foi capaz de explicar grande parte da variação nos dados. 

Eu ainda poderia tentar utilizar outros modelos de regressão, para ver se os resultados melhoravam, mas não era o foco do curso, eu não quis avançar e bordar o conteúdo de um curso que ainda não fiz um projeto sobre.

Com o projeto finalizado, fui ver o material da aula e percebi que cometi um grande erro:
-antes de começar qualquer manipulação com os dados, eu deveria ter verificado se os **Consumos** possuem uma distribuição normal. Se ela não fosse atendida, eu não poderia executar testes, pois não teria resultados confiáveis.

![image](https://github.com/fab-souza/regressao-linear-teste-e-prever-resultados/assets/67301805/9b3a264a-62ea-4c5c-9910-80e999a1fbec)

Sem contar que: ‘*Garbage in, garbage out*’

Não adianta tentar fazer milagre com um dataset que não apresenta bons dados, fica de lição para os próximos projetos.

## Ferramentas utilizadas 🧰

