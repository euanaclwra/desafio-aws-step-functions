# Boas Práticas - AWS Step Functions ✨
A AWS recomenda algumas práticas para gerenciar e otimizar os *workflows* do Step Functions:

## 🗂️ Workflows Aninhados
O Step Functions permite aninhar fluxos expressos em fluxos padrão, delegando tarefas com mais volume para um fluxo secundário e especializado. Vejamos um exemplo em um e-commerce:

### 🔀👨 Fluxo Pai: Standard
1. Valida o pagamento
2. Verifica a disponibilidade de estoque
3. Chama o **fluxo expresso** para calcular o melhor frete
4. Confirma o pedido
### 🔀👶 Fluxo Filho: Express
1. Recebe os dados do pedido
2. Dispara, em paralelo, chamadas para várias APIs de transporte
3. Analisa os resultados
4. Retorna só o frete mais barato para o **fluxo padrão**

Dessa forma, além de não sobrecarregar o fluxo principal sem necessidade, ainda otimizamos o cálculo do frete e economizamos custos, visto que fluxos do tipo expresso são mais baratos. ✨

## 🏷️ Tags em State Machines
Identificar os *workflows* com tags podem ajudar a rastrear/gerenciar cada recurso e fornecer uma melhor segurança nas políticas de acesso do IAM.  
Podemos, por exemplo, criar uma *policy* para **restringir acessos** somente em *state machines* com a tag `environment=production`, ou seja, fluxos que estão em ambiente de produção (já em uso pelo cliente).
