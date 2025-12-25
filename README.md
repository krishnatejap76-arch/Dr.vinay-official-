<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sai Clinic | Management</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --clinic-teal: #00a99d;
            --clinic-navy: #003366;
            --bg-light: #f4f7f9;
        }

        body {
            font-family: 'Inter', sans-serif;
            margin: 0;
            background-color: var(--bg-light);
        }

        /* Top Header - Profile on Left */
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
