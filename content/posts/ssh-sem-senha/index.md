---
title: "SSH Sem Senha no Linux"
date: 2023-11-15T09:06:21-03:00
draft: false
tags: ["Linux","SSH"]
---

A autenticação segura em servidores remotos é facilitada pelo método de conexão SSH sem o uso de senhas. Abaixo, apresento os passos para configurar a conexão entre o cliente e o servidor.

---
### 1 - Gerar a chave pública na máquina cliente

Para gerar o par de chaves, execute o seguinte comando na máquina cliente:

```shell
ssh-keygen -t rsa
```

A chave padrão é de 2048 bits. Caso precise de mais segurança basta, trocar o valor para 4096 bits. Neste caso o comando será:

```shell
ssh-keygen -t rsa -b 4096
```

O processo de geração da chave irá solicitar algumas perguntas como o nome de arquivo em que a chave será salva ( _/home/SEU-USUARIO/.ssh/id_rsa_ ) e também a definição de uma palavra-chave.
Você pode pressionar enter em ambas as perguntas para definir o valor padrão.  

A palavra-chave é utilizada para criptografar a chave privada, mas não é obrigatória e pode ser deixada em branco.  

A chave privada será salva na localização padrão **~/.ssh/id_rsa** e a chave pública será salva no arquivo **~/.ssh/id_rsa.pub**  
Nunca revele o conteúdo de sua chave privada e muito menos a distribua por aí, pois é através dela que o servidor remoto realizará a autenticação de sua conexão.

---

### 2 - Copiar a chave pública para a máquina destino (servidor)

A seguir, 3 métodos para copiar a chave pública para a máquina destino:

#### 1ª Opção: Comando _ssh-copy-id_

A sintaxe desse comando é:

```shell
ssh-copy-id usuario_remoto@endereço_IP_remoto
```

Será solicitada a autenticação SSH da máquina destino e uma vez que ela ocorrer com sucesso, a chave pública será adicionada ao arquivo de chaves autorizadas da máquina remota. Em seguida a conexão será encerrada.

#### 2ª Opção: Copiar a chave pública com SSH

Esse método utiliza o SSH para copiar a chave pública para a máquina destino

```shell
cat ~/.ssh/id_rsa.pub | ssh <usuario_remoto>@<edereço_IP_remoto> "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Um registro contendo a sua chave pública será adicionado ao arquivo de chaves autorizadas da máquina destino.


#### 3ª Opção: Copiar a chave pública manualmente

Método mais trabalhoso por ser totalmente manual, que consiste em adicionar manualmente o conteúdo do seu arquivo **id_rsa.pub** dentro do arquivo **~/.ssh/authorized_keys** na máquina destino.

Copie o seu arquivo de chave pública para a máquina destino:

```shell
scp ~/.ssh/id_rsa.pub <usuario_remoto>@<edereço_IP_remoto>:~
```

O comando acima irá copiar o arquivo da chave pública para a raiz do diretório /home do usuário que efetuou o login.  

Em seguida, efetue login SSH na máquina destino

```shell
ssh <usuario_remoto>@<endereço_IP_remoto>
```

e transfira o conteúdo da sua chave pública (que está no arquivo recém copiado) para o arquivo de chaves autorizadas da máquina destino:

```shell
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

Nesse ponto já é possível conectar-se ao servidor remoto sem a necessidade de senhas.

---
### 3 - Testando o acesso SSH sem senha

Para testar a conexão sem senha, proceda normalmente como uma conexão normal:

```shell
ssh <seu_usuario>@<endereço_IP_remoto>
```

Agora as conexões SSH iniciadas pelo cliente para o servidor serão efetuadas sem a necessidade de digitar a senha.

É possível também "enviar" comandos para serem executados remotamente no servidor. No exemplo a seguir, enviamos ao servidor o comando para reiniciar o servidor Web Apache em um servidor Debian:

```shell
ssh root@servidor 'systemctl reload apache2'
```

Importante observar que o usuário que está enviando o comando deve possuir permissão para executá-lo na máquina destino.

---

### 4 - Desabilitando o login SSH com senha

A realização deste passo é facultativa, uma vez que, nesta etapa, o seu servidor estará configurado para aceitar conexões SSH mediante autenticação por chaves pública e privada (sem senha), assim como pelo método convencional que utiliza senhas. Porém, qualquer usuário que estiver em posse de sua senha conseguirá se conectar ao servidor.  

Para melhorar a segurança do seu servidor, desabilite a conexão SSH com senha conforme os passos a seguir:

1. Conecte ao seu servidor via SSH
2. Edite o arquivo **/etc/ssh/sshd_config** utilizando algum editor de texto, como o **nano**

```shell
nano /etc/ssh/sshd_config
```

3. Localize a linha **PasswordAuthentication yes** e altere seu valor para **no** (Utilize o **CTRL + W** para abrir a ferramenta de busca)
4. Salve o arquivo com **CTRL + X** , digite **Y** e dê **enter**
5. Reinicie o serviço **SSHD** para que as alterações tenham efeito

```shell
systemctl reload sshd
```
---