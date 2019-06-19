# Versionamento de código

<img src="images/versoes_git.png" width="65%" style="display: block; margin: auto;" />

Na estatística, a todo momento estamos editando documentos, como por exemplo códigos, artigos, relatórios, aulas, apresentações, livros, entre outros. Nesse processo de edição dos mais variádos documentos, quase sempre sentimos a necessidade de versionar o conteúdo, uma vez que se não houver um versionamento e se desejarmos voltar à um estado de edição anterior, estariamos sobre uma tarefa extremamente difícil ou mesmo impossível, a depender do número de passos anteriores ao qual desejamos voltar.

Quando não dominamos nenhum sistema de controle de versão, normalmente o que fazemos para ter a possibilidade de voltar para uma dada versão de edição é armazenar diversas cópias do projeto em diretórios distintos. Versionar dessa forma pode servir quando temos poucas versões, proém, mesmo assim é comum os desarranjos e atrapalhos ao se tomar conta de diversos diretórios. Quando se domina um sistema de controle de versão evitamos esse tipo de problema, uma vez que continuaremos trabalhando sobre um mesmo diretório que terá seus estados modificados quando solicitado, isto é, será possível voltar para a distribuição de arquivos e conteúdos anteriores, mesmo se nesse processo de edição alguns arquivos foram deletados, renomeados ou fortemente modificados.


**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Não se preocupe se você voltar à estados anteriores e desistir. Você poderá retornar à estados mais recentes (incluindo o último) sem nenhum problema. **Deixe o trabalho sujo com um sistema de versionamento**.  

Além disso, para nós estatísticos que vivemos codificando e constantemente alterando códigos de programação, versionar de forma eficiente é algo crucial.
</div></div>\EndKnitrBlock{rmdimportant}

## Git

Visando ajudar o desenvolvedor na tarefa de versionamento de projetos/códigos, a ferramenta [**git**](https://git-scm.com/) foi desenvolvida, escrita utilizando a linguagem C, por [**Linus Torvalds**](images/linus_torvalds.jpg) (criador do Linux) e [**Jun Hamano**](images/ju_hamano.jpeg), um engenheiro de sofware japonês. No [**git**](https://git-scm.com/), cada diretório de trabalho é um repositório com histórico completo das versões e não depende de acesso à um servidor ou rede central. Essa é uma das características que torna o git uma ferramenta rápida, além, é claro, de ser escrito em C, que reduz a sobrecarga de tempos de execução que é algo normalmente comum em linguagens de nível superior.

Inicialmente essa ferramenta visava ajudar os desenvolvedores do kernel do Linux na tarefa de versionar, de forma eficiente, as mudanças no kernel que antes eram versionadas por meio do [**BitKeeper**](http://www.bitkeeper.org/), um software proprietário desenvolvido pela  BitMover Inc, Califórnia. Isso era um dilema entre os desenvolvedores do Linux, uma vez que ao contrário do [**BitKeeper**](http://www.bitkeeper.org/), o Linux é conhecido por suas [**iniciativas Open Source**](https://opensource.org/). À época, o projeto Linux tinha acesso gratuito ao [**BitKeeper**](http://www.bitkeeper.org/). Porém, com a acusação de programadores do kernel Linux estarem utilizando engenharia reversa, o acesso gratuito foi removido. 


Além do git, atualmente existem algumas ferramentas para versionamento de códigos. Entre tais ferramentas, enumero duas:

1. [**mercurial**](https://www.mercurial-scm.org): Trata-se de um sistema de versionamento, assim como o git, com [**iniciativas Open Source**](https://opensource.org/). Na internet é fácil encontrar diversos comparativos, em que muitos usuários citam como uma de suas vantagens a facilidade. O [**mercurial**](https://www.mercurial-scm.org) é o sistema de versionamento mais popular na plataforma de hospedagem de código fonte [**Bitbucket**](https://bitbucket.org/product/) que não é tão popular quanto o [**GitHub**](https://github.com/) e o [**GitLab**](https://about.gitlab.com/); 
  
2. [**subversion**](http://subversion.apache.org/): Trata-se de um sistema de versionamento distribuido sobre os termos da [**Apache License**](https://pt.wikipedia.org/wiki/Licen%C3%A7a_Apache) e que foi desenvolvido pela [**Apache Software Foundation**](https://pt.wikipedia.org/wiki/Apache_Software_Foundation).


Por se tratar do sistema de versionamento mais amplamente utilizado (mais popular) em versionamentos locais e remotos (a exemplo do [**GitHub**](https://github.com/) e [**GitLab**](https://about.gitlab.com/) que são plataformas de hospedagem de código em que é possível facilmente enviar códigos versionados usando git), trataremos aqui apenas do uso do [**git**](https://git-scm.com/).

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
A ferramenta [**git**](https://git-scm.com/) poderá ser facilmente instalada em Linux/Unix, Windows e macOS. Clique [**aqui**](https://git-scm.com/downloads) e faça o download da versão desejada e instale em seu sistema operacional. Há diversos vídeos na internet ensinando a configurar o [**git**](https://git-scm.com/) em sistemas Windows. 
</div></div>\EndKnitrBlock{rmdnote}

Após a instalação do [**git**](https://git-scm.com/) em seu sistema operacional, abaixo listarei algumas funções interessantes para o uso do [**git**](https://git-scm.com/) via o prompt de comando (terminal). O terminal ao qual você deverá trabalhar com o git é algo parecido com as imagens abaixo:

<div class="figure" style="text-align: center">
<img src="git_files/figure-html/unnamed-chunk-4-1.png" alt="A imagem mais a esquerda refere-se ao terminal bash no linux e a mais a direita refere-se terminal bash instalado no Windows para o uso do git. Essas imagens são meramente ilustrativas e poderão variar um pouco a depender do sitema operacional." width="768" />
<p class="caption">(\#fig:unnamed-chunk-4)A imagem mais a esquerda refere-se ao terminal bash no linux e a mais a direita refere-se terminal bash instalado no Windows para o uso do git. Essas imagens são meramente ilustrativas e poderão variar um pouco a depender do sitema operacional.</p>
</div>

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
  
Para usuários de sistemas baseados em Arch Linux, por exemplo, usuários do Manjaro Linux, a instalação do git é bastante fácil. No terminal do Linux, basta fazer: </br></br>
  </div>\EndKnitrBlock{rmdobservation}

```shell
                                sudo pacman -S git 
```
  
Usuários do sistema operacional Windows poderão instalar facilmente o git considerando o executável fornecido [**aqui**](https://gitforwindows.org/index.html). Para esses usuários, no processo de instalação aconselho, em **Adjusting your PATH environment** é importante selecionar a última opção, conforme a imagem abaixo: 

<img src="images/git_windows_opcao.png" width="75%" style="display: block; margin: auto;" />
</div>


## GitHub

