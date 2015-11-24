---
layout: post
title: "[Tópicos em Programação WEB] Introdução ao DOM"
date: 2015-09-24 16:33:32.000000000 -03:00
type: post
published: true
status: publish
categories: web javascript web-development tópicos em programação web
comments: true
---
O que é DOM? - DOM significa  DOCUMENT OBJECT MODEL. Ok mas e daí?  
Em termos gerais o DOM é uma API (application programming interface) que serve para interagirmos com documentos HTML e XML.
Provavelmente só esta explicação é um pouco confusa. Mas estamos aqui para explicar isso para você meu caro leitor. Vamos aprender como o DOM é manipulado e como utilizar os métodos corretos em Javascript para manipulá-lo.  
A melhor maneira de pensarmos a respeito do DOM, é que ele é uma árvore de objetos aninhados.
<br />
Uma analogia seria: Pense no DOM como uma _árvore genealógica_.  
<br />
<br />

![Genealogical_Tree]({{ site.url }}/assets/images/genealogical_tree-750x410.jpg)

<br />
<br />
Cada parte de um documento HTML é representado por um objeto dentro do DOM. O DOM possui objetos para representar

  - elementos HTML (tags)
  - Texto (conteúdo das tags)
  - Estilos (como este texto é apresentado para o usuário)

assim como objetos mais alto nível, como interação com o usuário através de "eventos". O DOM é organizado hierarquicamente, o que significa que um objeto DOM para o elemento **HEAD**, está embaixo do elemento **HTML**, que por sua vez está embaixo do objeto **DOCUMENT**.

{% highlight ruby %}
`Document`
  html
    head
      title
        `Arvore DOM`
      script
        `Codigo Javascript`
{% endhighlight %}

E assim por diante... A melhor maneira de observarmos o DOM é ver como ele imita uma estrutura HTML.

{% highlight ruby %}
body
  div id="artigo"
    <p>Bla bla bla bla bla</p>
  </div>
</body>
{% endhighlight %}

No exemplo acima a <em>tag</em> <strong>p</strong> está aninhada dentro da <em>tag</em> <strong>div </strong>que por sua vez está aninhada dentro da <em>tag</em> <strong>body</strong>, que por sua vez está aninhada dentro da <em>tag</em> <strong>html</strong>.  
Lembra da analogia do DOM com uma árvore genealógica? No DOM nós identificamos estas relações (aninhamentos), justamente como uma árvore genealógica. Uma<em> tag</em> que está aninhada à outra é chamada de <strong>“filha”</strong> desta outra <em>tag</em> que se torna o seu<strong>"pai"</strong>.  
Exemplo:

{% highlight ruby %}
var bodyTag = document.body;
var divTag  = document.body.firstChild;
var pTag    = document.body.firstChild.firstChild;
{% endhighlight %}

O objeto <em>Document</em>, representa o conteúdo de um documento HTML. Só que o objeto <em>Document</em> não é o nível mais superior do DOM. O nível mais superior do DOM é o objeto <b>Window</b>.
Por conta disso, o objeto <em>Window</em>, é o escopo <i>global</i> do DOM - ou seja, qualquer objeto no DOM pertence, ou está contido no objeto <em>Window</em>. Este objeto <em>Window</em>, representa uma janela aberta do seu browser (navegador), por exemplo.
<br />
<br />

![objectDocument_objectWindow]({{ site.url }}/assets/images/objectDocument_objectWindow.png)  
<br />
Azul = objeto Window (browser)  
Laranja = documento HTML (objeto Document)  
<br />  

Como já observamos, o DOM não é uma linguagem. O DOM foi desenvolvido para ser independente de qualquer linguagem de programação. Para manipular o DOM usamos uma linguagem de programação. Geralmente em se tratando de programação WEB nós usamos Javascript. Assim nós temos acesso à estrutura, estilo e conteúdo de um documento através do DOM e com o JavaScript poderemos manipulá-los.
Existem muito mais coisas a se falar sobre o nosso prezado DOM. Mas isso fica para outro post.
See ya!
