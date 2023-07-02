---
title: Como transferir o SEO do Blogger para o WordPress
date: 2023-07-02
author: M4rQu1Nh0S
tags: [seo, blogger, wordpress, transferir, como]
subtitle: Faça a mudança de endereço sem sua posição no ranking de pesquisa
category: [blogger, wordpress]
comments: true
---

<p><a href="https://1.bp.blogspot.com/-lRSl_siE4Hs/YQCeTah-bOI/AAAAAAAABxo/L1ki_3pIsHg1U6xYpz6WYQ1svckLv1TrACLcBGAsYHQ/s774/migracao-1.png" style="text-align: center;"><img alt="ilustração, transição blogger para wordpress" border="0" data-original-height="271" data-original-width="774" src="https://1.bp.blogspot.com/-lRSl_siE4Hs/YQCeTah-bOI/AAAAAAAABxo/L1ki_3pIsHg1U6xYpz6WYQ1svckLv1TrACLcBGAsYHQ/s16000/migracao-1.png" title="ilustração, transição blogger para wordpress" /></a></p>
Olá pessoal, hoje estou trazendo um guia exclusivo sobre como transferir o SEO do seu blog antigo para o novo blog que se encontra em uma nova plataforma.

Atualmente tem muito tutorial ensinando como migrar o Blogger para o WordPress, porem grande parte desses tutoriais ensinam apenas como importar e exportar as postagens que você tinha sem falar de um ponto muito importante, o  **SEO**.

O SEO, acredito eu, é a maior fonte de trafego que podemos ter em um site, com um bom SEO podemos atrair uma grande quantidade de visitas em nossos sites através dos  **motores de busca**  como o Google por exemplo, que na qual o site tanto pode aparecer na primeira página como também ser o primeiro link da lista dos motores de busca.

Como esses tutoriais não ensinam como transferir o SEO do Blogger para o WordPress vou ensinar neste post como fazer a migração do SEO.

Bom, esse tutorial vai ser muito objetivo já que não vou explicar o que é o SEO, como também não vou explicar como fazer a migração do Blogger para o WordPress já que a internet está cheia desses tutoriais, então é só pesquisar no google sobre como fazer a migração de conteúdo do Blogger no WordPress.

Porem esse tutorial foi destinado exclusivamente para aquele que mudaram do Blogger para o WordPress junto com o dominio do URL do blog (de .blogspot para .wordpress). Se o seu caso for diferente pode haver trechos desse tutorial que são válidos para você, mas recomendo fortemente que você tente procurar por guias existentes.

Antes de iniciar esse tutorial é necessário que você já tenha migrado todas as postagens que você tinha no Blogger para o WordPress, ok? Se você ainda não fez isso, siga os tutoriais de migração de Blogger para WordPress, se você já está com as postagens na nova plataforma continue com a leitura

***Antes de continuar, saiba que essa "migração do SEO" do blogger para o WordPress é uma tarefa sem reversão, pois não é possível desfazer a migração e migrar o SEO do WordPress para o Blogger, exceto se você tiver um plano pago no WordPress.**

