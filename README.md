## Directive’s Isolate Scope: “=” and “@”
### Isolate Scope
```
function MyDirective(){
    var ddo = {
        scope: {},
        ...
    };
    return ddo;
};
```
`scope: {}` - signals isolate scope: parent scope is NOT inherited

### Bidirectional Property Binding
#### --- 1 ---
```
function MyDirective(){
    var ddo = {
        scope: {
            myProp: '=attributeName'
        },
        ...
    };
    return ddo;
};
```
`myProp` - local scope property
`'=attributeName'` - HTML template attribute name (`=` is Bidirectional Binding)
#### --- 2 ---

```
function MyDirective(){
    var ddo = {
        scope: {
            myProp: '='
        },
        ...
    };
    return ddo;
};
```
`myProp: '='` - assumes the attribute is named the same as property name: my-prop

#### --- 3 ---
```
function MyDirective(){
    var ddo = {
        scope: {
            myProp: '=?'
        },
        ...
    };
    return ddo;
};
```
`myProp: '=?'` - signifies that the attribute is optional

#### Bidirectional Property Binding (HTML)
`<my-directive my-prop="outerProp"></my-directive>`

`my-prop` - attributes follow the same camelCase normalization (my-prop => myProp)

### DOM Attribute Property Binding
```
function MyDirective(){
    var ddo = {
        scope: {
            myProp: '@myAttribute'
        },
        ...
    };
    return ddo;
};
```
`'@myAttribute'` - binds myProp to the value of DOM attribute my-attribute
#### DOM Attribute Property Binding (HTML)
`<my-directive my-attribute="{{outerProp}}"></my-directive>`

`my-attribute` - as the value of outerprop changes, so does the value of my-attribute and so does the value of myProp inside the directive

We can do the regular interpolation inside of the my-attribute:

`<my-directive my-attribute="Hi {{outerProp + '!'}}"></my-directive>`
***
##### _Summary_
* Having isolate scope on the directive
    * breaks the prototypal inheritance of the scope from the parent;
    * makes the directive more independent, less coupled with the controller.
* We pass values into the derective using scope bindings.
* Bidirectional binding ('=') is such that directive scope property change affects the bound property and visa versa.
* DOM attribute value binding ('@') always results in directive property being a string.
    * Changes to DOM attribute value are propogated to the directive property, but not the other way around. 
***
