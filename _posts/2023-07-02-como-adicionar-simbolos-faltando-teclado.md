---
title: Como adicionar simbolos que não tem no teclado
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, adicionar, simbolos, não tem, faltando, no, teclado]
subtitle: Saiba como inserir os simbolos de outro jeito
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*25qjCaUBiEYNF_IE.png
share-img: https://cdn-images-1.medium.com/max/800/0*25qjCaUBiEYNF_IE.png
layout: post
---

<p align='center'><img alt='Teclado preto' src="https://cdn-images-1.medium.com/max/800/0*25qjCaUBiEYNF_IE.png"/></p>
Olhe para o seu teclado, todas os símbolos estão presentes? Dependendo do tipo e do modelo do teclado, vai ter teclas que estão presentes e outras que não estão, por exemplo as teclas **barra invertida** **“ \ “** e **barra vertical** **“ | “**.

## Tabela ASCII

Na tabela a seguir você verá vários caracteres disponíveis nos padrões ASCII como também o seu código de identificação em **decimal** e **hexadecimal**.

### Tabela regular ASCII (Código 0 até 127)

![Imagem da tabela do 0 até 127](https://cdn-images-1.medium.com/max/800/0*gzUcqDg3hnjTkmhm.png)

### Tabela estendida ASCII (Código 128 até 255)

![Imagem da tabela do 128 até 255](https://cdn-images-1.medium.com/max/800/0*Knwbxzjb1GlsrBpZ.png)

## Atalho dos caracteres no Windows
No Windows quando precisamos ativar um caractere mas ele não está no teclado, podemos abrir o aplicativo **Mapa de Caracteres,** ou de forma mais prática podemos usar um atalho com a tecla Alt + teclado numérico.

A combinação do Alt + números ativam caracteres especiais conforme a tabela **ASCII** usando o **sistema decimal** (dec).

Por exemplo: Para inserir a **“barra invertida ( \ )”**, o atalho é:

**Alt + 92**

## Atalho dos caracteres no Linux

Já no Linux, é usado a tabela **UNICODE** através do **sistema hexadecimal** (hex).

Para inserir um caractere no Linux, você deve usar o atalho Ctrl + Shift + U, digitar o código hexadecimal e apertar Enter. Ou Ctrl + Shift, digitar U e o código hexadecimal e soltar o Ctrl + Shift.

Por exemplo: Para inserir a **“barra invertida ( \ )”**, você deve usar o atalho:

**Ctrl + Shift + U**, digite: **5C**, aperte **Enter**.

_Nota: pode haver variações de como o atalho funciona, há distribuições que te obrigam a inserir a letra U antes do código hex, enquanto há outras que automaticamente adicionam a letra U, como é o caso do Linux Mint._

## Considerações finais
Eu sou um exemplo de usuário que era bem acostumado com o jeito Windows de inserir caracteres, embora a forma de inserir caracteres seja diferente, o processo se resume apenas em se readaptar, usar o novo atalho e memorizar o código hex do caractere.

Depois disso você fica tão familiarizado no Linux como era no Windows.

Se houver necessidade de consultar a tabela ASCII no Linux, abre o terminal de digite o comando abaixo:

	$ man ascii

Se você tiver alguma dica interessante sobre o assunto, deixe seu comentário

Isso é tudo pessoal, até a próxima.

### Referencias:
- [https://www.sg-electronic-systems.com/ascii-table/](https://www.sg-electronic-systems.com/ascii-table/)
- [https://askubuntu.com/questions/88347/how-can-i-type-ascii-characters-like-alt-numpad-in-windows](https://askubuntu.com/questions/88347/how-can-i-type-ascii-characters-like-alt-numpad-in-windows)
- [https://pt.wikipedia.org/wiki/Unicode](https://pt.wikipedia.org/wiki/Unicode)
- [https://man7.org/linux/man-pages/man7/ascii.7.html](https://man7.org/linux/man-pages/man7/ascii.7.html)
- [https://www.linux.org/threads/alt-keys-and-linux.11517/](https://www.linux.org/threads/alt-keys-and-linux.11517/)

