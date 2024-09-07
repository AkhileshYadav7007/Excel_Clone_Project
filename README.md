# Excel Clone Project
The Excel Clone Project is a web-based spreadsheet application that replicates the functionality of a basic Excel-like grid interface. It allows users to perform data entry, calculations, and manage multiple sheets, offering a simplified yet interactive experience similar to Microsoft Excel or Google Sheets.

 Live Demo https://akhileshyadav7007.github.io/Excel_Clone_Project/

# Features
### Data Entry and Editing: Input, modify, and delete data in a grid-based system, mimicking a spreadsheet.
### Formulas and Calculations: Perform basic arithmetic operations like addition, subtraction, multiplication, and division using simple formulas (e.g., =A1+B1).
### Multiple Sheets: Create and manage multiple sheets within a single workbook.
### Copy/Paste Functionality: Supports basic clipboard operations, enabling users to copy and paste values within the grid.
### Undo/Redo Functionality: Undo mistakes or redo actions with a simple click.
### Save and Load: Save your current work and reload it at any time.
## Responsive Design: Accessible on both desktop and mobile devices.
# Technologies Used
### HTML5: For structuring the grid and interface.
### CSS3: For layout and responsive design.
### JavaScript: For handling the spreadsheet logic, formulas, and event-based interactions.
### LocalStorage: Used for saving and loading data.
### GitHub Pages: For hosting the live demo of the project.
Installation
Steps to Run Locally:
Clone the repository:
bash
Copy code
git clone https://github.com/AkhileshYadav7007/Excel_Clone_Project.git
Navigate to the project directory:
bash
Copy code
cd Excel_Clone_Project
Open the index.html file in your web browser to start using the application.
One-to-One Explanation of Core Logic
The core logic of the Excel Clone Project revolves around handling user interactions on a grid (spreadsheet) and processing formulas for arithmetic operations.

## 1. Creating the Grid (Spreadsheet Structure):
The spreadsheet interface is a grid created dynamically using JavaScript. Each cell can be clicked and edited by the user. The following JavaScript snippet dynamically creates a table with rows and columns.

javascript
Copy code
function createGrid(rows, cols) {
    let grid = document.querySelector('#grid');
    for (let i = 0; i < rows; i++) {
        let row = document.createElement('tr');
        for (let j = 0; j < cols; j++) {
            let cell = document.createElement('td');
            cell.setAttribute('contenteditable', 'true');  // Makes the cell editable
            row.appendChild(cell);
        }
        grid.appendChild(row);
    }
}
createGrid(): Generates a table of rows and cols using HTML table elements.
contenteditable="true": Allows each cell to be edited directly by the user.
2. Handling Cell Selection and Editing:
Each time a user clicks on a cell, they can edit its content. The application captures the cell's position and value to use it for formula calculations.

javascript
Copy code
let selectedCell = null;

document.querySelectorAll('td').forEach(cell => {
    cell.addEventListener('click', (e) => {
        selectedCell = e.target;  // Tracks the currently selected cell
    });
});
selectedCell: Stores the current cell being interacted with for easy reference.
3. Processing Formulas:
The core feature of a spreadsheet is the ability to process formulas. When a user enters a formula (e.g., =A1+B1), the app parses it, retrieves the values from the specified cells, performs the operation, and displays the result.

javascript
Copy code
function evaluateFormula(formula) {
    if (formula.startsWith('=')) {
        try {
            // Parse the formula (e.g., =A1+B1)
            let expression = formula.substring(1);
            let result = eval(expression);  // Use eval to compute the formula
            return result;
        } catch (error) {
            return 'Error';
        }
    }
    return formula;  // Return as is if it's not a formula
}
evaluateFormula(): Detects if the input starts with = (indicating a formula), evaluates it, and returns the result.
eval(expression): Used to execute the parsed formula. Note: In a production environment, avoid using eval due to security concerns and use a proper expression parser instead.
4. Handling Multiple Sheets:
Users can add new sheets, which are essentially new grids. Each sheet is stored separately, and switching between sheets allows for easy data organization.

javascript
Copy code
let sheets = [];
let activeSheetIndex = 0;

function createNewSheet() {
    let newSheet = [];  // Empty array for new sheet
    sheets.push(newSheet);
    activeSheetIndex = sheets.length - 1;  // Switch to the new sheet
    createGrid(50, 26);  // Create a new grid for the new sheet
}
sheets[]: Array storing all sheets as individual grids.
createNewSheet(): Adds a new sheet and sets it as the active one.
5. Saving and Loading Data:
To persist data across sessions, the project uses localStorage to save the current state of the spreadsheet. Users can save their work and reload it later.

javascript
Copy code
function saveSheetData() {
    localStorage.setItem('sheetData', JSON.stringify(sheets));
}

function loadSheetData() {
    let data = JSON.parse(localStorage.getItem('sheetData'));
    if (data) {
        sheets = data;
        // Load the first sheet
        activeSheetIndex = 0;
        createGridFromData(sheets[0]);
    }
}
saveSheetData(): Saves the entire sheet data array to localStorage.
loadSheetData(): Loads the data from localStorage and restores the last saved state.
Contributing
Contributions are welcome! To improve this project, you can add new features, optimize existing code, or fix bugs. Here’s how you can contribute:

Fork the repository.
Create a new branch for your feature:
bash
Copy code
git checkout -b feature/AmazingFeature
Commit your changes:
bash
Copy code
git commit -m 'Add AmazingFeature'
Push to the branch:
bash
Copy code
git push origin feature/AmazingFeature
Open a pull request to merge your changes into the main branch.
License
This project is open-source and is licensed under the MIT License.
