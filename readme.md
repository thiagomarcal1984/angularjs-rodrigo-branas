# Material de Estudo

## <a href="https://www.youtube.com/watch?v=_y7rKxqPoyg&list=PLQCmSnNFVYnTD5p2fR4EXmtlR6jQJMbPb&index=1">AngularJS #1 - Introdução e Hello World</a>

<a href="https://www.youtube.com/watch?v=_y7rKxqPoyg&list=PLQCmSnNFVYnTD5p2fR4EXmtlR6jQJMbPb ">Playlist do Rodrigo Branas sobre AngularJS</a>


<a href="https://eduardocunha11.github.io/firstblog/aulas/lab-programacao/books/AngularJS-Essentials.pdf">Livro do Rodrigo Branas</a>


<a href="https://material.angularjs.org/1.1.8/getting-started">Modelo de template para projetos AngularJS (versão 1.1.8 é a única que tem o modelo)</a>

## <a href="https://www.youtube.com/watch?v=dCWkeFBCPnA&list=PLQCmSnNFVYnTD5p2fR4EXmtlR6jQJMbPb&index=2">AngularJS #2 - Usando Diretivas - Parte 1 </a>

> Diretivas são extensões da linguagem HTML que permitem a implementação de novos comportamentos, de forma declarativa.

| Diretiva      | Explicação |
| ---           | --- |
| ngApp         | Diretiva para definir as fronteiras da aplicação. |
| ngController  | Diretiva para vincular um elemento da View ao Controller. |
| ngBind        | Diretiva para substituir um elemento por uma expressão. É o inverso de ngModel: busca do escopo e exibe na view.|
| ngRepeat      | Diretiva para iterar sobre itens de uma coleção ou de um objeto. |
| ngModel       | Diretiva para vincular uma propriedade ao $scope. É o inverso de ngBind: busca da view e atribui ao escopo |
| ngClick       | Atribui comportamento ao evento. <a href="https://www.w3schools.com/angular/angular_events.asp">Diretivas-irmãs</a>: ng-blur, ng-dblclick, etc. |

## <a href="https://www.youtube.com/watch?v=VcF7SySRkHs&list=PLQCmSnNFVYnTD5p2fR4EXmtlR6jQJMbPb&index=3">AngularJS #3 - Usando Diretivas - Parte 2</a>
| Diretiva      | Explicação |
| ---           | --- |
| ngDisabled       | Desabilita elementos dinamicamente. |
| ngOptions       | Renderiza as opções de um select. |
| ngClass e ngStyle       | Aplica classes e estilos CSS dinamicamente. |
| ngShow       | Exibe elemento do DOM, se a condição for verdadeira. |
| ngHide       | Oculta elemento do DOM, se a condição for verdadeira. |
| ngIf       | Elemento do DOM só **existe** se a condição for verdadeira. |
| ngInclude       | Inclui conteúdo de arquivo dinamicamente. |


### Aplicando a ngOptions
Sintaxe para invocar a diretiva `ngOptions`:
```HTML
<select 
    ng-model="modelo.objeto"
    ng-options="objeto.nome for objeto in lista"
></select>
```
Com essa sintaxe, o objeto inteiro é salvo dentro do objeto de modelo (representado por `modelo.objeto`). A diretiva `ngOptions` vai indicar qual será o valor do objeto que será exibido no select (no caso, `objeto.nome`), e de onde esses objetos virão (no caso, `lista`).

A tag `<option>` é opcional dentro do `<select>`, mas é bom para personalizar o texto a ser exibido para a opção nula/padrão.


Outra sintaxe para invocar a diretiva `ngOptions`, para buscar chave/valor do objeto:
```HTML
<select 
    ng-model="modelo.objeto"
    ng-options="objeto.key as objeto.nome for objeto in lista"
></select>
```
A diferença para o código anterior é o texto `objeto.key as objeto.nome`: `objeto.key` é a propriedade que vai servir de chave do objeto; e `objeto.nome` é a propriedade que vai ser exibida como valor.

