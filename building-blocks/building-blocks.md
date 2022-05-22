# CSS Building Blocks
Getting deeper

# Cascade and inheritance
## Conflicting rules
We have seen **cascade** and **specificity** concepts.

*Inheritance*: Some CSS properties by default inherit values set on the current element's parent element, and some don't. 

Tudo isso pode causar comportamento inesperado. A famosa encheção de saco que me faz desgostar de CSS.

### Inheritance
Some CSS property values set on parent elements are inherited by their child elements, and some aren't.

For example, if you set a `color` and `font-family` on an element, every element inside it will also be styled with that color and font, unless you've applied different color and font values directly to them.

Algumas propriedades não são herdadas: `width` por exemplo, graças a Deus.

## Understanding inheritance
### Controlling inheritance
Quatro valores universais de controle de herança. Toda propriedade os aceita.
- `inherit`: o valor da propriedade no elemento será o mesmo do seu pai. This "turns on inheritance"
- `initial`: o valor da propriedade será o valor inicial daquela propriedade. OBS: *initial value* é o valor default da propriedade.
- `revert`: o valor da propriedade é resetado para o default do **browser**.
- `revert-layer`: o valor será o estabelecido em uma *cascade layer* anterior.
- `unset`: reseta o valor ao natural, ou seja: se a propriedade é naturalmente herdada, ele age feito `inherit`; senão, `initial`.

### Understanding the cascade
Three factros to consider, listed here in order of importance.

1. **Source order**: as últimas regras no CSS vencem. The rule that is nearer th element itself overwrites the earlier ones until the last one wins and gets to style the element.
2. **Specificity**: Mais específicos vencem. Class > element. 

Prática comum: definir propriedades genéricas para os elementos e mudar os específicos através de classes. 

Níveis de especificidade:
1. Thousands: inline styles;
2. Hundreds: id;
3. Tens: class;
4. Ones: element.

## The effect of CSS location
### Order of overriding declaration
1. Declarations in user agent style sheets (browser);
2. Normal declarations in user style sheets (deifinidas pelo user)
3. Normal declaration in author style sheets (developer)
4. Important declarations in author style sheets
5. Important declarations in user style sheets

# Selectors
## Selector lists
Mais de um seletor com as mesmas regras:

    h1, special {
        color: blue;
    }

## Tipos de seletores
### Type, class, and ID
    h1 {}
    .box {}
    #unique {}
### Atribute selectors
    a[title] {}
    a[href="example.com"] {}
### Pseudo-classes and pseudo-elements
Lembrando que pseudoclasses contêm o *estado* atual do elemento
    
    a:hover {}
Pseudo-elemento é uma parte de um elemento, em vez do próprio.

    p::first-line {} 
    /*seleciona a primeira linha de um <p>, como se ela estivesse dentro de um <span>*/

### Combinators
Combine other selectors in order to target elements within our document. The following selects paragraph that are direct children of `<article` using the child operator: 
    
    article > p {}

# The box model
Everything in CSS has a box around it.
## Block and inline boxes
Como a caixa se comporta em termos de page flow e em relação às outras caixas na página. 

Boxes also have an **inner display** tipe and an **outer display type**. 
- Display type of `block`:
    - The box will break onto a new line;
    - The box will extend in the inline direction to fill the space avaliable in its container. In most cases this means that the box will become as wide as its container, filling up 100% of the space avaliable.
    - The `width` and `height` properties are respected.
    - Padding, margin and border will cause other elements to be pushed away from the box.

- Display type of `inline`:
    - The box will not break onto a new line.
    - The `width` and `height` properties will not apply.
    - Vertical padding, margins and borders will apply but will not cause other inline boxes to move away from the box.
    - Horizontal padding, margins and borders will apply and will cause other inline boxes to move away from the box.

## Aside: Inner and outer display types
De que forma a caixa se comporta no todo e de que forma os elementos se comportam dentro dela. `display: flex;`, por exemplo: dentro, os elementos são flex, mas a caixa que os envolve é block.

