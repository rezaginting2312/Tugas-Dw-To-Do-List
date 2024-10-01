# Tugas-Dw-To-Do-List

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0 auto;
            padding: 20px;
            max-width: 600px;
        }

        h1 {
            text-align: center;
        }

        #task-input {
            width: 80%;
            padding: 10px;
            font-size: 16px;
        }

        #add-task-btn {
            padding: 10px;
            font-size: 16px;
        }

        ul {
            list-style-type: none;
            padding: 0;
        }

        li {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            border-bottom: 1px solid #ccc;
        }

        li.completed {
            text-decoration: line-through;
        }

        button {
            margin-left: 10px;
            padding: 5px;
        }
    </style>
</head>

<body>
    <h1>To-Do List</h1>
    <input type="text" id="task-input" placeholder="Enter a new task">
    <button id="add-task-btn">Add Task</button>

    <h3>Filter Tasks</h3>
    <button onclick="filterTasks('all')">All</button>
    <button onclick="filterTasks('active')">Active</button>
    <button onclick="filterTasks('completed')">Completed</button>

    <ul id="task-list"></ul>

    <script src="app.js"></script>
</body>

</html>

// app.js
class Task {
    constructor(name) {
        this.name = name;
        this.completed = false;
    }

    toggleCompleted() {
        this.completed = !this.completed;
    }
}

let tasks = [];

function addTask() {
    const taskInput = document.getElementById('task-input');
    const taskName = taskInput.value.trim();

    if (taskName === "") {
        alert("Task cannot be empty!");
        return;
    }

    const task = new Task(taskName);
    tasks.push(task);
    displayTasks();
    taskInput.value = ''; // Kosongkan input setelah menambahkan
}

document.getElementById('add-task-btn').addEventListener('click', addTask);

function displayTasks() {
    const taskList = document.getElementById('task-list');
    taskList.innerHTML = '';

    tasks.forEach((task, index) => {
        const taskItem = document.createElement('li');
        taskItem.className = task.completed ? 'completed' : '';

        const taskText = document.createElement('span');
        taskText.textContent = task.name;
        
        const taskCheckbox = document.createElement('input');
        taskCheckbox.type = 'checkbox';
        taskCheckbox.checked = task.completed;
        taskCheckbox.addEventListener('click', () => toggleTask(index));

        const deleteButton = document.createElement('button');
        deleteButton.textContent = 'Delete';
        deleteButton.addEventListener('click', () => deleteTask(index));

        taskItem.appendChild(taskCheckbox);
        taskItem.appendChild(taskText);
        taskItem.appendChild(deleteButton);

        taskList.appendChild(taskItem);
    });
}

function filterTasks(filter) {
    let filteredTasks = tasks;

    if (filter === 'active') {
        filteredTasks = tasks.filter(task => !task.completed);
    } else if (filter === 'completed') {
        filteredTasks = tasks.filter(task => task.completed);
    }

    const taskList = document.getElementById('task-list');
    taskList.innerHTML = '';

    filteredTasks.forEach((task, index) => {
        const taskItem = document.createElement('li');
        taskItem.className = task.completed ? 'completed' : '';

        const taskText = document.createElement('span');
        taskText.textContent = task.name;
        
        const taskCheckbox = document.createElement('input');
        taskCheckbox.type = 'checkbox';
        taskCheckbox.checked = task.completed;
        taskCheckbox.addEventListener('click', () => toggleTask(index));

        const deleteButton = document.createElement('button');
        deleteButton.textContent = 'Delete';
        deleteButton.addEventListener('click', () => deleteTask(index));

        taskItem.appendChild(taskCheckbox);
        taskItem.appendChild(taskText);
        taskItem.appendChild(deleteButton);

        taskList.appendChild(taskItem);
    });
}

