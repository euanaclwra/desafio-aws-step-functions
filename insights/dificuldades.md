# Dificuldades, Dúvidas e Obstáculos - AWS Step Functions ✨
Neste arquivo, veremos algumas dificuldades comuns que os usuários do Step Functions costumam encontrar, e também algumas dúvidas pessoais que me deparei durante os estudos.

## 😬 Obstáculos Comuns dos Usuários
#### Como saber quando usar cada tipo de *state machine*?  
***Resposta:*** Pense na duração e no volume 🕒  

Se o fluxo envolver muitas etapas complexas e durar horas, dias ou até meses, a escolha é a *Standard State Machine*.  
Se o fluxo for mais curto, tiver bastante tráfego e processamento rápido de dados, a escolha é a *Express State Machine*.

#### Os dados transferidos entre os estados do *workflow* tem um limite de **256 KB**... e se eu precisar transportar um arquivo maior?  
***Resposta:*** Amazon S3 🪣

A AWS recomenda que grandes volumes de dados sejam armazenados em *buckets* do nosso querido Amazon S3. Na hora de usar os dados do nosso fluxo, só precisamos passar o identificador (ARN) do *bucket*, e os estados conseguem ler os dados normalmente para processá-los. ✅  

#### Meu diagrama está ficando muito extenso e confuso... como posso deixá-lo mais organizado e legível?  
***Resposta:*** Dividir *state machines* 🔀

É esperado que, a medida que um fluxo cresce, fique mais fácil se perder entre os estados, condições etc. Por isso, a solução ideal é dividir sua *state machine* gigante em fluxos menores e reutilizáveis.  

Assim, além de deixar seu fluxo organizado, ainda podemos isolar os erros e reaproveitar *workflows*. ✅  

## ❓Dúvidas Pessoais
#### O Step Functions tem um limite de 1.000.000 execuções em aberto... e se eu precisar expandir esse limite?  
***Resposta:*** SQS e limpar execuções abertas 🔍  

Ao invés de acionar a *state machine* diretamente, você pode enviar o evento para uma fila SQS. Dessa forma, a fila vai gerenciando a execução do Step Functions para lidar com os picos de demanda.  

Além disso, é importante garantir que *todo* fluxo chegue a um estado final. Ou seja, todos os caminhos possíveis devem terminar em ``Success`` ou ``Fail``, para garantir que o fluxo chegue ao fim e libere espaço para uma nova execução. ✅  

***Obs.:*** Nesse caso, delegar tarefas para *workflows* menores também ajuda! Essa prática é sempre recomendada. ✨  

#### Os fluxos expressos tem um log menos detalhado... em quais casos um histórico detalhado é "dispensável"?
***Resposta:*** Processamento rápido de dados 💨  

Pensemos, por exemplo, em eventos *IoT* que enviam milhares de dados por segundo (temperatura, umidade, localização etc.).  
Não há porque pagar caro para armazenar o histórico de **cada** leitura de sensor.  

Ou ainda, num sistema de deteccção de fraudes em transações, onde cada compra é avaliada com base no valor, localização, histórico...  
Também não há porque guardar histórico aqui, o que importa para o fluxo é somente o **resultado** dessa análise. ✅  

#### Qual a diferença entre tipos de integração e padrões de integração?
***Resposta:*** Um é "como", o outro é "onde" 📌  

Os tipos de integração (request-response, run a job, wait for callback) definem **como** o Step Functions interage com o recurso: se vai esperar uma resposta, se vai prosseguir imediatamente...  

Já os padrões de integração (otimizada ou via SDK) definem por **onde** essa interação acontece: nativamente ou pelo kit de desenvolvimento da AWS. ✅ 
