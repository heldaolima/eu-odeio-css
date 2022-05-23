# CSS Layout
Agora a porra ficou séroa

# Overview
## **Normal flow**
This is how the browser lays out HTML pages when you do nothing to control page layout. Mas é comum que isso não seja suficiente. Os métodos capazes de mudar a forma como os elementos aparecem em css são:
- **The `display` property** - Valores-padrão (`block`, `inline`, `inline-block` etc) mudam o comportamento, transformam, por exemplo, um block-level em um inline-level. Aqui o Grid e o Flex funcionam, alterando o comportamento os child elements dentro de caixas-pai.
- **Float** - Applying a `float` value such as `left` can cause block-level elements to wrap along one side of an element, like the way images sometimes have text floating around them in magazine layouts.
- **The `position` property** - Allows you to precisely control the placement of boxes inside other boxes. Default is `static`, but you can fix elements in the top, for example.
- **Table layout**
- **Multi-column** - Can cause the content of a block element to layout in columns, like in a newspaper.

## The display property
Muda o display padrão dos elementos.

## Flexbox
Abreviação de Flexibile Box Layout, designed to make it easy for us to lay things out in one dimension - either as a row or as a column. Usa-se `display: flex` no pai dos elementos que a pessoa quer organizar. All its direct children then become *flex items*.

- O valor inicial da propriedade `flex-direction` é `row`. (eles vão se alinhar em uma linha, id est, as much columns as elements)
- O valor inicial da propriedade `align-items` é `stretch` -> the items stretch to the height of the flex container, which in this case is defined by the tallest item.
- Propriedades podem ser aplicadas aos flex-item. Se você definir a regra `flex: 1`, por exemplo, "this will cause all of the items to grow and fill the container, rather than leaving space at the end; if there is more space then the items will become wider; if there is less space they will become narrower.

## Grid Layout
Grid Layout is designed for two dimensions - lining things up in rows and columns.

- Usa-se `display: grid` and some row an columns *tracks* for the parent using `grid-template-row` and `grid-template-columns`, respectively.

// Ideia para o ForsendIC: Thalia queria que fossem três colunas, cada uma com um estado de formulário. Você cria 3 grids, cada um com uma coluna e n linhas, cada um representando um desses estados. A alternativa é fazer os cards.

- É possível ajustar o tamanho de um item, isto é, regular a track. Ele pode ocupar duas colunas, duas linhas, por exemplo. Isso se faz com as propriedades `grid-column` e `grid-row`.

## Floats
Floated elements in block level are moved to the left or right and removed from normal flow, and the surrounding content *floats* around it.

## Positioning techniques
- **Static positioning**: default. It means: "put the element into its normal position in the document layout flow - nothing special to see here."
- **Relative positioning**: Você pode mover o objeto em relação à sua posição no normal flow, e ele pode se sobrepor a outros.
- **Absolute positioning**: Remove o elemento completamente do normal flow, como se ele estivesse em uma camada separada. Lá você pode ajustar a posição "relative to the edges of its closest positioned ancestor".
- **Fixed positioning**: Similar ao absolute, só que aqui o elemento é fixado em relação ao viewport em vez de outro elemento. Isso ajuda a criar navbar que acompanham a página, por exemplo.
- **Sticky positioning**: O elemento age que nem em `position: static` "until it hits a defined offset from the viewport, at which point it acts like `position: fixed`.

# Normal flow
Starting with a solid, well-structured document that's readable in normal flow is the best way to begin any webpage. Dessa forma você trabalha *com* o documento, em vez de lutar *contra* ele.

## How are elements lid out by default?
It's just **box model**.

# Flexbox
- `display: flex`: multiple column layout with equal-sized columns, and the columns are all the same height.
    - The element we've given a `display: flex` rule is acting like a block-level element in terms of how it interacts with the rest of the page, but its children are laid out as flex items. 

## Columns or rows?
- The `flex-direction` property: directions the main axis runs (which direction the flexbox children are laid out in).
    - Default: `row` -> exibir em linha, n colunas
    - `column`: exibir em coluna, n linhas.

## Wrapping
Eventually your flexbox children will overflow their container, breaking the layout.

(No exemplo, há tantos artigos se espremendo em uma linha que eles vazam do container)
- `flex-wrap: wrap´: faz que cada linha contenha quantas flexbox children quanto possam. Any overflow is moved down to the next line. No final do doc, sobram duas caixas; o tamanho delas aumenta, pra que caibam na linha.

## flex-flow shorthand
Em vez de:

    {
        flex-direction: row;
        flex-wrap: wrap;
    }
Pode ser

    {
        flex-flow: row-wrap;
    }

## Flexible sizing of flex items
Controlar a proporção de espaço que os itens pegam em comparação aos outros.

Em um flex item fez:
    
    article {
        flex: 1;
    }

Isso quer dá a cada `article` o mesmo valor (1), então todos eles vão usar o mesmo espaço depois que as propriedades feito padding e margin são setadas.

## Horizontal and vertical alignment
You can use flexbox to align flex items along the main or cross axis.

`align-items` controls where the flex items sit on the cross axis (eixo y)
- `stretch`, wich streches all flex items to fill the parent in the direction of the cross axis. (default)
- `center`, causes the items to maintain their instrinsic dimensions, but be centered along the cross axis.

`justify-content` controls where the flex items sit on the main axis (eixo x)
- `flex-start`, makes all the items sit at the start of the main axis. (default)
- `flex-end`
- `center`: center of the main axis.
- `space-around`: distributes all the items evenly along the main axis with a bit of space left a either end.
- `space-between`: similar to space-around, but it doesn't leave any space at either end.

# Grids