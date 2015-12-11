---
layout: post
title: UCM 11g Performance
date: 2010-06-08 11:54:10.000000000 -03:00
type: post
published: true
status: publish
categories:
- UCM
comments: true
---
Muita gente se pergunta a respeito da performance do Oracle UCM. Eu mesmo me perguntava as vezes. Com o lançamento do Oracle UCM 11g algumas dúvidas (parecem) que foram sanadas. A documentação à respeito de performance e sizing da versão 10g era uma $%#@&amp;¨* (substitua $%#@&amp;¨* pelo elogio que quiser ;D) se é que existia alguma documentação oficial da ORACLE sobre esse assunto...  <br />  
Mas...consultando alguns documentos a respeito da nova versão 11g...achei alguns testes interessantes que podem servir de parâmetro para quando vocês estiverem fazendo um sizing ou medindo a performance do UCM em algum cliente.  <br />  
Vamos lá...a Oracle executou testes com a nova versão 11g do UCM e chegou a algumas conclusões interessantes.
Ela dividiu em 2 (dois), os principais tipos de aplicações feitas com o UCM: High-Performance Web Sites/Delivery e Imaging/High Volume Ingestion.  <br />  
A diferença entre essas 2 aplicações é que enquanto na High-Performance Web Sites/Delivery temos um cenário com um <em>input</em> de dados de baixo para médio com centenas ou milhões de <em>viewers</em> , busca Full-Text podendo ser ou não combinada com os metadados e conversões (para PDF, etc) extensivas, no outro cenário, Imaging/High Volume Ingestion, temos um <em>input</em> extremamente alto, poucos <em>viewers</em>, na busca temos alguns campos somente e quase nenhum processo de conversão sendo feito.  
Considerando testes feitos com um Hardware Commodity com as seguintes configurações:
<ul>
<li>único Node</li>
<li>2 cpu’s de 2.33 Ghz Xeon</li>
<li>16 GB de RAM</li>
</ul>
<p>Os testes foram conduzidos utilizando arquivos dos mais variados tamanhos (4KB – 250KB) e tipos (texto, MS OFFICE, PDF). Os resultados foram os seguintes:</p>
<p><strong>ALTO VOLUME DE ITEMS DE CONTEÚDO COM TAMANHOS VARIADOS DE ARQUIVOS</strong></p>
<table border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="96"><strong>Tamanho do arquivo</strong></td>
<td valign="top" width="96"><strong>4 KB</strong></td>
<td valign="top" width="96"><strong>20KB</strong></td>
<td valign="top" width="96"><strong>40 KB</strong></td>
<td valign="top" width="96"><strong>100 KB</strong></td>
<td valign="top" width="96"><strong>200 KB</strong></td>
</tr>
<tr>
<td valign="top" width="96"><strong>Check-In’s por segundo</strong></td>
<td valign="top" width="96">270</td>
<td valign="top" width="96">187</td>
<td valign="top" width="96">162</td>
<td valign="top" width="96">149</td>
<td valign="top" width="96">128</td>
</tr>
<tr>
<td valign="top" width="96"><strong>Check-In’s por 24 horas</strong></td>
<td valign="top" width="96">23.328,000</td>
<td valign="top" width="96">16.156,800</td>
<td valign="top" width="96">13.996,800</td>
<td valign="top" width="96">12.873,600</td>
<td valign="top" width="96">11.059,200</td>
</tr>
<tr>
<td valign="top" width="96"><strong>Uso de CPU do UCM Server (%) </strong></td>
<td valign="top" width="96">62,38</td>
<td valign="top" width="96">44,71</td>
<td valign="top" width="96">41</td>
<td valign="top" width="96">42,19</td>
<td valign="top" width="96">43,33</td>
</tr>
<tr>
<td valign="top" width="96"><strong>Uso do Servidor do Banco de Dados (%)</strong></td>
<td valign="top" width="96">51,07</td>
<td valign="top" width="96">58,53</td>
<td valign="top" width="96">57,19</td>
<td valign="top" width="96">57,20</td>
<td valign="top" width="96">58,54</td>
</tr>
</tbody>
</table>
<p>Como mostram os testes, um único node do Oracle UCM 11g pode suportar de <strong>11 milhões à 23 milhões</strong> de items de conteúdo por dia num hardware genérico.</p>
<p>A mesma configuração de hardware pode servir Web-sites dinâmicos incluindo intranets, extranets, e sites públicos. O UCM 11g oferece uma arquitetura chamada <em>Site Studio for External Applications.</em> Veja os testes:</p>
<p><strong>ORACLE UCM 11g WEB CONTENT MANAGEMENT / PERFORMANCE</strong></p>
<table border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="288">Acessos por segundo</td>
<td valign="top" width="288">124</td>
</tr>
<tr>
<td valign="top" width="288">Acessos por hora</td>
<td valign="top" width="288">446.400</td>
</tr>
<tr>
<td valign="top" width="288">Uso de CPU (%)</td>
<td valign="top" width="288">89 %</td>
</tr>
</tbody>
</table>
<p>Um ponto importante é que de acordo com o uso da CPU, o software pode processar altas quantidades de volume de dados com uma infraestrutura diferente da mostrada aqui nos testes. Isso é evidente porque nem o UCM nem o Banco de Dados chegam a utilizar 100% da capacidade do processador. Esse tipo de aplicação é chamada de <em>I/O Limited</em>, ou seja a performance geral é restrita também pela velocidade do seu hard-disk e a largura de banda da sua rede.</p>
<p>Se você quiser passar por cima dessa limitações de I/O você tem que usar um hardware específico para isso. A Oracle lógico, recomenda o Sun Oracle Database Machine que é baseada em servidores Exadata para storage, etc.</p>
<p>Com testes de arquivos de 100 KB um único-Node chegou a processar 1060 conteúdos por segundo e 91.584,000 a cada 24 horas. É um número impressionante.</p>
<p>Bom, com esses testes pelo menos dá pra gente ter uma idéia de como o UCM 11g se comporta nos diferentes cenários de colaboração.</p>
<p>See you next time...</p>
