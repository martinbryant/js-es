# Javascript - ES5 and beyond

Javascript ES5(ECMAscript 5) was released in December 2009, which was 10 years after the previous version, ES3.

## ES6/ES2015

This version was released in June 2015, hence the name ES2015. It was decided that the names for the different version will now coincide with the year of release to make it easier to understand.... maybe.

## ES5 vs ES2015

So now I will go through the major changes between the different versions.

### let and const

In ES5, variables were declared using the `var` keyword. ES2015 saw the introduction of `const` and `let` keywords

```markdown
const highlyMotivated = 'HIGHLY_MOTIVATED'
```

The `const` keyword will not be hoisted and cannot reassigned or redeclared.

```markdown
let highlyMotivated = 'HIGHLY_MOTIVATED'
```

The `let` keyword will not be hoisted, cannot be redeclared but can be reassigned.

````markdown
it('return initial state', () => {
const expected = {}
const action = {
type: 'init'
}
const callReducer = reducer.favouriteBeers(undefined, action)
expect(callReducer).toEqual(expected)
})
```

### Arrow Functions

### Object/Array Spread

### Object/Array Rest

```markdown
var moveToLondon = function(){
getAllThings()
}
```
````

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/martinbryant/js-es/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
