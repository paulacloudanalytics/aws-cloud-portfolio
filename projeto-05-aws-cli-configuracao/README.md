# Instalação e Configuração da AWS CLI

## Objetivo
Instalar e configurar a AWS Command Line Interface (AWS CLI) em uma instância Linux Red Hat, utilizando um ambiente Windows com acesso via PuTTY, permitindo a interação com serviços da AWS por linha de comando com autenticação segura via IAM.

## Serviços Utilizados
- Amazon EC2
- AWS Command Line Interface (AWS CLI)
- AWS Identity and Access Management (IAM)
- Amazon VPC
- SSH (Secure Shell)
- PuTTY (cliente SSH)

## Implementação

Durante este laboratório prático, foram realizadas as seguintes etapas:

1. Acesso ao ambiente AWS e obtenção das credenciais do laboratório.
2. Download da chave de acesso no formato `.ppk`.
3. Conexão com a instância EC2 Red Hat via SSH utilizando o PuTTY no Windows.
4. Download e instalação da AWS CLI na instância Linux.
5. Validação da instalação por meio de comandos de verificação.
6. Acesso ao console do IAM para análise de usuários e políticas.
7. Configuração da AWS CLI com credenciais (Access Key e Secret Key).
8. Execução de comandos para interação com o IAM via CLI.

## Arquitetura da Solução
A solução consiste em uma VPC contendo uma instância EC2 baseada em Linux Red Hat. O acesso à instância foi realizado a partir de um ambiente Windows utilizando o PuTTY para conexão SSH. Dentro da instância, a AWS CLI foi instalada e configurada, permitindo interação com serviços da AWS. O IAM foi utilizado para controle de acesso, garantindo segurança na autenticação e autorização das operações realizadas.

## Evidências

<img width="800" height="368" alt="image" src="https://github.com/user-attachments/assets/033b6f28-a048-4390-b305-594c35097d44" />

<img width="800" height="366" alt="image" src="https://github.com/user-attachments/assets/bd13a0bb-ae19-42ce-9a49-13f4c061e8b5" />

<img width="587" height="603" alt="image" src="https://github.com/user-attachments/assets/92b06984-d251-449d-b202-01a959d4ec9e" />




## Script
```bash
# Download da AWS CLI
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

# Descompactar
unzip -u awscliv2.zip

# Instalar
sudo ./aws/install

# Verificar instalação
aws --version

# Ajuda da CLI
aws help

# Configurar credenciais
aws configure

# Testar acesso ao IAM
aws iam list-users
```
## Aprendizado

Este laboratório proporcionou uma experiência prática completa na utilização da AWS CLI em um ambiente Windows com acesso remoto via PuTTY. Foi possível compreender o processo de conexão segura com instâncias EC2, além da instalação e configuração da CLI em um ambiente Linux. A prática reforçou a importância do uso de ferramentas de linha de comando e autenticação via IAM, habilidades essenciais para atuação profissional em Cloud Computing.
