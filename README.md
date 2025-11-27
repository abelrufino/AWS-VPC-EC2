# AWS-VPC-EC2
Criando na AWS VPC e iniciando um servidor EC2 Web 

Este laboratório **Criar uma VPC (Virtual Private Cloud) através do Console da AWS (Amazon Web Services).**.

---

## 🚀 Objetivo do laboratório 🚀

- Criar uma Virtual Private Cloud (VPC)
- Criar Criar sub-redes
- Configurar um grupo de segurança
- Executar uma instância do Amazon Elastic Compute Cloud (Amazon EC2) dentro da nova VPC

---

##  Etapa 1: Criar a VPC

1. Na página do Console da AWS, ir na busca e digitar VPC
2. Na lateral da página, clicar em Suas VPCs e em seguida Criar VPC
3. Na página Criar VPC, selecionar Somente VPC e em seguida digitar o nome da VPC: Lab VPC
4. Em CIDR IPv4 digitar o endereçamento IP conforme o diagrama: 10.0.0.0/16
5. Clicar em Criar VPC
6. Pronto, a VPC foi criada e configurada
---

##  Etapa 2: Criar as sub-redes

1. Na lateral da página, clicar em Sub-redes
2. Na página Criar sub-rede, clicar em ID da VPC e selecionar a VCP criada: Lab VPC
3. Em seguida clicar em Adicionar nova sub-rede
4. Em Sub-rede 1 de 1, digite o nome da sub-rede: Public Subnet 1
5. Em Zona de disponibilidade selecionar Oeste dos EUA (Oregon) / us-west-2-a
6. Em CIDR IPv4 digitar o endereçamento IP conforme o diagrama: 10.0.0.0/24
7. Em seguida clicar em Adicionar nova sub-rede
8. Em Sub-rede 2 de 2, digite o nome da sub-rede: Public Subnet 2
9. Em Zona de disponibilidade selecionar Oeste dos EUA (Oregon) / us-west-2-b
10. Em CIDR IPv4 digitar o endereçamento IP conforme o diagrama: 10.0.2.0/24
11. Em seguida clicar em Adicionar nova sub-rede
12. Em Sub-rede 3 de 3, digite o nome da sub-rede: Private Subnet 1
13. Em Zona de disponibilidade selecionar Oeste dos EUA (Oregon) / us-west-2-a
14. Em CIDR IPv4 digitar o endereçamento IP conforme o diagrama: 10.0.1.0/24
15. Em seguida clicar em Adicionar nova sub-rede
16. Em Sub-rede 4 de 4, digite o nome da sub-rede: Private Subnet 2
17. Em Zona de disponibilidade selecionar Oeste dos EUA (Oregon) / us-west-2-b
18. Em CIDR IPv4 digitar o endereçamento IP conforme o diagrama: 10.0.3.0/24
19. Em seguida clicar em Criar sub-rede
20. Pronto, as sub-redes foram criadas e configuradas
---

##  Etapa 3: Criar uma tabela de rotas

1. Primeiro, vamos configurar a tabela de rotas existente e associar as sub-redes públicas
2. Na lateral da página, clicar em Tabela de rotas
3. Localizar a tabela da VPC criada (Lab VPC) e renomear para Public Route Table
4. Selecionar a tabela Public Route Table, ir para a guia Associações de sub-rede e clicar em Editar associações de sub-rede
5. Na página Editar associações de sub-rede, selecionar a Public Subnet 1 e Public Subnet 2
6. Em seguida clicar em Salvar associações
7. Agora vamos criar uma nova tabela de rotas e associar as sub-redes privadas
8. Em Tabelas de rotas, clicar em Criar tabela de rotas
9. Em Configurações da tabela de rotas digitar o nome: Private Route Table
10. Em VPC, selecionar a VPC criada: Lab VPC
11. Em seguida clicar em Criar tabelas de rotas
12. Agora vamos associar a nova tabela de rotas criada às sub-redes privadas
13. Em Tabela de rotas, selecionar a tabela Private Route Table
14. Na guia Associações de sub-rede, clicar em Editar associações de sub-rede
15. Na página Editar associações de sub-rede, selecionar a Private Subnet 1 e Private Subnet 2
16. Em seguida clicar em Salvar associações
17. Pronto, as tabelas de rotas foram criadas e configuradas
---

