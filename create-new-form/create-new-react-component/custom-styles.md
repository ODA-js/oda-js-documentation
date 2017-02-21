#Custom styles

Use `import 'path/to/file_of_style.scss'` to add custom styles to the component.

If you want to use your own styles in your component: 
* Create `style` folder in the folder of your component. 
* Create in the `style` folder the files: 

**index.scss**
```
[dir=ltr] {
    @import "style";
}
``` 
**index.rtl.scss** - styles for the left direction of the text
```
[dir=rtl] {
    @import "style";
}
``` 
* Create **style.scss** file with custom styles of your component.

You can use React inline styles, too. See more: https://facebook.github.io/react/docs/dom-elements.html#style