# Eu odeio CSS e vou aprender essa bosta

Obs: é provável que essas notas só façam sentido para aquele que as escreveu.

# The basics
        selector {
            property: value; /* this is a rule */
        }

So there are modules. That set of properties for the same element, I guess.

## Terminologia e seleção básica

### Uso de tags e classes
    li.special {
        color: orange;
        font-weight: bol
    }
    /* Isso faz que apenas aos elementos <li> sejam aplicados as regras da classe 'special' */

### Descendant combinator
    li em {
        color: rebeccapurple;
    }
    /* Aqui o seletor vai atrás dos <em> que existam dentro de uma <li>, apenas*/

### Adjacent sibling combinator
    h1 + p {
        font-size: 200%;
    }
    /* Estiliza o <p> quando ele vem diretamente depois de um <h1>, no mesmo nível de hierarquia do HTML*/

### Estilizar baseado no estado
    a:link {
        color: pink;
    }
    a:visited {
        color: green;
    }
    a:hover {
        text-decoration: none;
    }
    /*Já é uma boa forma de distinguir o : do :: no CSS. Dois pontos diz respeito ao estado do elemento*/

### Combinando seletores
    /* selects any <span> that is inside a <p>, which is inside an <article>  */
        article p span { ... }

    body h1 + p .special {
        color: yellow;
        background-color: black;
        padding: 5px;
    }
    /*Seleciona elementos da classe .special que estejam dentro de um <p> que venha após um <h1>, o qual está dentro do <body> */

# How CSS is structured
Sobre inline, external etc não preciso ver.

### Specifity
Imagine a seguinte configuração CSS e HTML

    .special {
    color: red;
    }

    p {
    color: blue;
    }
    ---------------------
    <p class="special">What color am I?</p>

`.special` e `<p>` sendo modificados. Qual será a cor do `<p>` no html?

*Cascade rule*: Later styles replace conflicting styles that appear earlier in the stylesheet. Thus:

    p {
        color: red;
    }

    p {
        color: blue;
    }

O parágrafo será da cor azul, porque a última declaração prevalece.

*Specifity*: No primeiro exemplo, a **classe** prevalece e o parágrafo será vermelho. Isso porque a classe é mais *específica*, tem mais *especificidade* do que o seletor simples. 

### Functions
`calc()`: simple math

Exemplo:

    .box{
        padding: 10px;
        width: calc(90% - 30px);
        ...
    }

Funções boas pra ficar de olho: as que servem de valor pra propriedadae [transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform).

### @rules
Provide instruction for what CSS should perform or how it should behave.

`@import`

`@media`

# How CSS works
## In the browser

1. The browser loads the HTML
2. HTML -> DOM
3. Fetches links, including CSS
4. Aplies CSS through selector types

## About the DOM
Tree-like structure. Each element, attribute and piece of text in the markup language becomes a DOM node in the tree substructure. Nodes are defined by their relationship to other DOM nodes. Some elements are parents of child nodes, and child nodes have siblings.

    <p>
        Let's use:
        <span>Cascading</span>
        <span>Style</span>
        <span>Sheets</span>
    </p>

DOM:

    P
    ├─ "Let's use:"
    ├─ SPAN
    |  └─ "Cascading"
    ├─ SPAN
    |  └─ "Style"
    └─ SPAN
        └─ "Sheets"

## Assessment
Tasks:
1. Make the level one heading pink, using the CSS color keyword hotpink.
2. Give the heading a 10px dotted border-bottom which uses the CSS color keyword purple.
3. Make the level 2 heading italic.
4. Give the ul used for the contact details a background-color of #eeeeee, and a 5px solid purple border. Use some padding to push the content away from the border.
5. Make the links green on hover.