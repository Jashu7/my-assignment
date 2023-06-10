# my-assignment
#front end 
<!DOCTYPE html>
<html>
<head>
    <title>Drag and Drop Example</title>
    <style>
        .container {
            display: flex;
        }
        
        .item {
            padding: 10px;
            margin: 5px;
            background-color: #ccc;
            cursor: move;
        }
        
        .item:hover {
            background-color: #aaa;
        }
        
        .success-message {
            color: green;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h2>Drag and Drop Example</h2>
    
    <div class="container">
        <div id="container1" class="container">
            <div class="item" draggable="true">Item 1</div>
            <div class="item" draggable="true">Item 2</div>
            <div class="item" draggable="true">Item 3</div>
            <div class="item" draggable="true">Item 4</div>
        </div>
        
        <div id="container2" class="container">
            <div class="item" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
        </div>
    </div>
    
    <p id="successMessage" class="success-message"></p>
    
    <button onclick="resetContainers()">Reset</button>
    
    <script>
        function allowDrop(event) {
            event.preventDefault();
        }
        
        function drag(event) {
            event.dataTransfer.setData("text", event.target.id);
        }
        
        function drop(event) {
            event.preventDefault();
            var data = event.dataTransfer.getData("text");
            var draggedItem = document.getElementById(data);
            
            event.target.appendChild(draggedItem);
            
            document.getElementById("successMessage").innerText = "Item dropped successfully!";
        }
        
        function resetContainers() {
            var container1 = document.getElementById("container1");
            var container2 = document.getElementById("container2");
            
            while (container2.firstChild) {
                container1.appendChild(container2.firstChild);
            }
            
            document.getElementById("successMessage").innerText = "";
        }
    </script>
</body>
</html>
