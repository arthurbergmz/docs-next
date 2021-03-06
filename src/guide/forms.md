# Interligações em Formulários

## Uso Básico

Você pode usar a diretiva `v-model` para criar interligações de dados de mão dupla _(two-way data binding)_ em elementos input, textarea e select de formulários. Ele automaticamente escolhe a maneira correta de atualizar o elemento baseado no tipo do _input_. Embora um pouco mágico, `v-model` é essencialmente uma forma simplificada _(syntax sugar)_ para atualizar dados nos eventos de entrada do usuário, além de cuidado especial com casos extremos.

::: tip Nota
`v-model` irá ignorar o estado inicial dos atributos `value`, `checked` ou `selected` encontrado em qualquer elemento de formulário. Ele sempre irá tratar os dados da instância ativa com a fonte de verdade. Você pode declarar o valor inicial no lado do JavasScript, dentro da opção `data` do seu componente.
:::

`v-model` utiliza diferentes propriedades internamente e emite diferentes eventos para diferentes elementos input:

- elementos _text_ e _textarea_ usam a propriedade `value` e o evento `input`;
- _checkboxes_ e _radiobuttons_ utilizam a propriedade `checked` e o evento `change`;
- campos de seleção utilizam `value` como propriedade e `change` como um evento.

<span id="vmodel-ime-tip"></span>
::: tip Nota
Para idiomas que requerem um [IME](https://en.wikipedia.org/wiki/Input_method) (Chinês, Japonês, Koreano etc.), você notará que o `v-model` não é atualizado durante a composição IME. Se você também quiser atender a essas atualizações, use o evento do `input` ao invés do `v-model`.
:::

### Input

```html
<input v-model="message" placeholder="me edite" />
<p>A mensagem é: {{ message }}</p>
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="eYNPEqj" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lidando com formulários: v-model simples">
  <span>Veja o <i>Pen</i> <a href="https://codepen.io/vuejs-br/pen/rNeqvjd">
  Lidadndo com Fomulários: v-model simples</a> por Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  no <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### Textarea

```html
<span>Mensagem com múltiplas linhas:</span>
<p style="white-space: pre-line;">{{ message }}</p>
<br />
<textarea v-model="message" placeholder="Escreva bastante"></textarea>
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="xxGyXaG" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lidando com Formulários: textarea">
  <span>Veja o <i>Pen</i> <a href="https://codepen.io/vuejs-br/pen/bGpmMqw">
  Lidando com Formulários: textarea</a> por Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  no <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Interpolação em _textareas_ (`<textarea>{{text}}</textarea>`) não funcionará. Em vez disso, use `v-model`.

```html
<!-- ruim -->
<textarea>{{ text }}</textarea>

<!-- bom -->
<textarea v-model="text"></textarea>
```

### Checkbox

Caixa de seleção única, valor booleano:

```html
<input type="checkbox" id="checkbox" v-model="checked" />
<label for="checkbox">{{ checked }}</label>
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="PoqyJVE" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lidando com Formulários: checkbox">
  <span>Veja o <i>Pen</i> <a href="https://codepen.io/vuejs-br/details/KKzGRWq">
  Lidando com Formulários: checkbox</a> por Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  no <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Múltiplos _checkboxes_, associados ao mesmo Array:

```html
<div id="v-model-multiple-checkboxes">
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>
  <br />
  <span>Nomes selecionados: {{ checkedNames }}</span>
</div>
```

```js
Vue.createApp({
  data() {
    return {
      checkedNames: []
    }
  }
}).mount('#v-model-multiple-checkboxes')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="bGdmoyj" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lidando com Formulários: multiplos checkboxes">
  <span>Veja o <i>Pen</i> <a href="https://codepen.io/vuejs-br/pen/ExKdLWp">
  Lidando com Formulários: múltiplos <i>checkboxes</i></a> por Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  no <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### Radio

```html
<div id="v-model-radiobutton">
  <input type="radio" id="one" value="One" v-model="picked" />
  <label for="one">Um</label>
  <br />
  <input type="radio" id="two" value="Two" v-model="picked" />
  <label for="two">Dois</label>
  <br />
  <span>Escolhido: {{ picked }}</span>
</div>
```

```js
Vue.createApp({
  data() {
    return {
      picked: ''
    }
  }
}).mount('#v-model-radiobutton')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="MWwPEMM" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lidando com Formulários: radiobutton">
  <span>Veja o <i>Pen</i> <a href="https://codepen.io/vuejs-br/pen/dyMgeRE">
  Lidando com Formulários: radiobutton</a> por Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  no <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### Select

Seleção de um único item:

```html
<div id="v-model-select" class="demo">
  <select v-model="selected">
    <option disabled value="">Escolha um</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selecionado: {{ selected }}</span>
</div>
```

```js
Vue.createApp({
  data() {
    return {
      selected: ''
    }
  }
}).mount('#v-model-select')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="KKpGydL" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lidando com Formulários: select">
  <span>Veja o <i>Pen</i> <a href="https://codepen.io/vuejs-br/pen/VwaExpO">
  Lidando com Formulários: select</a> por Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  no <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

:::tip Nota
Se o valor inicial da expressão `v-model` não corresponder match nenhuma das optções, o element `<select>` será renderizado em um estado "não selecionado". No iOS, isso impedirá o usuário de selecionar o primeiro item, pois não há disparo do evento `change` neste caso. Portanto é recomendado fornecer uma opção desabilitada com um valor vazio, como demonstrado no exemplo acima.
:::

Seleção de múltiplos itens (vinculando a um Array):

```html
<select v-model="selected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<br />
<span>Selecionado: {{ selected }}</span>
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="html,result" data-user="Vue" data-slug-hash="gOpBXPz" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lidando com Formulários: seleção de múltiplos itens (vinculando a um Array)">
  <span>Veja o <i>Pen</i> <a href="https://codepen.io/vuejs-br/pen/abNRGWR">
  Lidando com Formulários: seleção de múltiplos itens (vinculando a um Array)</a> por Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  no <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Renderização dinâmica de _options_ com `v-for`:

```html
<div id="v-model-select-dynamic" class="demo">
  <select v-model="selected">
    <option v-for="option in options" :value="option.value">
      {{ option.text }}
    </option>
  </select>
  <span>Selecionado: {{ selected }}</span>
</div>
```

```js
Vue.createApp({
  data() {
    return {
      selected: 'A',
      options: [
        { text: 'Um', value: 'A' },
        { text: 'Dois', value: 'B' },
        { text: 'Três', value: 'C' },
      ]
    }
  }
}).mount('#v-model-select-dynamic')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="abORVZm" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Lidando com Formulários: select com opções dinâmicas">
  <span>Veja o <i>Pen</i> <a href="https://codepen.io/vuejs-br/pen/BaKqxRK">
  Lidando com Formulários: select com opções dinâmicas</a> por Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  no <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Interligação de Valores

Para _radio_, _checkbox_ e _select_, a interligação de valores do `v-model` são sempre _strings_ estáticas (ou valores _boolean_ no caso do _checkbox_):

```html
<!-- `picked` é uma string "a" quando assinalado -->
<input type="radio" v-model="picked" value="a" />

<!-- `toggle` é verdadeiro ou falso -->
<input type="checkbox" v-model="toggle" />

<!-- `selected` é uma string "abc" quando a primeira opção for selecionada -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```

Mas às vezes podemos querer vincular o valor à uma propriedade dinâmica na atual instância ativa. Nós podemos utilizar `v-bind` para alcançar isso. Além disso, utilizando `v-bind` nos permite vincular o valor de um _input_ para valores que não são uma _string_ _(non-string values)_.

### Checkbox

```html
<input type="checkbox" v-model="toggle" true-value="yes" false-value="no" />
```

```js
// quando assinalado:
vm.toggle === 'yes'
// quando não assinalado:
vm.toggle === 'no'
```

:::tip Dica
Os atributos `true-value` e `false-value` não afetam o atributo `value` dos _inputs_, porque os browsers não incluem caixas de seleção não assinaladas nas submissões de formulários. Para garantir que um dos dois valores seja enviado em um formulário (p. ex. "sim" ou "não"), use _inputs_ do tipo _radio_.
:::

### Radio

```html
<input type="radio" v-model="pick" v-bind:value="a" />
```

```js
// quando assinalado:
vm.pick === vm.a
```

### Select

```html
<select v-model="selected">
  <!-- Objeto literal atribuído para demonstração -->
  <option :value="{ number: 123 }">123</option>
</select>
```

```js
//  quando está assinalado:
typeof vm.selected // => 'object'
vm.selected.number // => 123
```

## Modificadores

### `.lazy`

Por padrão, `v-model` sincroniza o elemento _input_ com os dados após cada evento `input` (exceto para o caso de composição IME [descrito anteriormente](#vmodel-ime-tip)). Você pode adicionar o modificador `lazy` para sincronizar depois do evento `change`:

```html
<!-- sincronizado depois do "change" ao invés de "input" -->
<input v-model.lazy="msg" />
```

### `.number`

Se você deseja que a entrada do usuário seja automaticamente tipificada como um Number, pode adicionar o modificador `number` ao `v-model` do elemento:

```html
<input v-model.number="age" type="number" />
```

Isto geralmente é útil, porque mesmo com `type="number"`, o valor do elemento HTML _input_ sempre retorna uma string. Se o valor não puder ser convertido com `parseFloat()`, então o valor original é retornado.

### `.trim`

Se você quiser que os espaços em branco excedentes de um _input_ sejam automaticamente removidos, é possível adicionar o modificador `trim` ao `v-model` do elemento:

```html
<input v-model.trim="msg" />
```

## `v-model` com Componentes

> Se você ainda não está familiarizado com os componentes Vue, pode pular isto por enquanto.

Os tipos de _input_ nativos do HTML nem sempre atendem as suas necessidades. Felizmente, os componentes Vue te permitem construir _inputs_ reutilizáveis com comportamento completamente costumizável. Estes componentes também funcionam com `v-model`! Para saber mais, leia sobre [_inputs_ customizados](./component-basics.html#using-v-model-on-components) no guia de Componentes.
