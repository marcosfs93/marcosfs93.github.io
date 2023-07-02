---
title: Onde encontrar o Device ID do Android
date: 2023-07-02
author: M4rQu1Nh0S
tags: [onde, encontrar, device, id, android]
subtitle: Saiba como encontrar o numero do Device ID do Android
category: [Dicas e tutoriais, Android]
comments: true
#cover-img: https://cdn-images-1.medium.com/max/800/0*5Du1vkE-acW8FIhV.png
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*5Du1vkE-acW8FIhV.png
share-img: https://cdn-images-1.medium.com/max/800/0*5Du1vkE-acW8FIhV.png
layout: post
---

![Device ID](https://cdn-images-1.medium.com/max/800/0*5Du1vkE-acW8FIhV.png)
Se você já mexeu com o **Titanium Backup** sabe como é legal fazer o backup dos aplicativos e configurações, quando está para instalar uma versão mais nova do Android ou quer instalar uma outra ROM totalmente diferente. Infelizmente existem alguns aplicativos que mesmo restaurando os dados não permitem que você use o aplicativo da mesma forma que usava antes de trocar de rom.

Caso não saiba do que eu estou falando, vou dar um exemplo: **Aplicativo de Banco**

Enquanto na maioria dos aplicativos você só precisa dos dados de configuração, tem aplicativos que precisa também o **Android Device ID**.

O Android ID, sem querer entrar em detalhes, é um código de identificação que o seu aparelho recebe e que muda sempre que você faz um Factory Reset. Existe aplicativos que fazem detecção de Android ID no momento que você vai abri-lo.

Infelizmente os backups que a gente faz dos aplicativos não envolvem o ID do android, e por isso, mesmo que você restaure o backup no outro aparelho, ou sistema, o aplicativo vai bloquear o seu acesso.

Enfim, pro backup ser 100% falta a capacidade de se fazer o backup e repor o Android ID, na verdade o Titanium Backup já tem isso porem é algo bem superficial e não há simplicidade de se mexer com isso nesse aplicativo.

No meu caso eu queria repor o Android id que eu tinha no MIUI 8 que eu tinha instalado no aparelho no meu MIUI 11 que acabei de instalar no meu Redmi 4X (Santoni) porem não sabia onde esse dado ficava no aparelho e nem como fazer a alteração.

Hoje estou fazendo este post para compartilhar essa informação com vocês.

## Localizações do Android ID de acordo com a versão do android:

### Android 5 e anteriores:

/data/user/0/com.android.providers.settings/databases/settings.db

### Android 6 e Android 7:

/data/system/users/0/settings_secure.xml

Já no **Android 8+** a coisa é mais “dinâmica”, porque **cada aplicativo gera um Android ID próprio**. Essas informações ficam armazenadas dentro desse arquivo:

    /data/system/users/<User_ID>/settings_ssaid.xml

Eu, apesar de trocar o MIUI 8 pelo MIUI 11 ambos são feitos a base do Android 7.1.2. Sendo assim é só preciso editar o arquivo **settings_secure.xml** e trocar o Android ID pelo ID antigo que eu tinha antes de trocar de sistema.

Se eu fosse trocar o MIUI 8 pelo MIUI 12, onde o MIUI 12 é baseado no Android 10, eu teria que pegar meu antigo Android ID, abrir o arquivo **settings_ssaid.xml**, procurar pelo o Android ID **do aplicativo** que eu quero alterar.

Post baseado nesse topico:

[https://android.stackexchange.com/questions/219756/where-is-the-android-id-stored-and-when-does-it-change](https://android.stackexchange.com/questions/219756/where-is-the-android-id-stored-and-when-does-it-change)

