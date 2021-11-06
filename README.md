# Identificação de Similaridade entre Anomalias de Segurança, Meio Ambiente e Saúde

#### Alunas: Andrea Pitol Ferreira e Ludmila Junca Lopes (https://github.com/milajunker/tccpucrj)
#### Orientador: Leonardo Mendoza

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

### Resumo

Um dos principais objetivos da área de segurança de uma grande empresa de Oil & Gas é evitar que ocorram acidentes. Para isso, é necessário que o aprendizado com acidentes anteriores seja disseminado de forma eficaz para as áreas pertinentes e ações sejam tomadas de forma a que se evite a repetição do contexto e causas do evento. Mas como medir se estão realmente cumprindo seu papel? A análise de eficácia é um grande desafio para essa área e este projeto tem por objetivo ajudar a elaborá-la. A solução aqui apresentada se baseia em, a partir da análise de similaridade por cosseno dos textos dos incidentes registrados, indicar eventos que se repetem (recorrentes) ou que possuem um alto potencial de dano. Dessa forma, é possível gerir e avaliar os eventos em que o aprendizado e as ações foram eficazes e aqueles que ainda necessitam de atuação. Os resultados alcançados foram satisfatórios, com acurácia de 70%, e se encontram em uso em ambiente produtivo.


### 1. Introdução
Em uma grande indústria, a segurança das operações é um fator crítico para garantir a integridade das pessoas, das instalações e da continuidade da atividade. Um dos fatores cruciais para prover uma operação segura é o aprendizado com eventos ocorridos. Eventos estes que causaram algum dano ou que potencialmente poderiam causar algum dano de maiores proporções.

Para gerar e perpetuar esse aprendizado é necessário conhecer esses eventos, divulgá-los, corrigir suas causas, alterar padrões e procedimentos e acompanhar, ao longo do tempo, se outros eventos simillares tornam a acontecer. Se sim, é necessário reavaliar as ações tomadas para sanar as lacunas que possibilitaram a repetição do evento.

No entanto, quando estamos no contexto de uma grande indústria, esses eventos ou anomalias, que variam desde pisos desnivelados até grandes explosões, podem ser registrados às dezenas diariamente, espalhados por toda a distribuição geográfica das atividades. A simples análise de eventos semelhantes se repetindo beira o inexequível, uma vez que as informações estão espalhadas em textos descritivos de milhares de registros.

É na viabilização desta gestão de eficácia que o projeto deste trabalho atua. Através da análise de similaridade entre os registros de anomalias, ele é capaz de apontar eventos semelhantes e suas repetições ao longo do tempo. Além disso, é capaz de apontar eventos ocorrências que se assemelham a eventos que causaram grandes perdas e apontá-los como eventos de alto potencial.

As técnicas de Processamento de Linguagem Natural possibilitam que textos sejam compreendidos, comparados e interpretados pelas máquinas. No caso do problema em questão, a comparação entre textos foi utilizada  de forma a identificar eventos semelhantes, substituindo a ação humana nesse processo. Existem alguns algoritmos que realizam essa tarefa e alguns deles e suas combinações foram avaliados durante o processo de desenvolvimento.

### 2. Modelagem

A modelagem do problema se iniciou pela análise exploratória dos dados, cujo objetivo foi compreender um pouco mais sobre o dataset disponível e observar características que pudessem subsidiar os passos posteriores do processo. O dataset utilizado é composto por 327.145 registros de anomalias de segurança, meio ambiente e saúde, e contém como colunas o código de identificação da anomalia, a data de sua ocorrência e a descrição textual da mesma. Essa etapa evidenciou o quanto as descrições são heterogêneas, tendo sido constatadas diferenças significativas no estilo de escrita, além da existência de erros ortográficos. A média de palavras por registro foi de 18,8, apresentado como máxima 309, mínima 2 e desvio padrão 13,8. Também foram avaliadas as principais classes gramaticais presentes. Conforme esperado, há maior prevalência de verbos e substantivos. Como as demais classes gramaticais foram pouco significativas, não foi considerado pertinente aplicar filtro para restrição.

A etapa seguinte tratou do pré-processamento dos dados. Foram aplicados os seguintes tratamentos: padronização dos textos em formato unicode, remoção de pontuação, remoção de números, remoção de múltiplos espaços em branco, remoção de palavras muito curtas, remoção de stopwords, lematização e remoção de acentos. O objetivo desses tratamentos foi remover caracteres e palavras pouco significativas para o domínio do problema. Através da lematização, tentou-se evitar que um mesmo conceito não fosse reconhecido no caso de duas palavras de mesmo lema apresentarem flexões divergentes.

Na sequência, foram geradas, a partir da descrição textual, as características a serem utilizadas no modelo. Para tal, utilizou-se TF/IDF para geração do vetor de características.

Como o objetivo do projeto demanda avaliar a similaridade entre todos os registros do dataset, foi gerado o produto cartesiano dos registros. Posteriormente, filtrou-se os pares ordenados formados por dois registros iguais e também registros equivalentes, em que a diferença entre eles se dá apenas pela ordem em que os mesmos aparecem. 

Por fim, calculou-se o cosseno entre os vetores de características de cada par ordenado. Em função do grande número de registros a serem processados, o código foi desenvolvido utilizando Databricks e Spark, abordagens adequadas para problemas que requerem processamento distribuído.

Como estudos adicionais na fase de modelagem, foram consideradas as seguintes abordagens:
-Doc2Vec
-LDA+Cosseno
O emprego do Doc2Vec teve que ser abortado por incompatibilidade com a arquitetura disponível na empresa e a inviabilidade de ajustes devido ao cronograma. A alternativa LDA+Cosseno, em que primeiro se identificava os tópicos latentes nas anomalias (LDA) e depois se aplicava o cosseno apenas em anomalias pertencentes ao mesmo tópico, foi uma tentativa de melhoria nos resultados obtidos apenas com o cosseno. No entanto, mostrou-se computacionalmente custosa sem gerar melhorias que justificassem seu uso.


### 3. Resultados

Para avaliação dos resultados e definição do valor de cosseno a ser utilizado como limiar para definir se dois registros são similares foi gerado um gabarito, formado pelo conjunto de mil pares ordenados de anomalias, com a respectiva classsificação quanto a similaridade entre elas. Ao comparar os resultados obtidos com o gabarito, verificou-se que 0.65 é o limiar adequado para o problema em questão. Observou-se que utilizando esse limiar, a acurárcia do algoritmo foi de aproximadamente 70%, resultado considerado satisfatório pelos usuários envolvidos no projeto.

### 4. Conclusões

Os resultados apresentados mostram que é factível identificar similaridade, com base na descrição textual, entre anomalias de segurança, meio ambiente e saúde. A abordagem TF/IDF+Cosseno, apesar de "ingênua", se mostrou aderente ao problema e à natureza dos textos analisados. Como trabalho futuro, sugere-se experimentos com BERT e sent2vec, que são técnicas mais modernas e que conseguem capturar melhor o contexto envolvido.

---

Matrícula: 192.671.014 e 192.671.065

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
