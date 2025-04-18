
Desafio 1 👨🏽‍💻
Provisionamento de uma instância EC2 de forma automatizada via Terraform

A instância deve conter as seguintes características:

Formato: t3.medium
Nome: ec2-iac-site
Grupo de Segurança: Portas 80, 433 e 22 liberadas utilizando blocos dinâmicos
Tags: Deve conter tags locais, sendo elas:
Ambiente: Desenvolvimento
Horário: Mackenzie
Aplicação: Site
BU: Conta Digital
Na saída do provisionamento (Output) você deve obter as seguintes informações:

ARN da instância
IP público de instância
DNS público de instância
A arquitetura VPC deve ficar da seguinte forma:

Desafio 01

1 VPC
1 Gateway de Internet
1 Sub-rede pública
1 RouteTable (Pública, apontando para o Internet Gateway)
1 instância EC2 na sub-rede pública

+-------------------------------------------------------+
|                    AWS Region                         |
|                                                       |
|  +---------------------+                              |
|  |       VPC           |                              |
|  | 10.0.0.0/16         |                              |
|  |                     |                              |
|  |  +---------------+  |  +-----------------------+  |
|  |  | Public Subnet |  |  | Internet Gateway      |  |
|  |  | 10.0.1.0/24   |--|->| (igw-iac-site)        |  |
|  |  +---------------+  |  +-----------------------+  |
|  |          |          |                             |
|  |          v          |                             |
|  |  +---------------+  |                             |
|  |  | Route Table   |  |                             |
|  |  | (rt-public)   |  |                             |
|  |  | 0.0.0.0/0 -> |  |                             |
|  |  | Internet GW   |  |                             |
|  |  +---------------+  |                             |
|  |                     |                             |
|  |  +---------------+  |                             |
|  |  | EC2 Instance  |  |                             |
|  |  | (ec2-iac-site)|  |                             |
|  |  | t3.medium     |  |                             |
|  |  |               |  |                             |
|  |  | Security Group|  |                             |
|  |  | Ports: 22,80,443 |                             |
|  |  +---------------+  |                             |
|  |                     |                             |
|  +---------------------+                             |
|                                                       |
+-------------------------------------------------------+

Legenda do Diagrama:
VPC (10.0.0.0/16):

Contém todos os recursos da arquitetura

Subnet Pública (10.0.1.0/24):

Configurada para atribuir IPs públicos automaticamente

Associada à Route Table pública

Internet Gateway:

Conecta a VPC à internet

Ponto de saída para tráfego público

Route Table Pública:

Rota padrão (0.0.0.0/0) apontando para o Internet Gateway

Associada à subnet pública

Instância EC2:

Tipo: t3.medium

Nome: ec2-iac-site

Localizada na subnet pública

Tags: Ambiente=Desenvolvimento, Horário=Mackenzie, etc.

Security Group:

Regras de entrada para as portas 22 (SSH), 80 (HTTP) e 443 (HTTPS)

Regra de saída liberada para toda internet

Fluxo de Tráfego:
A instância EC2 na subnet pública pode se comunicar com a internet através do Internet Gateway

O tráfego de internet para a EC2 passa pelo Internet Gateway e é roteado pela Route Table pública

As conexões nas portas 22, 80 e 443 são permitidas pelo Security Group associado à instância

ariosto leal
