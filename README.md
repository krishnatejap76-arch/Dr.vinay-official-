<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dr. Vinay Official - Medical Store</title>
    <style>
        :root {
            --screw-silver: #b0b0b0;
            --screw-dark: #4a4a4a;
            --accent-blue: #007bff;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            background-color: #f4f4f4;
        }

        /* Top Navigation Bar */
        header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px 20px;
            background: #fff;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .profile-section {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .profile-img {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            object-fit: cover;
            border: 2px solid var(--screw-silver);
        }

        /* Secret Button - Hidden look */
        #secret-access {
            background: transparent;
            border: none;
            color: #eee; /* Faded so it's not obvious */
            cursor: pointer;
            font-size: 10px;
        }

        .search-container {
            flex-grow: 1;
            text-align: center;
            margin: 0 20px;
        }

        #medicineSearch {
            width: 60%;
            padding: 10px;
            border-radius: 20px;
            border: 1px solid #ccc;
        }

        /* Center Logo Section */
        .hero-logo {
            text-align: center;
            padding: 20px;
            background: white;
        }

        .company-logo {
            max-width: 200px;
            height: auto;
        }

        /* Medicine List Styling - Screw Theme */
        .medicine-container {
            max-width: 800px;
            margin: 20px auto;
            padding: 10px;
        }

        .medicine-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: linear-gradient(90deg, #e0e0e0, #ffffff);
            margin-bottom: 15px;
            padding: 15px 25px;
            border-radius: 10px;
            border-left: 8px solid var(--screw-dark); /* Screw-like edge */
            box-shadow: 3px 3px 10px rgba(0,0,0,0.1);
            position: relative;
        }

        /* Screw head decoration */
        .medicine-row::before {
            content: '+';
            position: absolute;
            left: -15px;
            background: #888;
            color: #444;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            text-align: center;
            line-height: 18px;
            font-weight: bold;
            box-shadow: inset 1px 1px 2px #fff;
        }

        .buy-btn {
            background-color: #25D366;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }

        /* Admin Modal */
        #admin-panel {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 30px;
            box-shadow: 0 0 20px rgba(0,0,0,0.5);
            z-index: 2000;
            border-radius: 10px;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 1500;
        }
    </style>
</head>
<body>

<header>
    <div class="profile-section">
        <button id="secret-access" onclick="checkSecret()">⚙</button>
        <img src="https://github.com/krishnatejap76-arch/Dr.vinay-official-/blob/main/IMG-20251223-WA0003.jpg?raw=true" alt="Dr Vinay" class="profile-img">
    </div>

    <div class="search-container">
        <input type="text" id="medicineSearch" placeholder="Search medicine..." onkeyup="filterMedicine()">
    </div>
</header>

<div class="hero-logo">
    <img src="https://via.placeholder.com/150?text=COMPANY+LOGO" alt="Company Logo" class="company-logo">
    <h1>Dr. Vinay Official Medicines</h1>
</div>

<div class="medicine-container" id="medList">
    <div class="medicine-row">
        <div>
            <strong class="med-name">Paracetamol 500mg</strong>
            <p style="margin:5px 0; font-size: 0.9em; color: #666;">Pain relief and fever.</p>
        </div>
        <button class="buy-btn" onclick="buyMedicine('Paracetamol 500mg')">Buy</button>
    </div>
    
    <div class="medicine-row">
        <div>
            <strong class="med-name">Amoxicillin</strong>
            <p style="margin:5px 0; font-size: 0.9em; color: #666;">Antibiotic treatment.</p>
        </div>
        <button class="buy-btn" onclick="buyMedicine('Amoxicillin')">Buy</button>
    </div>
</div>

<div class="overlay" id="overlay"></div>
<div id="admin-panel">
    <h3>Admin Control Panel</h3>
    <input type="text" id="newMedName" placeholder="Medicine Name"><br><br>
    <input type="text" id="newMedDesc" placeholder="Description"><br><br>
    <button onclick="addMedicine()">Add to List</button>
    <button onclick="closeAdmin()">Close</button>
</div>

<script>
    const whatsappNumber = "+919966021974";

    // 1. Secret Access Logic
    function checkSecret() {
        const code = prompt("Enter Secret Admin Code:");
        if (code === "dr vinay official") {
            document.getElementById('admin-panel').style.display = 'block';
            document.getElementById('overlay').style.display = 'block';
        } else {
            alert("Unauthorized access!");
        }
    }

    function closeAdmin() {
        document.getElementById('admin-panel').style.display = 'none';
        document.getElementById('overlay').style.display = 'none';
    }

    // 2. Add Medicine Logic
    function addMedicine() {
        const name = document.getElementById('newMedName').value;
        const desc = document.getElementById('newMedDesc').value;

        if(name && desc) {
            const container = document.getElementById('medList');
            const row = document.createElement('div');
            row.className = 'medicine-row';
            row.innerHTML = `
                <div>
                    <strong class="med-name">${name}</strong>
                    <p style="margin:5px 0; font-size: 0.9em; color: #666;">${desc}</p>
                </div>
                <button class="buy-btn" onclick="buyMedicine('${name}')">Buy</button>
            `;
            container.appendChild(row);
            closeAdmin();
            alert("Medicine added successfully!");
        }
    }

    // 3. Search Logic
    function filterMedicine() {
        const input = document.getElementById('medicineSearch').value.toUpperCase();
        const rows = document.getElementsByClassName('medicine-row');

        for (let i = 0; i < rows.length; i++) {
            let name = rows[i].getElementsByClassName('med-name')[0].innerText;
            if (name.toUpperCase().indexOf(input) > -1) {
                rows[i].style.display = "";
            } else {
                rows[i].style.display = "none";
            }
        }
    }

    // 4. WhatsApp Integration
    function buyMedicine(medName) {
        const userName = prompt("Please enter your Full Name:");
        const userAddress = prompt("Please enter your Delivery Address:");
        
        if (userName && userAddress) {
            const message = `Hello Dr. Vinay, I want to buy:\n\n*Medicine:* ${medName}\n*Customer:* ${userName}\n*Address:* ${userAddress}`;
            const encodedMessage = encodeURIComponent(message);
            window.open(`https://wa.me/${whatsappNumber}?text=${encodedMessage}`, '_blank');
        } else {
            alert("Name and Address are required to proceed.");
        }
    }
</script>

</body>
</html>
