# Projeto 13 - Monitoramento com CloudWatch, EventBridge e AWS Config

## Objetivo
Implementar uma solução completa de monitoramento e observabilidade na AWS, coletando métricas e logs de instâncias EC2, criando alarmes, automatizando respostas a eventos e garantindo conformidade com AWS Config.

---

## Serviços utilizados
- Amazon EC2
- Amazon CloudWatch (Logs, Metrics, Alarms)
- AWS Systems Manager
- Amazon EventBridge
- Amazon SNS
- AWS Config

---

## Implementação

### 🔹 Etapa 1: Instalação do CloudWatch Agent
- Utilização do Systems Manager (Run Command)
- Instalação do pacote AmazonCloudWatchAgent na instância EC2

### 🔹 Etapa 2: Configuração do Agent
- Criação de parâmetro no Parameter Store (Monitor-Web-Server)
- Aplicação da configuração via comando AmazonCloudWatch-ManageAgent

### 🔹 Etapa 3: Coleta de Logs
- Logs monitorados:
  - HttpAccessLog
  - HttpErrorLog
- Criação de filtro para erros 404 (métrica 404Errors)

### 🔹 Etapa 4: Criação de Alarme
- Condição: ≥ 5 erros em 1 minuto
- Integração com SNS para envio de notificações

### 🔹 Etapa 5: Automação com EventBridge
- Monitoramento de eventos da EC2 (stop e terminate)
- Disparo de notificações via SNS

### 🔹 Etapa 6: Teste prático
- Parada da instância EC2
- Validação do recebimento de alerta por e-mail

### 🔹 Etapa 7: Conformidade com AWS Config
- Regra de obrigatoriedade de tags (project)
- Verificação de uso de volumes (ec2-volume-inuse-check)

---

## Arquitetura da solução

<img width="2391" height="926" alt="image" src="https://github.com/user-attachments/assets/dcf492bf-4333-49e5-9c41-633e298ad84f" />



---


## Evidências
### CloudWatch Agent instalado e coletando dados

  <img width="1032" height="539" alt="lab 186" src="https://github.com/user-attachments/assets/71b6e419-e188-451c-8973-2266bcca56ab" />
<img width="1348" height="433" alt="lab 186 1" src="https://github.com/user-attachments/assets/77cedd0d-af3b-4b12-b1fa-faa5fd994acf" />

### Logs sendo enviados para CloudWatch Logs

  <img width="1071" height="387" alt="lab 186 2" src="https://github.com/user-attachments/assets/4cae08c8-7a1b-4c0c-896d-44db628ba9bd" />
  
### Métrica personalizada 404Errors criada

  <img width="1074" height="492" alt="lab 186 3" src="https://github.com/user-attachments/assets/1b0af16f-c98d-4c10-b089-179652ad40a3" />

### Alarme configurado e acionado

  <img width="1082" height="310" alt="lab 186 4" src="https://github.com/user-attachments/assets/08ffc811-a159-497a-91b8-171b16cd9169" />
<img width="1087" height="525" alt="lab 186 5" src="https://github.com/user-attachments/assets/0233290c-fea3-406e-b9d4-da0a237811a1" />

###Notificação recebida via SNS

  <img width="1046" height="448" alt="lab 186 6" src="https://github.com/user-attachments/assets/ab86baa1-ba7b-451b-89a4-f07d7a119f66" />

### Regra do EventBridge funcionando corretamente
  <img width="1039" height="341" alt="lab 186 8" src="https://github.com/user-attachments/assets/94eb228d-8208-4133-be6c-3e8f3ebe745a" />

### AWS Config avaliando conformidade dos recursos

<img width="1019" height="191" alt="lab 186 9" src="https://github.com/user-attachments/assets/0a55dd73-51f8-40c3-938e-881c0bfa22e0" />
<img width="1013" height="199" alt="lab 186 10" src="https://github.com/user-attachments/assets/0a663ab9-8ddc-46e7-afd7-1482d001f93c" />

---

## Script

### Instalação do Agent
```bash
aws ssm send-command \
--document-name "AWS-ConfigureAWSPackage" \
--parameters '{"action":["Install"],"name":["AmazonCloudWatchAgent"]}'
````
### Configuração do Agent
```bash
aws ssm send-command \
--document-name "AmazonCloudWatch-ManageAgent" \
--parameters '{"action":["configure"],"mode":["ec2"],"config-source":["ssm"]}'
````
### Filtro de métrica 404
```bash
[ip, id, user, timestamp, request, status_code=404, size]
````

## Aprendizado

Neste laboratório, aprendi na prática como estruturar um sistema completo de monitoramento na AWS, integrando diferentes serviços para observar, reagir e garantir a saúde da infraestrutura. Entendi como coletar métricas e logs detalhados de instâncias EC2 com o CloudWatch Agent, transformar esses dados em insights por meio de filtros e alarmes, e automatizar respostas a eventos com EventBridge e SNS. Além disso, compreendi a importância da governança com o AWS Config, garantindo que os recursos estejam em conformidade com boas práticas. Esse conjunto de ferramentas mostrou como construir soluções mais resilientes, observáveis e preparadas para cenários reais de produção.
