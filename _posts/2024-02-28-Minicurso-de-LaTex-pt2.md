---
layout: post
title:  "Minicurso de LaTeX - parte 2"
tags:   LaTeX
---

## Introdução

Este post é um apoio e resumo para o minicurso de LaTeX realizado na Semana da Matemática 2024, de nome "LaTeX: (quase) tudo o que você precisa saber de LaTeX sendo matemático", ministrado por mim.

> O objetivo do curso é dar uma boa base ja direcionada para a matemática + ABNT. Essa base vem dos princípios do *clean code* que aprendi durante minha experiência como programador e como aluno do curso de Matemática.

**E no overleaf, procure por templates (com as palavras chaves 'UFPR' ou 'ABNT' ou conforme sua necessidade) não precisa reinventar a roda!**

## Links e ferramentas uteis de LaTeX:

- [ctan.org](https://ctan.org)
- [tex.stackexchange.com](https://tex.stackexchange.com)
- [github.com/abntex/abntex2/wiki/PorOndeComecar](https://github.com/abntex/abntex2/wiki/PorOndeComecar)
- [overleaf.com/learn](https://www.overleaf.com/learn)
- [Detextify](https://detexify.kirelabs.org/classify.html)
- [Lista de simbolos matemáticos da OEIS](https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols)

No caso de trabalhar com diagramas do tipo no que se usa em Teoria de Categorias ou com *quivers* (que é o meu caso) tem esse site:

- [q.uiver.app](https://q.uiver.app)

> Ele da algum tipo de conflito com o pacote [portuguese]{babel}, mas não descobri ainda o que :(

## Outros Links

- [Conversor de ISBN para BIBTEX](https://www.bibtex.com/c/isbn-to-bibtex-converter/)
- [Conversor de DOI para BIBTEX](https://www.bibtex.com/c/doi-to-bibtex-converter/)

## ABNT e LaTeX

- [abntex.net.br](https://www.abntex.net.br)

> As normas de citações foram atualização com a **NBR 10520:2023**, e o *abntex2*, cuja ultima atualização foi em 2018 (no momento de escrita do minicurso) ja está desatualizado. Tem uma issue aberta sobre esse problema no [repositório do github do pacote](https://github.com/abntex/abntex2/issues/260).

> Uma solução foi encontrada, e um modelo (bem completo) está disponível [neste repositório](https://github.com/eekBR/ufpr-abntex2)

Minha solução para o minicurso: utilizar só o que comumente vi sendo cobrado de ABNT ao longo da minha graduação.

## Códigos para copiar e colar

### Finalmente, algo para usar de modelo

```latex
\documentclass[
    12pt,
    a4paper
    ]{article}

% para escrever em pt-br, não são mais necessários na nova versão do pdfLaTeX, mas nao machuca deixar.
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[brazilian]{babel}
\usepackage{csquotes} % carregamos esse também pois estamos usando biblatex

% margens
\usepackage{geometry}
\geometry{
    left=3cm,
    top=3cm,
    right=2cm,
    bottom=2cm
}

% Um jeito de usar a fonte Times New Roman ou Arial é compilando com XeLaTeX (nesse caso, deve retirar o inputenc):
\usepackage{fontspec}
\setmainfont{Times New Roman} % ou \setmainfont{Arial} 

% faz todo paragrafo depois de um \chapter ou \section ser identado
\usepackage{indentfirst}
% mudar o espaçamento do paragrafo
\usepackage{setspace}


% créditos ao usuario https://github.com/eekBR pela solução das refencias e citações para a NBR 10520:2023
\usepackage[
    style=abnt,
    hyperref=true,
    giveninits=true,
    mincitenames=1,
    maxcitenames=2]{biblatex}    
\addbibresource{nomeDoSeuArquivoDeReferencias.bib}

\renewcommand*{\mkbibnamefamily}[1]{#1}

% configuração de um ambiente de citação direta longa conforme ABNT
\usepackage[
    leftmargin=4cm, % recuo de margem da abnt
    rightmargin=0cm, % pra manter no mesmo tamanho do texto
    indentfirst=false, % tira o paragrafo
    font={singlespacing, small} % define espaçamento simples e texto pequeno
    ]{quoting}

% para incluir imagens
\usepackage{graphicx}

% fazer tabelas de mais de uma pagina
\usepackage{longtable}

% permite usar multiplas figuras
\usepackage{caption}
\usepackage{subcaption}

% para usar a opção 'H' no ambiente figure e table
\usepackage{float}

% permite manipular o enumerate pra facilitar customização
\usepackage[shortlabels]{enumitem}

% incluir código com highlights
\usepackage{listings}

% para uso de cores
\usepackage{color}
\usepackage[dvipsnames]{xcolor}

% inlcuir pdfs no meio do documento
\usepackage{pdfpages}

% permite o uso de varias colunas
\usepackage{multicol}

% pacotes matemáticos da AMS
\usepackage{amsfonts}
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{amsthm}
% outro pacote matemático
\usepackage{mathtools} 

% Normalmente é para ser o ultimo pacote importado. Permite customizar hiperlinks. ELe permite fazer a \tableofcontents com links
\usepackage[
    colorlinks=true,
    linkcolor=blue,
    filecolor=magenta,      
    urlcolor=cyan,
    pdftitle={Exemplo de titulo}, % Muda o titulo do pdf gerado (diferente do nome do arquivo)
    pdfpagemode=FullScreen, % faz o pdf ser aberto em full screen
]{hyperref}

% tamanho do paragrafo
\setlength\parindent{1.25cm}

% cria ambientes, todos numerados a partir da section (que poderia ser chapter também)
\newtheorem{theorem}{Teorema}[section]
\newtheorem{proposition}{proposição}[section]
\newtheorem{corollary}{Corolário}[section]
\newtheorem{lemma}{Lema}[section]
\newtheorem{definition}{Definição}[section]
\newtheorem{remark}{Observação}[section]
\newtheorem{example}{Exemplo}[section]
\newtheorem{problem}{Problema}[section]
\newtheorem{axiom}{Axioma}[section]
\newtheorem{conjecture}{Conjectura}[section]
\newtheorem{exercise}{Exercício}[section]

% mudança de estilo da pra ser feita com o pacote amsthm, e definição de ambiente sem numeração também
% ambiente sem numeração, o nome 'theorem*' é para não redefinir o comando 'theorem' o 'solving*' é para manter o mesmo padrão e ambos estarem em conformidade com align* e equation*
\newtheorem*{theorem*}{Teorema}
\newtheorem*{solving*}{Resolução}

\title{Titulo \\ \large subtitulo
} % no caso da configuração o padrão do title é maior que o \large
\author{Seu Nome Aqui\thanks{ex: Bolsista do PET Matemática - UFPR}}

\date{Data customizada} % ou \today

\begin{document}

% gera o título
\maketitle

% gera o sumário
\tableofcontents

% define espaçamento 1.5 em todo o texto
\onehalfspacing

% input{localizacao/da/suaPrimeiraSeção}

\nocite{*} % coloca todas as refenrencias, independente de terem sido citadas ou não no texto

\printbibliography

\end{document}
```