
# Projeto de Instalação e Configuração do UniFi Controller no Debian

1. Provisionamento do Servidor
Passos para provisionar o servidor Debian:
    1- Escolha do Sistema Operacional: 
        - Debian foi escolhido por sua estabilidade e suporte amplo.

    2 - Instalação do Debian:   
        -Faça o download da ISO do Debian e o provisione, em VM, Cloud ou até mesmo container.
        -Durante a instalação, configure a rede e o particionamento conforme necessário.

    3 - Configuração de Rede:
    Edite o arquivo /etc/network/interfaces para configurar IP estático caso não tenha DHCP se necessário.
    bash
    Copiar código
    nano /etc/network/interfaces
    Exemplo de configuração:
    bash
    Copiar código
    auto eth0
    iface eth0 inet static
        address 192.168.1.100
        netmask 255.255.255.0
        gateway 192.168.1.1
    Reinicie o serviço de rede:
    '''bash'''
    Copiar código
    systemctl restart networking
2. Instalação do UniFi Controller
Passos detalhados para instalar o UniFi Controller:

Atualize o sistema:

bash
Copiar código
sudo apt-get update && sudo apt-get upgrade -y
Adicionar repositório UniFi:

Adicione a chave GPG do repositório:
bash
Copiar código
sudo wget -O /etc/apt/trusted.gpg.d/unifi-repo.gpg https://dl.ui.com/unifi/unifi-repo.gpg
Adicione o repositório ao sources.list:
bash
Copiar código
echo 'deb [arch=amd64] https://www.ui.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/100-ubnt.list
Instalar dependências:

Instale libssl1.0.0 necessário para a versão do MongoDB usada pelo UniFi:
bash
Copiar código
echo "deb http://security.debian.org/debian-security jessie/updates main" | sudo tee -a /etc/apt/sources.list
sudo apt-get update
sudo apt-get install -y --no-install-recommends libssl1.0.0
Instalar MongoDB 3.6:

Adicione a chave e o repositório do MongoDB:
bash
Copiar código
wget -qO - https://www.mongodb.org/static/pgp/server-3.6.asc | sudo apt-key add -
echo "deb [trusted=yes] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list
sudo apt-get update
Instale o MongoDB:
bash
Copiar código
sudo apt-get install -y mongodb-org=3.6.23 mongodb-org-server=3.6.23 mongodb-org-shell=3.6.23 mongodb-org-mongos=3.6.23 mongodb-org-tools=3.6.23
Instalar UniFi Controller:

bash
Copiar código
sudo apt-get install -y unifi
3. Configuração do UniFi Controller
Configurações pós-instalação:

Iniciar o serviço UniFi:

bash
Copiar código
sudo systemctl start unifi
sudo systemctl enable unifi
Acessar a interface do UniFi:

Abra um navegador e acesse https://<IP_DO_SEU_SERVIDOR>:8443
Complete a configuração inicial seguindo o assistente.
4. Uso de Scripts Shell
Exemplos de scripts shell utilizados:

Script para atualização do sistema e instalação de pacotes essenciais:

bash
Copiar código
#!/bin/bash
apt-get update && apt-get upgrade -y
apt-get install -y curl wget gnupg
Script para backup automático do MongoDB:

bash
Copiar código
#!/bin/bash
MONGO_BACKUP_DIR="/var/backups/mongodb"
TIMESTAMP=$(date +"%F")
BACKUP_NAME="mongo-backup-$TIMESTAMP"
mkdir -p $MONGO_BACKUP_DIR/$BACKUP_NAME
mongodump --out $MONGO_BACKUP_DIR/$BACKUP_NAME
5. Documentação de Configurações e Pacotes
Documentação das principais configurações e pacotes:

Pacotes principais instalados:

unifi
mongodb-org
libssl1.0.0
Comandos úteis:

Reiniciar o serviço UniFi:
bash
Copiar código
sudo systemctl restart unifi
Verificar o status do serviço:
bash
Copiar código
sudo systemctl status unifi
6. Materiais e Referências Oficiais
Referências:

Documentação oficial do UniFi: Ubiquiti UniFi Documentation
Guia de instalação do MongoDB: MongoDB Documentation
Conclusão
Este documento serve como um guia detalhado para a instalação e configuração do UniFi Controller no Debian, incluindo todas as etapas e scripts necessários para garantir um processo suave e eficiente. Mantenha este documento atualizado e adapte conforme necessário para futuros projetos.