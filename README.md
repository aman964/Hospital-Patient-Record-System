<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Hospital Patient Record System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f6f8;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
      color: #333;
    }
    .container {
      max-width: 800px;
      margin: auto;
      background: #fff;
      padding: 20px;
      box-shadow: 0 0 15px rgba(0,0,0,0.1);
      border-radius: 10px;
    }
    input, button {
      padding: 10px;
      margin: 5px 0;
      width: 100%;
      box-sizing: border-box;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 15px;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
    }
    th {
      background-color: #e2e8f0;
    }
    .btn {
      background-color: #2b6cb0;
      color: white;
      border: none;
      cursor: pointer;
    }
    .btn:hover {
      background-color: #2c5282;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Hospital Patient Record System</h1>

    <input type="number" id="id" placeholder="Patient ID" />
    <input type="text" id="name" placeholder="Patient Name" />
    <input type="number" id="age" placeholder="Patient Age" />
    <input type="text" id="disease" placeholder="Disease" />
    <button class="btn" onclick="addPatient()">Add Patient</button>

    <input type="number" id="searchId" placeholder="Enter ID to Search/Delete" />
    <button class="btn" onclick="searchPatient()">Search Patient</button>
    <button class="btn" onclick="deletePatient()">Delete Patient</button>

    <h3>All Patient Records</h3>
    <table id="patientTable">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Age</th>
          <th>Disease</th>
        </tr>
      </thead>
      <tbody>
        <!-- Patient records will appear here -->
      </tbody>
    </table>
  </div>

  <script>
    let patients = [];

    function addPatient() {
      const id = parseInt(document.getElementById("id").value);
      const name = document.getElementById("name").value.trim();
      const age = parseInt(document.getElementById("age").value);
      const disease = document.getElementById("disease").value.trim();

      if (!id || !name || !age || !disease) {
        alert("Please fill all fields!");
        return;
      }

      // Check duplicate ID
      if (patients.some(p => p.id === id)) {
        alert("Patient with this ID already exists!");
        return;
      }

      patients.unshift({ id, name, age, disease });
      displayAll();
      clearInputs();
    }

    function deletePatient() {
      const searchId = parseInt(document.getElementById("searchId").value);
      const beforeCount = patients.length;
      patients = patients.filter(p => p.id !== searchId);

      if (patients.length === beforeCount) {
        alert("No patient found with this ID.");
      } else {
        alert("Patient deleted successfully.");
      }
      displayAll();
    }

    function searchPatient() {
      const searchId = parseInt(document.getElementById("searchId").value);
      const patient = patients.find(p => p.id === searchId);
      if (patient) {
        alert(Found:\nName: ${patient.name}\nAge: ${patient.age}\nDisease: ${patient.disease});
      } else {
        alert("Patient not found.");
      }
    }

    function displayAll() {
      const tbody = document.getElementById("patientTable").querySelector("tbody");
      tbody.innerHTML = "";
      patients.forEach(p => {
        const row = `<tr>
          <td>${p.id}</td>
          <td>${p.name}</td>
          <td>${p.age}</td>
          <td>${p.disease}</td>
        </tr>`;
        tbody.innerHTML += row;
      });
    }

    function clearInputs() {
      document.getElementById("id").value = "";
      document.getElementById("name").value = "";
      document.getElementById("age").value = "";
      document.getElementById("disease").value = "";
    }
  </script>

</body>
</html>
