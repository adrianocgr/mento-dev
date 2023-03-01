[‹ voltar ao README](./README-trilha-mentodev.md)

# FLUXO DE DESENVOLVIMENTO USANDO O GIT

## Padrão de nomeação de Branchs

* Versionamento semântico 1.0.0 
 -- 1(Major) - Controle de compatibilidade. Informa que existem funcionalidades/códigos incompatíveis com as versões anteriores.
 -- 0(Minor) -  controle de funcionalidade. Informa que novas funcionalidades foram adicionadas ao código.
 -- 0 (Patch) - controle de correção de bugs. Informa que um ou mais erros foram identificados e corrigidos.

Na AZ quando vamos atender um chamado e precisamos usamos um padrão de nome interno, como mostrado no exemplo abaixo:

6.3_COMSFW_997
"Major"."Minor"_"numero do chamado"

Normalmente quando vamos atender um novo chamado seguimos o seguinte fluxo:

* git checkout 6.3
* git pull
* git checkout -b 6.3_COMSFW_997

Assim teremos uma copia da branch atualizada para podemos trabalhar nela.

## Padrões de Commits

Quando estamos trabalhando na nossa branch podemos fazer varios commits e normar como quiser, porém quando vamos subir a alteração para a master temos que manter um commit só com o seguinte padrão:

"Major"."Minor"_"numero chamado" - "Titulo chamado"

Podemos usar o comando git [rebase](https://medium.com/cwi-software/utilizando-rebase-e-squash-para-melhorar-o-hist%C3%B3rico-do-git-fdb2d952c09c) para realizarmos a junção dos commits ou como falamos normalmente o squash, tem a opção de realizarmos o squash no ato do merge request que irei mostrar logo abaixo.

## Merge Requests

![gitpush](https://i.ibb.co/vdcBrZV/git-push.png)

![mergerequest](https://i.ibb.co/vqS89YR/merge-request.png)

## Resolução de conflitos

O Intellij ajuda bastante na resolução de confritos.

![](https://i.ibb.co/GCkvsRV/2022-01-10-16-20.png)
Como visto na imagem na esquerda mostra o conteúdo da branch master na direita mostra da branch_2, e no meio vai ser o resultado do seu merge, ai você pode gerenciar o que você ira aceitar de cada arquivo.

[‹ voltar ao README](./README-trilha-mentodev.md)

-----

© Copyright 2021 - All rights reserved | Todos os direitos Reservados

__AZ Tecnologia em Gestão__