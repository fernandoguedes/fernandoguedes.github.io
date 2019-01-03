---
categories:
- Desenvolvimento
date: 2016-01-15T18:31:09Z
feature-img: assets/2016-01-15/promises.jpg
published: true
status: publish
tags:
- tip
- dica
- angularjs
- promises
- javascript
- q
title: 'Dica: Vários promises simplificados com o $q no AngularJS'
type: post
url: /2016/01/15/varios-promises-de-forma-simplificada-no-angularjs/
---

O propósito dessa dica é abordar de forma superficial sobre como disparar diversas chamadas async e aguarda-lás, retornando todas conjuntamente utilizando o `$q`. Esse tipo de abordagem é útil quando temos uma dezena de microserviços e precisamos fazer alguma ação com o retorno deles de forma conjunta.

O AngularJS por padrão utiliza em suas [Promises](https://www.promisejs.org/) uma `lib` que se chama `$q`, como se trata de um padrão é bem fácil usar a mesma técnica com qualquer outra `lib` ou até mesmo com a API nativa. Nesse caso, utilizaremos o `$q.all`.

Vamos supôr que você tem um serviço implementado com Promises que consome uma API externa e que o mesmo está "injetado", bem como o `$q` que nesse contexto entra como dependência do próprio controller.

Dentro desse `controller`, vamos usar o `$q.all` para gerenciar os diversos requests que serão feitos de forma assíncrona. Aqui são basicamente dois passos, o primeiro é declarar os serviços dentro de um array, e o segundo chamar esse mesmo array através do comando `$q.all`.

{{< highlight javascript >}}
angular
    .module('seuApp')
    .controller('appCtrl', appCtrl);

appCtrl.$inject = ['$q', 'appService'];

function appCtrl($q, appService) {
    let id = 1;

    // Declare os serviços em um array
    let promises = [
        appService.getSalario(id),
        appService.getDividas(id)
    ];

    // Aguarda o retorno de todos os requests e guarda no escope
    $q.all(promises).then(val => {
        // Guarda no escopo caso queira usar os valores em outros lugares
        $scope.salario = val[0]; // getSalario
        $scope.dividas = val[1]; // getDividas
        $scope.sobrou = $scope.salario - $scope.dividas;
    });
};
{{< / highlight >}}

*Atualizado no dia 07/08/2017: Melhorei o texto e enxuguei o código, além da substituição do `var` por `let` e a adição de `arrow functions`.*
