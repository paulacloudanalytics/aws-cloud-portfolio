# AWS Systems Manager

## Objetivo
Explorar o AWS Systems Manager para centralizar a gestão operacional e automatizar tarefas em recursos da AWS, incluindo instâncias EC2 e outros ambientes.

## Serviços Utilizados
- AWS Systems Manager
- Amazon EC2

## Implementação

Durante este laboratório prático, foram realizadas as seguintes etapas:

1. Verificação das configurações e permissões necessárias para uso do Systems Manager.
2. Execução de tarefas em múltiplas instâncias de forma centralizada.
3. Atualização de configurações de aplicações por meio de automações.
4. Acesso à linha de comando das instâncias utilizando o Systems Manager, sem necessidade de conexão direta via SSH.

## Arquitetura da Solução
A solução utiliza o AWS Systems Manager como ferramenta central para gerenciamento de recursos, permitindo executar comandos, automatizar tarefas e acessar instâncias de forma segura. As instâncias EC2 são gerenciadas sem exposição direta à internet, aumentando a segurança operacional e reduzindo a dependência de acesso remoto tradicional.

## Evidências

<img width="800" height="320" alt="image" src="https://github.com/user-attachments/assets/d4ce7a17-3cae-4386-8f7f-b410c7f33558" />

<img width="800" height="267" alt="image" src="https://github.com/user-attachments/assets/cc5416e5-971a-42b4-8f6b-59daff2fb3d3" />


## Aprendizado
Este laboratório proporcionou uma visão prática sobre gerenciamento centralizado de recursos na AWS. Foi possível compreender como o Systems Manager facilita operações em escala, melhora a segurança ao evitar acesso direto às instâncias e permite automação de tarefas administrativas. Esse conhecimento é fundamental para ambientes corporativos que exigem eficiência operacional e controle sobre múltiplos recursos.
