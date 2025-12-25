<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sai Clinic | Digital Pharmacy</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --clinic-teal: #00a99d;
            --clinic-navy: #003366;
            --bg-color: #fcfcfc;
        }

        body {
            font-family: 'Inter', sans-serif;
            margin: 0;
            background-color: var(--bg-color);
            color: #1e293b;
        }

        /* Top Left Profile Header */
        .profile-header {
            background: #ffffff;
            padding: 10px 30px;
            display: flex;
            align-items: center;
            border-bottom: 1px solid #eee;
        }

        .profile-img {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: 2px solid var(--clinic-teal);
            object-fit: cover;
            margin-right: 12px;
        }

        .profile-name {
            font-weight: 700;
            color: var(--clinic-navy);
            font-size: 0.95rem;
        }

        /* Top Center Logo (Larger) */
        .logo-section {
            display: flex;
            justify-content: center;
            padding: 40px 20px 20px 20px;
        }

        .main-logo {
            width: 400px; /* Large professional size */
            max-width: 85%;
            height: auto;
        }

        /* Medicine Display */
        .container {
            max-width: 1100px;
            margin: 30px auto 100px auto;
            padding: 0 20px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 25px;
        }

        .med-card {
            background: #fff;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.04);
            border-top: 5px solid var(--clinic-teal);
        }

        /* INVISIBLE SECRET OPTION */
        .secret-screw {
            position: fixed;
            bottom: 10px;
            right: 10px;
            color: var(--bg-color); /* Matches background exactly */
            cursor: pointer;
            font-size: 14px;
            z-index: 9999;
        }

        .secret-screw:hover {
            color: #f0f0f0; /* Faintly visible only on hover */
        }

        /* Admin Management Panel */
        #adminPanel {
            display: none;
            position: fixed;
            top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 35px;
            border-radius: 20px;
            box-shadow: 0 30px 60px rgba(0,0,0,0.3);
            z-index: 10001;
            width: 350px;
            border: 1px solid #ddd;
        }

        #adminPanel input, #adminPanel textarea {
            width: 100%;
            margin-bottom: 15px;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 8px;
            box-sizing: border-box;
        }

        .submit-btn {
            width: 100%;
            padding: 12px;
            background: var(--clinic-navy);
            color: white;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            backdrop-filter: blur(3px);
            z-index: 10000;
        }
    </style>
</head>
<body>

    <div class="profile-header">
        <img src="https://raw.githubusercontent.com/krishnatejap76-arch/Dr.vinay-official-/main/IMG-20251223-WA0003.jpg" alt="Dr. Vinay" class="profile-img">
        <span class="profile-name">Dr. Vinay Official</span>
    </div>

    <div class="logo-section">
        <img src="https://raw.githubusercontent.com/krishnatejap76-arch/Dr.vinay-official-/main/image.png" alt="Sai Clinic Logo" class="main-logo">
    </div>

    <div class="container">
        <h2 style="color: var(--clinic-navy); text-align: center; margin-bottom: 40px;">Available Medicine List</h2>
        <div class="grid" id="medList">
            </div>
    </div>

    <i class="fas fa-screwdriver-wrench secret-screw" onclick="verifyUser()"></i>

    <div class="overlay" id="overlay" onclick="closeAdmin()"></div>

    <div id="adminPanel">
        <h3 style="margin-top:0; color: var(--clinic-navy);">Add New Entry</h3>
        <input type="text" id="mName" placeholder="Medicine Name">
        <textarea id="mDesc" rows="4" placeholder="Medicine Details"></textarea>
        <button class="submit-btn" onclick="saveMed()">Add to Website</button>
        <button onclick="localStorage.removeItem('sai_inventory'); location.reload();" style="margin-top:20px; background:none; border:none; color:red; cursor:pointer; width:100%; font-size:11px;">Reset Website Content</button>
    </div>

    <script>
        window.onload = loadData;

        function verifyUser() {
            let code = prompt("Enter Secret Access Code:");
            if (code === "dr.vinay official") {
                document.getElementById('adminPanel').style.display = 'block';
                document.getElementById('overlay').style.display = 'block';
            } else {
                alert("Incorrect Access Code.");
            }
        }

        function closeAdmin() {
            document.getElementById('adminPanel').style.display = 'none';
            document.getElementById('overlay').style.display = 'none';
        }

        function saveMed() {
            const name = document.getElementById('mName').value;
            const desc = document.getElementById('mDesc').value;
            if(name && desc) {
                let items = JSON.parse(localStorage.getItem('sai_inventory') || '[]');
                items.push({name, desc});
                localStorage.setItem('sai_inventory', JSON.stringify(items));
                document.getElementById('mName').value = '';
                document.getElementById('mDesc').value = '';
                closeAdmin();
                loadData();
            }
        }

        function loadData() {
            const list = document.getElementById('medList');
            let items = JSON.parse(localStorage.getItem('sai_inventory') || '[]');
            if(items.length === 0) {
                list.innerHTML = `<p style="grid-column: 1/-1; text-align:center; color:#999;">The medicine list is currently empty.</p>`;
                return;
            }
            list.innerHTML = items.map(i => `
                <div class="med-card">
                    <h3>${i.name}</h3>
                    <p>${i.desc}</p>
                </div>
            `).join('');
        }
    </script>
