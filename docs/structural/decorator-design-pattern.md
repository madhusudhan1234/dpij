## Decorator Design Pattern

Used to add new functionality to an existing object without being obtrusive.

In Decorator design pattern we can get these kinds of facility:
- More complete inheritance
- Wraps an Object
- Protects extended functionality
- Allows extended functionality

```JS
var Task = function(name) {
  this.name = name;
  this.completed = false;
}

Task.prototype.complete = function() {
  console.log('Completing Task: ' + this.name);
  this.completed = true;
}

Task.prototype.save = function() {
  console.log('Saving Task ' + this.name);
}

var myTask = new Task('Legacy Task');
myTask.complete();
myTask.save();

var urgentTask = new Task('Urgent Task');
urgentTask.priority = 2;
urgentTask.notify = function() {
  console.log('notifying important people');
};
urgentTask.notify();
urgentTask.complete();
urgentTask.save = function() {
  this.notify();
  Task.prototype.save.call(this);
};
urgentTask.save();
```

In above code snippet we can see that there is a urgentTask object is created from the Task function. urgentTask has the new property like priority, new function notify, and modified function save for the urgentTask. These modification only in urgentTask object and not affect to the original myTask object.

Okay, Let's see little bit more complex example here. Where we are creating new object from the existing Task and implemented new property and functions.

```JS
var Task = function(name) {
  this.name = name;
  this.completed = false;
}

Task.prototype.complete = function() {
  console.log('Completing Task: ' + this.name);
  this.completed = true;
}

Task.prototype.save = function() {
  console.log('Saving Task ' + this.name);
}

var myTask = new Task('Legacy Task');
myTask.complete();
myTask.save();

var UrgentTask = function (name, priority) {
  Task.call(this, name);
  this.priority = priority;
}
UrgentTask.prototype = Object.create(Task.prototype);
var ut = new UrgentTask('This is urgent', 1);

UrgentTask.prototype.notify = function() {
  console.log('notifying important people');
};

UrgentTask.prototype.save = function() {
  this.notify();
  console.log('do spend stuff before saving');
  Task.prototype.save.call(this);
};

ut.complete();
ut.save();
```