---
title: "Linux Commands Notepad"
date: 2023-11-12T21:38:35-03:00
draft: false
tags: ["Linux"]
---

### Compilação de comandos destinados a uma finalidade específica.

------------

### grep

Localizar conteúdos específicos dentro de arquivos sem a necessidade de abri-los.  
No exemplo abaixo, será executada uma busca pela sentença **apache** em todos os arquivos do diretório `/etc` apresentando uma listagem dos aquivos com esta sentença.

```shell
grep -rli 'apache' /etc/* 
```

------------

### ncdu

Analisador de uso de disco com uma interface de usuário em modo texto. O Ncdu permite que você encontre facilmente os hogs de armazenamento em seu sistema, escaneando suas unidades e organizando os resultados com base nos maiores arquivos no topo da lista. Ele os divide por diretório e depois por arquivo para que você possa encontrar facilmente quais arquivos estão ocupando mais espaço. Então você pode excluí-los rapidamente diretamente se quiser.

```shell
ncdu
```
O comando acima analisa o uso de disco na unidade /home do usuário logado

```shell
sudo ncdu / --color=dark
```
O comando acima analisa o uso de todo o disco a partir da raiz, com a opção de menus coloridos

------------