**Conteúdo**
 - [Configurando o redirecionamento](#configurando-o-redirecionamento)
 - [Search Console - Ferramenta Alteração de endereço](#search-console---ferramenta-alteração-de-endereço)


## Configurando o redirecionamento

Agora que as postagens do blog antigo estão no blog novo, você vai precisar editar todas as postagens do blog antigo para incluir o redirecionamento 301. Então entre em cada postagem, apague todo o conteúdo,  **vá no modo html do editor**  de textos e coloque o seguinte código:

```
<meta http-equiv="refresh" content="0; URL='http://sitenovo.com/postagem-tal'"/><p>301 - MOVIDO PERMANENTEMENTE</p>
```

Vamos simular um exemplo para ajudar a entender:

No meu blog antigo e no blog novo eu tenho uma postagem chamada:  
**Call of Duty – World at War – Atualizado 1.7 + Tradução**

No meu blog antigo, a postagem está nesse URL:  
https://**blogmrcs.blogspot.com/2016/09/call-of-duty-world-at-war-atualizado-17.html**

Já no meu blog novo, a postagem está nesse URL:  
https://**dicastechup.wordpress.com/2016/09/13/call-of-duty-world-at-war-atualizado-1-7-traducao/**

Então quando eu for no meu blog antigo e editar essa postagem, eu vou apagar todo o conteúdo e no lugar eu coloco o Código abaixo  **incluindo o URL**  dessa postagem  **do site novo**, veja:

```
<meta http-equiv="refresh" content="0; URL='https://dicastechup.wordpress.com/2016/09/13/call-of-duty-world-at-war-atualizado-1-7-traducao/'"/><p>301 - MOVIDO PERMANENTEMENTE</p>
```

Ao fazer isso qualquer pessoa que tentar acessar a postagem no blog antigo vai ser redirecionada para o blog novo contendo a postagem. Então é só editar todas as postagens do blog antigo e colocar o código incluindo o URL da postagem do blog novo, igual no exemplo acima.

Essa vantagem não se aplica somente aos visitantes, funciona também com os motores de busca. Além de direcionar o trafego para o site novo os motores de busca vão tratar o link da nova página como  **canônico**, com isso gradativamente os links do blog antigo vão ser excluídos no motor de busca dando lugar aos links do blog novo.

Com isso já configuramos o redirecionamento em todas as postagens do site antigo para o novo, agora só falta fazer o mesmo com a página inicial do blog antigo.

Para isso entre no  **Painel do Blogger**, vá em  **Configurações**  e desça a página até chegar na parte  **Postagens**, clique em "**Máximo de postagens mostradas na página principal**" e deixe a quantidade em  **1**  e depois  **Salve**. veja na imagem como deve ficar:

![definindo numero max de postagens](https://miro.medium.com/v2/resize:fit:720/format:webp/0*DQ7RmkesvRtENXCm.png "definindo numero max de postagens")

Depois disso vamos colocar um **Tema Basico**  para o blog antigo pois ele vai servir apenas para redirecionamento e um tema basico e leve vai agilizar esse processo.

Vá em  **Tema**, desça a página e escolha o tema  **Simple Simply Simple**  e depois clique em  **Aplicar**. conforme a imagem:

![aplicando o tema](https://miro.medium.com/v2/resize:fit:720/format:webp/0*vOEYTUo8-k8Stcub.png "aplicando o tema")

Agora que limitamos a página inicial de mostrar somente uma postagem e trocamos para um tema basico basta criar uma nova postagem chamada:  **Mudamos de Endereço** (ou o que preferir) e usar o codigo de redirecionamento para a página inicial do blog novo, no meu caso ficou assim:

![inserindo o codigo de redirecionamento](https://miro.medium.com/v2/resize:fit:720/format:webp/0*z3bRbal70p0j0B70.png "inserindo o codigo de redirecionamento")

Depois é só publicar. Como essa postagem é a mais recente e é a única que vai aparecer na página inicial, qualquer pessoa que tentar entrar no blog antigo pelo endereço da página inicial será redirecionado para o site novo. Faça a mesma coisa com as paginas do blog antigo para o blog novo, como a pagina de contato, por exemplo.

## Search Console - Ferramenta Alteração de endereço

Como a mudança de plataforma também vai mudar o nosso domínio e o URL de acesso ao novo site (de _.blogspot.com_  PARA _.wordpress.com_) é necessário informar ao Google sobre a alteração de endereço, para que assim ele nos ajude a migrar o resultado das pesquisas para o novo site.

_Porem se você tá mudando de plataforma mas o URL permanece a mesmo (https://meusite.com.br) basta usar as informações disponíveis na página  **[Mudar um site sem alterações no URL](https://developers.google.com/search/docs/advanced/crawling/site-move-no-url-changes?hl=pt-br)**._

Agora que todas as postagens e a página inicial já estão configuradas para redirecionar os visitantes para os respectivos conteúdos através do redirecionamento 301, vamos solicitar a mudança de endereço no Search Console, a ferramenta que permite gerenciar como o seu site deve aparecer no Google.

Clique no link abaixo para ir na página mudança de endereço  
[https://search.google.com/u/0/search-console/settings/change-address](https://search.google.com/u/0/search-console/settings/change-address)

Ao clicar no link acima o Google Search vai pedir para que você selecione a propriedade, no caso você deve selecionar o blog antigo, imagem:

![selecionando o site no search console](https://miro.medium.com/v2/resize:fit:720/0*-MNQUYji9lFSuiBk "selecionando o site no search console")

Depois disso você deve selecionar o blog/site novo e em seguida clicar em  **VALIDAR E ATUALIZAR**, igual na imagem:

![preparando a mudança de endereço](https://miro.medium.com/v2/resize:fit:720/0*e7NjEZoDfvy499fP "preparando a mudança de endereço")

Após isso, vai aparecer essa janela com o status aprovado, isso é fruto daquele redirecionamento que foi ensinado acima :-) clique em  **CONFIRMAR MUDANÇA**  para prosseguir. imagem:

![processo de mudança pré aprovado](https://miro.medium.com/v2/resize:fit:640/0*mavX5PtJT5WpzdlB "processo de mudança pré aprovado")

Com isso o processo de mudança foi aberto, agora só falta esperar as mudanças acontecerem, imagem:

![conclusão da solicitação](https://miro.medium.com/v2/resize:fit:720/0*O6gHy3m4YEpCHA0u "conclusão da solicitação")

Agora está terminado, configuramos o redirecionamento no blog antigo, alteramos o tema, limitamos o numero de postagens na pagina inicial do blog antigo, criamos uma postagem de redirecionamento da página inicial e fizemos abrimos a solicitação de mudança no Search Console do Google.

Com isso gradativamente o blog antigo vai saindo dos resultados do Google, enquanto isso você vai continuar recebendo trafego através do blog antigo ao mesmo tempo que os resultados de pesquisa vão incluir o site novo gradativamente. é só esperar pois o processo é demorado e os resultados não vão aparecer notavelmente nos primeiros dias.

Vai chegar o momento em que todas as paginas do novo site vão aparecer no google e todas as páginas do site antigo removidas, quando isso acontecer você já pode bloquear o acesso dos motores de busca no  **robots.txt**  do site antigo e  **manter as páginas com os redirecionamentos do site antigo para o novo**.

Para verificar quantos links do site antigo ainda está no google basta acessar o link abaixo:  
[https://search.google.com/u/0/search-console/index?resource_id](https://search.google.com/u/0/search-console/index?resource_id)

Depois selecione a Propriedade, no caso o site antigo e verificar o numero de páginas **Válidas**:

![mostrando as paginas validas](https://miro.medium.com/v2/resize:fit:720/0*61kbRhys4TSoDZk5 "mostrando as paginas validas")

No meu caso ainda há 51 páginas do meu site antigo no Google,  **quando**  esse numero chegar a  **zero**  eu vou seguir a recomendação acima de  **manter as páginas do site antigo e bloquear o acesso dos motores de busca**.

É importante bloquear os motores de busca no robots.txt e manter as páginas com o redirecionamento, porque primeiro: diminui a possibilidade das páginas serem indexadas novamente, segundo: qualquer outro site que não seja seu e que ainda tenha links do seu antigo ainda vai gerar tráfego, como o conteúdo ainda existe mas em outro local vale a pena manter o site antigo no ar com os redirecionamentos.

Se acontecer de você querer voltar para o site antigo, repagine todo o site e depois libere o acesso dos motores de busca no robots.txt novamente.

Caso queira saber mais sobre a ferramenta Search Console e tópicos relacionados:

-   [Ferramenta Alteração de endereço](https://support.google.com/webmasters/answer/9370220?hl=pt-BR)  - Search Console
-   [Adicionar uma propriedade do site](https://support.google.com/webmasters/answer/34592?hl=pt-BR)  - Search Console
-   [Ferramentas para Webmasters](https://wordpress.com/pt-br/support/ferramentas-para-webmasters/)  - WordPress
-   [Mudar um site sem alterações no URL](https://developers.google.com/search/docs/advanced/crawling/site-move-no-url-changes?hl=pt-br)  - Documentação Pesquisa do Google
-   [Mudar um site com alterações no URL](https://developers.google.com/search/docs/advanced/crawling/site-move-with-url-changes?hl=pt-br)  - Documentação Pesquisa do Google

Enfim, espero que tenham gostado do post de hoje, se tiver algum feedback use os comentários abaixo.

**O post será atualizado e melhorado se necessário**
