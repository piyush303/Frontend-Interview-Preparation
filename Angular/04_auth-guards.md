## Auth Guards

### What is Auth Guard ?
* Auth Guard is a technique which is used to protect our routes based on user authetication status.
* Whenever a user navigates to specific route, auth guards validates that whether that user is authenticated and authorized to access that route.
* If user is authenticated it redirects user to requested route else it redirect user to fallback routes which is generally not-authorized or login route.

### Types of Auth Guard

#### `CanActivate` Auth Guard
* If user is authenticated to naviagte to requested route it return boolean (true/false) value or an observable/promise that resolves to boolean.
* If user is not authenticated, it returns false and then user will be redirected to fallback route (e.g. login).

#### `CanActivateChild` Auth Guard
* This guard works same as `CanActivate` but this is specifically used to protect child route of a particular route.
* When we have nested routes and we need to protect all nested route based on some criteria then we use this route guard.

#### `CanDeactivate` Auth Guard
* This guard validates that whether a user is allowed to leave a particular route.
* It prompts a confirmation to user if user is leaving a route with unsaved changes or to perform other checks.

#### `CanLoad` Auth Guard
* This guard prevents module to load if user is not authenticated.

### Note - Most asked interview question
#### What is the difference between `CanActivate` and `CanLoad` Guards ?
* CanActivate is used to prevent unauthorized users to access routes.
* CanLoad is used to prevent loading module is user is not authorized. (In this scenario entire module will not load untill user is autheticaed, this improves performance)


### Example
```js
import { Injectable } from "@angular/core";
import { Router } from "@angular/router";
import { AuthService } from "../services/auth.service";

@Injectable({
  providedIn: 'root'
})
export class AuthGuard {
  constructor(private authService: AuthService, private router: Router) {}

  canActivate(): boolean {
    if (this.authService.isAuthenticated()) {
      return true;
    } else {
      this.router.navigate(['/login']);
      return false;
    }
  }
}
```

```js
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { ProductsComponent } from './products/products.component';
import { LoginComponent } from './components/login/login.component';
import { RegisterComponent } from './components/register/register.component';
import { AuthGuard } from './shared/AuthGuard';

const routes: Routes = [
  { path : "products",component : ProductsComponent,
    canActivate: [AuthGuard] 
  },
  { path: "login",component : LoginComponent },
  { path: "register",component : RegisterComponent },
  { path: "",redirectTo: "products", pathMatch: "full" }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```
