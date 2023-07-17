######################
Test of Rendering HTML
######################

.. raw:: html

   <!DOCTYPE html>
    <html>
    <head>
      <title>Input Box Example</title>
      <script>
        function showText() {
          var inputText = document.getElementById("myInput").value;
          document.getElementById("output").textContent = inputText;
        }
      </script>
    </head>
    <body>
      <label for="myInput">Enter text:</label>
      <input type="text" id="myInput" />
      <button onclick="showText()">Show Text</button>
      <p id="output"></p>
    </body>
    </html>