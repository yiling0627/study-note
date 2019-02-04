#<font color="#0099ff" face="黑体">Angular.js 2</font>
>CLI

		The Angular CLI is a tool to initialize, 
		develop, scaffold and maintain Angular 
		applications
		it can running the unit test both with the
		end to end tests.
		ng new 
		ng serve
		ng test
		ng e2e
		ng g c + name :convenient to add component
		               automatically add html/css/
		               ts/ and component
		               app.module
		ng g c xxx/name : inside xxx folder
		ng g c name --spec false : not include the 
						test ts file 
		exit server  ctrl+C
		
		deployment:
		ng build --prod --aot
		
>bootstrap

	add bootstrap to the root of the application
	1.npm install --save bootstrap
	2.open angular-cli.json find styles:[]
	3."styles":[
		"../node_modules/bootstrap/dist/css/bootstrap.min.css",
	   ]
	
		
>TypeScript

	TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. Any browser. Any 
	host. Any OS. Open source.

	interface Person {
  		readonly id: number;
  		name: string;
  		age?: number;
  		[propName: string]: any;
	}

	let xcatliu: Person = {
  		id: 89757,
  		name: 'Xcat Liu',
  		website: 'http://xcatliu.com',
	};

#<font color="red">Angular2</font>

	in terminal, type ng genarate component name
	(ng g c name) to create an component folder
	with all the files we need.

	Component selector
	@component({
		//selector:'[app-server]',
		//selector:'.app-server',
		selector:'app-server',
		templateUrls:'',
		styleUrls:['']
	})
	
	
>##data-binding

	Data binding in AngularJS is the 
	synchronization between the model and the view.
	like a communication between the HTML template 
	and database.
	
	Two way data-binding:
	When data in the model changes, the view 
	reflects the change, and when data in the view 
	changes, the model is updated as well. This 
	happens immediately and automatically, which 
	makes sure that the model and the view is 
	updated at all times.
	
	
	Property-binding:
	<button class="btn btn-primary" [disabled] = 
	"XXX">
	----------------------------------------------
	export class sss {
		XXX
		function
	}
	
	Event-binding:
	<button class="btn btn-primary" (click)="A()">
	----------------------------------------------
	export class sss {
		XXX
		function A
	}

>###<font color="blue">difference between * and []</font> 

	* structure directive, means the directive
	  change the DOM
	[] not change the DOM, but like change the
	   property or the attributes.
	
>ng-if

	<p *ngIf="check; else nocheck">sdsd</p>
	<ng-template #nocheck>
		<p>dsdsdsd</p>
	</ng-template>
	
>ng-style

	export class sss{
		getColor(){}
	}
	----------------------------------------------
	<p [ngStyle]="{background-color:getColor()}">
	</p>
	
>ng-class

	@component({
		selector:'app-server',
		templateUrls:'',
		styles:[`
			.classname:xxxxx;
		`]
	})
	----------------------------------------------
	<p [ngClass]="{classname: condition}">
	</p>


>ng-for

	<a *ngFor='let ingredient of ingredients'></a>
	----------------------------------------------
	export class ShoppingListComponent{
  		ingredients:Ingredient[] = [
    		new Ingredient('Apples',5),
    		new Ingredient('Tomatoes',10)
  		];
  		constructor() { }
	}
	
>ng-model

	For two way data-binding:
	 <input type="text" class="form-
	 control" [(ngModel)]="newServerName">
	 --------------------------------------------
	 export class CockpitComponent{
	 	newServerName = '';
	 }

>ng-content

	app.component.html:
	
	 <app-server-element
        *ngFor="let serverElement of serverElements"
        [element] = 'serverElement'
      >
        <p>
          <strong *ngIf="serverElement.type === 'server'" style="color: red">{{ serverElement.content }}</strong>
          <em *ngIf="serverElement.type === 'blueprint'">{{ serverElement.content }}</em>
        </p>
      </app-server-element>	
      ------------------------------------------
      server-element.component.html:
      
      <ng-content></ng-content>    

	
#<font color='red'>Components & Data Binding</font>