##  Etapa 4: Criar uma Internet Gateway

1. Na lateral da página, clicar em Gateways da internet
2. Em seguida, clicar em Criar Gateway da Internet
3. Na página, digitar o nome da Gateway: Lab-gateway
4. Clicar em Criar Gateway da Internet
5. Agora vamos associar a gateway à nossa VPC
6. Em Gateway da internet, selecionar Lab-gateway
7. Em seguida, clicar em Ações e selecionar Associar à VPC
8. Na página Associar à VPC, selecionar a opção Lab-VPC
9. Em seguida, clicar em Associar gateway da Internet
10. Pronto, a gateway de internet foi criada e configurada
---

##  Etapa 5: Configurar as sub-redes públicas

1. Na lateral da página, clicar em Tabela de rotas
2. Em Tabela de rotas, selecionar Public Route Table
3. Ir para a guia Rotas e clicar em Editar rotas
4. Em Editar rotas, clicar em Adicionar rota
5. Em Destino, digitar o endereço: 0.0.0.0/0
6. Em Alvo, selecionar Gateway da Internet
7. Em seguida, clicar em Salvar alterações
8. Pronto, as sub-redes públicas foram configuradas
---

##  Etapa 6: Criar um Gateway NAT

1. Na lateral da página, clicar em Gateways NAT
2. Em seguida clicar em Criar gateway NAT
3. Em nome, digitar o nome da NAT gateway: Lab-NAT
4. Em Sub-rede selecionar uma sub-rede pública: Public Subnet 1
5. Em ID de alocação do IP elástico, clicar em Alocar IP Elástico
6. Em seguida clicar em Criar gateway NAT
7. Pronto, o gateway NAT foi criado e configurado
---

##  Etapa 7: Configurar as sub-redes privadas

1. Na lateral da página, clicar em Tabela de rotas
2. Em Tabela de rotas, selecionar Private Route Table
3. Ir para a guia Rotas e clicar em Editar rotas
4. Em Editar rotas, clicar em Adicionar rota
5. Em Destino, digitar o endereço: 0.0.0.0/0
6. Em Alvo, selecionar NAT Gateway
7. Em seguida, clicar em Salvar alterações
8. Pronto, as sub-redes privadas foram configuradas
---

Etapa 8: Configurar a atribuição automática de IP

1. Agora vamos configurar a sub-rede púbica, para que os recursos recebam um IP automático ao serem provisionados
2. Na lateral da página, clicar em Sub-redes
3. Em Sub-redes, selecionar Public Subnet 1
4. Em seguida, clicar em Ações e selecionar Editar configurações de sub-rede
5. Em atribuição automática de IP, clicar em Habilitar endereço IPv4
6. Em seguida clicar em Salvar
7. Repetir o processo na segunda sub-rede pública
8. Em Sub-redes, selecionar Public Subnet 2
9. Em seguida, clicar em Ações e selecionar Editar configurações de sub-rede
10. Em atribuição automática de IP, clicar em Habilitar endereço IPv4
11. Em seguida clicar em Salvar
12. Pronto, as sub-redes públicas foram configuradas
---

Etapa 9: Criar um Security Group

1. Agora vamos criar um grupo de segurança, que atua como um firewall para a instância EC2
2. Na lateral da página, clicar em Grupos de segurança
3. Em seguida, clicar em Criar grupo de segurança
4. Em Nome do grupo de segurança digitar: Web Security Group
5. Em Descrição digitar: Ativar acesso HTPP
6. Em VPC, selecionar a VPC criada: Lab VPC
7. Agora vamos configurar as Regras de entrada
8. Em Tipo selecionar o protocolo HTPP
9. Em Origem, selecionar Qualquer local-IPv4 e digitar o endereço 0.0.0.0/0
10. Em seguida clicar em Criar grupo de segurança
11. Pronto, o grupo de segurança foi criado e configurado
---

