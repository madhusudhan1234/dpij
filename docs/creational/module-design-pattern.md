## Module Design Pattern 

This pattern is the simple way to encapsulate methods. Which creates a "Toolbox" of functions to use. for e.g.

```js
  var Module = {
    method: function() {...},
    netMethod: function() {
      ...
    }
  }
```

We can also create a private variable inside only. The Function like this way.

```js
  var Module = {
    var privateVar = 'I am private...';

    return {
      method: function() {...},
      nextMethod: function() {...
      }
    }
  }
```

In above code snippet the private variables is only inside of Module and can not access from the outside. 

To demonistrate the Module design pattern we can create a following example in code. In the below code you can see we are using the same Task example as previous. We are creating a repo function in the Module pattern let's say it handles all the database related work. 

For now we are created a get and save only for the demonistration of Module design pattern. Those methods can be access from the task object in the following way.

```js
var repo = function(name) {
  return {
    get: function(id) {
      console.log('Getting task ' + id);
      return {
        name: 'new task from db'
      }
    },
    save: function(task) {
      console.log('Saving ' + task.name + ' to the db'); 
    }
  }
}

var Repositery = repo();

var Task = function(data) {
	this.name = data.name;
	this.complete = false;

	this.complete = function() {
		console.log('Completing Task: ' + this.name );	
		this.completed = true;
	}
  
  this.save = function() {
		console.log('Saving Task: ' + this.name);
        Repositery.save(this);
	}
}

var task1 = new Task(Repositery.get(1));
var task2 = new Task({ name: 'Create a demo for Modules' });
var task3 = new Task({ name: 'Create a demo for Singletons' });
var task4 = new Task({ name: 'Create a demo for Prototypes' });

task1.complete();
task2.save();
task3.save();
task4.save();
```

If we want to use the module revealing pattern we can do the followings:

```js
var repo = function(name) {
  var get = function(id) {
    console.log('Getting task ' + id);
    return {
      name: 'new task from db'
    }
  }
  
  var save = function(task) {
    console.log('Saving ' + task.name + ' to the db'); 
  }

  return {
    get: get,
    save: save
  }
}

var Repositery = repo();

var Task = function(data) {
	this.name = data.name;
	this.complete = false;

	this.complete = function() {
		console.log('Completing Task: ' + this.name );	
		this.completed = true;
	}
  
  this.save = function() {
		console.log('Saving Task: ' + this.name);
        Repositery.save(this);
	}
}

var task1 = new Task(Repositery.get(1));
var task2 = new Task({ name: 'Create a demo for Modules' });
var task3 = new Task({ name: 'Create a demo for Singletons' });
var task4 = new Task({ name: 'Create a demo for Prototypes' });

task1.complete();
task2.save();
task3.save();
task4.save();
```