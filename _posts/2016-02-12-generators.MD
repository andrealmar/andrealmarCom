---
layout: post
title:  "Python Generators"
date:   2016-02-04 19:00:00 -0200
categories: python, generators
comments: true
published: true
---
> I'm the Generator, firing whenever you quit
Yeah whatever it is, you go out and it's on
Yeah can't you hear my motored heart
You're the one that started it

<br />
![Generator_Foo_Fighters]({{ site.url }}/assets/images/Generator_FooFighters.jpg)
<br />  
<br />
Não...eu não vou escrever neste post sobre a ótima música do Foo Fighters (embora recomendo que você a escute =P). Estamos aqui para falar de uma função bastante legal na nossa linguagem de programação preferida: Os famosos **Generators**.
<br />  
Em termo simples os **Generators** são *funções que permitem a você declarar uma função que se comporta como um iterador, ou seja, que pode ser usado dentro de um loop* **for**.  
<br />
Simplificando mais ainda: **Generators** são uma forma simples de criarmos iteradores.  Ele irá retornar um objeto (iterador) para que nós possamos iterar sobre este objeto (um valor de cada vez).  
<br />  
