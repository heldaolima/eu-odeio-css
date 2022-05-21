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