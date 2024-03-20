# SASS Quesions

1. What is SaaS ?  
   R: SaaS is a style pre-processor that adds new feature to CSS making creating styles easier

2. What is a style pre-processor ?  
   R: It is something that adds new features and syntax to CSS.

3. Does SaaS has two syntaxis ?  
   R: It has two syntaxis (.scss and .saas). The .scss syntax is more popular.

   - .scss -> It looks similar to regular css. It uses curley brackets
   - .saas -> It removes the brackets from the syntax.

## Variables

SASS allows you to create variables.

4. How to create a variable ?  
   R: They start with dollar sign, example: `$my-variable`: 32px;

## Nesting

5. What is nesting ?  
   R: It allows you to create classes inside other classes. Example:

   ```css
   .class {
     h1 {
       color: red;
     }
   }
   ```

   That would be translated into `.class h1 {...}`

## Partials

6. What are partials ?  
   R: A partial is a SaaS file that contains variables, mixins and other code snippets.

   The file name starts with `_`. And they can be bring into other SaaS files using `@use 'my-partial';`.

## Modules

7. What are modules ?  
   R: They allow you to modularize you SaaS code into multiple files. You can "import" them into other files using `@use 'header';`

   They can contain variables, class styles and other SaaS datatypes.

## Mixins

8. What are mixins ?  
   R: They are a reusable scope of css propertis that can be inserted into other class tags. They can receive parameters.

   You can include them into other classes using the `@include theme($theme: DarkRed)` keyword.

   ```css
   @mixin theme($theme: DarkGray) {
     background: $theme;
     box-shadow: 0 0 1px rgba($theme, 0.25);
     color: #fff;
   }

   .info {
     @include theme;
   }
   .alert {
     @include theme($theme: DarkRed);
   }
   ```

## Extend/Inheritance

9. What is inheritance ?  
   R: It allows you to insert the style properties from one class into another one.

   You can insert another class into another on using the `@extend` keyword.

   ```css
   %message-shared {
     border: 1px solid #ccc;
     padding: 10px;
     color: #333;
   }

   .success {
     @extend %message-shared;
     border-color: green;
   }
   ```

## Operators

10. What are operators ?  
    R: They allow you to perform operations like "sum, rest, division" inside saas files.

11. Give me an example in where they can be used ?  
    R: You can use them to substract certain quantity of width from a div.
