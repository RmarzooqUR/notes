# Components
- components are defined by passing params like `selector, templates, style, templatesUrl, styleUrl` to the  `@Component` decorator before a class based component the dev declares
- the UI **presentation** is determined by html template passed to the decorator.
- the component behavior like *state mgmt, data fetch, event handling* is performed inside the component
```ts
@Component({
    selector: 'my-component',
    templates: `<li>My Data<\li>`,
    styles: `li { color: blue }`
})
export class MyComponent {
}
```
- a child Component can be used in a parent as follows
```ts
import { MyComponent } from 'my-component/index.ts'

@Component({
    selector: 'parent-component',
    templates: `
        <ul>
            <my-component></my-component>   // selector text is used.
        </ul>
    `
})
export class ParentComponent {}
```

# State & its management
class attributes are state, & the methods that modify them using `this` manage said state.

### Dynamic Rendering/Properties/Attributes
- some data in template may be dynamic, render using state with `{{}}` inside template
- some html properties may be required dynamically, use in template as `[prop]="dynamicAttrState"`
- dynamic val of custom attributes like `data-`, `aria-` can also be set, using `[attr.dynamic-attr] = "customAttrState"`
```ts
@Component({
    selector: 'my-component',
    template: `
        <li> Static content {{ dynamicContent }}</li>
        <button [disabled]="dynamicAttrState" />
        <button [attr.data-custom-attr]="customAttrState" />
    `
})
export class MyComponent {
    dynamicContent = "This is rendered dynamically"
    dynamicAttrState = false
    customAttrState = "custom-val"
}
```

# Conditional/loop Rendering
Angular template language provides `@if, @else, @for` blocks.
```ts
@Component({
    ...,
    templates: `
        @if (state1) {
            <html />
        } @else {
            <html /> 
        }
        @for ( item of listItems ; track item.id ) {
            <li>{{item.name}} - {{item.cost}} </li>
        }
    `
})
```

# Event handling
- event handlers are written inside template html tags with `()`
```html
<button (click)="compnentEventHnndler($event)"></button>
```
- `$event` object can be used by the handler defined inside component if required
    - not required to pass to handler
- `(keyup), (keydown), `

# Services
this is basically a way to share common code (i.e. Dependency Injection)
- we can create services using `@Injectable` directive
```ts
@Injectable({providedIn: 'root'})
export class FindingService {
    found(a: number[], b: number) {
        return a.findIndex(b);
    }
}
```
```ts
import { FindingService } from 'destination.ts'

@Component({
    templates: `
        <p> {{ toFind }} is 
            @if (render){
                available
            } @else {
                not available 
            }
        </p>
    `
})
export class Mycomopnent{
    findingService = inject(FindingService)
    a = []
    toFind = '2'
    render = this.findingService.found(a, this.toFind)
}
```