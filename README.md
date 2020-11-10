![](https://spacein.co.uk/images/logo.svg)
# :notebook: CSS Guidebook

To develop **SASS** with **SCSS** syntax and **BEM Methodology** is used.

## BEM Methodology

The Block, Element, Modifier methodology (commonly referred to as BEM) is a popular naming convention for classes in HTML and CSS. Developed by the team at Yandex, its goal is to help developers better understand the relationship between the HTML and CSS in a given project.

Here’s an example of what a CSS developer writing in the BEM style might write:
```
/* Block component */
.btn {}

/* Element that depends upon the block */ 
.btn__price {}

/* Modifier that changes the style of the block */
.btn--orange {} 
.btn--big {}
```
More info [here](https://en.bem.info/methodology/quick-start/) and [here](https://css-tricks.com/bem-101/) 

## CSS Preprocessors
CSS preprocessors are easly described as css with super powers :). It compiles the code into readble css files on build time which helps the development and keep goo dstadards for the team.


More about it [here](https://sass-lang.com/)

#### SASS vs SCSS
What is de difference between **SASS** and **SCSS**?
Once of the mains diferences are that SASS is used when we need a original syntax, code syntax is not required for SCSS. SASS follows strict indentation, SCSS has no strict indentation. SASS has a loose syntax with white space and no semicolons, the SCSS resembles more to CSS style and use of semicolons and braces are mandatory.

### Variables

Variables in SCSS works the same as in javascript, they can store value which can be passed on to your stylesheets to use.
A variable is initialized like:
```
$variable: 1px;
```
and called in your `.scss` files like:
```
border-width: $variable;
```

### Functions

Functions allow you to define complex operations on SASS values that you can re-use throughout your stylesheet. They make it easy to abstract out common formulas and behaviors in a readable way.

A function that returns a value based on a argument
```
@function notification-user-icon-border($value){
    @if $value == 'px' {
        @return 3px;
    } @else {
        @return 0.19rem;
    }
}
```
and use it 
```
padding-left: 0.8rem + 0.9rem + ($notification-user-icon-size + (notification-user-icon-border('rem') * 2));
```

### Mixin

Mixins allow you to define styles that can be re-used throughout your stylesheet. They make it easy to avoid using non-semantic classes like .float-left, and to distribute collections of styles in libraries.

Lets define a shape. For it we need width and height
```
// mixin to reset a property and it's value
@mixin reset-property($prop,$value) {
  #{$property}:$value
}

// mixin to create a new shape 
@mixin shape($width,$height) {
    // set it's inital width and height to 0
    @include reset-property(width,0);
    @include reset-property(height,0);
    // set new width and height
    width:$width;
    height:$height;
}
```
and call it like
```
.square{
    @include shape(20px, 20px);
}
```

### Concatenation / &(The Sass Ampersand)

The & is an extremely useful feature in Sass (and Less). It’s used when nesting. It can be a nice time-saver when you know how to use it, or a bit of a time-waster when you’re struggling and could have written the same code in regular CSS. 
It is easier to class names, class depenedcies and construct class names that derive from a parent class.

```
<div class="user-icon">
    <div class="user-name initials">
    </div>
</div>
```

```
.user-icon {
    border-radius:50%;
    border:1px solid red;
    &-name{
    text-transform:uppercase;
     & .initials {
        background: white;
        height: 100%;
        width: 100%;
        text-align: center;
        align-content: center;
      }
    }
     
  }

  
```

### How to createa and use scss file inside Vue component

To use scss inside a Vue component the `<style>` node has to be have `lang="scss"` attribute.
```
<style lang="scss" scoped>
</style>
```

To call a `.scss` file you need to import it inside the `<style>`
```
<style lang="scss">
@import '~@/scss/components/user_icon.scss';
</style>
```

## Project Structure

The project structure changes with the integration of SCSS. As all of the css inside each components has been moved into it's own `.scss` coresponding file inside a new folder called `scss` in the `.src`.
The `scss/` folder copys the folder structure of the Vue components.

#### Structure description

- `.scss/` folder - holds all the sass files 
- `./scss/components/` - holds all the Vue components sass files
- `./scss/pages/` - holds all the Vue pages components sass files
- `./scss/_colors.scss` - holds all the color variables which is injected into `variables.scss` file
- `./scss/variables.scss` - holds all the variables
- `./scss/functions.scss` - holds all the functions
- `./scss/mixins.scss` - holds all the mixin declarations
- `./scss/main.scss` - imports mixin, function and variables `.scss` files. this is the root file that gets imported in each components upon build.

![](https://raw.githubusercontent.com/victormccglc/CSSHandbook/main/project-structure.PNG)
