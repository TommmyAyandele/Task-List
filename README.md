# Task-List
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.1.1/css/fontawesome.min.css" integrity="sha384-zIaWifL2YFF1qaDiAo0JFgsmasocJ/rqu7LKYH8CoBEXqGbb9eO+Xi3s6fQhgFWM" crossorigin="anonymous">
  <title>Task List</title>
</head>
<body>
<div class="container">
  <div class="row">
    <div class="col s12">
      <div id="main" class="card">
        <div class="card-content">
          <span class="class-title">Task List</span>
          <div class="row">
            <form id="task-form">
              <div class="input-field col s12">
                <input type="text" name="task" id="task">
                <label for="task">New Task</label>
                </div>
                <input type="submit" value="Add task" class="btn">
            </form>
          </div>
        </div>
        <div class="card-action">
          <h5 id="task-title">Tasks</h5>
          <div class="input-field col s12">
            <input type="text" name="filter" id="filter">
            <label for="filter">Filter Tasks</label>
            </div>
            <ul class="collection"></ul>
            <a href="#" class="clear-tasks btn black">Clear Tasks</a>
        </div>
      </div>
    </div>
  </div>
</div>
  <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>
  <script src="app.js"></script> 
</body>
</html>



const form = document.querySelector('#task-form');
const taskList = document.querySelector('.collection');
const clearBtn = document.querySelector('.clear-tasks');
const filter = document.querySelector('#filter');
const taskInput = document.querySelector('#task');

loadEventListener();

function loadEventListener(){
  document.addEvenntListener('DOMContentLoaded', getTasks)
form.addEventListener('submit', addTask);
taskList.addEventListener('click', removeTask)
clearBtn.addEventListener('click', clearTasks)
filter.addEventListener('keyup', filterTasks)
};


function addTask(e){
if(taskInput.value === ''){
alert('Please add task');
}

const li = document.createElement('li')
li.className = 'collection-item';
li.appendChild(document.createTextNode(taskInput.value));

const link = document.createElement('a');
link.className = 'delete-item secondary-content';
link.innerHTML = '<i class="fa fa-trash"></i>';
li.appendChild(link);

taskList.appendChild(li);

taskInput.value = '';

  e.preventDefault();
}

function removeTask(e){
  if(e.target.parentElement.classList.contains('delete-item')){
   if(confirm('Are you sure?')){
    e.target.parentElement.parentElement.remove();
  } 
  }
}

function clearTasks() {
  // taskList.innerHTML = ""

  while(taskList.firstChild){
    taskList.removeChild(taskList.firstChild)
  }
};

function filterTasks(e) {
  const text = e.target.value.toLowerCase();

  document.querySelectorAll('.collection-item').forEach(function(task){
    const item = task.firstChild.textContent;
    if(item.toLowerCase().indexOf(text) != -1){
      task.style.display = 'block';
    } else {
      task.style.display = 'none';
    }
  });
}

storeTasksInLocalStorage(taskInput.value)
function storeTaskInLocalStorage(task){
  let tasks;
  if(localStorage.getItem('tasks')=== null){
    tasks = []
  } else {
    tasks = Json.parse(localStorage.getItem('tasks'));
  }
  tasks.push(task);

localStorage.setItem('tasks', JSON.stringify(tasks));
}

function removeTaskFromLocalStorage(taskItem) {
  let tasks;
  if(localStorage.getItem('tasks') === null){
    tasks = [];
  } else {
    tasks = JSON.parse(localStorage.getItem('tasks'));
  }

  tasks.forEach(function(task, index){
    if(taskItem.textContent === task){
      tasks.splice(index, 1);
    }
  });

  localStorage.setItem('tasks', JSON.stringify(tasks));
}







