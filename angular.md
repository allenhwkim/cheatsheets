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

### ngZone.runOutsideAngualr(() => …..)






