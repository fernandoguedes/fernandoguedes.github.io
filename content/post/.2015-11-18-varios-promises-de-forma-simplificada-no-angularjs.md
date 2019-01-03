---
categories:
- Desenvolvimento
date: 2015-11-18T18:31:09Z
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
url: /2015/11/18/varios-promises-de-forma-simplificada-no-angularjs/
---

O propósito dessa dica é abordar de forma superficial sobre como disparar diversas chamadas async e aguarda-lás, retornando todas conjuntamente utilizando o $q. Esse tipo de abordagem é útil quando temos uma dezena de microserviços e precisamos fazer alguma ação com o retorno deles.

O AngularJS tem uma implementação própria das funcionalidades de Promises que se chama **$q**, como se trata de um padrão - que inclusive vem como *default* na ES6 -, é bem fácil usar a mesma técnica com qualquer outra lib. Nesse caso, utilizaremos o **$q.all**.

Vamos supôr que você tem um serviço implementado com Promises que consome uma API externa  e que o mesmo está injetado, bem como o $q que nesse contexto entra como dependência do próprio controller.

{{< highlight javascript >}}

angular
    .module('seuApp')
    .controller('appCtrl', appCtrl);

appCtrl.$inject = ['$scope', '$q', 'appService'];

function appCtrl($scope, $q, appService) {

};

{{< / highlight >}}

Dentro desse *controller*, vamos usar o $q.all para gerenciar os diversos requests que serão feitos de forma assíncrona. Aqui são basicamente dois passos, o primeiro é declarar os serviços dentro de um array, e o segundo chamar esse mesmo array através do comando **$q.all**.

{{< highlight javascript >}}
angular
    .module('seuApp')
    .controller('appCtrl', appCtrl);

appCtrl.$inject = ['$scope', '$q', 'appService'];

function appCtrl($scope, $q, appService) {

    var id = 1;

    // Declare os serviços em um array
    var promises = [
        appService.getGastos(id),
        appService.getVendas(id)
    ];

    $q.all(promises).then(function(val) {
        $scope.gastos = val[0];
        $scope.vendas = val[1];
        $scope.
    });
};
{{< / highlight >}}
