<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Report di Sistema</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            color: #333;
        }
        .container {
            width: 50%;
            margin: 50px auto;
            padding: 20px;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        table, th, td {
            border: 1px solid #ccc;
        }
        th, td {
            padding: 10px;
            text-align: left;
        }
        th {
            background-color: #f0f0f0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Report di Sistema</h1>
        <table id="reportTable">
            <tr>
                <th>Tipo di Informazione</th>
                <th>Valore</th>
            </tr>
        </table>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            fetch('sistema.txt')
                .then(response => response.text())
                .then(data => {
                    const lines = data.split('\\n');
                    const info = {};
                    lines.forEach(line => {
                        const [key, value] = line.split(': ');
                        info[key.trim()] = value.trim();
                    });
                    
                    const reportTable = document.getElementById('reportTable');
                    
                    Object.keys(info).forEach(key => {
                        const row = document.createElement('tr');
                        const cellKey = document.createElement('td');
                        const cellValue = document.createElement('td');
                        cellKey.textContent = key;
                        cellValue.textContent = info[key];
                        row.appendChild(cellKey);
                        row.appendChild(cellValue);
                        reportTable.appendChild(row);
                    });
                })
                .catch(error => {
                    console.error('Errore nel caricamento del file di testo:', error);
                });
        });
    </script>
</body>
</html>
