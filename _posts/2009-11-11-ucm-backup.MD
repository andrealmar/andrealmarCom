---
layout: post
title: UCM Backup
date: 2009-11-11 12:41:34.000000000 -02:00
type: post
published: true
status: publish
categories:
- UCM
tags:
- backup
- Oracle
- UCM
comments: true
---
Há basicamente 4 áreas no Content Server em que devem ser feitos backups regulares:

<ul>
<li>Repositório de arquivos nativos (“Vault”)</li>
<li>Repositório dos arquivos web-viewable (“Web       Layout”)</li>
<li>Content Information database (banco de dados       onde ficam os metadados)</li>
<li>search index (indices de busca)</li>
</ul>


<p>Dessas 4 áreas ,os dois repositórios de arquivos e o <em>content information database</em> são os mais importantes<span style="text-decoration:line-through;"> </span>o UCM não vai poder ser recuperado com sucesso se não tivermos o backup deles. Sem os arquivos do repositório, não há conteúdo. Sem o content information database (que armazena os metadados), o Content Server não saberá nada sobre o conteúdo, o que significa que o conteúdo não existe.</p>  
<ul>
<li>Os backups dos arquivos no repositório e do <em>content information database</em> devem      ser sincronizados sempre que possivel. O ideal seria que o Content Server e      o banco de dados sejam parados antes do backup. Isso nos permite uma      sincronização máxima, visto que nenhum conteúdo pode ser armazenado      enquanto o backup está sendo feito. Se isso não puder acontecer, esteja      certo de que o backup está sendo feito durante periodos de baixa atividade      do sistema (por exemplo, nas madrugadas ou nos finais de semana).</li><br />
<li>É recomendado que você inclua também na sua      politica de backup toda a estrutura de diretórios do Content Server. Isso      assegura que voce irá fazer backup de todos os arquivos de configuração e      outros arquivos importantes (por exemplo, componentes customizados, etc).</li>
</ul>
<p>&nbsp;</p>
<p>Com base nessas  informações segua abaixo a lista dos diretórios que devem ser feitos backups e uma sugestão da frequência com que devem ser feitos os backups.</p>
- D:\diretorio de instalação\server\weblayout (BACKUP DIÁRIO)<br />
* D:\diretorio de instalação\server\vault (BACKUP DIÁRIO)
- D:\diretorio de instalação\server\config (BACKUP SEMANAL)<br />
* D:\diretorio de instalação\server\custom (BACKUP SEMANAL)<br />
- D:\diretorio de instalação\server\bin (BACKUP SEMANAL)<br />
* D:\diretorio de instalação\server\admin (BACKUP SEMANAL)

Até a próxima
