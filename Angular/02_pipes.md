## Pipes
### What are Pipes in Angular ?
* Pipes are simple function in angular which accept an input value and returns a transformed value.
* **Pipes are of two types, pure pipe and impure pipe.**
* In general pipes are "pure function" which does not causes any side effect.

### Build in Pipes in Angular
* DatePipe: Formats a date value according to locale rules.
* UpperCasePipe: Transforms text to all upper case.
* LowerCasePipe: Transforms text to all lower case.
* CurrencyPipe: Transforms a number to a currency string, formatted according to locale rules.
* DecimalPipe: Transforms a number into a string with a decimal point, formatted according to locale rules.
* PercentPipe: Transforms a number to a percentage string, formatted according to locale rules.
* AsyncPipe: Subscribe and unsubscribe to an asynchronous source such as an observable.
* JsonPipe: Display a component object property to the screen as JSON for debugging.

### Example: Build-in pipe
```js
import {Component} from '@angular/core';
import { LowerCasePipe } from '@angular/common';

@Component({
  selector: 'app-root',
  template: `
    {{ username | lowercase}}
  `,
  standalone: true,
  imports: [LowerCasePipe],
})
export class AppComponent {
  username = 'ANGULAR';
}
```
Output - angular

### Example: Custom pipe

```js
// reverse.pipe.ts
import {Pipe, PipeTransform} from '@angular/core';

@Pipe({
    standalone: true,
    name: 'reverse'
})
export class ReversePipe implements PipeTransform {
  transform(value: string): string {
    let reverse = '';
    for (let i = value.length - 1; i >= 0; i--) {
        reverse += value[i];
    }
    return reverse;
  }
}
```

```js
// app.component.ts
import {Component} from '@angular/core';
import {ReversePipe} from './reverse.pipe';

@Component({
  selector: 'app-root',
  template: `
    Reverse Machine: {{ word | reverse }}
  `,
  standalone: true,
  imports: [ReversePipe],
})
export class AppComponent {
  word = 'You are a champion';
}

// Output - Reverse Machine: noipmahc a era uoY
```

