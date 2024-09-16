---
title: "DHCP Snooping - Proteção contra servidores DHCP não autorizados"
date: 2021-10-02T21:29:05-03:00
draft: false
tags: ["Redes","Segurança"]
---


Um servidor DHCP não autorizado na rede pode ocasionar diversos incidentes, desde indisponibilidade e até a falha no acesso a serviços internos e externos. Outra situação mais preocupante são os ataques do tipo DHCP Spoofing, onde os clientes recebem os parâmetros IP de um servidor DHCP manipulado, direcionando-os a um gateway preparado para interceptar o tráfego de rede ou até mesmo entregando parâmetros de DNS que direcionem a servidores manipulados para resolverem endereços de sites legítimos para servidores maliciosos.

A funcionalidade **DHCP Snooping**, presente em diversos switches gerenciáveis, tem a finalidade de proteger a rede contra estes servidores DHCP não autorizados, permitindo que somente determinadas portas possam responder às requisições de *DHCP Discovery* disparadas pelos *DHCP Clients* de uma rede.

------------
#### HABILITANDO A CONFIGURAÇÃO EM SWITCHES DELL

Entrando em modo de configuração

```console
console> enable
console# config
```

Habilitando o DHCP snooping globalmente.

```console
console(config)# ip dhcp snooping
```

Habilite o snooping na VLAN principal. (Caso sua rede possua somente uma e o ID desta VLAN seja 1.

```console
console(config)# ip dhcp snooping vlan 1
```

Se houver mais alguma VLAN na rede, execute o comando acima, identificando cada uma delas.

Habilite a porta confiável para a distribuição de DHCP. (repetindo os comandos abaixo para cada porta, caso existe mais de uma).

```console
console(config)# interface ethernet g1
console(config-if)# ip dhcp snooping trust
```

Você pode executar este comando para verificar as configurações.

```console
console# show ip dhcp snooping
```

Para salvar as configurações, execute:

```console
console# copy running-config startup-config
console# exit
```
