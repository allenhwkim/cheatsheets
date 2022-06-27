# Angular CheetSheet

## Angular forms.
* Template-driven forms
  * [(ngModel)] / mutable / validation with directives / simple + easy
  ```
  <input required minlength="4" [(ngModel)]="hero.name" #name="ngModel">
  {{ name.dirty }}
  {{ name.valid }}
  {{ name.errors.required }}
  {{ name.errors.minLength }}
  ```
  * classes
    * ng-valid
    * ng-invalid
    * ng-pending
    * ng-pristine
    * ng-dirty
    * ng-touched
    * ng-untouched

* Reactive Forms [example](https://stackblitz.com/edit/angular-ivy-6w7zoo)
  * [formControl], [formGroup], formControlName / immutable / validation with function / flexible

## Angular directive vs component.
* A component must have a template associated but a directive must not
* A DOM element can have only one component, but can have multiple directives
* A component is a directive with a template

## NgRx
* [example](https://stackblitz.com/edit/angular-ivy-s4tnk7)
* Actions (event object)
* Dispatcher (Command)
* Reducers (Observable Reactor)

## `<ng-container>`
A special element that can hold a structural directive without creating a DOM element E.g., 
```
<ng-container *ngIf=”condition; else templateB”>..</ng-container>
<ng-template #templateB>condition B</ng-template>
```
## Translate
* Ngx-translate
* TranslateService
* translate pipe. E.g. ‘Hello’ | translate
* translate directive e.g.,
 `<div [translate]=”Hello” [translateParams]="{value: 'world'}"></div>`
 
## Design Patterns
* Factory Pattern -> object. e.g. `ShapeFactory.getShape(shape)`
* Singleton Pattern -> single instance e.g. `new A() === new A()`
* Proxy Pattern -> (agent) -> real obeject
* Observer Pattern = Pub/Sub Pattern, Subject/Observer Pattern
* Adapter Pattern -> (bridge) -> read object e.g. media adapter
* Strategy Pattern(Policy Pattern) -> (algorithm) -> result. e.g. Ad. strategy

## SSL Handshake
* Client says hello (SYN)
* Server says hello (SYN ACK) with public key + certificate
* Client sends small data encrypted with public key
* Server says good / Client says good

## Data Structure
* Queue - LIFO
* Stack - FIFO
* Binary Tree
* Heap (BinaryTree data structure, max heap / min heap)
* Sets (TreeSet) - Keys in order without dupe.
* Map(TreeMap) - Keys / values in order without dupe - Dictionary
* HashTable - Keys in a hashed position with a value pointer, not-in-order
* Graph - node and edges(connections)

## Directives
### Structural Directives
* *ngFor 
* *ngIf
* *ngSwitch

## Component
### Template
* `[attr.foo]=”varFoo”`
* `[class.sale]=”isOnSale”`
* `[style.backgroundColor]=”myColor”`
```
  @Component({
    selector, 
    templateUrl, 
    styleUrls, 
    viewEncapsulation: (ShadowDom, Emulated, None), 
    changeDetection: ChangeDetectionStrategy.OnPush
  })
```

* Life Cycle
  * OnChanges(SimpleChanges)
  * OnInit
  * OnDestroy
  * AfterViewInit
  * AfterContentInit
  * DoCheck
  * AfterContentChecked
  * AfterViewChecked

* ViewChild
```
<app-countdown-timer #timer><app-countdown-timer> / timer.start(), timer.stop()
@ViewChild(TimerComponent) timer: TimerComponent / this.timer.start(), this.timer.stop()
```

* Dynamic Contents
```
<ng-template adHost></ng-template>
Class AdDirective {
  @ViewChild(AdDirective, {static: true}) adHost: AdDirective;
  constructor(vcr: ViewContainerRef) {}
  ngOnInit() {
    const vcr = this.adHost.viewContainerRef;
    const cr = vcr.createComponent(adComponent);
    cr.instance.data = ‘123’;
  }
}
```

## Router
* RouterModule.forRoot([{path, component}])
* `[routerLink]=”[‘/products’, product.id]”`
* ActivatedRoute
* Routes
  * `{path, component, canActivate: [MyGuard]}`
  * `{path, redirectTo, pathMatch}`
  * `{path, title, component, children: []}`
  * `{path:’**’, component: NotFoundComponent}`
* `this.router.navigate`
* `this.route.snapshot.paramMap.get(‘id’)`
* `[routerLink]=[‘/members’, member.id]`
* `routerLinkActive=”myClassName”`
* `<router-outlet></router-outlet>`
* `<router-outlet name=”popup”></router-outlet>`

### Resolve
```
{
	path: ‘/members’,
  component: MembersListComponent,’
	resolve: {
	  members: AllMembersResolveService
  }
}
```
### Route Guards
```
{
  path: 'admin',
  component: 'AdminComponent',
  canActivate: [AuthGuard],
  canDeactivate: [DoNotLeaveWithoutSaveGuard],
  children: [{
    path: '',
    canActivateChild: [AuthGuard],
    children: [...]
  }]
}
```

### Lazy Loading
```
{
  path: ‘admin’,
  loadChildern: import('./path/to/module').then(resp => resp.AdminModule),
  canLoad: [AuthGuard],
  data: {preload: true}
}
```

## Pipe
* date
* currency
* upperCase
* lowerCase
* percent
* decimal
* async
```
 <input (keyup)="search($event.target.value)" />

 <li *ngFor="let package of packages$ | async">
    <b>{{package.name}} v.{{package.version}}</b> -
    <i>{{package.description}}</i>
  </li>
 
 private searchText$ = new Subject<string>();
 search(packageName: string) {
   this.searchText$.next(packageName);
 }

 this.packages$ = this.searchText$.pipe(
    debounceTime(500),
    distinctUntilChanged(),
    switchMap(packageName =>
      this.searchService.search(packageName, this.withRefresh))
  );
}
```

## Services/Dependency Injection
* `@Injectable({providedIn: ‘root’})`
* `@Injectable({providedIn: UserModule})`
* `@ngModule({providers: [MyService]})`
* `@Component({providers:[MyServie]})`

### ngZone.runOutsideAngualr(() => …..)

## AOT / IVY
compile Angular html and typescript to DOM html and Javascript before downloading to browser. It provides faster rendering performance than JIT compile. It’s default from Angular9. Before Angular 9, JIT is default

Ivy is the code name for Angular's next-generation compilation and rendering pipeline (Starts from Angular9)
AOT compilation with Ivy is faster and should be used by default. In version 9, ivy is default

## Different Env.
```
src/environments/environment.ts
src/environments/environment.prod.ts
src/environments/environment.staging.ts

import { environment } from './../environments/environment';

$ vi angular.json
configurations: {
  production: {
    fileReplacements: [
      replace: “src/environments/environment.ts”,
      with: “src/environments/environments.prod.ts”,
    ]
  },
  staging: { . . .  }
},

$ ng build –configuration=production
```

### Observable 
* Is cancellable(unsubscribe, takeUntil, take)
* Can have multiple subscribers
* Lazily executed(until subscribe, it does not execute)
  ```
  myObservable.subscribe({
    next(num) { console.log('Next num: ' + num)},
    error(err) { console.log('Received an error: ' + err)},
    complete() { console.log('Completed'); }
  });
  ```

## Rxjs operators [example])(https://stackblitz.com/edit/angular-ivy-xzxbes)
For Angular applications, we prefer combining operators with pipes, rather than chaining.
Chaining is used in many RxJS examples. observables are named with a trailing "$" sign.
* map
* switchMap
* mergeMap
* filter
* tap
* take, takeUntil
* catchError
* retry


### Loading
* Eager loading is loading modules before application starts (sync. loading)
* Lazy loading is loading modules on demand (async loading)
* Preloading is loading modules in background just after application starts(async loading)
