# Identificação de Similaridade entre Anomalias de Segurança, Meio Ambiente e Saúde

#### Alunas: Andrea Pitol Ferreira e Ludmila Junca Lopes 
#### Orientador: Leonardo Mendoza

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

### Resumo

Um dos principais objetivos da área de segurança de uma grande empresa de Oil & Gas é evitar que ocorram acidentes. Para isso, é necessário que o aprendizado com acidentes anteriores seja disseminado de forma eficaz para as áreas pertinentes e ações sejam tomadas de forma a que se evite a repetição do contexto e causas do evento. Mas como medir se estão realmente cumprindo seu papel? A análise de eficácia é um grande desafio para essa área e este projeto tem por objetivo ajudar a elaborá-la. A solução aqui apresentada se baseia em, a partir da análise de similaridade por cosseno dos textos dos incidentes registrados, indicar eventos que se repetem (recorrentes) ou que possuem um alto potencial de dano. Dessa forma, é possível gerir e avaliar os eventos em que o aprendizado e as ações foram eficazes e aqueles que ainda necessitam de atuação. Os resultados alcançados foram satisfatórios, com acurácia de 70%, e se encontram em uso em ambiente produtivo.


### 1. Introdução
Em uma grande indústria, a segurança das operações é um fator crítico para garantir a integridade das pessoas, das instalações e da continuidade da atividade. Um dos fatores cruciais para prover uma operação segura é o aprendizado com eventos ocorridos. Eventos estes que causaram algum dano ou que potencialmente poderiam causar algum dano de maiores proporções.

Para gerar e perpetuar esse aprendizado é necessário conhecer esses eventos, divulgá-los, corrigir suas causas, alterar padrões e procedimentos e acompanhar, ao longo do tempo, se outros eventos simillares tornam a acontecer. Se sim, é necessário reavaliar as ações tomadas para sanar as lacunas que possibilitaram a repetição do evento.

No entanto, quando estamos no contexto de uma grande indústria, esses eventos ou anomalias, que variam desde pisos desnivelados até grandes explosões, podem ser registrados às dezenas diariamente, espalhados por toda a distribuição geográfica das atividades. A simples análise de eventos semelhantes se repetindo beira o inexequível, uma vez que as informações estão espalhadas em textos descritivos de milhares de registros.

É na viabilização desta gestão de eficácia que o projeto deste trabalho atua. Através da análise de similaridade entre os registros de anomalias, ele é capaz de apontar eventos semelhantes e suas repetições ao longo do tempo. Além disso, é capaz de apontar eventos recentes que se assemelham a eventos que causaram grandes perdas e apontá-los como eventos de alto potencial.

As técnicas de Processamento de Linguagem Natural possibilitam que textos sejam compreendidos, comparados e interpretados pelas máquinas. No caso do problema em questão, a comparação entre textos foi utilizada  de forma a identificar eventos semelhantes, substituindo a ação humana nesse processo. Existem alguns algoritmos que realizam essa tarefa e alguns deles e combinações foram avaliados durante o processo de desenvolvimento.

### 2. Modelagem


Para fazer a análise de similaridade, inicialmente, foram consideradas 3 possíveis abordagens:
-Doc2Vec
-Cosseno
-LDA+Cosseno
A abordagem Doc2Vec teve que ser abortada por incompatibilidade com da arquitetura disponível na empresa e inviabilidade de ajustes devido ao cronograma. Já a abordagem Cosseno, apesar de "ingênua", se mostrou aderente ao problema e à natureza dos textos analisados. A terceira implementação, LDA+Cosseno, foi uma tentativa de melhoria nos resultados obtidos com o cosseno. No entanto, mostrou-se computacionalmente custosa sem gerar melhorias que justificassem seu uso.

### 3. Resultados

Para avaliação dos resultados e definição do valor de cosseno a ser utilizado como limiar para definir se dois registros são similares foi gerado um gabarito, formado pelo conjunto de mil pares ordenados de anomalias com a respectiva classsificação quanto a similaridade entre elas. Ao comparar os resultados obtidos com o gabarito, verificou-se que 0.65 é o limiar adequado para o problema em questão. Observou-se que utilizando esse limiar, a acurárcia do algoritmo foi de aproximadamente 70%. 

### 4. Conclusões

Os resultados apresentados mostram que a abordagem empregada é factível para identificar similaridade, com base na descrição textual, entre anomalias de segurança, meio ambiente e saúde. 

---

Matrícula: 123.456.789

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
