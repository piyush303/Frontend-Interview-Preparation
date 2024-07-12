## Dependency Injection (DI)
### What is Dependency Injection ?
* It is a design pattern and mechanism for creating and delivering some parts of an application to other parts of an application that require them.
* For example, you may need an HTTP service to make backend calls.
* Angular facilitates the interaction between dependency consumers and dependency providers using an abstraction called Injector. When a dependency is requested, the injector checks its registry to see if there is an instance already available there. If not, a new instance is created and stored in the registry. Angular creates an application-wide injector (also known as the "root" injector) during the application bootstrap process. In most cases you don't need to manually create injectors, but you should know that there is a layer that connects providers and consumers.


### How to provide a dependency ?
* Consider we have a `UsersService` service which will act as a dependency for a component.
* Fist step is to add `@Injectable` decorator which tell angular that this class can be injected.

```
@Injectable()
class UserService {}
```
* Now we have to make it available to DI by providing it.
* There are multiple ways to provide dependency, which are given below.
  <ol></ol>
  1. Preferred: At application root level by using `providedIn`. <br/>
  2. At component level.<br/>
  3. At application root level using `ApplicationConfig`.<br/>
  4. Using `NgModule`.<br/>
 
  #### 1. Preferred: At application root level by using `providedIn`
  * This allows injecting service into all other classes.
  * This enables Angular to optimize and efficiently remove services that are unused (tree-shaking).
  * When using this Angular create **single instance** of service and inject that same instance into every class who asks for it. <br/>

  ```
  @Injectable({
    providedIn: 'root'
  })
  class UserService {}
  ```
  #### 2. At component level
  * In this case service becomes available to all instances of this component and other components and directives used in the template.
  * Tree shaking does not work in this scenario.
 
  ```
  @Component({
    standalone: true,
    selector: 'user-details',
    template: '...',
    providers: [UserService]
  })
  class UserDetailsComponent {}
  ```

  #### 3. At application root level using `ApplicationConfig`
  * In this scenario service is available to all components, directives, and pipes.
    

  ```
  export const appConfig: ApplicationConfig = {
    providers: [
      { provide: UserService },
    ]
  };
  ```

  ```
  // main.ts
  bootstrapApplication(AppComponent, appConfig)
  ```

  #### 4. Using `NgModule`
  * A service provided in a module is available to all declarations of the module, or to any other modules which share the same ModuleInjector.

### Consuming a Dependency
* There are two ways to consume a dependency, which are given below.

```
@Component({ … })
class UserDetailComponent {
  constructor(private service: UserService) {}
}
```

```
@Component({ … })
class UserDetailComponent {
  private service = inject(UserService);
}
```
