---
layout: post
title: Setting-Up-VIM
date: 2022-02-08 13:25 +0600
image: "/images/vim.png"
permalink: /Setting-Up-VIM/
tags: VIM
featured: true
---

<p>

I came across this video <a href="https://www.youtube.com/watch?v=SYExiynPEKM">https://www.youtube.com/watch?v=SYExiynPEKM</a>  where tomnomnom is doing recon on shopify along with nahamsec.

I am using nano for a long time and as a person who spends long time on terminal i wanted to make the experience of writing code and editing files etc better for myself.

I used vim sometimes and i know that vim has a great power. After watching tomnomnom vim terminal look, i wanted to setup like that.

</p>

<h2> Setting up vim </h2>

* I Downloaded the vimrc file https://github.com/tomnomnom/dotfiles/blob/master/.vimrc into your ~/.vimrc

<div class="language-bash"><div class="highlight"><pre class="highlight"><code>mkdir -p ~/.vim/bundle
cd ~/.vim/bundle
git clone https://github.com/VundleVim/Vundle.vim.git
git clone https://github.com/tpope/vim-fugitive.git
git clone https://github.com/sjl/gundo.vim.git
git clone https://github.com/godlygeek/tabular.git
git clone https://github.com/vim-airline/vim-airline.git
git clone https://github.com/vim-airline/vim-airline-themes.git
git clone https://github.com/altercation/vim-colors-solarized.git
git clone https://github.com/preservim/nerdtree.git
git clone https://bitbucket.org/TomNomNom/xoria256.vim
git clone https://github.com/fatih/vim-go.git
git clone https://github.com/rust-lang/rust.vim.git
</code></pre></div></div>

* I installed the above plugins which tomnomnom uses ( go and rust plugins ar optoinal sue it if you code in those languages )

* Finished setting up and now my vim looks like this :)

![vimfinal](/images/vimfinal.png)