Etapa 10: Criar uma instância EC2

1. Agora vamos criar o servidor web, aquele que será nosso atendente na cafeteria
2. Na página do Console da AWS, ir na busca e digitar EC2
3. Na lateral da página, clicar em Instâncias
4. Em seguida, clicar em Executar instâncias
5. Em Iniciar uma instância, digitar o nome do servidor web: Lab-servidor
6. Em Imagem de máquina da Amazon selecionar: Amazon Linux 2 AMI
7. Em Tipo de instância selecionar: t2.micro
8. Em Par de chaves selecionar: vockey
9. Em Configurações de rede, clicar em Editar
10. Em VPC selecionar: Lab VPC
11. Em Sub-rede selecionar: Public Subnet 1
12. Em Firewall, selecionar grupo de segurança existente
13. Em Grupos de segurança comuns selecionar: Web Security Group
14. Em Detalhes avançados, copie e cole este código na caixa Dados do usuário:
---

## 🖥️ Execução Local
1. Baixe ou clone este repositório.
2. Abra o arquivo `index.html` em um navegador.
3. (Opcional) Se estiver em uma instância **EC2**, a página exibirá automaticamente a **Região e AZ**.

---
User Data - Deploy Automático da Página 

 Esse script para faz o deploy automático do seu site quando a instância EC2 com imagens de aplicação e de sistemas operacional AMI AMAZON LINUX é iniciada.
Ele instala o Apache, clona o repositório e exibe a página diretamente no navegador via IP público da instância.

```
#!/bin/bash
#Install Apache Web Server and PHP
dnf install -y httpd wget php mariadb105-server

#Download Lab files
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCLFO-2/2-lab2-vpc/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/

#Turn on web server
chkconfig httpd on
service httpd start 

```


User Data - Deploy Automático da Página 

 Esse script para faz o deploy automático do seu site quando a instância EC2 com imagens de aplicação e de sistemas operacional AMI LINUX UBUNTU é iniciada.
Ele instala o Apache, clona o repositório e exibe a página diretamente no navegador via IP público da instância.

```
#!/bin/bash

# === Update packages ===
sudo apt update -y
sudo apt upgrade -y

# === Install Git and Apache2 ===
sudo apt install -y git apache2

# === Start and enable Apache ===
sudo systemctl start apache2
sudo systemctl enable apache2

# === Clone the repository ===
cd /var/www/html
sudo git clone https://github.com/abelrufino/AWS-EC2--PaginaTest.git

# Copy content to web root
sudo cp -r AWS-EC2--PaginaTest/* /var/www/html/

# === Get IMDSv2 token ===
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
-H "X-aws-ec2-metadata-token-ttl-seconds: 21600" -s)

# === Fetch metadata ===
AZ=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" \
-s http://169.254.169.254/latest/meta-data/placement/availability-zone)

REGION=${AZ::-1}

# === Update HTML with Region and AZ ===
sudo sed -i "s/<span id=\"region\" class=\"font-semibold text-cyan-300\">Detecting...<\/span>/<span id=\"region\" class=\"font-semibold text-cyan-300\">${REGION}<\/span>/g" /var/www/html/index.html

sudo sed -i "s/<span id=\"az\" class=\"font-semibold text-cyan-300\">Detecting...<\/span>/<span id=\"az\" class=\"font-semibold text-cyan-300\">${AZ}<\/span>/g" /var/www/html/index.html

# === Fix permissions for Ubuntu (Apache user = www-data) ===
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

# Restart Apache
sudo systemctl restart apache2

```

##  Autor
**Abel Neto**  
© 2025 - Amanzon AWS  
🔗 [LinkedIn](https://www.linkedin.com/in/abel-joão-rufino-neto-9a2a1b49/)










