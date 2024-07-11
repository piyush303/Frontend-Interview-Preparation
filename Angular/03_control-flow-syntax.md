## Control Flow Syntax

* Prior to Angular 17 we used to use `*ngIf`, `*ngFor` and `ngSwitch` structural directives.
* Angular 17 introduced new control flow syntax which are `@if`, `@for`, @switch.

### `@if` block
* Conditionally display content.

```
@if (a > b) {
  {{a}} is greater than {{b}}
}
```

```
@if (a > b) {
  {{a}} is greater than {{b}}
} @else if (b > a) {
  {{a}} is less than {{b}}
} @else {
  {{a}} is equal to {{b}}
}
```

### `@for` block
* Repeatedly renders the content for each item in collection.

```
@for (item of items; track item.id) {
  {{ item.name }}
}
```

* while using `@for` block if there are no items in collection we can use `@empty` block to render empty data message.
```
@for (item of items;) {
  <li> {{ item.name }}</li>
} @empty {
  <li> There are no items.</li>
}
```

* While using `@for` block if items in collection are updated all items will be updated on DOM, even if their value is not changed.
* This can impact performace of the application. To prevent this we can use `track` expression. 
* While using `track` we have to mention unique property, which will be used by Angular to determine which items are updated only.
* Then Angular updates DOM only for those items which has updated value and not for those whose value didn't change.

```
@for (item of items; track item.id;) {
  Item #{{ idx }}: {{ item.name }}
}
```

### `@switch` block
* Angular's `@switch` is similar to Javascript's `switch` statement.

```
@switch (condition) {
  @case (caseA) {
    Case A.
  }
  @case (caseB) {
    Case B.
  }
  @default {
    Default case.
  }
}
```
