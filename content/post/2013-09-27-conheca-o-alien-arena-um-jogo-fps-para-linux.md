---
categories:
- Jogos
date: 2013-09-27T09:57:08Z
feature-img: assets/2013-09-27/alien_arena.jpg
meta:
  _edit_last: "2"
  bwps_enable_ssl: ""
  dsq_thread_id: "1802267423"
  socialize: 11,12,23,25,27
  socialize_text: ""
published: true
status: publish
tags:
- alien arena
- game
- jogo
- open-source
- software livre
- tutorial
- video
title: Conheça o Alien Arena, um jogo FPS para Linux
type: post
url: /2013/09/27/conheca-o-alien-arena-um-jogo-fps-para-linux/
---

Recentemente andei pesquisando algum jogo para dar uma relaxada nas horas vagas e encontrei o <a title="Alien Arena" href="http://red.planetarena.org/" target="_blank">Alien Arena</a>, na minha opinião - apesar de não ser um <em>expert</em> em jogos - achei os gráficos de altíssima qualidade, com uma boa jogabilidade (rápida e suave), e ainda, existem mais de 60 mapas (!).

[![Alien Arena @ Game](/assets/2013-09-27/topo_alienarena.png)](/assets/2013-09-27/topo_alienarena.png)

### Sobre o jogo
Como dito no título, o jogo é em <a title="First Person Shooter" href="http://pt.wikipedia.org/wiki/Tiro_em_primeira_pessoa" target="_blank">FPS</a> e os personagens são em sua maioria seres extra-terrestres com itens futurísticos, tornando-o ainda mais original.

[![Alien Arena @ Game](/assets/2013-09-27/post_alienarena.png)](/assets/2013-09-27/post_alienarena.png)

É possível jogar em dois modos, single player (<a title="deathmatch" href="http://pt.wikipedia.org/wiki/Deathmatch" target="_blank">deathmatch</a> com <a title="Bots" href="http://en.wikipedia.org/wiki/Video_game_bot" target="_blank">bots</a>) ou multiplayer podendo ser jogado online ou em rede com os amigos, e ainda, com diversas opções de modo de jogo, entre elas:

<ul>
<li><a title="deathmatch" href="http://pt.wikipedia.org/wiki/Deathmatch" target="_blank">Deathmatch</a>: todo mundo contra todo mundo, matança total;</li>
<li><a title="Capture the flag" href="http://en.wikipedia.org/wiki/Capture_the_flag" target="_blank">Capture the flag</a>: dividido por times, o objetivo é capturar a bandeira do adversário;</li>
<li>Tactical: mistura tática com itens de <a title="First Person Shooter" href="http://pt.wikipedia.org/wiki/Tiro_em_primeira_pessoa" target="_blank">FPS</a>, humanos vs aliens, o objetivo é destruir a base do adversário (<strong>atenção: versão alpha</strong>);</li>
<li>Deathball: as balas são substituídas por bolas,  estilo deathmatch.</li>
</ul>
Ainda existem mais opções para jogo em multiplayer, confira! ;)

### Beleza Fernando, mas como eu instalo?
Aí vão, existem três formas de instalar o game:

<ul>
<li>SVN: Você pode compilar o código fonte do jogo diretamente do servidor de versionamento dos desenvolvedores, isso significa que você vai ter sempre a versão mais recente. É passível de bugs, e isso é legal, você pode ajudar os desenvolvedores a melhorar o jogo reportando possíveis erros;</li>
</ul>
<ul>
<li>Normal: Compilar o jogo a partir do download do site oficial do <a title="Alien Arena" href="http://red.planetarena.org/aquire.html" target="_blank">Alien Arena</a>;</li>
<li>Mamão com açúcar: Baixar diretamente do repositório via terminal ou central de programas.</li>
</ul>
Mas antes vamos instalar as dependências:<br />
<em>Obs: os comandos funcionam no Ubuntu e distro derivadas e obviamente devem ser digitados no terminal.</em>

{{< highlight bash >}}
sudo apt-get install build-essential subversion libsdl1.2-dev libsdl-image1.2-dev libsdl-ttf2.0-dev libsdl-mixer1.2-dev libcurl4-openssl-dev libxxf86dga-dev libxxf86vm-dev libopenal-dev
{{< / highlight >}}

#### SVN
Para a instalação:

{{< highlight bash >}}
sudo apt-get install subversion
mkdir ~/alienarena
svn co svn://svn.icculus.org/alienarena/trunk ~/alienarena
cd ~/alienarena/source
sudo make clean
sudo make install
{{< / highlight >}}

Para atualizá-lo:

{{< highlight bash >}}
cd ~/alienarena
svn update
cd source
sudo make clean
make
sudo make install
{{< / highlight >}}

#### Normal
Faça o download jogo em um dos <a href="http://red.planetarena.org/aquire.html" target="_blank">links</a> (Alien Arena: Combat Edition(7.66) for Linux/Unix/OSX(Includes Tactical Demo Alpha)) e abra o terminal:

{{< highlight bash >}}
tar -zxvf alienarena.tar.gz
cd alienarena
./configure
make 
sudo make install
{{< / highlight >}}

#### Mamão com Açúcar
{{< highlight bash >}}
sudo apt-get install alienarena
{{< / highlight >}}

Ou através da Central de Programas do Ubuntu.

### Jogando
Para executar o jogo basta digitar no terminal

{{< highlight bash >}}
alienarena
{{< / highlight >}}

Aproveitei e gravei um rápido vídeo mostrando o jogo (perdoem-me pela edição e pela qualidade do vídeo, mas ainda sim é possível ver em 720p HD), enjoy!<br />

<iframe src="//www.youtube.com/embed/DPKp2McGUqQ?rel=0" height="480" width="640" allowfullscreen="" frameborder="0"></iframe>

### Links Úteis
<a href="http://red.planetarena.org/index.html" target="_blank">http://red.planetarena.org/index.html</a>

<a href="http://www.moddb.com/games/alien-arena-2008/news/alien-arena-tactical-alpha-due-out-soon" target="_blank">http://www.moddb.com/games/alien-arena-2008/news/alien-arena-tactical-alpha-due-out-soon</a>

<a href="http://www.indiedb.com/games/alien-arena-2008/" target="_blank">http://www.indiedb.com/games/alien-arena-2008/</a>

<a href="http://alienarena.wikia.com/wiki/Alien_Arena_Wiki:About">http://alienarena.wikia.com/wiki/Alien_Arena_Wiki:About</a>

