<!DOCTYPE html>
<html>
<head>
  <title>Drag and Drop Example</title>
  <style>
    .container {
      display: flex;
      justify-content: space-between;
      padding: 20px;
    }
    .container div {
      width: 200px;
      height: 200px;
      border: 1px solid #ccc;
      padding: 10px;
      box-sizing: border-box;
    }
    .draggable {
      cursor: move;
    }
    .droppable {
      background-color: #eaf6ff;
    }
  </style>
</head>
<body>
  <div class="container">
    <div id="firstContainer">
      <div class="draggable" draggable="true">Item 1</div>
      <div class="draggable" draggable="true">Item 2</div>
      <div class="draggable" draggable="true">Item 3</div>
    </div>
    <div id="secondContainer" class="droppable"></div>
  </div>
  <button onclick="resetContainers()">Reset</button>

  <script>
    // Store references to the containers
    var firstContainer = document.getElementById('firstContainer');
    var secondContainer = document.getElementById('secondContainer');

    // Add event listeners for drag and drop events
    firstContainer.addEventListener('dragstart', dragStart);
    secondContainer.addEventListener('dragenter', dragEnter);
    secondContainer.addEventListener('dragover', dragOver);
    secondContainer.addEventListener('drop', drop);

    // Function called when the dragging starts
    function dragStart(event) {
      event.dataTransfer.setData('text/plain', event.target.id);
    }

    // Function called when the dragged item enters the second container
    function dragEnter(event) {
      event.preventDefault();
      secondContainer.classList.add('droppable');
    }

    // Function called when the dragged item is over the second container
    function dragOver(event) {
      event.preventDefault();
    }

    // Function called when the dragged item is dropped into the second container
    function drop(event) {
      event.preventDefault();
      var itemId = event.dataTransfer.getData('text/plain');
      var item = document.getElementById(itemId);
      secondContainer.appendChild(item);
      secondContainer.classList.remove('droppable');
      alert('Item dropped!');
    }

    // Function to reset the containers
    function resetContainers() {
      while (secondContainer.firstChild) {
        secondContainer.firstChild.remove();
      }
      firstContainer.innerHTML = `
        <div class="draggable" draggable="true">Item 1</div>
        <div class="draggable" draggable="true">Item 2</div>
        <div class="draggable" draggable="true">Item 3</div>
      `;
    }
  </script>
</body>
</html>

