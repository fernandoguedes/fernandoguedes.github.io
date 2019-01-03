---
categories:
- Development
date: 2015-05-29T18:31:09Z
published: true
status: publish
tags:
- linux
- vim
- patterns
- english
title: 'Short Tip: Vim - Redefine tabs to spaces'
type: post
url: /2015/05/29/tip-converting-tabs-to-space-vim/
---

For redefine tabs to space (whatever many spaces, the development default is four) is very simple.

Open the ~/.vimrc:

{{< highlight bash >}}

vim ~/.vimrc

{{< / highlight >}}

So, paste the configuration into the file:

{{< highlight bash >}}

set tabstop=4       " The width of a TAB is set to 4.
                    " Still it is a \t. It is just that
                    " Vim will interpret it to be having
                    " a width of 4.
set shiftwidth=4    " Indents will have a width of 4
set softtabstop=4   " Sets the number of columns for a TAB
set expandtab       " Expand TABs to spaces

{{< / highlight >}}

Save and restart (:wq!) vim.
