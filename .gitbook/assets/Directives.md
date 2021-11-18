## What is a directive

**An Angular directive is a function that executes whenever the Angular compiler finds it in the DOM.**

These functions extend the capability of html. Examples include styling based on conditions and being able to add/remove items from the DOM.

There are 3 types of directive:
1. **Components** — directives with a template.
2. **Structural** — change the DOM layout by adding and removing DOM elements.
3. **Attribute** — change the appearance or behaviour of an element, component, or another directive.

## Built in directives
Out of the box Angular provides some built in directives:

### Attribute

* **NgClass** — `ngClass` - adds and removes a set of CSS classes.
* **NgStyle** — `ngStyle` - adds and removes a set of HTML styles.
* **NgModel** — `ngModel` - adds two-way data binding to an HTML form element.

### Structural

* **NgIf** — `*ngIf` - conditionally creates or destroys subviews from the template.
* **NgFor** — `*ngFor` - repeat a node for each item in a list.
* **NgSwitch** — `*ngSwitch` - a set of directives that switch among alternative views.

## Components

Components are are directives with templates that encompass logic, template and styles into reusable blocks.

Using the `@Component` decorator on a class turns that class into a component. The decorator requires a configuration object as an argument. This object specifies the **selector**, **template** and **styles**.

A typical component structure would be:
- `**my-component**
  - **my-component.component.ts**
  - **my-component.component.html**
  - **my-component.scss**

### Selector

The selector for a component represents how Angular will know to load in the component in the template. For example the selector `'my-component'` will be used in the template as `<my-component></my-component>`.

### Template

The template can be provided as an inline string or as a reference to an external html file

### Styles

The styles can be provided as inline or as a reference to an external stylesheet such as css

