## Facade Design Pattern

This design pattern is used to provide a simplified interface to a complicate system.

- When we think about facade its like thinking about the front of a building.
- Facade hides a Choas from us
- Simplifies the interface
- Query is a good implementation of facade pattern

Let's look on the following code snippet:

```JS
var Task = function(data) {
  this.name = data.name;
  this.priority = data.priority;
  this.project = data.project;
  this.user = data.user;
  this.completed = data.completed;
}

var TaskService = function() {
  return {
    complete: function(task) {
      task.completed = true;
      console.log('Completing Task: ' + task.name);
    },
    setCompleteDate: function(task) {
      task.completeDate = new Date();
      console.log(task.name + 'completed on' + task.completedDate);
    },
    notifyCompletion: function(task, user) {
      console.log('Notifying ' + user + 'of the completion of ' + task.name);
    },
    save: function(task) {
      console.log('Saving task ' + task.name);
    }
  }
}();

var myTask = new Task({
  name: 'MyTask',
  priority: 1,
  project: 'Courses',
  user: 'John',
  completed: false
});

console.log(myTask);

TaskService.complete(myTask);

if(myTask.completed) {
  TaskService.setCompleteDate(myTask);
  TaskService.notifyCompletion(myTask, myTask.user);
  TaskService.save(myTask);
}

console.log(myTask);
```

In above code we have created a service with the functions so can hide the complexity of the service in the main js file by using the following Wrapper.

```JS
var Task = function(data) {
  this.name = data.name;
  this.priority = data.priority;
  this.project = data.project;
  this.user = data.user;
  this.completed = data.completed;
}

var TaskService = function() {
  return {
    complete: function(task) {
      task.completed = true;
      console.log('Completing Task: ' + task.name);
    },
    setCompleteDate: function(task) {
      task.completeDate = new Date();
      console.log(task.name + 'completed on' + task.completedDate);
    },
    notifyCompletion: function(task, user) {
      console.log('Notifying ' + user + 'of the completion of ' + task.name);
    },
    save: function(task) {
      console.log('Saving task ' + task.name);
    }
  }
}();

var TaskServiceWrapper = function() {
  var completeAndNotify = function(task) {
    TaskService.complete(myTask);
    if(myTask.completed) {
      TaskService.setCompleteDate(myTask);
      TaskService.notifyCompletion(myTask, myTask.user);
      TaskService.save(myTask);
    }
  }
  return {
    completeAndNotify: completeAndNotify
  }
}();

var myTask = new Task({
  name: 'MyTask',
  priority: 1,
  project: 'Courses',
  user: 'John',
  completed: false
});

console.log(myTask);

TaskServiceWrapper.completeAndNotify();

console.log(myTask);
```
