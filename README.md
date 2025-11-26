# AWS-VPC-EC2
Criando na AWS VPC e iniciando um servidor EC2 Web 

Este laboratório **Criar uma VPC (Virtual Private Cloud) através do Console da AWS (Amazon Web Services).**.

---

## 🚀 Objetivo do laboratório 🚀
Esta página demonstra:
- Criar uma Virtual Private Cloud (VPC);
- **Criar sub-redesa**;
- **Configurar um grupo de segurança**
- Criar uma Virtual Private Cloud (VPC);

---

##  Etapa 1: Criar a VPC
- Na página do Console da AWS, ir na busca e digitar VPC
- Na lateral da página, clicar em Suas VPCs e em seguida Criar VPC
- Na página Criar VPC, selecionar Somente VPC e em seguida digitar o nome da VPC: Lab VPC
- Em CIDR IPv4 digitar o endereçamento IP conforme o diagrama: 10.0.0.0/16
- Clicar em Criar VPC
- Pronto, a VPC foi criada e configurada  

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
# Update packages
sudo yum update -y

# Install Git and Apache
sudo yum install -y git httpd

# Start and enable Apache
sudo systemctl start httpd
sudo systemctl enable httpd

# Clone the repository
cd /var/www/html
sudo git clone https://github.com/abelrufino/AWS-EC2--PaginaTest.git
sudo cp -r AWS-EC2--PaginaTest/* /var/www/html/

# ===== Get IMDSv2 token =====
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
-H "X-aws-ec2-metadata-token-ttl-seconds: 21600" -s)

# ===== Fetch metadata =====
AZ=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" \
-s http://169.254.169.254/latest/meta-data/placement/availability-zone)
REGION=${AZ::-1}

# ===== Insert into the page =====
sudo sed -i "s/<span id=\"region\" class=\"font-semibold text-cyan-300\">Detecting...<\/span>/<span id=\"region\" class=\"font-semibold text-cyan-300\">${REGION}<\/span>/g" /var/www/html/index.html

sudo sed -i "s/<span id=\"az\" class=\"font-semibold text-cyan-300\">Detecting...<\/span>/<span id=\"az\" class=\"font-semibold text-cyan-300\">${AZ}<\/span>/g" /var/www/html/index.html

# Permissions
sudo chown -R apache:apache /var/www/html
sudo systemctl restart httpd
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










