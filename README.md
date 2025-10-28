<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ToDo List</title>
    <style>
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #ADB2D4;
            height: 100vh;
            margin: 0;
        }
        .list-container {
            width: 50%;
            min-height: 300px;
            background-color: #C7D9DD;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-between;
            padding: 20px;
            border-radius: 10px;
        }
        .list-header, .list-foot {
            display: flex;
            gap: 10px;
        }
        .list-body {
            width: 100%;
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin: 20px 0;
        }
        .list-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #D5E5D5;
            padding: 10px;
            border-radius: 5px;
            width: 90%;
        }
        .Enter {
            background-color: #EEF1DA;
            padding: 8px;
            border: none;
            border-radius: 5px;
            flex: 1;
        }
        .btn {
            background-color: #97e18b;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
        }
        .Clear {
            background-color: #db7f77;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            color: white;
        }
    </style>
</head>
<body>
    <div class="list-container">
        <div class="list-header">
            <input class="Enter" type="text" id="task-input" placeholder="Enter task">
            <button class="btn" onclick="addNewTask()">Add Task</button>
        </div>

        <div class="list-body"></div>

        <div class="list-foot">
            <p id="pending-task">Pendings: 0</p>
            <button class="Clear" onclick="reset()">Clear All</button>
        </div>
    </div> 

    <script>
        const input = document.getElementById('task-input');
        const listBody = document.querySelector('.list-body');
        const pendingText = document.getElementById('pending-task');
        const tasks = [];

        function addNewTask() {
            const taskValue = input.value.trim();
            if (taskValue !== "") {
                tasks.push({ text: taskValue, done: false });
                input.value = "";
                render();
            } else {
                alert("Task cannot be empty!");
            }
        }

        function deleteTask(index) {
            tasks.splice(index, 1);
            render();
        }

        function reset() {
            tasks.length = 0;
            render();
        }

        function done(checkbox, index) {
            tasks[index].done = checkbox.checked;
            render();
        }

        function updatePending() {
            const pendingCount = tasks.filter(task => !task.done).length;
            pendingText.innerHTML = `Pendings: ${pendingCount}`;
        }

        function render() {
            let htmlData = '';
            for (let i = tasks.length - 1; i >= 0; i--) {
                htmlData += `
                    <div class="list-item">
                        <input type="checkbox" ${tasks[i].done ? "checked" : ""} onclick="done(this, ${i})">
                        <p id="task-para-${i}" style="text-decoration: ${tasks[i].done ? 'line-through' : 'none'};">
                            ${tasks[i].text}
                        </p>
                        <button onclick="deleteTask(${i})">X</button>
                    </div>`;
            }
            listBody.innerHTML = htmlData;
            updatePending();
        }
    </script>
</body>
</html>
