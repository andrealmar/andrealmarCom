---
layout: post
title:  "Big Word Alert"
date:   2015-12-16 15:00:00 -0200
categories: software engineering
comments: true
published: false
---

Namespaces - 

References - 

Sequences - 

Iterators - 

Valor logico de um objeto - curto-circuito, quando que uma lista é interpretada como verdadeira ou como falsa

Mutability - todo objeto que voce pode mudar o estado interno dele

Imutability - vc nao troca o estado interno dele depois que ele foi criado, vc pode no maximo derivar ele, gerar um novo objeto e a partir deste novo objeto vc tem esse novo contexto que vc pegou, legal para abordagens de programação funcional que o python suporta. Na FP o input nunca muda, tudo eh imutavel, ou seja, vc sempre esta gerando um novo dado. Vantagem = Paralelismo, se eu nao tenho compartilhamento de contexto, se eu nao tenho uma memoria compartilhada entre 2 processos eu posso paralizar tudo deles. Quanto mais encadeado atraves de processos imutaveis sem efeito colateral, o seu codigo estiver estruturado, mais facil sera paralelizar a execucao do codigo.  

Magic/Special Methods - metodos "dunder"  __main__, __blabla__ sao protocolos da linguagem, sao especiais para vc criar seus proprios objetos e faze-los utilizarem a potencia da abstracao da linguagem 

Operators Overloading - SET documentacao conjunto algebrico do python, sobscreve um monte de operadores, 

Strong Types - uma vez criado um objeto vc nao muda ele de tipo. 

Strings that aren't bytes - strings nao sao uma cadeia de caracteres em memoria, nao sao uma cadeia de CHARS. isso nos traz a um outro universo, podemos trabalhar com strings como objetos com seu proprio contexto. 

Functions são objects - flexibilidade, crirar funcoes dinamicamente enquanto uma funcao eh executada
