<!DOCTYPE html>
<html lang="he" dir="rtl">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>ניהול משטחים</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
</head>

<body class="bg-gray-100 font-sans">
  <!-- Header -->
  <header class="bg-gradient-to-r from-blue-600 to-blue-400 text-white p-6 shadow">
    <div class="container mx-auto text-center">
      <h1 class="text-2xl font-bold">ניהול משטחים ומשקלי חביות</h1>
      <p class="text-sm">הזנת משקלי חביות לפי מספר משטח</p>
    </div>
  </header>

  <main class="container mx-auto p-4 space-y-6">
    <!-- הוספת משטח -->
    <section class="bg-white p-4 rounded shadow">
      <h2 class="text-lg font-bold mb-2">הוספת משטח חדש</h2>
      <div class="flex flex-col sm:flex-row items-center gap-2">
        <button onclick="addRow()" class="bg-blue-600 text-white px-4 py-2 rounded">הוסף משטח</button>
        <input type="text" placeholder="OF149875 :דוגמה" class="border p-2 rounded flex-1" />
      </div>
    </section>

    <!-- רשימת משטחים -->
    <section class="bg-white p-4 rounded shadow overflow-x-auto">
      <div class="flex flex-wrap gap-2 mb-4">
        <button onclick="printTable()" class="bg-gray-700 text-white px-4 py-2 rounded">הדפס טבלה</button>
        <button onclick="exportPDF()" class="bg-green-600 text-white px-4 py-2 rounded">ייצא ל-PDF</button>
        <button onclick="clearTable()" class="bg-red-600 text-white px-4 py-2 rounded">נקה הכל</button>
      </div>

      <table id="table" class="min-w-full table-auto border text-center">
        <thead class="bg-gray-200">
          <tr>
            <th class="p-2">מספר משטח</th>
            <th class="p-2">חבית 1 (ק"ג)</th>
            <th class="p-2">חבית 2 (ק"ג)</th>
            <th class="p-2">חבית 3 (ק"ג)</th>
            <th class="p-2">חבית 4 (ק"ג)</th>
            <th class="p-2">סה"כ משקל (ק"ג)</th>
            <th class="p-2">פעולות</th>
          </tr>
        </thead>
        <tbody id="table-body">
        </tbody>
      </table>

      <p class="mt-4 font-bold" id="summary">סיכום: 0 משטחים, 0 ק"ג סה"כ</p>
    </section>
  </main>

  <!-- Footer -->
  <footer class="bg-gray-800 text-white text-center p-4 mt-10">
    מערכת ניהול משטחים ומשקלי חביות © 2023
  </footer>

  <!-- Scripts -->
  <script>
    let rowCount = 0;

    function addRow() {
      const tbody = document.getElementById('table-body');
      const row = document.createElement('tr');
      row.className = 'bg-white border-b';

      const id = 'OF' + Math.floor(100000 + Math.random() * 900000);
      row.innerHTML = `
        <td class="p-2">${id}</td>
        <td><input type="number" class="p-1 border rounded w-20" onchange="updateWeight(this)" /></td>
        <td><input type="number" class="p-1 border rounded w-20" onchange="updateWeight(this)" /></td>
        <td><input type="number" class="p-1 border rounded w-20" onchange="updateWeight(this)" /></td>
        <td><input type="number" class="p-1 border rounded w-20" onchange="updateWeight(this)" /></td>
        <td class="total p-2 font-bold">0</td>
        <td><button onclick="removeRow(this)" class="text-red-600">🗑️</button></td>
      `;
      tbody.appendChild(row);
      rowCount++;
      updateSummary();
    }

    function removeRow(btn) {
      btn.closest('tr').remove();
      rowCount--;
      updateSummary();
    }

    function updateWeight(input) {
      const row = input.closest('tr');
      const inputs = row.querySelectorAll('input');
      let sum = 0;
      inputs.forEach(i => sum += parseFloat(i.value) || 0);
      row.querySelector('.total').innerText = sum.toFixed(1);
      updateSummary();
    }

    function updateSummary() {
      const totals = document.querySelectorAll('.total');
      let sum = 0;
      totals.forEach(t => sum += parseFloat(t.innerText) || 0);
      document.getElementById('summary').innerText = `סיכום: ${rowCount} משטחים, ${sum.toFixed(1)} ק"ג סה"כ`;
    }

    function clearTable() {
      document.getElementById('table-body').innerHTML = '';
      rowCount = 0;
      updateSummary();
    }

    function printTable() {
      window.print();
    }

    function exportPDF() {
      const {{ jsPDF }} = window.jspdf;
      const doc = new jsPDF();
      doc.text('רשימת משטחים', 10, 10);
      let y = 20;
      document.querySelectorAll('#table tbody tr').forEach(row => {
        const cells = row.querySelectorAll('td');
        const data = Array.from(cells).map(c => c.innerText.trim()).join(' | ');
        doc.text(data, 10, y);
        y += 10;
      });
      doc.save('רשימת_משטחים.pdf');
    }
  </script>
</body>

</html>
