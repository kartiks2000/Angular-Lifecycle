# Angular-Lifecycle
Angular Lifecycle

Angular gives us 8 hooks to allow us to tap into the lifecycle of our components and trigger actions at specific points in the lifecycle.

This post discusses lifecycle hooks in Angular 2 and up.

Here are the lifecycle hooks available, in the order in which they are invoked:

ngOnChanges: Called every time a data-bound input property changes. It’s called a first time before the ngOnInit hook. The hook receives a SimpleChanges object that contains the previous and current values for the data-bound inputs properties. This hook gets called often, so it’s a good idea to limit the amount of processing it does.
ngOnInit: Called once upon initialization of the component.
ngDoCheck: Use this hook instead of ngOnChanges for changes that Angular doesn’t detect. It gets called at every change detection cycle, so keeping what it does to a minimum is important for performance.
ngAfterContentInit: Called after content is projected in the component.
ngAfterContentChecked: Called after the projected content is checked.
ngAfterViewInit: Called after a component’s view or child view is initialized.
ngAfterViewChecked: Called after a component’s view or child view is checked.
ngOnDestroy: Called once when the component is destroyed and a good hook to use to cleanup and unsubscribe from observables.
ngOnInit
Let’s give you a simple example using the ngOnInit hook. The ngOnInit lifecycle hook is probably the one you’ll use most often. If you have a lot of processing to do when the component gets created, it’s good practice to do it in the ngOnInit hook rather than in the constructor:

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit {
  constructor() {}

  ngOnInit() {
    this.setupData();
    this.doStuff();
    // ...
  }

  setupData() {
    // ...
  }

  doStuff() {
    // ...
  }
}
Notice how we import OnInit, but we implement it with the ngOnInit method. It’s the same principle for the other lifecycle hooks.

Multiple Lifecycle hooks
Implementing multiple hooks is just as easy:

import { Component, OnInit, OnDestroy } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit, OnDestroy {
  constructor() {}

  ngOnInit() {
    console.log('Component Init');
  }

  ngOnDestroy() {
    console.log('Component Destroy');
  }
}
ngOnChanges
The ngOnChanges hook, with it’s SimpleChanges object, is a little different. Here’s how you would implement it. Let’s say we have a component used like this:

<my-todo [title]="title" [content]="content"></my-todo>
Now say that we want to do something when the title property changes:

Child Component: my-todo.component.ts
import { Component, Input, SimpleChanges, OnChanges }
  from '@angular/core';

@Component({
  // ...
})
export class MyTodoComponent implements OnChanges {
  @Input() title: string;
  @Input() content: string;
  constructor() { }
