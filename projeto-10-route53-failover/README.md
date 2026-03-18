# Failover com Route 53

## Objetivo
Implementar um mecanismo de alta disponibilidade utilizando o Amazon Route 53, configurando failover automático entre duas instâncias EC2 em diferentes Zonas de Disponibilidade.

## Serviços Utilizados
- Amazon EC2
- Amazon Route 53
- Amazon CloudWatch
- AWS SNS (Simple Notification Service)
- AWS CloudFormation

## Implementação

Durante este laboratório prático, foram realizadas as seguintes etapas:

1. Validação das duas instâncias EC2 (primária e secundária) com aplicação web ativa.
2. Verificação de que as instâncias estão em diferentes Zonas de Disponibilidade.
3. Teste de acesso às URLs individuais de cada instância.
4. Criação de uma Health Check no Route 53 para monitorar o endpoint da instância primária.
5. Configuração de verificação com intervalo de 10 segundos e limite de falha 2.
6. Configuração de alerta via SNS com envio de e-mail.
7. Confirmação da assinatura do tópico SNS por e-mail.
8. Criação de registro DNS do tipo A para o servidor primário.
9. Configuração de política de roteamento Failover (Primary).
10. Associação da Health Check ao registro primário.
11. Criação de registro DNS do tipo A para o servidor secundário.
12. Configuração de política de roteamento Failover (Secondary).
13. Teste de resolução DNS apontando para a instância primária.
14. Simulação de falha ao parar a instância primária.
15. Monitoramento da Health Check identificando falha.
16. Verificação do failover automático para a instância secundária.
17. Confirmação do envio de alerta por e-mail.

## Arquitetura da Solução
A arquitetura é composta por duas instâncias EC2 executando a mesma aplicação em diferentes Zonas de Disponibilidade. O Amazon Route 53 atua como serviço de DNS inteligente, monitorando a saúde da instância primária através de uma Health Check. Em caso de falha, o tráfego é automaticamente redirecionado para a instância secundária. O Amazon SNS é utilizado para envio de alertas em tempo real.

## Evidências

<img width="1048" height="502" alt="176 1" src="https://github.com/user-attachments/assets/e05f3368-a3ee-41a7-828f-991ca911e69c" />
<img width="984" height="590" alt="176 2" src="https://github.com/user-attachments/assets/198f1f57-1540-4f8e-a3ee-ba6476710f23" />
<img width="978" height="582" alt="176 3" src="https://github.com/user-attachments/assets/6e3ae04c-9827-40ba-ad17-7c1044766cca" />


## Aprendizado
Este laboratório demonstrou na prática como implementar alta disponibilidade utilizando DNS com o Route 53. Foi possível entender como funcionam as Health Checks, o roteamento baseado em failover e a importância de distribuir aplicações entre múltiplas Zonas de Disponibilidade. Além disso, reforçou o uso de monitoramento e alertas com CloudWatch e SNS, garantindo rápida resposta a falhas. Esse tipo de arquitetura é amplamente utilizado em ambientes produtivos para garantir resiliência e continuidade de serviços.
