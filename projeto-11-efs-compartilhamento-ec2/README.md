# Projeto 11 — Compartilhamento de Arquivos com Amazon EFS

---

## Objetivo

Implementar um sistema de armazenamento compartilhado na AWS utilizando o Amazon EFS (Elastic File System), permitindo que múltiplas instâncias EC2 acessem e manipulem os mesmos arquivos simultaneamente.

---

## Serviços utilizados

- Amazon VPC
- Amazon EC2
- Amazon EFS
- AWS CLI / Terminal Linux
- EC2 Instance Connect / Secure Shell

---

## Implementação

O laboratório foi executado seguindo as etapas abaixo:

1. Criação de uma VPC completa
   - Utilização de sub-redes públicas

2. Criação de três instâncias EC2
   - Distribuídas em diferentes zonas de disponibilidade

3. Criação do sistema de arquivos no Amazon EFS
   - Endpoint criado:
     fs-0bfdadb3e6d87f951.efs.us-west-2.amazonaws.com

4. Montagem do EFS em duas instâncias EC2
   - Instalação de dependências
   - Criação de diretório
   - Montagem do sistema de arquivos

5. Validação do compartilhamento
   - Arquivos criados em uma instância são acessíveis na outra

---

## Arquitetura da solução
<img width="1536" height="1024" alt="Diagrama Arquitetura Lab 10 04" src="https://github.com/user-attachments/assets/03991c06-36c9-43f3-8e45-c149ce647d71" />


A arquitetura consiste em:

- Uma VPC com sub-redes públicas
- Três instâncias EC2
- Um sistema de arquivos Amazon EFS
- Duas instâncias montando o mesmo EFS simultaneamente

Isso permite armazenamento compartilhado e persistente entre servidores.

---

## Evidências


### VPC e Sub-redes criadas e configuradas com IPV4 automático
<img width="1346" height="408" alt="Lab 10 04 - 1" src="https://github.com/user-attachments/assets/c2ee514c-8e97-4e61-bb14-3ef66be88e80" />

### Grupo de segurança criado
<img width="1344" height="341" alt="Lab 10 04 - 2" src="https://github.com/user-attachments/assets/1c7737d8-9f5e-4f6a-a807-94f6e6a174d7" />

### Sistema de arquivos EFS criado
<img width="1353" height="476" alt="Lab 10 04 - 3" src="https://github.com/user-attachments/assets/e75e778c-c50a-420a-bcd7-6f60fc81641c" />

### Conexão via Secure Shell
<img width="1321" height="569" alt="Lab 10 04 - 4" src="https://github.com/user-attachments/assets/9954c3ac-b255-40c4-8835-c237113496fd" />

### Verificação com df -h
<img width="1361" height="574" alt="Lab 10 04 - 5" src="https://github.com/user-attachments/assets/82945d6c-bf8c-4147-8665-e4ea5e83d14f" />

### As 3 instâncias criadas e configuradas
<img width="1366" height="725" alt="Lab 10 04 - 6" src="https://github.com/user-attachments/assets/d403089e-4763-46f6-afea-deb1bc5e72df" />


---

## Script

Comandos utilizados para montar o EFS:

```bash
sudo -s
yum -y update
yum install -y amazon-efs-utils

mkdir financeiro

sudo mount -t efs -o tls fs-0bfdadb3e6d87f951.efs.us-west-2.amazonaws.com:/ financeiro

df -h
````
## Aprendizado

Este laboratório proporcionou uma compreensão prática sobre:

- Como implementar armazenamento compartilhado na AWS
- Diferença entre armazenamento local e distribuído
- Uso do Amazon EFS para aplicações escaláveis
- Montagem de sistemas de arquivos em múltiplas instâncias
- Importância do EFS em arquiteturas resilientes

Além disso, reforçou o entendimento de como serviços da AWS se integram para formar soluções completas em cloud computing.
