# Angular-interview-Questions
### Q1: What is Routing Guard in Angular?  
Angular’s route guards are interfaces which can tell the router whether or not it should allow navigation to a requested route. They make this decision by looking for a true or false return value from a class which implements the given guard interface.
There are five different types of guards and each of them is called in a particular sequence. The router’s behavior is modified differently depending on which guard is used. The guards are:
- CanActivate
- CanActivateChild
- CanDeactivate
- CanLoad
- Resolve
```import { Injectable } from '@angular/core';
import { Router, CanActivate } from '@angular/router';
import { AuthService } from './auth.service';

@Injectable()
export class AuthGuardService implements CanActivate {
  constructor(public auth: AuthService, public router: Router) {}
  canActivate(): boolean {
    if (!this.auth.isAuthenticated()) {
      this.router.navigate(['login']);
      return false;
    }
    return true;
  }
}
```
### Q2: What is a Module, and what does it contain?  
An Angular __module__ is set of Angular basic building blocks like __component, directives, services__ etc. An app can have more than one module.
A module can be created using __@NgModule__ decorator.
```
@NgModule({
  imports:      [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```
### Q3: What's the difference between an Angular Component and Module?  
- __Components__ control views (html). They also communicate with other components and services to bring functionality to your app.
- __Modules__ consist of one or more components. They do not control any html. Your modules declare which components can be used by components belonging to other modules, which classes will be injected by the dependency injector and which component gets bootstrapped. Modules allow you to manage your components to bring modularity to your app.
### Q4: What is a Component? Why would you use it?  
__Components__ are the most basic building block of an UI in an Angular application. An Angular application is a tree of Angular components. Angular components are a subset of directives. Unlike directives, components always have a template and only one component can be instantiated per an element in a template.
A component must belong to an NgModule in order for it to be usable by another component or application. To specify that a component is a member of an NgModule, you should list it in the declarations field of that NgModule.
```
@Component({selector: 'greet', template: 'Hello {{name}}!'})
class Greet {
  name: string = 'World';
}
```
### Q5: What is a Service, and when will you use it?  
Angular __services__ are singleton objects which get instantiated only once during the lifetime of an application. They contain methods that maintain data throughout the life of an application, i.e. data does not get refreshed and is available all the time. The main objective of a service is to organize and share business logic, models, or data and functions with different components of an Angular application.
The separation of concerns is the main reason why Angular services came into existence. An Angular service is a stateless object and provides some very useful functions.
### Q6: What is the difference between @Component and @Directive in Angular?   
- __Directives__ add behaviour to an existing DOM element or an existing component instance.
- __A component__, rather than adding/modifying behaviour, actually creates its own view (hierarchy of DOM elements) with attached behaviour.
### Q7: How would you protect a component being activated through the router?  
The Angular router ships with a feature called guards. These provide us with ways to control the flow of our application. We can stop a user from visitng certain routes, stop a user from leaving routes, and more. The overall process for protecting Angular routes:
- Create a guard service: _ng g guard auth_
- Create _canActivate()_ or _canActivateChild()_ methods
- Use the guard when defining routes
```
// import the newly created AuthGuard
const routes: Routes = [
  {
    path: 'account',
    canActivate: [AuthGuard]
  }
];
```
Some other available guards:
- __CanActivate__: Check if a user has access
- __CanActivateChild__: Check if a user has access to any of the child routes
- __CanDeactivate__: Can a user leave a page? For example, they haven't finished editing a post
- __Resolve__: Grab data before the route is instantiated
- __CanLoad__: Check to see if we can load the routes assets
### Q8: What are Observables?  
__Observables__ are declarative which provide support for passing messages between publishers and subscribers in your application.
They are mainly used for event handling, asynchronous programming, and handling multiple values. In this case, you define a function for publishing values, but it is not executed until a consumer subscribes to it. The subscribed consumer then receives notifications until the function completes, or until they unsubscribe.
### Q9:  What is an Observer?  
__Observer__ is an interface for a consumer of push-based notifications delivered by an Observable.
### Q10: What is an Observable?  
An __Observable__ is a unique Object similar to a Promise that can help manage async code. Observables are not part of the JavaScript language so we need to rely on a popular Observable library called RxJS.
The observables are created using new keyword. Let see the simple example of observable,
```
import { Observable } from 'rxjs';

    const observable = new Observable(observer => {
      setTimeout(() => {
        observer.next('Hello from a Observable!');
      }, 2000);
    });
    ```
