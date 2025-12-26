<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dr. Vinay Official - Medical Store</title>
    <style>
        :root {
            --steel: #b0b0b0;
            --dark-metal: #333;
            --screw-slot: #444;
        }

        body {
            font-family: 'Segoe UI', sans-serif;
            margin: 0;
            background-color: #e9e9e9;
        }

        /* Header */
        header {
            display: flex;
            align-items: center;
            background: #fff;
            padding: 10px 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        /* SCREW THEMED SECRET OPTION */
        .secret-screw {
            width: 35px;
            height: 35px;
            background: radial-gradient(circle, #ddd, #888);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            border: 2px solid #666;
            position: relative;
            margin-right: 15px;
            box-shadow: inset 2px 2px 5px rgba(255,255,255,0.5), 2px 2px 4px rgba(0,0,0,0.3);
        }

        /* The 'X' slot on the screw head */
        .secret-screw::before, .secret-screw::after {
            content: "";
            position: absolute;
            background: var(--screw-slot);
            border-radius: 2px;
        }
        .secret-screw::before { width: 4px; height: 20px; transform: rotate(45deg); }
        .secret-screw::after { width: 4px; height: 20px; transform: rotate(-45deg); }

        .profile-img {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            object-fit: cover;
            border: 1px solid #ccc;
        }

        .search-container {
            flex-grow: 1;
            margin: 0 20px;
        }

        #searchInput {
            width: 100%;
            padding: 10px 15px;
            border-radius: 25px;
            border: 1px solid #bbb;
            outline: none;
        }

        /* Center Logo Sizing */
        .main-logo-area {
            text-align: center;
            padding: 15px 0;
        }

        .company-logo {
            height: 70px;
            width: auto;
        }

        /* Vertical Medicine List - Screw Shaped */
        .medicine-list {
            max-width: 600px;
            margin: 20px auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .medicine-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: linear-gradient(90deg, #d8d8d8 0%, #ffffff 15%);
            padding: 15px 25px;
            border-radius: 8px;
            border-left: 12px solid var(--dark-metal); /* The Screw Shank */
            box-shadow: 4px 4px 0px #bbb;
            position: relative;
        }

        .med-info h3 { margin: 0; font-size: 1.1rem; color: #222; }
        .med-info p { margin: 5px 0 0; color: #666; font-size: 0.9rem; }

        .buy-btn {
            background-color: #25D366;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
        }

        /* Admin Panel */
        #adminPanel {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 25px;
            border: 4px solid var(--dark-metal);
            z-index: 2000;
            border-radius: 10px;
            width: 280px;
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
        <div class="secret-screw" onclick="openAdmin()" title="Admin Access"></div>
        
        <img src="https://github.com/krishnatejap76-arch/Dr.vinay-official-/blob/main/IMG-20251223-WA0003.jpg?raw=true" class="profile-img" alt="Profile">

        <div class="search-container">
            <input type="text" id="searchInput" placeholder="Search for medicine..." onkeyup="search()">
        </div>
    </header>

    <div class="main-logo-area">
        <img src="https://github.com/krishnatejap76-arch/Dr.vinay-official-/blob/main/image.png?raw=true" class="company-logo" alt="Company Logo">
    </div>

    <div class="medicine-list" id="medContainer">
        <div class="medicine-row">
            <div class="med-info">
                <h3>Example Medicine</h3>
                <p>Dosage: 500mg | Price: ₹150</p>
            </div>
            <button class="buy-btn" onclick="buy('Example Medicine')">Buy</button>
        </div>
    </div>

    <div class="overlay" id="overlay" onclick="closeAdmin()"></div>
    <div id="adminPanel">
        <h2 style="margin-top:0;">Add Medicine</h2>
        <input type="text" id="mName" placeholder="Name" style="width:100%; margin-bottom:10px; padding:8px;"><br>
        <input type="text" id="mDetails" placeholder="Details/Price" style="width:100%; margin-bottom:15px; padding:8px;"><br>
        <button onclick="addMed()" style="width:100%; padding:10px; background:#333; color:white; border:none; cursor:pointer;">Update List</button>
    </div>

    <script>
        const phone = "+919966021974";

        function openAdmin() {
            let code = prompt("Enter Secret Code:");
            if (code === "dr vinay official") {
                document.getElementById('adminPanel').style.display = 'block';
                document.getElementById('overlay').style.display = 'block';
            } else {
                alert("Wrong Code!");
            }
        }

        function closeAdmin() {
            document.getElementById('adminPanel').style.display = 'none';
            document.getElementById('overlay').style.display = 'none';
        }

        function addMed() {
            let name = document.getElementById('mName').value;
            let details = document.getElementById('mDetails').value;
            if(name && details) {
                let html = `
                <div class="medicine-row">
                    <div class="med-info">
                        <h3>${name}</h3>
                        <p>${details}</p>
                    </div>
                    <button class="buy-btn" onclick="buy('${name}')">Buy</button>
                </div>`;
                document.getElementById('medContainer').innerHTML += html;
                closeAdmin();
            }
        }

        function search() {
            let filter = document.getElementById('searchInput').value.toUpperCase();
            let rows = document.getElementsByClassName('medicine-row');
            for (let i = 0; i < rows.length; i++) {
                let name = rows[i].querySelector('h3').innerText;
                rows[i].style.display = name.toUpperCase().indexOf(filter) > -1 ? "" : "none";
            }
        }

        function buy(medName) {
            let name = prompt("Enter Your Name:");
            let addr = prompt("Enter Your Address:");
            if(name && addr) {
                let msg = encodeURIComponent(`Order Details:\nMedicine: ${medName}\nCustomer: ${name}\nAddress: ${addr}`);
                window.open(`https://wa.me/${phone}?text=${msg}`, '_blank');
            }
        }
    </script>
</body>
</html>
