---
title: "Proxy Reverso, HTTPS e Load Balancer com Nginx no CentOS"
date: 2022-05-24T21:26:26-03:00
draft: true
tags: ["Nginx","Linux"]
---


Usando o Nginx no Centos 7 para atuar como proxy reverso para serviços internos ou containers, load balancer para servidores de aplicação e servir conexões HTTPS através da utilização de certificados SSL fornecidos gratuitamente pela [Let's Encrypt](https://letsencrypt.org/)


**Bold**

*Italic*

**Leonardo Manfredini**


------------
#### HABILITANDO A CONFIGURAÇÃO EM SWITCHES DELL

Entrando em modo de configuração

    console> enable
    console# config

Habilitando o DHCP snooping globalmente.

    console(config)# ip dhcp snooping

Leo