</body>
</html>
header {
            background: #ffffff;
            height: 80px;
            display: flex;
            align-items: center;
            padding: 0 40px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        /* Profile Top Left */
        .header-left {
            flex: 1;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .profile-img {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            border: 2px solid var(--clinic-teal);
            object-fit: cover;
        }

        .profile-info {
            line-height: 1.2;
        }

        .profile-info b {
            display: block;
            font-size: 14px;
            color: var(--clinic-navy);
        }

        .profile-info span {
            font-size: 12px;
            color: #64748b;
        }

        /* Logo Top Center */
        .header-center {
            flex: 2;
            display: flex;
            justify-content: center;
        }

        .main-logo {
            height: 55px;
            width: auto;
        }

        /* Empty flex to balance the header right side */
        .header-right {
            flex: 1;
        }

        /* Product Grid Section */
        .container {
            max-width: 1200px;
            margin: 50px auto;
            padding: 0 20px;
        }

        .section-header {
            text-align: center;
            margin-bottom: 40px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 25px;
        }

        .med-card {
            background: #ffffff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05);
            border: 1px solid #e2e8f0;
            transition: transform 0.2s;
        }

        .med-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1);
        }

        .med-card h3 {
            margin: 0 0 10px 0;
            color: var(--clinic-navy);
            font-size: 1.25rem;
        }

        .med-card p {
            margin: 0;
            color: #475569;
            font-size: 15px;
            line-height: 1.6;
        }

        /* SECRET OPTION - Hidden from End Users */
        .secret-screw {
            position: fixed;
            bottom: 15px;
            right: 15px;
            color: rgba(0,0,0,0.02); /* Almost invisible */
            cursor: pointer;
            font-size: 16px;
            transition: color 0.3s;
            z-index: 9999;
        }

        .secret-screw:hover {
            color: rgba(0,0,0,0.2); /* Slightly visible when you know where to look */
        }

        /* Admin Popup */
        #adminPanel {
            display: none;
            position: fixed;
            top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 20px 25px -5px rgba(0,0,0,0.2);
            z-index: 10001;
            width: 350px;
            border: 1px solid var(--clinic-teal);
        }

        #adminPanel input, #adminPanel textarea {
            width: 100%;
            margin-bottom: 15px;
            padding: 12px;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            box-sizing: border-box;
            font-family: inherit;
        }

        .btn-update {
            width: 100%;
            padding: 12px;
            background: var(--clinic-navy);
            color: white;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.6);
            backdrop-filter: blur(4px);
            z-index: 10000;
        }

        @media (max-width: 768px) {
            header { padding: 0 15px; }
            .profile-info { display: none; }
            .main-logo { height: 40px; }
        }
    </style>
