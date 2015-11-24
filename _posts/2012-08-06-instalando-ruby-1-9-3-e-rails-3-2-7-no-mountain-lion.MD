---
layout: post
title: Instalando Ruby 1.9.3 e Rails 3.2.7 no Mountain Lion
date: 2012-08-06 16:04:12.000000000 -03:00
type: post
published: true
status: publish
categories: [ruby]
comments: true
---
Fala pessoal...enfim mais um post depois de um longo hiato! Resolvi brincar um pouco com Ruby on Rails (I need fresh air) e para fazer a instalação da linguagem Ruby e do framework Rails no novo Mountain Lion existem varias documentações e páginas na internet ensinando a se fazer isso, mas elas estão fragmentadas na minha opinião. Resolvi juntar tudo nesse post e espero que ajude vocês.
Portanto aqui estão os passos para instalar o Rails no brand new Mountain Lion.
Faça o download do XCode (se ainda não o tiver), execute-o e depois entre em Preferences depois Downloads. Faça a instalação do Command Line Tools como na figura abaixo:  
<br />
![Rails_1]({{ site.url }}/assets/images/rails1.png)  
<br />
Terminada a instalação, feche o XCode e abra o Terminal. Execute o seguinte comando:  

```
sudo chown -R 'seuNomedeUsuario' /usr/local
```

Execute a seguinte linha de comando:

```
curl https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer | bash -s stable
```

![Rails_2]({{ site.url }}/assets/images/rails2.png)  
<br />
Digite ```rvm -v``` para testar se a instalação ocorreu corretamente:  
<br />
![Rails_3]({{ site.url }}/assets/images/rails3.png)  
<br />
Instale o Homebrew com o seguinte comando:  
<br />
```
/usr/bin/ruby -e "$(/usr/bin/curl -fsSL https://raw.github.com/mxcl/homebrew/master/Library/Contributions/install_homebrew.rb)"
```
<br />![Rails_5]({{ site.url }}/assets/images/rails5.png)  
<br />
Execute um ```brew update```  
<br />
![Rails_6]({{ site.url }}/assets/images/rails6.png)  
<br />
Agora você precisa instalar uma library chamada <span style="text-decoration:underline;">libksba</span>. Faça isso usando o <span style="text-decoration:underline;">Homebrew</span>:  
<br />
![Rails_7]({{ site.url }}/assets/images/rails7.png)  
<br />
Instale o <span style="text-decoration:underline;">XQuartz</span>: <em>http://xquartz.macosforge.org/landing/ (faça o download do arquivo .dmg e instale normalmente)</em>
<br />
Depois de instalado ele (XQuartz) pede para você fazer log-off e login novamente. Faça isso!
Por fim abra o Terminal novamente e digite:  
<br />
```
rvm install 1.9.3
```
<br />  
![Rails_9]({{ site.url }}/assets/images/rails9.png)  
<br />
Se aparecer alguma mensagem de erro como essa:  
<br />

```
There has been an error while trying to extract the source.
Halting the installation.
There has been an error fetching the ruby interpreter.
```
<br />
Tente rodar o seguinte comando:
<br />
```
rvm get head
```
E depois tente rodar o ```rvm install 1.9.3``` novamente.
<br />
Feito isso é só setar a sua nova versão do ruby que você acabou de instalar:  
<br />

```ruby
rvm --default use ruby-1.9.3-p194
```

<br />
E finalmente ```ruby -v``` para verificar se você setou corretamente a versão do ruby.  
<br />
![Rails_10]({{ site.url }}/assets/images/rails10.png)  
<br />

Ufa...estamos quase acabando. Agora só falta instalar o Rails. Para instalar a última versão é só utilizar o comando:
<br />

```ruby
gem install rails
```

<br />
![Rails_11]({{ site.url }}/assets/images/rails11.png)  
<br />
Terminada a instalação do Rails verifique com um <strong>rails -v</strong> se a versão está correta.  
<br />  
![Rails_12]({{ site.url }}/assets/images/rails12.png)  
<br />
Pronto! É isso! Depois (não sei quando hehe) volto com mais posts. See ya!