## What is the CSS box model?
O modelo define como as diferentes partes de uma caixa - margin, border, padding, and content - work together to create a box that you can see on a page.
### Parts of a box
- **Content box**: The area where your content is displayed, which can be sized using properties like `width` and `height`.
- **Padding box**: The padding sits around the content as white space; its size can be controlled using `padding` and related properties.
- **Border box**: The border box wraps the content and any padding. Use `border` to controll it.
- **Margin box**: The outermost layer, wraping the content, padding, and border as white space between this box and other elements. Use `border` to controll it.

#### Margin collapsing
If you have two elements whose margins touch, and both margins are positive, those margins will comibine to become one margin, ad its size will be equal to the largest individual margin. If one margin is negative, its value will be subtracted from the total. Where both are negative, the margins will collapse and the smallest value will be used.

## Using display: inline-block
Useful for situations where you do not want an item to break onto a new line, but do wnat it to respect `width` and `height` to avoid overlapping.
- The `width` and `height` properties are respected.
- padding, margin and border will cause other elements to be pushed away from the box.

But it does not break onto a new line, and will only become larger than its content if you explicitly add width and height properties.

# Overflowing content
- `overflow: hidden`: esconde o que houver de overflow. Então se o texto vazava pra fora de uma caixa, ele passa a ser escondido, como que se ela fosse um frame impermeável.
- `overflow: auto`: cria scrolls à medida que for necessário dentro daquela caixa, mas você pode controlar se quer só no eixo x ou só no eixo y.
- `overflow-wrap`: esse eu achei legal: ele adadpta o tamanho da caixa conforme o conteúdo. Num overflow, a caixa aumenta pra conter o conteúdo vazado. Ele também pode quebrar a palavra (`break-word`) pra caber na caixa.
 
# Values and units
Valores são especificados nas propriedades. Ex: `color: white`, 'white' é valor.
 
## Lenghts
Pode ser relativa ou absoluta. Vejamos os valores relativos, que parecem ser mais úteis:
- `em`: Font-size do pai, no caso de propriedades tipográficas feito `font-size`, e do font-size mesmo, em caso de `width`.
- `ex`: x-height of the element's font.
- `ch`: The advance measure (width) of the glyph "0" of the element's font.
- `rem`: Font size of the root element.
- `lh`: Line height of the element
- `vw`: 1% of the viewport's width
- `vh`: 1% of the viewport's height.
- `vmin`: 1% of the viewport's smaller dimension.
- `vmax`: % of the viewport's larger dimension.
 
### ems and rems
É bom entender as diferenças entre eles. 
 
**em unit means "my parent element's font-size"**. Se um elemento tem 1.3em, siginifica que ele tem 1.3 vezes o tamanho do pai. Então, se você for aninhando elementos e eles usam em, a fonte vai ficando maior quanto mais dentro eles estiverem, porque a multiplicação vai se sucedendo. 
 
**rem unit means "The root element's font-size"**. O tamanho do elemento virá da raiz `<html>` e não vai aumentar devido a aninhamentos. Você setou um tamanho fixo pra servir de referência;

### Percentages
Valores percentuais são relativos a outros valores. For example, if you set an element's `font-size` as a percentage, it will be a percentage of the `font-size` of the element's parent.

### Images
Image value type is used whenever an image is a valid value. This can be an actual imagine file pointed to via a `url()` function, or a grandient.

### Position
It represents a set of 2D coordinates, used to position an item such as a background image. It can take keywords: `top`, `left`, `bottom`, `right` and `center`.

### Strings
Exemplo: Specifying generated content.
    
    .box::after {
        content: "This is a string. I know because it is quoted in the CSS."
    }

# Sizing items
Alguns elementos têm tamanho natural, feito uma img. An empy `<div>`, on the other hand, has no sie of its own.

## Setting a specific size
This is called **extrinsic size**. You can give the element specific width and height values. Por causa do risco de overflow, é necessário ajustar cuidadosamente o tamanho usando lenghts ou percentagens.

## min- and max- sizes
- If you have a box that might contain a variable amount of content, and you always want it to be *at least* a certain height, you could set the `min-height` property on it. A caixa terá esse tamanho mínimo, mas crescerá em height à medida que mais conteúdo for adicionado a ela.
- A commmon use of `max-width` is to cause images to scale down if there is not enough space to display them at their instrinsic width making sure they don't become larger than that width.
