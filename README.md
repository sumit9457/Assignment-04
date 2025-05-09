
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Domain Reminder System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f2f2f2;
      padding: 20px;
      display: flex;
      justify-content: center;
    }

    .container {
      width: 380px;
      background-color: white;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-top: 10px;
      font-weight: bold;
    }

    input[type="text"],
    input[type="date"] {
      width: 100%;
      padding: 8px;
      margin-top: 5px;
      box-sizing: border-box;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    .row {
      display: flex;
      gap: 20px;
      justify-content: space-between;
    }

    .row input {
      flex: 1;
    }

    .buttons {
      margin-top: 15px;
      display: flex;
      gap: 10px;
    }

    button {
      flex: 1;
      padding: 10px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .submit-btn {
      background-color: #007bff;
      color: white;
    }

    .reset-btn {
      background-color: #f0f0f0;
      color: black;
    }

    .error {
      color: red;
      font-size: 12px;
      margin-top: 3px;
    }

    table {
      margin-top: 20px;
      width: 100%;
      border-collapse: collapse;
    }

    th, td {
      border: 1px solid #ccc;
      padding: 8px;
      text-align: center;
    }

    th {
      background-color: #f8f8f8;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>Domain Reminder System</h2>
    <form id="domainForm">
      <label for="domainId">Domain ID</label>
      <input type="text" id="domainId" name="domainId">
      <div id="domainIdError" class="error"></div>

      <label for="domainName">Domain Name</label>
      <input type="text" id="domainName" name="domainName">
      <div id="domainNameError" class="error"></div>

      <label for="vendorName">Vendor Name</label>
      <input type="text" id="vendorName" name="vendorName">
      <div id="vendorNameError" class="error"></div>

      <div class="row">
        <div>
          <label for="purchaseDate">Domain Purchase Date</label>
          <input type="date" id="purchaseDate" name="purchaseDate">
          <div id="purchaseDateError" class="error"></div>
        </div>
        <div>
          <label for="expiryDate">Domain Expiry Date</label>
          <input type="date" id="expiryDate" name="expiryDate">
          <div id="expiryDateError" class="error"></div>
        </div>
      </div>

      <div class="buttons">
        <button type="submit" class="submit-btn">Submit</button>
        <button type="button" class="reset-btn" onclick="resetForm()">Reset</button>
      </div>
    </form>

    <table id="outputTable">
      <thead>
        <tr>
          <th>Domain ID</th>
          <th>Domain Purchase Date</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </div>

  <script>
    const form = document.getElementById('domainForm');

    form.addEventListener('submit', function (e) {
      e.preventDefault();

      // Clear previous errors
      document.querySelectorAll('.error').forEach(el => el.textContent = '');

      // Get input values
      const domainId = document.getElementById('domainId').value.trim();
      const domainName = document.getElementById('domainName').value.trim();
      const vendorName = document.getElementById('vendorName').value.trim();
      const purchaseDate = document.getElementById('purchaseDate').value.trim();
      const expiryDate = document.getElementById('expiryDate').value.trim();

      let valid = true;

      if (!domainId) {
        document.getElementById('domainIdError').textContent = 'Domain ID cannot be blank';
        valid = false;
      }
      if (!domainName) {
        document.getElementById('domainNameError').textContent = 'Domain Name cannot be blank';
        valid = false;
      }
      if (!vendorName) {
        document.getElementById('vendorNameError').textContent = 'Vendor Name cannot be blank';
        valid = false;
      }
      if (!purchaseDate) {
        document.getElementById('purchaseDateError').textContent = 'Purchase Date cannot be blank';
        valid = false;
      }
      if (!expiryDate) {
        document.getElementById('expiryDateError').textContent = 'Expiry Date cannot be blank';
        valid = false;
      }

      if (valid) {
        const table = document.getElementById('outputTable').querySelector('tbody');
        const row = document.createElement('tr');
        row.innerHTML = `
          <td>${domainId}</td>
          <td>${purchaseDate}</td>
        `;
        table.appendChild(row);
        resetForm();
      }
    });

    function resetForm() {
      form.reset();
      document.querySelectorAll('.error').forEach(el => el.textContent = '');
    }
  </script>

</body>
</html>

