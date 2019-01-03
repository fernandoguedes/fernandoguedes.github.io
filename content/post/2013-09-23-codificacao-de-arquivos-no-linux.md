---
categories:
- Desenvolvimento
date: 2013-09-23T18:31:09Z
published: true
status: publish
tags:
- codificação
- iso-8859-1
- linux
- utf-8
title: Codificação de arquivos no Linux
type: post
url: /2013/09/23/codificacao-de-arquivos-no-linux/
---

Vou iniciar o blog, colocando a resolução de um problema que eu estava enfrentando com projetos com vários programadores utilizando o git como versionamento. <br>

Acontece que algumas IDEs estavam codificações diferentes, e quando o arquivo era aberto por outro programador acabava corrompendo tudo. Atrás de uma solução rápida, descobri que a codificação e até mesmo a alteração da codificação de um arquivo pode ser feita via terminal.

## Mão na Massa

Bom, para saber a codificação de um arquivo basta digitar no terminal:

{{< highlight bash >}}
file -i arquivo.php
arquivo.php: text/x-php; charset=us-ascii
{{< / highlight >}}

Para convertê-lo basta utilizar o comando **iconv** ou **recode**:

{{< highlight bash >}}
iconv arquivo.php --to-code UTF-8 > arquivo2.php
recode UTF-8 arquivo.php
{{< / highlight >}}

O post tá bem resumindo para solucionar esse problema em específico, mas se deseja ler mais:

{{< highlight bash >}}
man iconv
{{< / highlight >}}

Para ver a lista de formatos suportados:
{{< highlight bash >}}
iconv --list
{{< / highlight >}}
