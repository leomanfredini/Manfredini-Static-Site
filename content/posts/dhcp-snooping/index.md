---
title: "DHCP Snooping - Proteção contra servidores DHCP não autorizados"
date: 2021-09-23T21:29:05-03:00
draft: true
tags: ["Redes","Segurança"]
---


Um servidor DHCP não autorizado na rede pode ocasionar diversos incidentes, desde indisponibilidade e até a falha no acesso a serviços internos e externos. Outra situação mais preocupante é a sua utilização para fins maliciosos, direcionando os clientes a um gateway preparado para interceptar o tráfego de rede ou até mesmo entregando parâmetros de DNS que direcionem a servidores manipulados para resolverem endereços de sites legítimos para servidores maliciosos.

A funcionalidade *DHCP Snooping*, presente em diversos switches gerenciáveis, tem a finalidade de proteger a rede contra estes servidores DHCP não autorizados, permitindo que somente determinadas portas possam responder às requisições de DHCP Discovery disparadas pelos DHCP Client de uma rede.
