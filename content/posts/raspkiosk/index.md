---
title: "Raspkiosk - Modo quiosque no Raspberry Pi"
date: 2021-09-16T15:53:49-03:00
draft: false
tags: ["Linux","RaspberryPi"]
---


**Kiosk Mode no Raspberry Pi usando a distribuição Raspbian**

O *Kiosk Mode* (ou Modo Quiosque) é um recurso utilizado em totens de auto atendimento e painéis informativos, onde há a necessidade de disponibilizar ao usuário somente um navegador de internet com uma ou mais páginas específicas, ocultando todos os outros atalhos disponíveis do sistema operacional.

- **Distribuição utilizada:** Raspberry Pi OS with desktop - Release date: January 11th 2021
- **Download:** [https://www.raspberrypi.org/software/operating-systems/](https://www.raspberrypi.org/software/operating-systems/ "https://www.raspberrypi.org/software/operating-systems/")
- **Repositório com os arquivos necessários:** [https://github.com/leomanfredini/raspkiosk](https://github.com/leomanfredini/raspkiosk)


------------

### MÉTODO 1 - INSTALAÇÃO MANUAL

#### 1. REMOVER PACOTES DESNECESSÁRIOS

```shell
sudo apt-get purge wolfram-engine scratch scratch2 nuscratch sonic-pi idle3 -y
sudo apt-get purge smartsim java-common minecraft-pi libreoffice* -y
```


#### 2. LIMPAR ARQUIVOS RESIDUAIS

```shell
sudo apt-get clean
sudo apt-get autoremove -y
```

#### 3. ATUALIZAR O SISTEMA

```shell
sudo apt-get update
sudo apt-get upgrade
```

#### 4. INSTALAR PACOTES NECESSÁRIOS PARA O *KIOSK MODE*

```shell
sudo apt-get install xdotool unclutter sed
```

#### 5. HABILITAR O LOGIN AUTOMÁTICO

```shell
sudo raspi-config
```

1. Opcao 1 - System Options
2. Opcao S5 - Boot/Autologin
3. Opção B4 - Desktop Autologin


#### 6. CRIAR O SCRIPT RESPONSÁVEL POR INICIAR O *KIOSK MODE*

Criar o arquivo para o script

```shell
nano /home/pi/kiosk.sh
```

Copiar o conteúdo do arquivo *kiosk.sh* disponível no repositório do Github

#### 7. CRIANDO O SERVIÇO PARA INICIAR O SCRIPT NO BOOT

Criar o arquivo para o script

```shell
sudo nano /lib/systemd/system/kiosk.service
```

Copiar o conteúdo do arquivo *kiosk.service* disponível no repositório do Github

#### 8. HABILITAR O SCRIPT NA INICIALIZAÇÃO

```shell
sudo systemctl enable kiosk.service
```

#### 9. USO

Seguindo os passos anteriores, o script já fica habilitado para iniciar no *Kiosk Mode* sempre que o sistema for iniciado. Para efetuar qualquer interação manualmente, utilize os seguintes comandos:


##### 9.1 Comando para iniciar manualmente o Kiosk Mode

```shell
sudo systemctl start kiosk.service
```
##### 9.2 Comando para finalizar manualmente o Kiosk Mode

```shell
sudo systemctl stop kiosk.service
```

------------

### MÉTODO 2 - INSTALAÇÃO AUTOMÁTICA VIA SCRIPT

Em um terminal, executar o seguinte comando:

```shell
sudo wget -qO - https://raw.githubusercontent.com/leomanfredini/raspkiosk/master/install.sh | bash
```


Na sequência, editar o arquivo _/home/pi/kiosk.sh_ personalizando o final da linha 23 com as URLs desejadas para exibição.