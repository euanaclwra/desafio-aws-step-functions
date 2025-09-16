# Conceitos - AWS Step Functions ✨
Chamamos um workflow do AWS Step Functions de ***state machines***. Cada *state machine* é composto por vários ***states***, que são as etapas do fluxo.


## 🔀 Tipos de Workflow
O AWS Step Functions possui dois tipos de *workflows*, e a decisão entre os dois vai depender do tempo de execução, custo, volume e necessidade de histórico detalhado:
### Standard Workflow 🕒
- Processos de longa duração (até 1 ano)
- Menor volume de execuções
- Mantém um histórico detalhado da execução
- Cada etapa do fluxo só é executada uma vez
### Express Workflow 💨
- Processamento de eventos em tempo real (até 5 minutos)
- Alto volume de execuções
- Sem histórico detalhado, apenas logs resumidos no *CloudWatch*
- Cada etapa do fluxo pode ser executada várias vezes

## 📝 Tipos de State
Como sabemos, os *states* são os blocos de execução dentro da *state machine*. Cada bloco desse pode ser um(a):
- **Task:** Executa uma tarefa (Lambda, ECS, atividade externa, etc.)
- **Choice:** Uma decisão condicional (espécie de if/else)
- **Parallel:** Executa etapas em paralelo
- **Wait:** Aguarda um determinado e tempo e continua o fluxo
- **Pass:** Só continua o fluxo, sem fazer nada
- **Map:** Itera sobre uma lista
- **Fail/Succeed:** Finaliza o fluxo com erro ou sucesso
<br>
Com esses tipos de state, podemos montar um fluxo complexo envolvendo decisões baseadas em dados, tarefas envolvendo outros recursos etc. ✨

## 🔗 Tipos de Integração
No último tópico, vimos que ***task states*** permitem a comunicação com outros recursos da AWS. Para chamar esses serviços, existem dois tipos de integração:
### Integrações Otimizadas ✅
- Integrações nativas
- Sintaxe enxuta no JSON, sem precisar escrever muito código
- Usam o IAM da AWS para permissões
### Integrações via SDK 🛠️
- Total flexibilidade de integração (mesmo as não otimizadas)
- Sintaxe um pouco mais verbosa
- Bom para serviços novos ou menos usados
<br>
Em resumo, é bom optar pela integração otimizada sempre que possível, porque é mais fácil, mas barata e mais rápida. Recorremos ao SDK quando precisamos de algo que ainda não tem integração otimizada. ✨
<br><br>
Além disso, as integrações também podem seguir três **padrões** de integração:
- Request/Response: Prossegue pra próxima etapa assim que recebe um retorno 
- **Run a Job:** Espera o serviço finalizar pra prosseguir pra próxima etapa
- **Wait for a callback:** Chama o serviço com um *token*, e aguarda o serviço devolver esse *token*


