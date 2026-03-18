# Hospedagem de Site Estático no Amazon S3

## Objetivo
Criar e hospedar um site estático utilizando o Amazon S3, utilizando a AWS CLI para automação do processo, além de configurar permissões de acesso com IAM.

## Serviços Utilizados
- Amazon S3
- AWS Command Line Interface (AWS CLI)
- AWS Identity and Access Management (IAM)
- Amazon EC2
- AWS Systems Manager (Session Manager)

## Implementação

Durante este laboratório prático, foram realizadas as seguintes etapas:

1. Conexão com a instância EC2 utilizando o Session Manager (SSM).
2. Configuração da AWS CLI com credenciais de acesso.
3. Criação de um bucket S3 com nome único.
4. Criação de um usuário IAM com acesso ao serviço S3.
5. Associação de políticas de acesso ao usuário IAM.
6. Configuração das permissões do bucket para acesso público.
7. Extração dos arquivos do site estático em ambiente Linux.
8. Upload dos arquivos para o bucket utilizando AWS CLI.
9. Configuração do bucket para hospedagem de site estático.
10. Acesso ao site por meio do endpoint público do S3.
11. Criação de um script em bash para automatizar atualizações do site.
12. Alteração do conteúdo do site e reimplantação utilizando o script.

## Arquitetura da Solução
A solução consiste em uma instância EC2 acessada via Systems Manager, onde a AWS CLI é utilizada para interagir com os serviços da AWS. Um bucket S3 é criado para armazenar os arquivos do site estático e configurado para hospedagem pública. O IAM é utilizado para gerenciar permissões de acesso. A atualização do site é automatizada por meio de um script em bash, permitindo deploy rápido e eficiente das alterações.

## Evidências

<img width="1322" height="609" alt="Lab 170 1" src="https://github.com/user-attachments/assets/cc0314b9-a36e-4ff2-9bc8-6af7671177b2" />
<img width="1345" height="617" alt="Lab 170 3" src="https://github.com/user-attachments/assets/380f7903-6adb-42c3-b4a1-0f6b346b512c" />
<img width="587" height="603" alt="Lab 170 2" src="https://github.com/user-attachments/assets/0189f280-bac3-4bea-aeb9-2bcbbf51d390" />


## Script
```bash
# Configurar CLI
aws configure

# Criar bucket
aws s3api create-bucket --bucket <nome-do-bucket> --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2

# Configurar site estático
aws s3 website s3://<nome-do-bucket>/ --index-document index.html

# Upload dos arquivos
aws s3 cp /home/ec2-user/sysops-activity-files/static-website/ s3://<nome-do-bucket>/ --recursive --acl public-read

# Listar arquivos no bucket
aws s3 ls s3://<nome-do-bucket>/

# Script de atualização
#!/bin/bash
aws s3 cp /home/ec2-user/sysops-activity-files/static-website/ s3://<nome-do-bucket>/ --recursive --acl public-read
````
## Aprendizado

Este laboratório proporcionou uma experiência prática completa na criação e hospedagem de um site estático utilizando o Amazon S3. Foi possível compreender o processo de configuração de permissões, uso da AWS CLI para automação e integração com o IAM para controle de acesso. Além disso, a criação de um script para atualização do site reforçou conceitos importantes de automação e deploy contínuo, habilidades essenciais para atuação profissional em Cloud Computing.
