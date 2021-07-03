---
title: "Erro 0x80070534 ao executar tarefa agendada no Windows"
date: 2021-07-01T22:07:25-03:00
draft: false
tags: ["windows","ad"]
---

**Problema:** Erro 0x80070534 exibido nos logs do Windows ao tentar executar uma tarefa agendada que exige permissões administrativas.

**Solução:** Configurar a tarefa para executar com o usuário **`NT AUTHORITY\System`**, conforme imagem a seguir:

{{< figure src="0x80070534.png" >}}