## Constructor Prototype design pattern

 ```JS
 function ObjectName(param1, param2) {
   this.param1 = param1;
   this.param2 = param2;
   this.toString = function () {
     return this.param1 + ' ' + this.param2;
   }
 }
 ```

#### In above constructor design pattern there is one drawback which is following:
 - Whenever we create a object the toString function is re-initilized
every time of new object creation which is not good idea

**So We have a solution for this using Prototype**

#### What is prototype in js?
- An Encapsulation of properties that an object links to
- All the copy of Object links to the Same Prototype
- Structure to link the function in prototype is followings

```JS
  TasK.prototype.methodName = function (arguments) {
    // Implementation Detail
  }
```

```JS
var Task = function(name) {
	this.name = name;
	this.complete = false;
}

Task.prototype.doComplete = function() {
  console.log('completing task: ' + this.name);
  this.completed = true;
}

Task.prototype.save = function() {
  console.log('Saving Task: ' + this.name);
}

var task1 = new Task('Create a demo for Constructors');
var task2 = new Task('Create a demo for Modules');
var task3 = new Task('Create a demo for Singletons');
var task4 = new Task('Create a demo for Prototypes');

task1.doComplete();
task2.save();
task3.save();
task4.save();
```