</head>
<body>

    <header>
        <div class="header-left">
            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/Dr.vinay-official-/main/IMG-20251223-WA0003.jpg" alt="Dr. Vinay" class="profile-img">
            <div class="profile-info">
                <b>Dr. Vinay</b>
                <span>Sai Clinic Admin</span>
            </div>
        </div>

        <div class="header-center">
            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/Dr.vinay-official-/main/image.png" alt="Sai Clinic Logo" class="main-logo">
        </div>

        <div class="header-right"></div>
    </header>

    <div class="container">
        <div class="section-header">
            <h2 style="color: var(--clinic-navy); font-size: 2rem;">Pharmacy Inventory</h2>
            <p style="color: #64748b;">Browse our available medicines. Contact us for latest availability.</p>
        </div>

        <div class="grid" id="medicineDisplay">
            </div>
    </div>

    <i class="fas fa-screwdriver-wrench secret-screw" onclick="openAdmin()"></i>

    <div class="overlay" id="blurOverlay" onclick="closeAdmin()"></div>

    <div id="adminPanel">
        <h3 style="margin-top:0; color: var(--clinic-navy);">Manage Inventory</h3>
        <input type="text" id="mName" placeholder="Medicine Name">
        <textarea id="mDetails" rows="4" placeholder="Description & Usage Details"></textarea>
        <button class="btn-update" onclick="submitMed()">Add to Website</button>
    </div>

    <script>
        // Load data on start
        window.onload = render;

        function openAdmin() {
            let accessCode = prompt("Enter Security Passcode:");
            if (accessCode === "dr.vinay official") {
                document.getElementById('adminPanel').style.display = 'block';
                document.getElementById('blurOverlay').style.display = 'block';
            } else {
                alert("Unauthorized Access Attempt.");
            }
        }

        function closeAdmin() {
            document.getElementById('adminPanel').style.display = 'none';
            document.getElementById('blurOverlay').style.display = 'none';
        }

        function submitMed() {
            const name = document.getElementById('mName').value;
            const details = document.getElementById('mDetails').value;
            if(name && details) {
                let storage = JSON.parse(localStorage.getItem('sai_inventory') || '[]');
                storage.push({name, details});
                localStorage.setItem('sai_inventory', JSON.stringify(storage));
                
                document.getElementById('mName').value = '';
                document.getElementById('mDetails').value = '';
                closeAdmin();
                render();
            }
        }

        function render() {
            const list = document.getElementById('medicineDisplay');
            let storage = JSON.parse(localStorage.getItem('sai_inventory') || '[]');
            
            if(storage.length === 0) {
                list.innerHTML = `<p style="grid-column: 1/-1; text-align:center; color:#94a3b8; padding: 40px;">No items in the list currently.</p>`;
                return;
            }

            list.innerHTML = storage.map(item => `
                <div class="med-card">
                    <h3>${item.name}</h3>
                    <p>${item.details}</p>
                </div>
            `).join('');
        }
    </script>
</body>
</html>
/* Top Header Area */
        header {
            background: #fff;
            padding: 15px 5%;
            display: flex;
            align-items: center;
            justify-content: center; /* Centers the logo */
            box-shadow: 0 2px 8px rgba(0,0,0,0.06);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        /* Profile - Absolute positioned to top left */
        .profile-container {
            position: absolute;
            left: 5%;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .profile-img {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: 2px solid var(--clinic-teal);
            object-fit: cover;
        }

        .profile-name {
            font-weight: 700;
            color: var(--clinic-navy);
            font-size: 0.9rem;
            display: block;
        }

        /* Logo - Centered in Header */
        .main-logo {
            max-width: 200px;
            height: auto;
        }

        /* Medicine Display Area */
        .main-container {
            max-width: 1100px;
            margin: 40px auto;
            padding: 0 20px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
        }

        .med-card {
            background: #ffffff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.04);
            border-top: 5px solid var(--clinic-teal);
            transition: 0.3s;
        }

        /* Secret Settings Screw Icon */
        .screw-btn {
            position: fixed;
            bottom: 20px;
            right: 20px;
            color: rgba(0,0,0,0.08); /* Faint icon */
            cursor: pointer;
            font-size: 18px;
            z-index: 2000;
        }

        #admin-panel {
            display: none;
            position: fixed;
            top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 0 40px rgba(0,0,0,0.3);
            z-index: 3000;
            width: 340px;
        }

        #admin-panel input, #admin-panel textarea {
            width: 100%;
            margin-bottom: 15px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 6px;
            box-sizing: border-box;
        }

        .save-btn {
            width: 100%;
            padding: 12px;
            background: var(--clinic-navy);
            color: white;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 2500;
        }

        @media (max-width: 600px) {
            .profile-name { display: none; } /* Hide name on mobile for space */
            .main-logo { max-width: 150px; }
        }
    </style>
