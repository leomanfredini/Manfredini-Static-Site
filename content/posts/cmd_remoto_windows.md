---
title: "Executar um prompt administrativo em uma estação Windows remota"
date: 2021-06-27T20:30:44-03:00
draft: true
tags: ["windows"]
---

Dica rápida para acessar CMD remotamente usando a solução do UAC de administrador.

<!--more-->


Para esta tarefa, precisamos do programa PSEXEC (disponível na suite PSTOOLS / link ao final do post). 

Com o CMD aberto no diretório onde se encontra `psexec.exe` vamos executar o seguinte comando:

```html
psexec \\172.16.1.11 -s cmd
```
No exemplo acima, assume-se que vamos conectar no computador remoto de endereço ip `172.16.1.11`.

A opção **-s** é para logar-se como `user system`


https://docs.microsoft.com/pt-br/sysinternals/downloads/psexec
