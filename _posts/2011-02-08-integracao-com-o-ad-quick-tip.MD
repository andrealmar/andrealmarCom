---
layout: post
title: Integração com o AD - Quick TIP
date: 2011-02-08 16:47:55.000000000 -02:00
type: post
published: true
status: publish
categories:
- Dicas e Truques
- UCM
comments: true
---
Um cliente fez a integração do AD (Active Directory) com o UCM (rodando em cima do Apache).
Até aí tudo bem, mas esqueceu de algumas coisinhas...<br />  
Como por exemplo mapear no Role Prefix o seu Domain Controler (DC).
Outro "mistake" foi cadastrar como CN (Container) ao invés de OU (Organizational Unit) aonde ficariam os Grupos do AD relacionados as Roles do UCM.<br />  
Isso estava afetando o refresh automático de usuários quando eles mudavam de Grupo (AD) ou Role (UCM).
A configuração correta segue abaixo:<br />  
![Active_Directory]({{ site.url }}/assets/images/adad.png)
