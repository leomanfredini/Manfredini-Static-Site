---
title: "Linux Commands Notepad"
date: 2023-11-11T07:58:05-03:00
draft: false
tags: ["linux"]
---

### Compilação de comandos destinados a uma finalidade específica.

------------

### grep

Localizar conteúdos específicos dentro de arquivos sem a necessidade de abri-los.  
No exemplo abaixo, será executada uma busca pela sentença **apache** em todos os arquivos do diretório `/etc` apresentando uma listagem dos aquivos com esta sentença.

    $ grep -rli 'apache' /etc/* 


------------

