# Projeto de Instalação e Configuração do UniFi Controller no Debian

1. Provisionamento do Servidor
   Passos para provisionar o servidor Debian:
   1. Escolha do Sistema Operacional:
      - Debian foi escolhido por sua estabilidade e suporte amplo.

   2. Instalação do Debian:
      - Faça o download da ISO do Debian e o provisione, em VM, Cloud ou até mesmo container.
      - Durante a instalação, configure a rede e o particionamento conforme necessário.

   3. Configuração de Rede:
      - Edite o arquivo /etc/network/interfaces para configurar IP estático caso não tenha DHCP se necessário.

2. Instalação do UniFi Controller
   Passos detalhados para instalar o UniFi Controller:
   1. Atualize o sistema:
      ```bash
      sudo apt update
      sudo apt upgrade
      ```
   2. Adicione o repositório UniFi:
      ```bash
      echo 'deb http://www.ui.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/100-ubnt-unifi.list
      ```
   3. Importe a chave GPG:
      ```bash
      sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 06E85760C0A52C50
      ```
   4. Instale o UniFi Controller:
      ```bash
      sudo apt update
      sudo apt install unifi -y
      ```
   5. Inicie o serviço UniFi Controller:
      ```bash
      sudo systemctl start unifi
      ```