Mais uma sintaxe para invocar a diretiva `ngOptions`, para agrupar as opções por categoria:
```HTML
<select 
    ng-model="modelo.objeto"
    ng-options="obj.nome group by obj.categoria for obj in lista"
></select>
```
As opções no `<select>` serão agrupadas por `obj.categoria`.

### Aplicando a ngClass:
1. uma única classe: 
```HTML
<style>
    .estilo {
        font-color: navy;
    }
</style>
<script>
    angular.module('modulo', [])
        .controller('meuCtrl', function($scope){
            $scope.classe = 'estilo';
        })
</script>
<body ng-controller="meuCtrl>
    <div ng-class="classe">Texto em azul-marinho.</div>
</body>
```
2. mais de uma classe, como array:
```HTML
<style>
    .azul {
        font-color: navy;
    }
    .negrito {
        font-weight: bolder;
    }
</style>
<script>
    angular.module('modulo', [])
        .controller('meuCtrl', function($scope){
            $scope.classe1 = 'azul';
            $scope.classe2 = 'negrito';
        })
</script>
<body ng-controller="meuCtrl>
    <div ng-class="[classe1, classe2]">
        Texto em negrito na cor azul-marinho.
    </div>
</body>
```
3. mais de uma classe, como dicionário:
```HTML
<style>
    .azul {
        font-color: navy;
    }
    .negrito {
        font-weight: bolder;
    }
</style>
<script>
    angular.module('modulo', [])
        .controller('meuCtrl', function($scope){
            $scope.selecionado = false;
        })
</script>
<body ng-controller="meuCtrl>
    <!-- 
        Repare que a chave é a classe CSS, 
        e o valor é um booleando do Angular
    -->
    <div ng-class="{azul : selecionado, negrito : selecionado}">
        <input type="checkbox" ng-model="selecionado"/>
        Se marcar o checkbox, o texto fica em negrito e azul-marinho.
    </div>
</body>
```
É possível aplicar muitas classes de uma vez baseada num mesmo booleano da seguinte forma: `<tag ng-class={'class1 class2' : meuBooleano }>`.

### Filter
Usando filtro com JavaScript:
```JavaScript
$scope.filtrado = function(lista) {
    var filtrado = lista.filter(function (obj) {
        // Quando o retorno da função for True,
        // o objeto entra no array. 
        if (obj.selecionado) return obj;
    })
};
```
### Some
Verificando se há algum objeto com um parâmetro verdadeiro, em JavaScript:
```JavaScript
$scope.isSelecionado = function(lista) {
    return lista.some(function (obj) {
        return obj.selecionado;
    });
}
```
### ngStyle
Aplicação de um estilo conforme variáveis de um objeto.

```JavaScript
$scope.contatos = [
    { nome : "Pedro", cor : "blue"},
    { nome : "Ana", cor : "yellow"},
    { nome : "Maria", cor : "red"},
];
```

```HTML
<td>
    <div style="width: 30px; height: 30px;"
        ng-style="{'background-color' : contato.cor}"
    ></div>
</td>
```

### ngShow e ngHide
O elemento é exibido ou ocultado se a condição for verdadeira. Use para elementos **simples**: 
```HTML
<table ng-show="!cart.vazio">...</table>
<button ng-hide="cart.vazio">Confirmar compra</button>
```

### ngIf
O elemento **desaparece** do DOM, se a condição for falsa. Use em elementos do DOM muito **complexos**, que demoram pra carregar:
```HTML
<button ng-if="cart.vazio">Confirmar compra</button>
```

### ngInclude
Insere um arquivo conforme a **string** que você inserir como parâmetro (note que no exemplo usamos aspas simples dentro das aspas duplas, pois sem elas o nome do arquivo seria procurado dentro de $scope):
```HTML
<div ng-include="'footer.html'"></div>    
```

## <a href="https://www.youtube.com/watch?v=HDjpIT2TLP0&list=PLQCmSnNFVYnTD5p2fR4EXmtlR6jQJMbPb&index=4">AngularJS #4 - Validando Formulários</a>

