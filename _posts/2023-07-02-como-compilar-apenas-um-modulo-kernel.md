---
title: Como compilar apenas um modulo no kernel
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, compilar, apenas, um modulo, kernel]
subtitle: Aprendar a compilar apenas o módulo que você precisa
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*9UDs4DOtRq6smV0P.png
share-img: https://cdn-images-1.medium.com/max/800/0*9UDs4DOtRq6smV0P.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*9UDs4DOtRq6smV0P.png)
A compilação dos módulos do kernel Linux é um processo que ocorre na compilação do próprio kernel, se você quer compilar um kernel novo é necessário compilar os módulos também.

Mas há quem pense que não dá pra compilar os módulos do kernel sem compilar o kernel junto, ou seja, por causa de um único módulo o usuário pode acabar compilando o kernel inteiro desnecessariamente.

Hoje vou compartilhar com vocês uma forma para recompilar apenas o módulo que você precisa sem ter que compilar todo o kernel junto.

## Compilando somente os módulos
Vamos começar, digamos que você queira apenas compilar um módulo para o kernel que você já está utilizando, aquele que foi instalado pelo próprio sistema, por exemplo.

Primeiro precisamos instalar as dependências necessárias para a compilação, dependências como o pacote build-essentials, ncurses-dev e libssl-dev.

Segundo, abrir o terminal e seguir os comandos:

	$ sudo su

_Para entrar no modo root_

	# apt install linux-headers-$(uname -r)

_Para baixar código fonte das configurações do kernel_

	# apt source linux-image-$(uname -r)

_Para baixar o código fonte do kernel, necessário para suprir quais quer componentes que o modulo possa precisar na hora da compilação._

	# cd /usr/src/
	# tar xf linux-source-5.10.tar.xz

(5.10 é um exemplo, lembre-se disso)

	# cd /usr/src/linux-source-5.10

Com esses 3 comandos acima, o terminal vai ir para o diretório **/usr/src** que contem os headers e sources, descompactar o pacote contendo o kernel a ser compilado e entrar na pasta nova que foi criada ao extrair o kernel.

	# cp ../linux-headers-$(uname -r)/Module.symvers .

_Para copiar a “lista de simbolos exportados” do sistema para o código fonte do kernel._

	# make oldconfig

_Para copiar o arquivo .config do kernel atual._

A seguir vamos precisar editar o arquivo .config e fazer com que o módulo seja compilado.

Use um editor de texto, como o nano por exemplo:

	# nano .config

A seguir vamos precisar que o comando make, que vai ser executado em breve, inclua o módulo para compilação.

Por exemplo, preciso compilar o modulo da minha placa de rede, no comando **lsmod** o módulo é o r8169, e como eu quero compilar ele a linha que eu devo procurar é:

CONFIG_**R8169**

Ao encontrar a **CONFIG_** edite a linha e faça com que o final seja “**=m**”

Ficando: CONFIG_R8169**=m**

Agora podemos continuar, use o comando abaixo:

	# make prepare

_Para preparar os arquivos para compilação e checar previamente por erros antes de rodar o make install._

	# make modules_prepare

_Mesma coisa do comando acima, mas dedicado aos módulos_

	# make M=scripts/mod

	# make M=drivers/net/ethernet/realtek/ modules

_Para executar o script de compilação para módulos e em seguida iniciar a compilação dos módutos._

Com isso você já compilou o módulo, agora só precisa aplica-lo no diretório de módulos do sistema.

Você pode simplesmente usar o comando **cp** para copiar o módulo diretamente para o diretório do kernel.

	# cp drivers/net/ethernet/realtek/r8169.ko /lib/modules/5.10.0-14-amd64/kernel/drivers/net/ethernet/realtek/

ou

	# make M=drivers/net/ethernet/realtek/ modules_install

	# depmod

_Que vai instalar todos os módulos que estão presentes junto com o que você precisa e em seguida rodar o depmod para gerar os arquivos de mapeamento de modulo do kernel._

	# modprobe r8169

_Que vai carregar e ativar o módulo novo, que consequentemente vai ativar o driver ou função no sistema._

Passo a passo reproduzido no Q4OS ‘Gemini’ (Baseado no Debian Bullseye)

Com isso concluímos, seu módulo foi rapidamente compilado e você se livrou de minutos sem PC ao evitar de compilar o kernel inteiro.

Espero que tenha sido útil, até a próxima.

**Referencias:**
[https://serverfault.com/questions/674415/compiling-an-individual-kernel-module-debian-ubuntu](https://serverfault.com/questions/674415/compiling-an-individual-kernel-module-debian-ubuntu)
[https://askubuntu.com/questions/168279/how-do-i-build-a-single-in-tree-kernel-module#338403](https://askubuntu.com/questions/168279/how-do-i-build-a-single-in-tree-kernel-module#338403)

