---
title: "Instalando Docker, Docker Compose e Portainer no Debian 12"
date: 2024-09-13T23:55:06-03:00
draft: false
tags: ["Linux","Docker","Docker Compose"]
---

Docker é uma plataforma que utiliza contêineres para virtualização, permitindo o empacotamento, distribuição e execução de aplicações, juntamente com suas dependências, de forma isolada. Essa solução otimiza tanto o desenvolvimento quanto a implantação, ao criar ambientes homogêneos em diferentes sistemas, promovendo portabilidade e melhor uso dos recursos disponíveis. Cada contêiner é uma unidade leve e independente, possibilitando a execução consistente de aplicações em qualquer ambiente compatível com Docker.

Já o Docker Compose é uma ferramenta voltada para a gestão de aplicações que dependem de múltiplos contêineres. Com ele, é possível definir e gerenciar essas configurações em um único arquivo, o que automatiza tanto a criação quanto a conexão entre os contêineres. Isso facilita o desenvolvimento e testes de sistemas mais complexos, garantindo a manutenção de ambientes replicáveis e consistentes.

O Portainer, por sua vez, é uma interface gráfica de gerenciamento de contêineres, que simplifica a administração de ambientes Docker e Kubernetes. Ele oferece uma maneira intuitiva de gerenciar, monitorar e controlar contêineres, redes e volumes, sem a necessidade de utilizar a linha de comando, tornando a operação de ambientes de contêineres mais acessível e eficiente.


---
## 1. Instalando o Docker CE

### Atualizando o sistema

```shell
sudo apt update && sudo apt upgrade -y
```


### Instalando as dependências necessárias

```shell
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

### Instalando o Docker

No próximo passo, vamos instalar o Docker Community Edition (Docker CE), que é uma versão de código aberto, disponível gratuitamente para download e uso.

Primeiramente iremos adicionar a chave GPG

```shell
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Em seguida, instalamos o Docker

```shell
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

Após a instalação, vamos habilitar e iniciar o serviço do Docker

```shell
sudo systemctl enable docker
sudo systemctl start docker
```

Em seguida, vamos adicionar o usuário atual ao grupo docker para que ele consiga executar o docker sem precisar a elevação de permissão (invocando o sudo)

```shell
sudo usermod -aG docker $USER
newgrp docker
```
*Necessário reiniciar o servidor para que os comandos acima executados surtam efeito*

Verificando a versão do Docker

```shell
docker --version
```
{{< figure src="docker-version.png" >}}

---
## 2. Instalando o Docker Compose

Após a instalação do Docker, vamos prosseguir com a instalação do Docker Compose.


```shell
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Em seguida, vamos configurar as permissões para que o arquivo possa ser executado.

```shell
sudo chmod +x /usr/local/bin/docker-compose
```
Verificando a instalação e a versão do Docker Compose

```shell
docker-compose --version
```
{{< figure src="docker-compose-version.png" >}}


---
## 3. Instalando o Portainer

Vamos instalar o Portainer Community Edition (CE) que é a versão gratuita e open source.

Primeiro, vamos criar o volume que o Portainer usará para armazenar seu banco de dados.

```shell
docker volume create portainer_data
```

Em seguida, vamos instalar e executar o conteiner do serviço portainer.

```shell
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

O servidor Portainer foi instalado. Você pode verificar se o contêiner do servidor Portainer foi iniciado executando o comando `docker ps`

{{< figure src="portainer-ps.png" >}}

Para acessar a interface web do Portainer e concluir a configuração, abra a seguinte URL em um navegador:

```shell
https://<IP-DO-SERVIDOR-DOCKER>:9443/
```
{{< figure src="portainer-setup.png" >}}
