# Projeto: Credit Risk Decision Engine
### Modelo para Decisão de Risco de Crédito  
Este é meu primeiro projeto de portfólio desenvolvido para demonstrar meus conhecimentos em Data Science. O projeto foi desenvolvido com o suporte de Inteligência Artificial como ferramenta de apoio técnico ao longo de sua construção. O objetivo desse projeto é desenvolver um sistema de risco de crédito para apoiar decisões de concessão. Ao longo do projeto foram utilizadas as seguintes ferramentas: (xxx)  
## 1) Definição do cenário
Um banco fictício oferece cartão de crédito para pessoas físicas. Quando um cliente solicita um cartão, o banco precisa decidir se aprova ou reprova automaticamente a liberação ou se faz a revisão manualmente da decisão final. O modelo precisa aprender a analisar o histórico dos últimos 6 meses de um cliente (análise de dados) e qual a probabilidade de um cliente entrar em inadimplência nos próximos 6 meses (Cálculo de PD).
## 2) Objetivos principais
O modelo deve, primeiramente, realizar um cálculo de PD (Probability of Default) para cada cliente, que em seguida será convertido em uma tomada de decisão (Cálculo de Dafault).
## 3) Perguntas norteadoras
_Como instituições financeiras definem default?_  
Default representa que o cliente ultrapassou o tempo esperado de pagamento (atraso) e agora se encontra com possibilidades baixas de pagar o que deve. O default também pode representar que o cliente não está cumprindo outros fatores internos do banco.  
_O que é atraso de 30, 60, 90 dias (DPD — Days Past Due)?_  
Até 30 dias é um "atraso curto", cujas conclusões podem estar relacionadas com esquecimento, virada de mês e/ou burocracia do salário. Até 60 dias é um "atraso intermediário", cujas conclusões podem estar relacionadas com um problema de fluxo de caixa e/ou o cliente priorizou outra conta. Até 90 dias é um "atraso longo", em que as causas não necessariamente são compreendidas, mas dificilmente o cliente vai pagar 4 contas em atraso numa vez só. O banco não consegue mais colocar os juros do pagamento como receita esperada e o banco perde lucro, já que tem que gastar do seu saldo de reserva de proteção.  
_Qual a diferença entre atraso e default?_  
O atraso significa que o pagamento não foi efetuado, mas ainda há possibilidade de ser feito. Já o default significa que o banco pode classificar como baixa a possibilidade de pagamento.  
_O que é "cure" em crédito?_  
É quando um cliente retoma os pagamentos regulares após ter passado por um processo de default. No entanto, isso fica registrado no histórico do cliente e pode ser decisivo para liberação de crédito.  
_Por que utilizar disponibilidade de saldo para determinar a causa do atraso pode ser problemático?_  
Por causa dos atrasos de 30 e 60 dias. O cliente pode ter esquecido, priorizado outra dívida, transferido o dinheiro, investido, reservado para outra despesa, tido algum problema operacional ou ter escolhido não pagar.  
_Quais as regras para o Default = 1 e Default = 0 no modelo?_  
Se DPD >= 90 no período de 6 meses - default 1. Se DPD < 90 no período de 6 meses - default 0  
_O que significa performance window em credit scoring?_  
Performance window (horizonte de previsão) é o tempo futuro em que será observado se o cliente atingiu os critérios para default = 1. Será utilizado o período de 6 meses. O foco do performance window é determinar targets, ou seja, o que queremos que o modelo aprenda.  
_O que significa observation window?_  
Observation window (horizonte de observação) é o tempo passado que será estudado para alimentar o modelo que criará uma estimativa de PD. Será utilizado o período de 6 meses. É com ele que são criadas as variáveis do modelo. Alguns exemplos de variáveis são: quantidade de atrasos, maior DPD, frequência de utilização do limite, saldo médio, quantidade de pagamentos, comportamento de pagamento. O foco do observtion window é a criação de features, ou seja, informações que representam o comportamento do cliente.  
_Como se escolhe o horizonte de previsão de um modelo de crédito?_  
Depende do objetivo do modelo e de que forma ele auxiliará. Para esse projeto de análise de crédito, será escolhido o formato de 6 meses. O tempo estendido de 12 meses pode ser avaliado posteriormente conforme a necessidade do projeto.  
_Por que modelos de PD podem utilizar 12 meses?_  
Porque quanto maior o performance window (horizonte de previsão), mais chances do evento de default = 1 ocorrer. Outro ponto que justifica é o estudo do ciclo em 1 ano, em que é possível prever o comportamento do cliente frente a, por exemplo, eventos sazonais como férias ou datas comemorativas.  
_Como se dá o fluxo do projeto?_  
O estudo do Observation Window gera Features. O estudo do Performance Window gera Target (no caso desse modelo, um Default 0 ou 1). O conjunto de Features e Target resulta em treinamento do modelo. Por fim, o modelo retorna um PD.
