## Signals

### What are Signal ?
* Signals are a specific type of observable designed to optimize change detection for asynchronous data.
* There are two types of signals: Writable Signals and Computed Signals (read-only).

### How to write Signal in Angular ?
```
import { Component, signal } from '@angular/core';

@Component({
  standalone: true,
  selector: 'signals-example',
  template: `
    Counter Value: {{ counterSignal() }}
    <button (click)="updateCounter()">Click</button>
  `,
})
export class SignalsExampleComponent {
  counterSignal = signal(0);

  updateCounter() {
    this.counterSignal.set(this.counterSignal() + 1);
    // We can update signal value by using update also.
    // this.counterSignal.update((value) => value + 1);
  }
}
```

### What are Computed Signals ?
* Computed signals are derived from other signals.
* They allow you to create dynamic value based on existing signals.
* When a signal is updated, computed signal (which is deriving from that signal) is automatically recalculated.
* Unlike writable signals (which can be directly assigned values), computed signals cannot be assigned values directly.
* Computed signals are both lazily evaluated and memoized.
* doubleCount's derivation function does not run to calculate its value until the first time you read doubleCount. The calculated value is then cached, and if you read doubleCount again, it will return the cached value without recalculating.

```
import { Component, computed, signal } from '@angular/core';

@Component({
  standalone: true,
  selector: 'signals-example',
  template: `
    Counter Value: {{ counterSignal() }} <br />
    Double Counter Value: {{ doubleCounter() }} <br />
    <button (click)="updateCounter()">Click</button>
  `,
})
export class SignalsExampleComponent {
  counterSignal = signal(0);
  doubleCounter = computed(() => this.counterSignal() * 2);

  updateCounter() {
    this.counterSignal.set(this.counterSignal() + 1);
  }
}
```

### Output


https://github.com/piyush303/Frontend-Interview-Preparation/assets/20353112/b3864742-8730-40b2-b010-3db726fd4a4e




