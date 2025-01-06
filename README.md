<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FI Data Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 50px;
        }
        form {
            max-width: 600px;
            margin: auto;
        }
        input, textarea, button {
            display: block;
            width: 100%;
            margin-bottom: 10px;
            padding: 8px;
        }
        textarea {
            resize: vertical;
        }
    </style>
</head>
<body>

    <h2>FI Data Form</h2>
    <form id="fiForm">
        <label for="fiDate">FI Initiate Date:</label>
        <input type="text" id="fiDate" readonly>

        <label for="wheelsId">Wheels ID:</label>
        <input type="text" id="wheelsId" placeholder="Enter Wheels ID" required>

        <label for="customerName">Customer Name:</label>
        <input type="text" id="customerName" placeholder="Enter Customer Name" required>

        <label for="contactNo">Contact No:</label>
        <input type="text" id="contactNo" placeholder="Enter Contact No" required>

        <label for="resiAddress">Resi Address:</label>
        <textarea id="resiAddress" placeholder="Enter Resi Address" ></textarea>

        <label for="resiPinCode">Resi Pin Code:</label>
        <input type="text" id="resiPinCode" placeholder="Enter Resi Pin Code" >

        <label for="officeAddress">Office Address:</label>
        <textarea id="officeAddress" placeholder="Enter Office Address" ></textarea>

        <label for="officePinCode">Office Pin Code:</label>
        <input type="text" id="officePinCode" placeholder="Enter Office Pin Code" >

        <label for="particulars">Particulars:</label>
        <textarea id="particulars" placeholder="Enter Particulars" required></textarea>

        <label for="pan">PAN:</label>
        <input type="text" id="pan" placeholder="Enter PAN" required>

        <button type="submit">Submit</button>
    </form>

    <script>
        function formatDate(date) {
            const options = { day: '2-digit', month: 'short', year: 'numeric' };
            return new Intl.DateTimeFormat('en-US', options).format(date).replace(/,/g, '');
        }

        document.addEventListener('DOMContentLoaded', () => {
            const fiDateInput = document.getElementById('fiDate');
            fiDateInput.value = formatDate(new Date());
        });

        document.getElementById('fiForm').addEventListener('submit', async (e) => {
            e.preventDefault();

            const data = {
                fiDate: document.getElementById('fiDate').value,
                wheelsId: document.getElementById('wheelsId').value,
                customerName: document.getElementById('customerName').value,
                contactNo: document.getElementById('contactNo').value,
                resiAddress: document.getElementById('resiAddress').value,
                resiPinCode: document.getElementById('resiPinCode').value,
                officeAddress: document.getElementById('officeAddress').value,
                officePinCode: document.getElementById('officePinCode').value,
                particulars: document.getElementById('particulars').value,
                pan: document.getElementById('pan').value
            };

            try {
                const response = await fetch('https://script.google.com/macros/s/AKfycbyxoZUQsDtCKv9gbeKHFaXxTPWn6K8gvfHPJTUcB85H_odWjgOfPVqV63Jrs-_n3VY_/exec', 
                   {
                    method: 'POST',
                    body: JSON.stringify(data),
                    headers: {
                        'Content-Type': 'application/json',
                    },
                });

                if (response.ok) {
                    alert('Data submitted successfully!');
                } else {
                    alert('Failed to submit data.');
                }
            } catch (error) {
                console.error('Error:', error);
            }
        });
    </script>

</body>
</html>
