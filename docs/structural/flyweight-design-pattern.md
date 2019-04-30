## Flyweight Design Pattern

Conserves memory by sharing portions of an object between objects.

- Our tasks had a lots of non unique data
- Flyweight Shares data across objects
- Results in a Smaller memory footprint
- But only if you have large numbers of objects

Let's see the following code example:

```JS
var task = function(data) {
  this.name = data.name;
  this.priority = data.priority;
  this.project = data.project;
  this.user = data.user;
  this.completed = data.completed;
}

function TaskCollection() {
  var tasks = {};
  var count = 0;
  var add = function(data) {
    tasks[data.name] = new Task(data);
    count++;
  };
  var get = function(name) {
    return tasks[name];
  };
  var getCount = function() {
    return count;
  }
  return {
    add: add,
    get: get,
    getCount: getCount
  };
}

var tasks = new TaskCollection();

var projects = ['name', 'courses', 'trainings', 'project'];
var priorities = [1, 2, 3, 4, 5];
var users = ['John', 'Erica', 'Amanda', 'Nathan'];
var completed = [true, false];

var initialMemory = process.memoryUsage().heapUsed;
for(var i=0; i< 100; i++) {
  tasks.add({
    name: 'task' + i,
    priority: priorities[Math.floor(Math.random())],
    project: projects[Math.floor(Math.random() * 4)],
    computed: completed[Math.floor(Math.rendom() *2)]
  });
}

var afterMemory = process.memoryUsage().heapUsed;
console.log('used memory ' + (afterMemory - initialMemory)/1000000);
console.log("tasks" + tasks.getCount());
```