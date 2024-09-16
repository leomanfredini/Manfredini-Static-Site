---
title: "Mover ou deletar computadores e usuários inativos do AD"
date: 2021-06-27T20:27:34-03:00
draft: false
tags: ["AD", "Windows"]
---

Dicas rápidas para gerenciar usuários e computadores inativos no Windows Active Directory

<!--more-->

## Mover Computadores Inativos
Rodar o comando abaixo em um prompt com permissões de admin para mover os computadores inativos por mais de 10 semanas para a OU `InativosComp`

```cmd
for /f "Tokens=*" %s in ('dsquery computer -inactive 10 -limit 200') do dsmove %s -newparent "OU=InativosComp,DC=dominio,DC=local" 
```


## Mover Usuários Desabilitados
Rodar o comando abaixo em um prompt com permissões de admin para mover os as contas de usuário desabilitadas para a OU `InativosUsuarios`

```cmd
for /f "Tokens=*" %s in ('dsquery user -disabled -limit 200') do dsmove %s -newparent "OU=InativosUsuarios,DC=dominio,DC=local" 
```


## Deletar Computadores Inativos
Rodar o comando abaixo em um prompt com permissões de admin para deletar as contas de computadores inativos por mais de 10 semanas

```cmd
dsquery computer -inactive 10 | dsrm -subtree -noprompt -c > c:\teste.txt
```


Explicação:

**dsquery computer -inactive 10** : faz uma consulta no Active Directory por computadores com 10 semanas de inatividade. Alterando este valor podemos alterar para quantidade de semanas desejada.

**dsrm -subtree -noprompt -c > c:\teste.txt** : dsrm é um parâmetro utilizado para apagar computadores no Active Directory, os parâmetros -subtree -noprompt -c são para apagar recursivamente e sem interação do usuários e > c:\teste.txt insere o resultado do comando em um arquivo teste.txt no C:/ este caminho pode ser alterado. ( Lembrando de executar este comando com elevação no prompt , para pode salvar arquivo no C:/).