</head>
<body>

    <header>
        <div class="profile-container">
            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/Dr.vinay-official-/main/IMG-20251223-WA0003.jpg" alt="Dr. Vinay" class="profile-img">
            <span class="profile-name">Dr. Vinay Official</span>
        </div>

        <img src="https://raw.githubusercontent.com/krishnatejap76-arch/Dr.vinay-official-/main/image.png" alt="Sai Clinic" class="main-logo">
    </header>

    <div class="main-container">
        <h2 style="color: var(--clinic-navy); border-left: 5px solid var(--clinic-teal); padding-left: 15px; margin-bottom: 30px;">Medicine Inventory</h2>
        <div class="grid" id="med-list">
            </div>
    </div>

    <i class="fas fa-screwdriver-wrench screw-btn" title="Settings" onclick="openSecret()"></i>

    <div class="overlay" id="bg-overlay" onclick="closeSecret()"></div>

    <div id="admin-panel">
        <h3 style="margin-top:0; color: var(--clinic-navy);">Add New Medicine</h3>
        <input type="text" id="m-name" placeholder="Medicine Name">
        <textarea id="m-desc" rows="3" placeholder="Medicine Details (Usage, Dosage, etc.)"></textarea>
        <button class="save-btn" onclick="addMed()">Update Inventory</button>
    </div>

    <script>
        window.onload = renderMeds;

        function openSecret() {
            let pass = prompt("Enter Administration Code:");
            if (pass === "dr.vinay official") {
                document.getElementById('admin-panel').style.display = 'block';
                document.getElementById('bg-overlay').style.display = 'block';
            } else {
                alert("Access Denied.");
            }
        }

        function closeSecret() {
            document.getElementById('admin-panel').style.display = 'none';
            document.getElementById('bg-overlay').style.display = 'none';
        }

        function addMed() {
            const name = document.getElementById('m-name').value;
            const desc = document.getElementById('m-desc').value;
            if(name && desc) {
                let items = JSON.parse(localStorage.getItem('clinic_items') || '[]');
                items.push({name, desc});
                localStorage.setItem('clinic_items', JSON.stringify(items));
                document.getElementById('m-name').value = '';
                document.getElementById('m-desc').value = '';
                closeSecret();
                renderMeds();
            }
        }

        function renderMeds() {
            const container = document.getElementById('med-list');
            let items = JSON.parse(localStorage.getItem('clinic_items') || '[]');
            if(items.length === 0) {
                container.innerHTML = `<p style="color:#999; grid-column: 1/-1; text-align: center;">Your medicine list is currently empty. Use the secret screw icon to add items.</p>`;
                return;
            }
            container.innerHTML = items.map(i => `
                <div class="med-card">
                    <h3 style="margin-top:0; color:var(--clinic-navy)">${i.name}</h3>
                    <p>${i.desc}</p>
                </div>
            `).join('');
        }
    </script>
