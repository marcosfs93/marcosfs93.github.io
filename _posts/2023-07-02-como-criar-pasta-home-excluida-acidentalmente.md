---
title: Como criar pasta /home que foi excluída acidentalmente
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, criar, pasta, /home, excluida, acidentamente, recriar]
subtitle: Aprenda a criar uma nova pasta /home após excluir acidentalmente
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*DUIxs4gh1jnLMlTc.png
share-img: https://cdn-images-1.medium.com/max/800/0*DUIxs4gh1jnLMlTc.png
layout: post
---

<p align='center'><img alt='Ilustração da pasta home' src="https://cdn-images-1.medium.com/max/800/0*DUIxs4gh1jnLMlTc.png"/></p>
Perder a pasta home não é algo que se resolve apenas criando outras com o mesmo nome, nesse tutorial vamos aprender a recriar a sua pasta de usuário com as configurações padrão.

Ao contrário do que muitos acreditam, criar a pasta home com o mesmo nome de usuário não é o suficiente para “resetar” os dados.

Ao criar a pasta nova de usuário e feito login no sistema, o próprio sistema se encarregar de criar as outras pastas e os outros arquivos, mas nem todos, por exemplo algumas customizações personalizadas pré definidas pela distro.

**Conteúdo**

- [ - Como criar uma nova pasta de usuário do jeito certo](#como-criar-uma-nova-pasta-de-usuário-do-jeito-certo)
- 1[. Criar a nova pasta](#1--criar-a-nova-pasta)
- 2[. Copiar os arquivos de configuração](#2--copiar-os-arquivos-de-configuração)
- 3[. Alterar o dono da pasta](#3--alterar-o-dono-da-pasta)
- 4[. Modificar as permissões para pastas e arquivos](#4--modificar-as-permissões-para-pastas-e-arquivos)
- [ - Conclusão](#conclusão)
- [ - Referencias](#referencias)

## Como criar uma nova pasta de usuário do jeito certo:

### 1- Criar a nova pasta:
Como eu havia dito, criar só uma nova pasta não basta, há mais além disso, precisamos criar a pasta, mudar as permissões, o dono do diretório e o grupo do usuário:

1- Supondo que você não tá mais logado na conta de usuário após ter apagado os arquivos, faça login na conta **root**, ou use o comando **sudo su** para mudar para a conta root.

	# sudo su

_Se você está se deparando com uma tela preta, que não deixa você fazer login na conta de usuário, use os atalhos do teclado Ctrl + Alt + F4 (F4 é uma das teclas, você pode escolher entre o F1 até o F12) para alterar para outra instância, depois de fazer isso você conseguirá fazer login na conta_ **_root_**_._

2- Após fazer o login nós devemos criar a pasta de usuário de novo.

	# mkdir /home/marcos

### 2- Copiar os arquivos de configuração:
Quando instalamos uma nova distro e criamos o usuário, o sistema copia os arquivos da pasta **/etc/skel** para a pasta do usuário, e essa pasta **skel** contem os arquivos de configurações para o ambiente gráfico, terminal, do navegador, etc, depende da distro que você está instala.

Ao excluir a pasta de usuário, você exclui também esses arquivos e para recupera-los precisamos fazer a copia manual deles para a pasta do usuário recriada.

Use o comando abaixo para copiar os arquivos da pasta skel para a pasta do usuário:

	# cp -Rfv /etc/skel/.* /home/marcos/

### 3- Alterar o dono da pasta:
Até o momento nós fizemos todos esses procedimentos com o usuário root, e alguns desses arquivos vão estar com as permissões de root.

Precisamos aplicar permissões adequadas para os arquivos da pasta de usuário para que não haja problemas de leitura e escrita por parte do usuário e principalmente apps de sistema e de terceiros.

Dito isso, vamos começar trocando o proprietário e o grupo da pasta de usuário:

Use o comando abaixo para alterar o titular da pasta de usuário:

	# chown -R marcos /home/marcos/

	# chgrp -hR marcos /home/marcos/

Com isso o usuário se torna proprietário de sua pasta e tem controle completo a partir dela.

Agora é só deslogar da conta root e logar na sua conta de usuário.

### 4- Modificar as permissões para pastas e arquivos
A partir daqui vamos terminar de aplicar as permissões com a conta de usuário.

Vamos começar mudando as permissões de leitura e escrita das outras pastas e arquivos, isso é importante já que as permissões da pasta home vão afetar como os seus apps vão funcionar, até mesmo apps do sistema.

No geral, as permissões para pastas e arquivos de usuário devem seguir esse padrão:

-   755 (rwxr-xr-x) para as pastas comun
-   644 (rw-r — r — ) para arquivos
-   775 (drwxrwxr-x) para pastas usadas por apps.

Para as pastas acessadas por aplicativos, como por exemplo a pasta **.config** e **.local** da pasta home, a permissão correta é **775**, mas no momento que o sistema recria essas pastas a permissão correta é aplicada automaticamente.

Alias se você quiser saber o que significa as letras e números usados para aplicar permissões, acesse a calculadora de chmod abaixo

[https://chmod-calculator.com/](https://chmod-calculator.com/)

Enfim, para aplicar as permissões adequadas aos arquivos e pastas:

	$ sudo chmod -R a+rwX,o-w /home/$USER

Isso vai aplicar a permissão 755 para os diretórios e a permissão 644 para os arquivos, com exceção dos quais já receberam a permissão de execução (arquivos .sh shell script, por exemplo).

## Conclusão
Recuperar a pasta de usuário vai mais além do que só criar outra, há configurações e permissões pré definidas que são perdidas e que fazem falta nos apps do sistema e de terceiros, espero que isso seja o suficiente para resolver os problemas de configuração do usuário no sistema.

Como não podia de ser diferente, eu passei por isso e estou aqui compartilhando a solução que deu certo pra mim.

### Referencias:

- [https://www.vivaolinux.com.br/topico/UbuntuBR/Apaguei-pasta-raiz-do-usuario](https://www.vivaolinux.com.br/topico/UbuntuBR/Apaguei-pasta-raiz-do-usuario)
- [https://help.ubuntu.com/community/dmrcErrors](https://help.ubuntu.com/community/dmrcErrors)

