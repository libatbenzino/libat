
<!DOCTYPE html>
<html lang="he">
<head>
  <meta charset="UTF-8">
  <title>ניהול מלאי</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
  <style>
    body { font-family: Arial; direction: rtl; margin: 0; padding: 0; background-color: #f9f9f9; }
    .navbar { background-color: #f413a9; overflow: hidden; padding: 10px; }
    .navbar a { float: right; color: white; text-align: center; padding: 10px; text-decoration: none; font-size: 16px; cursor: pointer; }
    .navbar a:hover { background-color: #f5e9f2; }
    .content { padding: 20px; display: none; }
    .active { display: block; }
    input, button { margin: 5px; padding: 8px; font-size: 16px; border-radius: 4px; border: 1px solid #ccc; }
    button { background-color: #4CAF50; color: white; border: none; cursor: pointer; }
    button:hover { background-color: #45a049; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; background-color: white; }
    table, th, td { border: 1px solid #ccc; }
    th, td { padding: 10px; text-align: right; }
    img { max-height: 50px; }
  </style>
</head>
<body>

<div class="navbar">
  <img src="logoLB.png.png.png" alt="לוגו האתר" style="height: 50px; float:right; margin-left:10px;">
  <a onclick="showSection('inventoryEntry')">כניסה למלאי</a>
  <a onclick="showSection('viewInventory')">צפייה במלאי</a>
  <a onclick="showSection('stockCounting')">ספירות מלאי</a>
  <a onclick="showSection('about')">אודות</a>
</div>

<div id="inventoryEntry" class="content active">
  <h1>כניסה למלאי</h1>
  <input type="text" id="clientName" placeholder="שם לקוח">
  <input type="text" id="productCode" placeholder='מק"ט'>
  <input type="number" id="palletCount" placeholder="כמות משטחים">
  <input type="number" id="boxesPerPallet" placeholder="כמות קרטונים במשטח">
  <input type="file" id="itemImage" accept="image/*">
  <button onclick="saveEntry()">שמור</button>
</div>

<div id="viewInventory" class="content">
  <h1>צפייה במלאי</h1>
  <button onclick="exportToExcel()">ייצוא לאקסל</button>
  <button onclick="clearInventory()">ניקוי מלאי</button>
  <table>
    <thead>
      <tr>
        <th>תאריך</th>
        <th>שם לקוח</th>
        <th>מק"ט</th>
        <th>מספר משטח</th>
        <th>כמות קרטונים</th>
        <th>תמונה</th>
        <th>ברקוד QR</th>
        <th>פעולות</th>
      </tr>
    </thead>
    <tbody id="inventoryTableBody"></tbody>
  </table>
</div>

<div id="stockCounting" class="content">
  <h1>ספירות מלאי</h1>

  <input type="file" id="uploadExcel" accept=".xlsx" onchange="handleFileUpload(event)">
  <br><br>
  <input type="text" id="scanBarcode" placeholder="סרוק ברקוד..." oninput="handleScanInput()" style="font-size: 18px;">

  <br><br>
  <button onclick="exportStockDataToExcel()">ייצוא ספירת מלאי לאקסל</button>
  <button onclick="clearStockCounting()">ניקוי ספירת מלאי</button>
  <input type="text" id="searchBarcode" placeholder="חיפוש לפי מזהה או ברקוד..." oninput="filterStockTable()">
  <table border="1">
    <thead id="stockTableHead"></thead>
    <tbody id="stockTableBody"></tbody>
  </table>
</div>


<div id="about" class="content">
  <h1>אודות האפליקציה</h1>
  <p>אפליקציה פשוטה לניהול מלאינבנתה באהבה ליבת בנזינו</p>
</div>
<script>
  const successSound = new Audio("https://actions.google.com/sounds/v1/cartoon/clang_and_wobble.ogg");
const errorSound = new Audio("https://actions.google.com/sounds/v1/alarms/beep_short.ogg");
  let inventory = JSON.parse(localStorage.getItem('inventory')) || [];
  let palletCounter = parseInt(localStorage.getItem('palletCounter')) || 1;
  let stockData = [];
  let headers = [];
  let barcodeColumn = '';
 
  function showSection(id) {
    document.querySelectorAll('.content').forEach(section => section.classList.remove('active'));
    const selected = document.getElementById(id);
    if (selected) selected.classList.add('active');
    if (id === 'viewInventory') updateInventoryView();
  }
  
  function saveEntry() {
    const client = document.getElementById('clientName').value;
    const code = document.getElementById('productCode').value;
    const palletCount = parseInt(document.getElementById('palletCount').value);
    const boxes = parseInt(document.getElementById('boxesPerPallet').value);
    const imageInput = document.getElementById('itemImage');
    const date = new Date().toLocaleString();
  
    if (client && code && palletCount && boxes) {
      const reader = new FileReader();
      reader.onload = function (e) {
        const base64Image = e.target.result;
        const palletNumbers = generatePalletNumbers(palletCount);
        palletNumbers.forEach(pallet => {
          inventory.push({ client, code, pallet, boxes, date, image: base64Image });
        });
        localStorage.setItem('inventory', JSON.stringify(inventory));
        updateInventoryView();
        alert("נשמר בהצלחה!");
      };
  
      if (imageInput.files[0]) {
        reader.readAsDataURL(imageInput.files[0]);
      } else {
        const palletNumbers = generatePalletNumbers(palletCount);
        palletNumbers.forEach(pallet => {
          inventory.push({ client, code, pallet, boxes, date, image: '' });
        });
        localStorage.setItem('inventory', JSON.stringify(inventory));
        updateInventoryView();
        alert("נשמר בהצלחה!");
      }
  
      document.getElementById('clientName').value = '';
      document.getElementById('productCode').value = '';
      document.getElementById('palletCount').value = '';
      document.getElementById('boxesPerPallet').value = '';
      imageInput.value = '';
    }
  }
  
  function generatePalletNumbers(count) {
    const numbers = [];
    for (let i = 0; i < count; i++) {
      const num = "LB" + String(palletCounter).padStart(4, '0');
      numbers.push(num);
      palletCounter++;
    }
    localStorage.setItem('palletCounter', palletCounter);
    return numbers;
  }
  
  function updateInventoryView() {
    const tableBody = document.getElementById('inventoryTableBody');
    tableBody.innerHTML = '';
    inventory.forEach((item, index) => {
      const row = document.createElement('tr');
      row.innerHTML = `
        <td>${item.date}</td>
        <td>${item.client}</td>
        <td>${item.code}</td>
        <td>${item.pallet}</td>
        <td>${item.boxes || ''}</td>
        <td>${item.image ? `<img src="${item.image}" style="height:30px;cursor:pointer" onclick="showImage('${item.image}')">` : ''}</td>
        <td><div id="qrcode-${index}"></div></td>
        <td><button onclick="deleteRow(${index})">❌</button></td>
      `;
      tableBody.appendChild(row);
      new QRCode(document.getElementById(`qrcode-${index}`), { text: item.pallet, width: 50, height: 50 });
    });
  }
  
  function showImage(src) {
    const w = window.open();
    w.document.write(`<img src="${src}" style="max-width:100%">`);
  }
  
  function deleteRow(index) {
    if (confirm("למחוק את השורה?")) {
      inventory.splice(index, 1);
      localStorage.setItem('inventory', JSON.stringify(inventory));
      updateInventoryView();
    }
  }
  
  function clearInventory() {
    if (confirm("למחוק את כל המלאי?")) {
      inventory = [];
      localStorage.removeItem('inventory');
      localStorage.removeItem('palletCounter');
      updateInventoryView();
    }
  }
  
  function exportToExcel() {
    const cleanedInventory = inventory.map(item => ({
      תאריך: item.date,
      'שם לקוח': item.client,
      'מק"ט': item.code,
      'מספר משטח': item.pallet,
      'כמות קרטונים': item.boxes || ''
    }));
  
    const ws = XLSX.utils.json_to_sheet(cleanedInventory);
    const wb = XLSX.utils.book_new();
    XLSX.utils.book_append_sheet(wb, ws, "Inventory");
    XLSX.writeFile(wb, "inventory.xlsx");
  }
  
  // ------------------------
  // ספירות מלאי
  // ------------------------
  
  function handleFileUpload(event) {
  const file = event.target.files[0];
  if (!file) return;

  const reader = new FileReader();
  reader.onload = function(e) {
    const data = new Uint8Array(e.target.result);
    const workbook = XLSX.read(data, { type: 'array' });
    const sheet = workbook.Sheets[workbook.SheetNames[0]];
    stockData = XLSX.utils.sheet_to_json(sheet, { defval: '' });
    updateStockTable();    // מציג את הטבלה באתר
    saveStockDataToStorage();   // שומר את הנתונים בזיכרון!
  };
  reader.readAsArrayBuffer(file);
}
function updateStockTable() {
  const tbody = document.getElementById('stockTableBody');
  const thead = document.getElementById('stockTableHead');
  tbody.innerHTML = '';
  thead.innerHTML = '';

  if (stockData.length === 0) return;

  headers = Object.keys(stockData[0]);
  barcodeColumn = headers.find(h => h.trim().toUpperCase().includes('BAR-CODE')) || '';

  if (!barcodeColumn) {
    alert("❗️ לא נמצאה עמודת BAR-CODE בקובץ.");
    return;
  }

  // יצירת כותרות
  const headerRow = document.createElement('tr');
  headers.forEach(header => {
    const th = document.createElement('th');
    th.textContent = header;
    headerRow.appendChild(th);
  });

  const noteTh = document.createElement('th');
  noteTh.textContent = 'הערה';
  headerRow.appendChild(noteTh);

  const actionTh = document.createElement('th');
  actionTh.textContent = 'פעולות';
  headerRow.appendChild(actionTh);

  thead.appendChild(headerRow);

  // יצירת שורות
  stockData.forEach((item, index) => {
    const row = document.createElement('tr');
    row.setAttribute('data-index', index);

    row.innerHTML =
      headers.map(h => `<td>${item[h] ?? ''}</td>`).join('') +
      `<td><input type="text" value="${item['הערה'] || ''}" onchange="saveNote(${index}, this.value)" style="width: 100%;"></td>` +
      `<td>
        <button onclick="markAsProblem(${index})" style="background-color: red; color: white;">בעיה</button>
        <button onclick="clearMark(${index})" style="background-color: gray; color: white;">נקה</button>
      </td>`;

    if (item['נמצא'] === 'נמצא') {
      row.style.backgroundColor = '#90ee90';
    } else if (item['נמצא'] === 'בעיה') {
      row.style.backgroundColor = 'red';
    }

    tbody.appendChild(row);
  });
}

function loadStockDataFromStorage() {
  const saved = localStorage.getItem('stockData');
  if (saved) {
    stockData = JSON.parse(saved);
    updateStockTable();
  }
}
// פונקציה לניקוי ספירת מלאי
function clearStockCounting() {
  if (confirm('למחוק את טבלת הספירות?')) {
    stockData = [];
    localStorage.removeItem('stockData');
    updateStockTable();
  }
}

// פונקציה ייצוא ספירת מלאי
function exportStockDataToExcel() {
  if (stockData.length === 0) {
    alert("אין נתונים לייצוא");
    return;
  }

  const ws = XLSX.utils.json_to_sheet(stockData);
  const wb = XLSX.utils.book_new();
  XLSX.utils.book_append_sheet(wb, ws, "StockCount");
  XLSX.writeFile(wb, "stock_count.xlsx");
}
window.onload = function() { loadStockDataFromStorage(); };
// פונקציה שמסמנת שורה כבעייתית
function handleScan() {
  console.log("הפונקציה handleScan הופעלה");

  const barcodeInput = document.getElementById('scanBarcode');
  const barcode = barcodeInput.value.trim();
  if (!barcode || !barcodeColumn) return;

  const index = stockData.findIndex(item =>
    item[barcodeColumn] && item[barcodeColumn].toString().trim() === barcode
  );

  if (index !== -1) {
    stockData[index]['נמצא'] = 'נמצא';
    saveStockDataToStorage();
    updateStockTable();

    setTimeout(() => {
      const row = document.querySelector(`#stockTableBody tr[data-index="${index}"]`);
      if (row) {
        row.style.backgroundColor = '#90ee90';
        row.scrollIntoView({ behavior: 'smooth', block: 'center' });
      }
      successSound.play().catch(() => {});
    }, 100);
  } else {
    errorSound.play().catch(() => {});
    alert("ברקוד לא נמצא בטבלה!");

    const newRow = {
      [barcodeColumn]: barcode,
      'הערה': 'ברקוד לא נמצא'
    };
    stockData.push(newRow);
    saveStockDataToStorage();
    updateStockTable();

    setTimeout(() => {
      const newIndex = stockData.length - 1;
      const newRowEl = document.querySelector(`#stockTableBody tr[data-index="${newIndex}"]`);
      if (newRowEl) {
        newRowEl.scrollIntoView({ behavior: 'smooth', block: 'center' });
        newRowEl.style.backgroundColor = 'red';
      }
    }, 100);
  }

  barcodeInput.value = '';
  barcodeInput.focus();
}

function markAsProblem(index) {
  const row = document.querySelector(`#stockTableBody tr[data-index="${index}"]`);
  if (row) {
    row.style.backgroundColor = 'red'; // צובע את השורה באדום
    const lastCell = row.querySelector('td:last-child');
    lastCell.textContent = 'בעיה';
    stockData[index]['נמצא'] = 'בעיה'; // גם לעדכן בזיכרון
    saveStockDataToStorage(); // לשמור
  }
}
function saveNote(index, value) {
  stockData[index]['הערה'] = value;
  saveStockDataToStorage();
}
function filterStockTable() {
  const searchTerm = document.getElementById('searchBarcode').value.trim().toLowerCase();
  const rows = document.querySelectorAll('#stockTableBody tr');

  // מחפשים את העמודה עם שם שכולל 'מזהה'
  const idColumn = headers.find(h => h.replace(/[\s"']/g, '').includes('מזהה')) || '';

  rows.forEach(row => {
    const index = row.getAttribute('data-index');
    const item = stockData[index];
    const barcodeValue = (item[barcodeColumn] || '').toString().toLowerCase();
    const idValue = (item[idColumn] || '').toString().toLowerCase();

    if (barcodeValue.includes(searchTerm) || idValue.includes(searchTerm)) {
      row.style.display = '';
    } else {
      row.style.display = 'none';
    }
  });
}
function clearMark(index) {
  const row = document.querySelector(`#stockTableBody tr[data-index="${index}"]`);
  if (row) {
    row.style.backgroundColor = ''; // מחיקת צבע
    const lastCell = row.querySelector('td:last-child');
    lastCell.textContent = ''; // מחיקת טקסט
    stockData[index]['נמצא'] = ''; // הסרת סימון מהזיכרון
    saveStockDataToStorage(); // עדכון בזיכרון
  }
}
function enableSounds() {
  successSound.play().catch(() => {});
  errorSound.play().catch(() => {});
}
function saveStockDataToStorage() {
  localStorage.setItem('stockData', JSON.stringify(stockData));
}
let scanTimeout;

function handleScanInput() {
  clearTimeout(scanTimeout); // מבטל כל סריקה קודמת

  scanTimeout = setTimeout(() => {
    handleScan(); // מפעיל סריקה אחרי הפסקה קצרה
  }, 300); // 300 אלפיות שנייה (0.3 שניות)
}

  </script>
  
</body>
</html>
