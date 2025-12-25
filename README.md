<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sai Clinic | Online Pharmacy</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --clinic-teal: #00a99d; /* Matches the 'Sai' and heart-rate line */
            --clinic-navy: #003366; /* Matches the 'Clinic' text */
            --bg-light: #f9fbfc;
        }

        body {
            font-family: 'Inter', sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--bg-light);
            color: #333;
        }

        /* Top Navigation */
        nav {
            background: #ffffff;
            padding: 10px 5%;
            display: flex;
            justify-content: flex-end;
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
            text-decoration: none;
            color: var(--clinic-navy);
            font-weight: 600;
        }

        .profile-img {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            border: 2px solid var(--clinic-teal);
            object-fit: cover;
        }

        /* Branding Section */
        .header-main {
            text-align: center;
            background: #ffffff;
            padding: 40px 20px;
            border-bottom: 1px solid #eee;
        }

        .main-logo {
            max-width: 250px;
            height: auto;
            margin-bottom: 10px;
        }

        /* Product Section */
        .shop-container {
            max-width: 1100px;
            margin: 40px auto;
            padding: 0 20px;
        }

        .section-title {
            color: var(--clinic-navy);
            border-left: 5px solid var(--clinic-teal);
            padding-left: 15px;
            margin-bottom: 30px;
        }

        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
        }

        .medicine-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            transition: 0.3s ease;
        }

        .medicine-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.1);
        }

        .medicine-card img {
            width: 100%;
            height: 180px;
            object-fit: contain;
            margin-bottom: 15px;
        }

        .price-tag {
            font-size: 1.25rem;
            color: var(--clinic-teal);
            font-weight: 700;
            margin: 10px 0;
        }

        .order-btn {
            background: var(--clinic-navy);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 6px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: 0.2s;
        }

        .order-btn:hover {
            background: var(--clinic-teal);
        }

        footer {
            text-align: center;
            padding: 50px 20px;
            color: #888;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

    <nav>
        <a href="#" class="profile-container">
            <span>Admin Profile</span>
            <img src="1000018685.jpg" alt="Profile Photo" class="profile-img">
        </a>
    </nav>

    <header class="header-main">
        <img src="1000018723.png" alt="Sai Clinic Logo" class="main-logo">
        <p style="margin-top: -10px; color: #666; font-style: italic;">Dedicated to your health and care</p>
    </header>

    <main class="shop-container">
        <h2 class="section-title">Available Medicines & Supplies</h2>
        
        <div class="product-grid">
            <div class="medicine-card">
                <img src="https://via.placeholder.com/200x150?text=Medicine+A" alt="Medicine">
                <h3>General Health Tablets</h3>
                <p>Effective relief for common symptoms.</p>
                <div class="price-tag">₹150.00</div>
                <button class="order-btn">Add to Cart</button>
            </div>

            <div class="medicine-card">
                <img src="https://via.placeholder.com/200x150?text=Medicine+B" alt="Medicine">
                <h3>Immunity Support</h3>
                <p>Boost your health with essential vitamins.</p>
                <div class="price-tag">₹450.00</div>
                <button class="order-btn">Add to Cart</button>
            </div>

            <div class="medicine-card">
                <img src="https://via.placeholder.com/200x150?text=Medicine+C" alt="Medicine">
                <h3>First Aid Essentials</h3>
                <p>Complete care for minor injuries.</p>
                <div class="price-tag">₹890.00</div>
                <button class="order-btn">Add to Cart</button>
            </div>
        </div>
    </main>

    <footer>
        &copy; 2025 Sai Clinic. All rights reserved. <br>
        Professional Medical Services & Pharmacy
    </footer>

</body>
</html>
