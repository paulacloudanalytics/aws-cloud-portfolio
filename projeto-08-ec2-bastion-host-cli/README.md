# Arquitetura com EC2 Bastion Host e Provisionamento via AWS CLI

## Objetivo
Criar uma arquitetura com um Bastion Host utilizando Amazon EC2 e provisionar uma segunda instância (servidor web) por meio da AWS CLI, aplicando conceitos de acesso seguro e automação.

## Serviços Utilizados
- Amazon EC2
- AWS CLI
- AWS Systems Manager (Parameter Store)
- Amazon VPC
- Security Groups

## Implementação

Durante este laboratório prático, foram realizadas as seguintes etapas:

1. Criação de uma instância EC2 atuando como Bastion Host.
2. Configuração da instância utilizando Amazon Linux 2.
3. Definição de Security Group permitindo acesso SSH.
4. Associação de Role IAM para permitir uso da AWS CLI.
5. Conexão segura ao Bastion Host utilizando EC2 Instance Connect.
6. Utilização da AWS CLI para automação de recursos.
7. Recuperação da AMI mais recente via AWS Systems Manager Parameter Store.
8. Recuperação do ID da sub-rede pública via CLI.
9. Recuperação do Security Group do servidor web.
10. Download de script de dados do usuário (User Data).
11. Criação de uma instância EC2 via AWS CLI.
12. Configuração automática do servidor web (Apache) via script.
13. Monitoramento do status da instância via CLI.
14. Obtenção do DNS público da instância.
15. Teste do servidor web em execução no navegador.

## Arquitetura da Solução
A arquitetura consiste em um Bastion Host em uma sub-rede pública que serve como ponto seguro de acesso. A partir dele, uma segunda instância EC2 é provisionada via AWS CLI, configurada automaticamente como servidor web por meio de User Data. O controle de acesso é realizado com Security Groups, e a automação é feita utilizando comandos da AWS CLI, garantindo padronização e eficiência no provisionamento.

## Evidências

<img width="1118" height="309" alt="Lab 171 1" src="https://github.com/user-attachments/assets/a50799d6-f225-482f-a454-cc3c8ab40c8d" />
<img width="1158" height="382" alt="Lab 171 2" src="https://github.com/user-attachments/assets/0bbe61f9-28cd-49f5-9a9c-613b5507b77d" />


## Script

```bash
# Definir região automaticamente
AZ=`curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone`
export AWS_DEFAULT_REGION=${AZ::-1}

# Obter AMI mais recente
AMI=$(aws ssm get-parameters --names /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2 --query 'Parameters[0].[Value]' --output text)

# Obter Subnet
SUBNET=$(aws ec2 describe-subnets --filters 'Name=tag:Name,Values=Public Subnet' --query Subnets[].SubnetId --output text)

# Obter Security Group
SG=$(aws ec2 describe-security-groups --filters Name=group-name,Values=WebSecurityGroup --query SecurityGroups[].GroupId --output text)

# Baixar script de configuração
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-RSJAWS-1-23732/171-lab-JAWS-create-ec2/s3/UserData.txt

# Criar instância Web Server
INSTANCE=$(aws ec2 run-instances \
--image-id $AMI \
--subnet-id $SUBNET \
--security-group-ids $SG \
--user-data file:///home/ec2-user/UserData.txt \
--instance-type t3.micro \
--tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=Web Server}]' \
--query 'Instances[*].InstanceId' \
--output text)

# Verificar status
aws ec2 describe-instances --instance-ids $INSTANCE --query 'Reservations[].Instances[].State.Name' --output text

# Obter DNS público
aws ec2 describe-instances --instance-ids $INSTANCE --query Reservations[].Instances[].PublicDnsName --output text
````
## Aprendizado

Este laboratório foi fundamental para consolidar conhecimentos sobre arquitetura em nuvem e automação na AWS. Foi possível entender na prática o conceito de Bastion Host como ponto seguro de acesso, além de utilizar a AWS CLI para provisionar recursos de forma automatizada. Também foram reforçados conceitos como uso de User Data para configuração automática, recuperação dinâmica de recursos (AMI, sub-rede e Security Groups) e boas práticas de segurança. Esse tipo de abordagem é essencial para ambientes profissionais que exigem escalabilidade, padronização e redução de erros manuais.
