<!DOCTYPE html>
<html>
<head>
  <title>Google Sheets Clone</title>
</head>
<body>
  <header>
    <nav>
      <button id="download-btn">Download</button>
    </nav>
  </header>

  <main>
    <table id="spreadsheet">
      <!-- Generate the 10 rows and 5 columns dynamically using JavaScript -->
    </table>
  </main>

  <script src="app.js"></script>
</body>
</html>
// Get references to the DOM elements
const downloadBtn = document.getElementById('download-btn');
const spreadsheet = document.getElementById('spreadsheet');

// Create an empty data array to store the state of the input fields
let inputData = [];

// Generate the rows and columns dynamically
for (let i = 0; i < 10; i++) {
  const row = document.createElement('tr');

  for (let j = 0; j < 5; j++) {
    const cell = document.createElement('td');
    const input = document.createElement('input');

    // Add event listener to update the input data when the value changes
    input.addEventListener('input', (event) => {
      inputData[i * 5 + j] = event.target.value;
    });

    cell.appendChild(input);
    row.appendChild(cell);
  }

  spreadsheet.appendChild(row);
}

// Restore the input data from AsyncStorage if available
const storedData = JSON.parse(localStorage.getItem('inputData'));
if (storedData) {
  inputData = storedData;
  updateInputFields();
}

// Update the input fields with the stored data
function updateInputFields() {
  const inputFields = spreadsheet.getElementsByTagName('input');
  for (let i = 0; i < inputFields.length; i++) {
    inputFields[i].value = inputData[i] || '';
  }
}

// Save the input data to AsyncStorage whenever it changes
function saveInputData() {
  localStorage.setItem('inputData', JSON.stringify(inputData));
}

// Add event listener to the download button
downloadBtn.addEventListener('click', () => {
  // Generate the Excel file using a suitable library (e.g., SheetJS, ExcelJS)
  // Store or download the generated file in the desired format
});

// Add event listener to save the input data when the window is closed or refreshed
window.addEventListener('beforeunload', () => {
  saveInputData();
});