| Diretiva      | Explicação |
| ---           | --- |
| ngRequired         | Determina a obrigatoriedade de um campo, e recebe um boolenao. |
| ngMinlength         | Determina o tamanho mínimo de um campo. |
| ngMaxlength         | Determina o tamanho maximo de um campo. |
| ngPattern         | Aplica uma RegEx a um campo. |
| ngMessages e ngMessage         | Agrupa mensagens de erro. |


### Propriedades <form>.$valid e <form>.$invalid
Ao criar um formulário **nomeado** dentro do HTML de um controller, o nome desse formulário será atribuído ao escopo do controller. Ele tem dois elementos: $valid e $invalid. Todos os campos que contenham as diretivas ngModel e ngRequired (tem que ter os dois) serão usados para determinar se o formulário é ou não válido:

```HTML
<p>É válido: {{ contatoForm.$valid }}</p>
<p>É inválido: {{ contatoForm.$invalid }}</p>
<p>{{ contatoForm }}</p>
<!-- O formulário já será válido se contato.nome for preenchido -->
<form name="contatoForm">
    <input type="text" ng-model="contato.nome" ng-required="true">
    <input type="text" ng-model="contato.telefone" >
    <button type="submit">Enviar</button>
</form>
```

Os nomes dos campos dão origem a outras subvariáveis do formulário declarado no controller:
```HTML
<form name="contatoForm">
    <input type="text" name="nome" ng-model="contato.nome" ng-required="true">
    <input type="text" name="telefone" ng-model="contato.telefone" ng-required="true">
    <!-- 
        Perceba como a mensagem de validação pode ser aplicada a cada campo 
        do formulário. Basta usar <formulario>.<campo>.$invalid ou $valid.
    -->
    <div class="msg" ng-show="contatoForm.nome.$invalid">
        Por favor, preencha o nome.
    </div>
    <div class="msg" ng-show="contatoForm.telefone.$invalid">
        Por favor, preencha o telefone.
    </div>
    <button ng-click="adicionarContato(contato)">Adicionar Contato</button>
</form>
```

### Propriedades <form>.$pristine e <form>.$dirty
O atributo `$pristine` (não tocado) é o contrário de `$dirty` (já alterado):
```HTML
<form name="form">
    <input type="text" name="nome" ng-model="contato.nome" ng-required="true">
    <input type="text" name="tel" ng-model="contato.telefone" ng-required="true">
    <!-- 
        Perceba como a mensagem de validação pode ser aplicada a cada campo 
        do formulário. Basta usar <formulario>.<campo>.$invalid ou $valid.
    -->
    <div class="msg" ng-show="form.nome.$invalid && form.nome.$dirty">
        Por favor, preencha o nome.
    </div>
    <div class="msg" ng-show="!(form.tel.$invalid && form.tel.$pristine)">
        Por favor, preencha o telefone.
    </div>
    <button ng-click="adicionarContato(contato)">Adicionar Contato</button>
</form>
```

### Propriedade `<form>.<campo>.$error`
A propriedade `$error` é um conjunto de validação para diferentes validadores.
Aplique ela no HTML para ver quais os validadores possíveis (required, minlength etc.).


### ngPattern
As RegEx aplicadas na diretiva ngPattern no Angular precisam estar entre barras:
```HTML
<form name="formulario">
    <input name="telefone" ng-pattern="/^\d{4,5}-?\d{4}$/">
    <div ng-hide="formulario.telefone.$error.pattern" class="alert">
        O campo telefone deve ter o formato DDDDD-DDDD.
    </div>
</form>
```

### ngMessages e ngMessage
As diretivas ngMessages e ngMessage **não** estão no angular.js. É necessário baixar o `angular-messages.js`.

A diretiva ngMessages recebe a lista de erros do campo. E a diretiva ngMessage recebe a diretiva correspondente ao erro que se pretende reportar.
```HTML
<div ng-messages="contatoForm.telefone.$error">
    <div ng-message="required">
        Por favor, preencha o telefone.
    </div>
    <div ng-message="pattern">
        O campo telefone deve ter o formato DDDDD-DDDD.
    </div>
</div>
```
