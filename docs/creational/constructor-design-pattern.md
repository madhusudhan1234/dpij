## Constructor Design Pattern

- In this design pattern we can create a Object from the function 
- Below is the Task Function from which we can create a Object with new Syntax
- name and complete are the the properties where as complete and save are methods
- task1, task2, task3 and task4 are the objects created from Task Function

```JS
var Task = function(name) {
	this.name = name;
	this.complete = false;

	this.complete = function() {
		console.log('Completing Task: ' + this.name );	
		this.completed = true;
	}
  
  this.save = function() {
		console.log('Saving Task: ' + this.name);
	}
}

var task1 = new Task('Create a demo for Constructors');
var task2 = new Task('Create a demo for Modules');
var task3 = new Task('Create a demo for Singletons');
var task4 = new Task('Create a demo for Prototypes');

task1.complete();
task2.save();
task3.save();
task4.save();
```