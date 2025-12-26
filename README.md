<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dr. Vinay Official - Medicine Store</title>
    <style>
        :root {
            --metal-silver: #c0c0c0;
            --metal-dark: #333;
            --whatsapp-green: #25D366;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            background-color: #f0f2f5;
        }

        /* Top Header */
        header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px 20px;
            background: #ffffff;
            border-bottom: 2px solid var(--metal-silver);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .profile-img {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            object-fit: cover;
            border: 2px solid var(--metal-dark);
        }

        .search-container {
            flex-grow: 1;
            margin: 0 30px;
        }

        #medSearch {
            width: 100%;
            padding: 10px 15px;
            border-radius: 20px;
            border: 1px solid #ccc;
            outline: none;
        }

        /* SCREW THEMED SECRET OPTION (Top Right) */
        .secret-screw {
            width: 35px;
            height: 35px;
            background: radial-gradient(circle, #eee, #999);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            border: 2px solid #777;
            position: relative;
            box-shadow: 2px 2px 5px rgba(0,0,0,0.2);
        }

        /* The Screw Slot (X) */
        .secret-screw::before, .secret-screw::after {
            content: "";
            position: absolute;
            background: #444;
            width: 3px;
            height: 18px;
            border-radius: 1px;
        }
        .secret-screw::before { transform: rotate(45deg); }
        .secret-screw::after { transform: rotate(-45deg); }

        /* Company Logo Section */
        .logo-center {
            text-align: center;
            padding: 20px 0;
            background: #fff;
        }

        .company-logo {
            max-height: 100px; /* Visible but not overwhelming */
            width: auto;
        }

        /* Medicine List Styling */
        .medicine-list {
            max-width: 600px;
            margin: 20px auto;
            padding: 0 15px;
        }

        .medicine-card {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #fff;
            margin-bottom: 12px;
            padding: 20px;
            border-radius: 8px;
            border-left: 10px solid var(--metal-dark); /* Screw-themed vertical bar */
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }

        .med-details h3 { margin: 0; font-size: 1.2rem; }
        .med-details p { margin: 5px 0 0; color: #555; }

        .buy-btn {
            background-color: var(--whatsapp-green);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .buy-btn:active { transform: scale(0.95); }

        /* Admin Modal */
        #adminModal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 0 20px rgba(0,0,0,0.3);
            z-index: 2001;
            width: 300px;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 2000;
        }

        .admin-input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
        }
    </style>
</head>
<body>

    <header>
        <img src="https://github.com/krishnatejap76-arch/Dr.vinay-official-/blob/main/IMG-20251223-WA0003.jpg?raw=true" alt="Profile" class="profile-img">
        
        <div class="search-container">
            <input type="text" id="medSearch" placeholder="Search for a medicine..." onkeyup="filterMeds()">
        </div>

        <div class="secret-screw" onclick="checkSecret()" title="Admin Access"></div>
    </header>

    <div class="logo-center">
        <img src="https://github.com/krishnatejap76-arch/Dr.vinay-official-/blob/main/image.png?raw=true" alt="Dr. Vinay Official Logo" class="company-logo">
    </div>

    <div class="medicine-list" id="medList">
        <div class="medicine-card">
            <div class="med-details">
                <h3>Paracetamol 500mg</h3>
                <p>Relief from fever and pain.</p>
            </div>
            <button class="buy-btn" onclick="buyOnWhatsApp('Paracetamol 500mg')">Buy</button>
        </div>
    </div>

    <div class="overlay" id="overlay" onclick="closeAdmin()"></div>
    <div id="adminModal">
        <h2 style="margin-top:0;">Update Medicine</h2>
        <input type="text" id="newMedName" class="admin-input" placeholder="Medicine Name">
        <input type="text" id="newMedDesc" class="admin-input" placeholder="Description/Price">
        <button onclick="addNewMed()" style="width:100%; padding:10px; background:var(--metal-dark); color:white; border:none; border-radius:5px; cursor:pointer;">Update List</button>
    </div>

    <script>
        const myWhatsApp = "919966021974";

        // 1. Secret Access Logic
        function checkSecret() {
            const code = prompt("Enter Secret Code:");
            if (code === "dr vinay official") {
                document.getElementById('adminModal').style.display = 'block';
                document.getElementById('overlay').style.display = 'block';
            } else {
                alert("Incorrect Secret Code");
            }
        }

        function closeAdmin() {
            document.getElementById('adminModal').style.display = 'none';
            document.getElementById('overlay').style.display = 'none';
        }

        // 2. Add/Update Medicine
        function addNewMed() {
            const name = document.getElementById('newMedName').value;
            const desc = document.getElementById('newMedDesc').value;
            if (name && desc) {
                const list = document.getElementById('medList');
                const div = document.createElement('div');
                div.className = 'medicine-card';
                div.innerHTML = `
                    <div class="med-details">
                        <h3>${name}</h3>
                        <p>${desc}</p>
                    </div>
                    <button class="buy-btn" onclick="buyOnWhatsApp('${name}')">Buy</button>
                `;
                list.appendChild(div);
                closeAdmin();
                document.getElementById('newMedName').value = '';
                document.getElementById('newMedDesc').value = '';
            }
        }

        // 3. Search Bar
        function filterMeds() {
            const input = document.getElementById('medSearch').value.toLowerCase();
            const cards = document.getElementsByClassName('medicine-card');
            for (let card of cards) {
                const title = card.querySelector('h3').innerText.toLowerCase();
                card.style.display = title.includes(input) ? "flex" : "none";
            }
        }

        // 4. WhatsApp Integration
        function buyOnWhatsApp(medName) {
            const userName = prompt("Enter your Name:");
            const address = prompt("Enter your Delivery Address:");
            if (userName && address) {
                const text = `Order Details:\nMedicine: ${medName}\nCustomer: ${userName}\nAddress: ${address}`;
                window.open(`https://wa.me/${myWhatsApp}?text=${encodeURIComponent(text)}`, '_blank');
            } else {
                alert("Please fill in your details to buy.");
            }
        }
    </script>
</body>
</html>