Component 的参数只能在当前的Component Scope 使用（parent 和 child 都不行）	

	例如： Component A
		  在 A 的.ts文件中定义参数，例如数组
		  在 A 的.html文件中使用
		  
如果要想parent 使用 child 的参数或属性
input can put the parameters into global

	child:
	import { Input } from '@angular/core'
	export class A{
		@Input('alias name') element:{a:string, b:number, c:string}
	}
 	----------------------------------------
 	parent:
 	<app-a 
 	*ngFor='let serverElement of serverElements'
 	[element]='serverElement'
 	或者[alias name] = 'serverElement'
 	></app-a>
 	此处 把子类element的类型定义传给了serverElement
 	
 	
>Event-Emitter

	父类和子类之间事件绑定
	binding event
	passing the data from child to parent
	
	export class CockpitComponent{
		@Output() serverCreated = new 
		EventEmitter<{serverName:string, 
		serverContent:string}>();
		
		onAddServer() {
    		this.serverCreated.emit({
      		serverName: this.newServerName,
      		serverContent:this.newServerContent
    		});
  		}
	}
	-----------------------------------------------
	export class AppComponent {
	  	 serverElements = [{type:'server',name:'server-1',content:'this is test'}];
		 onServerAdded(serverData:{serverName:string, 
		 serverContent:string}) {
	    	this.serverElements.push({
	      		type: 'server',
	      		name: serverData.serverName,
	      		content: serverData.serverContent
	    	});
	  	}
	}
	-----------------------------------------------
	<app-cockpit
		(serverCreated)="onServerAdded($event)"
	></app-cockpit>


>##<font color='red'>@Input and @Output</font>

	@Input:
	it has the ability to make your property 
	bindable from outside, from the parent 
	component using input.
	@Output:
	allow parent component using output to listen
	to your own events which you carried with
	Event-Emitter. 
	
>View Encapsulation(none,native,emulated(default))

	by default, the css style will just effect
	its own componet, but when we set
	ViewEncapsulation to none. it will effecting
	other components.
	
>Local reference

	can be only used in the current HTML template
	
	<input type="text" class="form-control"
      #serverNameInput>
    <button
      class="btn btn-primary"
      (click)="onAddServer(serverNameInput)">
      Add Server
    </button>
    ---------------------------------------------
    export class xxxxx {
    	  onAddServer(nameInput:HTMLInputElement) {
    		this.serverCreated.emit({
      			serverName: nameInput.value,
      			serverContent:this.newServerContent
    	   });
  		  }
    }
	
<font color="blue">@ViewChild('serverNameInput') serverNameInput:ElementRef;
Don't need to pass the element to menthod</font>

	<input type="text" class="form-control"
      #serverNameInput>
    <button
      class="btn btn-primary"
      (click)="onAddServer(serverNameInput)">
      Add Server
    </button>
    ---------------------------------------------
    export class xxxxx {
    	@ViewChild('serverNameInput') serverNameInput:ElementRef;
    	  onAddServer() {
    		this.serverCreated.emit({
    		serverName:this.serverNameInput
    		.nativeElement.value	
    	   });
  		  }
    }	
    
   @ContentChild('serverNameInput') serverNameInput:ElementRef;
   
 	
 <font color="darkyellow" size="5">Lifecycle</font>
 
 	Hooks as following:
 	
 	ngOnChanges: called after a bound input
 	             property changes
 	ngOnInit: called once the component is
 	          initialized
 	ngDoCheck: called during every change detection
 				 run
 	ngAfterContentInit: called after(ng-content)
 				has been projected into view
 	ngAfterViewInit: called after the component's
 				view(and child views) has been
 				initialized
 	ngAfterViewCheck: called every time the view
 				(and the child view) has been checked
 	ngOnDestroy: called once the component is 
 				about to be destroyed
 				
 	
 	
##<font color="red">Directives</font>
>Attribute Directives
	
	1.Look like a normal HTML Attribute
	2.only change the element they are added to
	
>Structural Directives
	
	1.Look like a normal HTML Attribute but have a 
	  leading *
	2.Affect a whole area in the DOM
	  (element get added or removed)
	
	
	
	