</body>
</html>
nav {
            background: #fff;
            padding: 10px 5%;
            display: flex;
            justify-content: flex-start; /* Moves profile to the left */
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .profile-container {
            display: flex;
            align-items: center;
            gap: 12px;
            color: var(--clinic-navy);
            font-weight: 600;
        }

        .profile-img {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: 2px solid var(--clinic-teal);
            object-fit: cover;
        }

        /* Branding - Logo under the Nav */
        .branding {
            text-align: center;
            padding: 40px 20px;
            background: #fff;
            border-bottom: 1px solid #eee;
        }

        .logo-img {
            max-width: 280px; /* Larger logo display */
            height: auto;
        }

        /* Medicine Display Area */
        .container {
            max-width: 1100px;
            margin: 40px auto;
            padding: 0 20px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
        }

        .med-card {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            border-left: 6px solid var(--clinic-teal);
            position: relative;
        }

        .med-card h3 {
            margin-top: 0;
            color: var(--clinic-navy);
            font-size: 1.4rem;
        }

        .med-card p {
            color: #555;
            line-height: 1.6;
            margin-bottom: 0;
        }

        /* Secret Menu - Screw Icon */
        .screw-icon {
            position: fixed;
            bottom: 20px;
            right: 20px;
            color: rgba(0,0,0,0.05); /* Faint screw icon */
            cursor: pointer;
            font-size: 20px;
            transition: 0.3s;
        }

        .screw-icon:hover {
            color: var(--clinic-navy);
        }

        /* Admin Panel Modal */
        #admin-modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 0 50px rgba(0,0,0,0.4);
            z-index: 10001;
            width: 350px;
        }

        #admin-modal input, #admin-modal textarea {
            width: 100%;
            margin-bottom: 15px;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 6px;
            box-sizing: border-box;
        }

        .admin-btn {
            width: 100%;
            padding: 12px;
            background: var(--clinic-teal);
            color: white;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.6);
            z-index: 10000;
        }

        footer {
            text-align: center;
            padding: 60px 20px;
            color: #999;
            font-size: 0.85rem;
        }
    </style>
</head>
<body>

    <nav>
        <div class="profile-container">
            <img src="1000018685.jpg" alt="Dr. Vinay" class="profile-img">
            <span>Dr. Vinay Official</span>
        </div>
    </nav>

    <div class="branding">
        <img src="1000018723.png" alt="Sai Clinic Logo" class="logo-img">
    </div>

    <div class="container">
        <h2 style="color: var(--clinic-navy); margin-bottom: 30px;">Available Medicines</h2>
        <div class="grid" id="med-display">
            </div>
    </div>

    <i class="fas fa-screwdriver-wrench screw-icon" onclick="verifyAccess()"></i>

    <div class="overlay" id="overlay" onclick="closeAdmin()"></div>
    
    <div id="admin-modal">
        <h3 style="margin-top:0; color: var(--clinic-navy);">Add New Medicine</h3>
        <input type="text" id="new-name" placeholder="Medicine Name">
        <textarea id="new-detail" rows="4" placeholder="Medicine Details & Usage"></textarea>
        <button class="admin-btn" onclick="saveMedicine()">Update Website</button>
        <p style="text-align:center; font-size:11px; color:#999; margin-top:15px;">Sai Clinic Internal Management</p>
    </div>

    <script>
        // Initialize the website content
        window.onload = displayMedicines;

        function verifyAccess() {
            let pass = prompt("Enter Secret Access Code:");
            if (pass === "dr.vinay official") {
                document.getElementById('admin-modal').style.display = 'block';
                document.getElementById('overlay').style.display = 'block';
            } else {
                alert("Incorrect Code.");
            }
        }

        function closeAdmin() {
            document.getElementById('admin-modal').style.display = 'none';
            document.getElementById('overlay').style.display = 'none';
        }

        function saveMedicine() {
            const name = document.getElementById('new-name').value;
            const detail = document.getElementById('new-detail').value;

            if (name && detail) {
                let meds = JSON.parse(localStorage.getItem('sai_meds') || '[]');
                meds.push({ name, detail });
                localStorage.setItem('sai_meds', JSON.stringify(meds));
                
                document.getElementById('new-name').value = '';
                document.getElementById('new-detail').value = '';
                closeAdmin();
                displayMedicines();
            }
        }

        function displayMedicines() {
            const container = document.getElementById('med-display');
            let meds = JSON.parse(localStorage.getItem('sai_meds') || '[]');
            
            if(meds.length === 0) {
                container.innerHTML = `<p style="color:#888;">No medicines listed. Click the secret icon to add items.</p>`;
                return;
            }

            container.innerHTML = meds.map(m => `
                <div class="med-card">
                    <h3>${m.name}</h3>
                    <p>${m.detail}</p>
                </div>
            `).join('');
        }
    </script>
</body>
</html>
