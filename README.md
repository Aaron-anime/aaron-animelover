# aaron-animelover
A web-based tool for managing e-bike inventory, rentals, sales, and maintenance.
   <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Bike Store and Rental Management</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #3498db;
            --primary-dark: #2980b9;
            --secondary: #2ecc71;
            --secondary-dark: #27ae60;
            --danger: #e74c3c;
            --danger-dark: #c0392b;
            --warning: #f39c12;
            --warning-dark: #e67e22;
            --dark: #2c3e50;
            --darker: #1a252f;
            --light: #ecf0f1;
            --lighter: #f8f9fa;
            --gray: #95a5a6;
            --dark-gray: #7f8c8d;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            --transition: all 0.3s ease;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Poppins', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: var(--dark);
            background-color: var(--lighter);
            overflow-x: hidden;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        header {
            background: linear-gradient(135deg, var(--dark), var(--darker));
            color: white;
            padding: 1.5rem;
            text-align: center;
            box-shadow: var(--shadow);
            position: relative;
            overflow: hidden;
        }
        
        header::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary), var(--warning));
        }
        
        header h1 {
            font-size: 2.2rem;
            margin-bottom: 0.5rem;
            animation: fadeIn 0.8s ease-out;
        }
        
        header p {
            font-size: 1rem;
            opacity: 0.9;
        }
        
        nav {
            background-color: white;
            padding: 0.5rem;
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        nav ul {
            list-style-type: none;
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 0.5rem;
        }
        
        nav a {
            color: var(--dark);
            text-decoration: none;
            padding: 0.75rem 1.5rem;
            border-radius: 50px;
            transition: var(--transition);
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }
        
        nav a:hover, nav a.active {
            background-color: var(--primary);
            color: white;
            transform: translateY(-2px);
        }
        
        nav a i {
            font-size: 1rem;
        }
        
        main {
            padding: 2rem;
            max-width: 1400px;
            margin: 0 auto;
        }
        
        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }
        
        .stat-card {
            background-color: white;
            border-radius: 10px;
            padding: 1.5rem;
            box-shadow: var(--shadow);
            transition: var(--transition);
            animation: fadeIn 0.6s ease-out;
            position: relative;
            overflow: hidden;
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        
        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 5px;
            height: 100%;
            background-color: var(--primary);
        }
        
        .stat-card h3 {
            font-size: 1rem;
            color: var(--gray);
            margin-bottom: 0.5rem;
        }
        
        .stat-card .value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--dark);
        }
        
        .stat-card .icon {
            position: absolute;
            right: 1.5rem;
            top: 1.5rem;
            font-size: 2.5rem;
            opacity: 0.2;
            color: var(--primary);
        }
        
        section {
            background-color: white;
            border-radius: 10px;
            padding: 1.5rem;
            margin-bottom: 2rem;
            box-shadow: var(--shadow);
            animation: fadeIn 0.6s ease-out;
        }
        
        section h2 {
            color: var(--dark);
            border-bottom: 2px solid var(--lighter);
            padding-bottom: 0.75rem;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }
        
        section h2 i {
            color: var(--primary);
        }
        
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }
        
        .section-actions {
            display: flex;
            gap: 0.75rem;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 1.5rem 0;
            font-size: 0.95rem;
        }
        
        th, td {
            padding: 1rem;
            text-align: left;
            border-bottom: 1px solid var(--lighter);
        }
        
        th {
            background-color: var(--lighter);
            font-weight: 600;
            color: var(--dark);
            text-transform: uppercase;
            font-size: 0.8rem;
            letter-spacing: 0.5px;
        }
        
        tr:hover {
            background-color: rgba(52, 152, 219, 0.05);
        }
        
        .badge {
            display: inline-block;
            padding: 0.35rem 0.75rem;
            border-radius: 50px;
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .badge-primary {
            background-color: rgba(52, 152, 219, 0.1);
            color: var(--primary);
        }
        
        .badge-success {
            background-color: rgba(46, 204, 113, 0.1);
            color: var(--secondary);
        }
        
        .badge-warning {
            background-color: rgba(243, 156, 18, 0.1);
            color: var(--warning);
        }
        
        .badge-danger {
            background-color: rgba(231, 76, 60, 0.1);
            color: var(--danger);
        }
        
        button, .btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 50px;
            cursor: pointer;
            transition: var(--transition);
            font-weight: 500;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.95rem;
        }
        
        button:hover, .btn:hover {
            background-color: var(--primary-dark);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(52, 152, 219, 0.3);
        }
        
        button:disabled, .btn:disabled {
            background-color: var(--gray);
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .btn-sm {
            padding: 0.5rem 1rem;
            font-size: 0.85rem;
        }
        
        .btn-success {
            background-color: var(--secondary);
        }
        
        .btn-success:hover {
            background-color: var(--secondary-dark);
            box-shadow: 0 4px 8px rgba(46, 204, 113, 0.3);
        }
        
        .btn-warning {
            background-color: var(--warning);
        }
        
        .btn-warning:hover {
            background-color: var(--warning-dark);
            box-shadow: 0 4px 8px rgba(243, 156, 18, 0.3);
        }
        
        .btn-danger {
            background-color: var(--danger);
        }
        
        .btn-danger:hover {
            background-color: var(--danger-dark);
            box-shadow: 0 4px 8px rgba(231, 76, 60, 0.3);
        }
        
        .btn-outline {
            background-color: transparent;
            border: 1px solid var(--primary);
            color: var(--primary);
        }
        
        .btn-outline:hover {
            background-color: var(--primary);
            color: white;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 0.75rem 1rem;
            border: 1px solid #ddd;
            border-radius: 8px;
            margin: 0.5rem 0 1rem;
            font-family: inherit;
            font-size: 0.95rem;
            transition: var(--transition);
        }
        
        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }
        
        .form-group {
            margin-bottom: 1rem;
        }
        
        .form-row {
            display: flex;
            gap: 1rem;
        }
        
        .form-row .form-group {
            flex: 1;
        }
        
        label {
            font-weight: 500;
            font-size: 0.9rem;
            color: var(--dark);
            display: block;
            margin-bottom: 0.25rem;
        }
        
        .ebike-gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 1.5rem;
            padding: 0;
        }
        
        .ebike-card {
            background-color: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: var(--shadow);
            transition: var(--transition);
            position: relative;
        }
        
        .ebike-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        
        .ebike-card .card-img {
            height: 200px;
            overflow: hidden;
            position: relative;
        }
        
        .ebike-card .card-img img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: var(--transition);
        }
        
        .ebike-card:hover .card-img img {
            transform: scale(1.05);
        }
        
        .ebike-card .card-badge {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background-color: var(--secondary);
            color: white;
            padding: 0.25rem 0.75rem;
            border-radius: 50px;
            font-size: 0.75rem;
            font-weight: 600;
        }
        
        .ebike-card .card-content {
            padding: 1.5rem;
        }
        
        .ebike-card .card-title {
            font-size: 1.25rem;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: var(--dark);
        }
        
        .ebike-card .card-price {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 0.5rem;
        }
        
        .ebike-card .card-price small {
            font-size: 0.9rem;
            color: var(--gray);
            font-weight: 400;
        }
        
        .ebike-card .card-meta {
            display: flex;
            justify-content: space-between;
            margin-top: 1rem;
            font-size: 0.9rem;
            color: var(--gray);
        }
        
        .ebike-card .card-actions {
            display: flex;
            gap: 0.5rem;
            margin-top: 1rem;
        }
        
        .alert {
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            gap: 1rem;
            animation: fadeIn 0.5s ease-out;
        }
        
        .alert i {
            font-size: 1.5rem;
        }
        
        .alert-success {
            background-color: rgba(46, 204, 113, 0.1);
            color: var(--secondary);
            border-left: 4px solid var(--secondary);
        }
        
        .alert-info {
            background-color: rgba(52, 152, 219, 0.1);
            color: var(--primary);
            border-left: 4px solid var(--primary);
        }
        
        .alert-warning {
            background-color: rgba(243, 156, 18, 0.1);
            color: var(--warning);
            border-left: 4px solid var(--warning);
        }
        
        .alert-danger {
            background-color: rgba(231, 76, 60, 0.1);
            color: var(--danger);
            border-left: 4px solid var(--danger);
        }
        
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: var(--transition);
        }
        
        .modal.active {
            opacity: 1;
            visibility: visible;
        }
        
        .modal-content {
            background-color: white;
            border-radius: 10px;
            width: 90%;
            max-width: 600px;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            transform: translateY(20px);
            transition: var(--transition);
            position: relative;
        }
        
        .modal.active .modal-content {
            transform: translateY(0);
        }
        
        .modal-header {
            padding: 1.5rem;
            border-bottom: 1px solid var(--lighter);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .modal-header h3 {
            font-size: 1.5rem;
            color: var(--dark);
        }
        
        .modal-close {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--gray);
            transition: var(--transition);
        }
        
        .modal-close:hover {
            color: var(--danger);
            transform: rotate(90deg);
        }
        
        .modal-body {
            padding: 1.5rem;
        }
        
        .modal-footer {
            padding: 1rem 1.5rem;
            border-top: 1px solid var(--lighter);
            display: flex;
            justify-content: flex-end;
            gap: 0.75rem;
        }
        
        .tabs {
            display: flex;
            border-bottom: 1px solid var(--lighter);
            margin-bottom: 1.5rem;
        }
        
        .tab {
            padding: 0.75rem 1.5rem;
            cursor: pointer;
            font-weight: 500;
            color: var(--gray);
            border-bottom: 2px solid transparent;
            transition: var(--transition);
        }
        
        .tab.active {
            color: var(--primary);
            border-bottom-color: var(--primary);
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease-out;
        }
        
        .search-bar {
            display: flex;
            margin-bottom: 1.5rem;
        }
        
        .search-bar input {
            flex: 1;
            border-radius: 50px 0 0 50px;
            margin: 0;
        }
        
        .search-bar button {
            border-radius: 0 50px 50px 0;
            padding: 0.75rem 1.5rem;
            margin: 0;
        }
        
        .pagination {
            display: flex;
            justify-content: center;
            gap: 0.5rem;
            margin-top: 1.5rem;
        }
        
        .pagination button {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0;
            border-radius: 50%;
        }
        
        .pagination button.active {
            background-color: var(--dark);
        }
        
        .chart-container {
            height: 300px;
            margin-top: 1.5rem;
        }
        
        .empty-state {
            text-align: center;
            padding: 3rem;
            color: var(--gray);
        }
        
        .empty-state i {
            font-size: 3rem;
            margin-bottom: 1rem;
            opacity: 0.3;
        }
        
        .empty-state p {
            margin-bottom: 1.5rem;
        }
        
        .toast {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            background-color: var(--dark);
            color: white;
            padding: 1rem 1.5rem;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            display: flex;
            align-items: center;
            gap: 1rem;
            z-index: 1100;
            transform: translateY(100px);
            opacity: 0;
            transition: var(--transition);
        }
        
        .toast.show {
            transform: translateY(0);
            opacity: 1;
        }
        
        .toast i {
            font-size: 1.5rem;
        }
        
        .toast-success {
            background-color: var(--secondary);
        }
        
        .toast-warning {
            background-color: var(--warning);
        }
        
        .toast-danger {
            background-color: var(--danger);
        }
        
        @media (max-width: 768px) {
            nav ul {
                flex-direction: column;
                gap: 0.25rem;
            }
            
            nav a {
                justify-content: center;
            }
            
            .dashboard {
                grid-template-columns: 1fr;
            }
            
            .form-row {
                flex-direction: column;
                gap: 0;
            }
            
            .ebike-gallery {
                grid-template-columns: 1fr;
            }
            
            .modal-content {
                width: 95%;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>E-Bike Store and Rental Management</h1>
        <p>Manage your e-bike inventory, rentals, and sales in one place</p>
    </header>

    <nav>
        <ul>
            <li><a href="#dashboard" class="active"><i class="fas fa-tachometer-alt"></i> Dashboard</a></li>
            <li><a href="#inventory"><i class="fas fa-warehouse"></i> Inventory</a></li>
            <li><a href="#available-ebikes"><i class="fas fa-bicycle"></i> Available Bikes</a></li>
            <li><a href="#rent-ebike"><i class="fas fa-calendar-check"></i> Rentals</a></li>
            <li><a href="#maintenance"><i class="fas fa-tools"></i> Maintenance</a></li>
            <li><a href="#payment"><i class="fas fa-receipt"></i> Invoices</a></li>
            <li><a href="#buy-sell"><i class="fas fa-shopping-cart"></i> Sales</a></li>
        </ul>
    </nav>

    <main>
        <!-- Dashboard Section -->
        <section id="dashboard">
            <h2><i class="fas fa-tachometer-alt"></i> Dashboard Overview</h2>
            
            <div class="dashboard">
                <div class="stat-card">
                    <h3>Total E-Bikes</h3>
                    <div class="value" id="total-bikes">0</div>
                    <i class="fas fa-bicycle icon"></i>
                </div>
                
                <div class="stat-card">
                    <h3>Available for Rent</h3>
                    <div class="value" id="available-bikes">0</div>
                    <i class="fas fa-check-circle icon"></i>
                </div>
                
                <div class="stat-card">
                    <h3>Active Rentals</h3>
                    <div class="value" id="active-rentals">0</div>
                    <i class="fas fa-calendar-alt icon"></i>
                </div>
                
                <div class="stat-card">
                    <h3>Revenue (30 days)</h3>
                    <div class="value">₱<span id="month-revenue">0</span></div>
                    <i class="fas fa-chart-line icon"></i>
                </div>
            </div>
            
            <div class="chart-container">
                <canvas id="revenueChart"></canvas>
            </div>
        </section>

        <!-- Inventory Section -->
        <section id="inventory">
            <div class="section-header">
                <h2><i class="fas fa-warehouse"></i> Inventory Management</h2>
                <div class="section-actions">
                    <button id="add-model-btn"><i class="fas fa-plus"></i> Add Model</button>
                </div>
            </div>
            
            <div class="search-bar">
                <input type="text" id="inventory-search" placeholder="Search e-bike models...">
                <button><i class="fas fa-search"></i></button>
            </div>
            
            <div class="alert alert-info">
                <i class="fas fa-info-circle"></i>
                <div>Low stock alert: <span id="low-stock-alert">Model A (1 left), Model B (1 left)</span></div>
            </div>
            
            <table id="inventory-table">
                <thead>
                    <tr>
                        <th>Model</th>
                        <th>Stock</th>
                        <th>Purchase Price</th>
                        <th>Rental Price</th>
                        <th>Status</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Inventory rows will be dynamically generated -->
                </tbody>
            </table>
            
            <div class="pagination">
                <button><i class="fas fa-chevron-left"></i></button>
                <button class="active">1</button>
                <button>2</button>
                <button>3</button>
                <button><i class="fas fa-chevron-right"></i></button>
            </div>
        </section>

        <!-- Available E-Bikes Section -->
        <section id="available-ebikes">
            <div class="section-header">
                <h2><i class="fas fa-bicycle"></i> Available E-Bikes for Rent</h2>
                <div class="section-actions">
                    <button class="btn-outline"><i class="fas fa-filter"></i> Filter</button>
                </div>
            </div>
            
            <div class="tabs">
                <div class="tab active" data-tab="all">All Models</div>
                <div class="tab" data-tab="premium">Premium</div>
                <div class="tab" data-tab="standard">Standard</div>
            </div>
            
            <div class="tab-content active" id="tab-all">
                <ul id="ebike-list" class="ebike-gallery">
                    <!-- E-Bike items will be dynamically generated -->
                </ul>
            </div>
            
            <div class="tab-content" id="tab-premium">
                <div class="empty-state">
                    <i class="fas fa-bicycle"></i>
                    <h3>No Premium E-Bikes Available</h3>
                    <p>Currently all our premium e-bikes are rented out or under maintenance.</p>
                    <button class="btn-outline"><i class="fas fa-bell"></i> Notify Me</button>
                </div>
            </div>
            
            <div class="tab-content" id="tab-standard">
                <ul class="ebike-gallery">
                    <!-- Standard e-bikes would be here -->
                </ul>
            </div>
        </section>

        <!-- Rent E-Bike Section -->
        <section id="rent-ebike">
            <div class="section-header">
                <h2><i class="fas fa-calendar-check"></i> Rent an E-Bike</h2>
                <div class="section-actions">
                    <button id="quick-rent-btn" class="btn-success"><i class="fas fa-bolt"></i> Quick Rent</button>
                </div>
            </div>
            
            <div class="alert alert-warning">
                <i class="fas fa-exclamation-triangle"></i>
                <div>Remember to check the bike condition before renting it out to customers.</div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="customer-name">Customer Name</label>
                    <input type="text" id="customer-name" placeholder="Enter customer name">
                </div>
                <div class="form-group">
                    <label for="customer-contact">Contact Number</label>
                    <input type="text" id="customer-contact" placeholder="Enter contact number">
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="rent-model">E-Bike Model</label>
                    <select id="rent-model"></select>
                </div>
                <div class="form-group">
                    <label for="rent-duration">Rental Duration (days)</label>
                    <input type="number" id="rent-duration" min="1" value="1">
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="rent-date">Start Date</label>
                    <input type="date" id="rent-date">
                </div>
                <div class="form-group">
                    <label for="insurance">Add Insurance</label>
                    <select id="insurance">
                        <option value="none">No Insurance</option>
                        <option value="basic">Basic (₱200)</option>
                        <option value="premium">Premium (₱500)</option>
                    </select>
                </div>
            </div>
            
            <div class="form-group">
                <label for="rent-notes">Notes</label>
                <textarea id="rent-notes" rows="2" placeholder="Any special requests or notes..."></textarea>
            </div>
            
            <div class="form-actions">
                <button id="rent-btn"><i class="fas fa-check"></i> Confirm Rental</button>
                <button id="return-btn" class="btn-danger" style="display:none;"><i class="fas fa-undo"></i> Return E-Bike</button>
            </div>

            <div id="rent-confirmation" class="alert alert-success" style="display:none;">
                <i class="fas fa-check-circle"></i>
                <div>
                    <h3>Rental Confirmed</h3>
                    <p><strong>Customer:</strong> <span id="confirmed-customer-name"></span></p>
                    <p><strong>E-Bike Model:</strong> <span id="rented-bike-model"></span></p>
                    <p><strong>Duration:</strong> <span id="rented-duration"></span> days (Due: <span id="due-date"></span>)</p>
                    <p><strong>Total Cost:</strong> ₱<span id="rental-cost"></span></p>
                </div>
            </div>
        </section>

        <!-- Upcoming Maintenance Section -->
        <section id="maintenance">
            <div class="section-header">
                <h2><i class="fas fa-tools"></i> Maintenance Schedule</h2>
                <div class="section-actions">
                    <button id="add-maintenance-btn"><i class="fas fa-plus"></i> Schedule</button>
                </div>
            </div>
            
            <table>
                <thead>
                    <tr>
                        <th>E-Bike</th>
                        <th>Date</th>
                        <th>Details</th>
                        <th>Status</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="maintenance-list"></tbody>
            </table>
        </section>

        <!-- Payment & Invoice Tracking Section -->
        <section id="payment">
            <div class="section-header">
                <h2><i class="fas fa-receipt"></i> Invoice Tracking</h2>
                <div class="section-actions">
                    <button class="btn-outline"><i class="fas fa-file-export"></i> Export</button>
                </div>
            </div>
            
            <table>
                <thead>
                    <tr>
                        <th>Invoice #</th>
                        <th>Date</th>
                        <th>Description</th>
                        <th>Customer</th>
                        <th>Amount</th>
                        <th>Status</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="invoice-list"></tbody>
            </table>
        </section>

        <!-- Sell E-Bikes Section -->
        <section id="buy-sell">
            <div class="section-header">
                <h2><i class="fas fa-shopping-cart"></i> E-Bike Sales</h2>
                <div class="section-actions">
                    <button id="new-order-btn" class="btn-success"><i class="fas fa-plus"></i> New Order</button>
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="sell-customer-name">Customer Name</label>
                    <input type="text" id="sell-customer-name" placeholder="Enter customer name">
                </div>
                <div class="form-group">
                    <label for="sell-customer-email">Email (Optional)</label>
                    <input type="email" id="sell-customer-email" placeholder="Enter customer email">
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="sell-model">E-Bike Model</label>
                    <select id="sell-model"></select>
                </div>
                <div class="form-group">
                    <label for="sell-quantity">Quantity</label>
                    <input type="number" id="sell-quantity" min="1" value="1">
                </div>
            </div>
            
            <div class="alert alert-info">
                <i class="fas fa-info-circle"></i>
                <div>
                    <p><strong>Model:</strong> <span id="sell-bike-model">-</span></p>
                    <p><strong>Unit Price:</strong> ₱<span id="sell-bike-price">0</span> | <strong>Available:</strong> <span id="sell-bike-stock">0</span></p>
                    <p><strong>Total:</strong> ₱<span id="total-sale-amount">0</span></p>
                </div>
            </div>
            
            <div class="form-group">
                <label for="payment-method">Payment Method</label>
                <select id="payment-method">
                    <option value="cash">Cash</option>
                    <option value="credit">Credit Card</option>
                    <option value="gcash">GCash</option>
                    <option value="bank">Bank Transfer</option>
                </select>
            </div>
            
            <div class="form-actions">
                <button id="sell-btn"><i class="fas fa-check"></i> Complete Sale</button>
                <button class="btn-outline"><i class="fas fa-print"></i> Print Invoice</button>
            </div>
        </section>
    </main>

    <!-- Add Model Modal -->
    <div class="modal" id="add-model-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Add New E-Bike Model</h3>
                <button class="modal-close">&times;</button>
            </div>
            <div class="modal-body">
                <div class="form-group">
                    <label for="new-model-name">Model Name</label>
                    <input type="text" id="new-model-name" placeholder="Enter model name">
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="new-model-price">Purchase Price (₱)</label>
                        <input type="number" id="new-model-price" min="0" placeholder="Enter price">
                    </div>
                    <div class="form-group">
                        <label for="new-rental-price">Rental Price (₱/day)</label>
                        <input type="number" id="new-rental-price" min="0" placeholder="Enter rental price">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="new-model-quantity">Initial Quantity</label>
                        <input type="number" id="new-model-quantity" min="0" placeholder="Enter quantity">
                    </div>
                    <div class="form-group">
                        <label for="new-model-category">Category</label>
                        <select id="new-model-category">
                            <option value="standard">Standard</option>
                            <option value="premium">Premium</option>
                        </select>
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="new-model-description">Description</label>
                    <textarea id="new-model-description" rows="3" placeholder="Enter model description"></textarea>
                </div>
                
                <div class="form-group">
                    <label for="new-model-image">Upload Image</label>
                    <input type="file" id="new-model-image" accept="image/*">
                </div>
            </div>
            <div class="modal-footer">
                <button class="btn-outline modal-close">Cancel</button>
                <button id="confirm-add-model" class="btn-success">Add Model</button>
            </div>
        </div>
    </div>

    <!-- Quick Rent Modal -->
    <div class="modal" id="quick-rent-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Quick Rental</h3>
                <button class="modal-close">&times;</button>
            </div>
            <div class="modal-body">
                <div class="form-group">
                    <label for="quick-customer-phone">Customer Phone</label>
                    <input type="text" id="quick-customer-phone" placeholder="Enter phone number">
                </div>
                
                <div class="form-group">
                    <label for="quick-bike-model">Select Available E-Bike</label>
                    <select id="quick-bike-model"></select>
                </div>
                
                <div class="form-group">
                    <label>Duration</label>
                    <div class="duration-options">
                        <button class="btn-sm duration-option active" data-duration="1">1 Day</button>
                        <button class="btn-sm duration-option" data-duration="3">3 Days</button>
                        <button class="btn-sm duration-option" data-duration="7">1 Week</button>
                        <button class="btn-sm duration-option" data-duration="30">1 Month</button>
                    </div>
                </div>
                
                <div class="alert alert-info">
                    <i class="fas fa-info-circle"></i>
                    <div>Standard rental agreement terms will apply. Customer can be registered later.</div>
                </div>
            </div>
            <div class="modal-footer">
                <button class="btn-outline modal-close">Cancel</button>
                <button id="confirm-quick-rent" class="btn-success">Complete Rental</button>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast" id="toast-notification">
        <i class="fas fa-check-circle"></i>
        <div class="toast-message">Operation completed successfully</div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        const eBikeStore = {
            inventory: {
                "Model A": { 
                    stock: 2, 
                    price: 15000, 
                    rentalPrice: 500,
                    category: "standard",
                    description: "City commuter e-bike with 50km range"
                },
                "Model B": { 
                    stock: 1, 
                    price: 7000, 
                    rentalPrice: 700,
                    category: "standard",
                    description: "Basic e-bike with 30km range"
                },
                "Model C": { 
                    stock: 5, 
                    price: 20000, 
                    rentalPrice: 900,
                    category: "premium",
                    description: "Mountain e-bike with 80km range"
                },
                "Model D": { 
                    stock: 3, 
                    price: 10000, 
                    rentalPrice: 1200,
                    category: "standard",
                    description: "Folding e-bike perfect for urban areas"
                },
                "Model E": { 
                    stock: 4, 
                    price: 55000, 
                    rentalPrice: 9000,
                    category: "premium",
                    description: "High-performance e-bike with 120km range"
                }
            },
            maintenance: [
                {
                    model: "Model B",
                    date: "2023-06-15",
                    details: "Battery replacement",
                    completed: false
                },
                {
                    model: "Model D",
                    date: "2023-06-20",
                    details: "Regular service",
                    completed: true
                }
            ],
            invoices: [
                {
                    number: 1001,
                    date: "2023-06-01",
                    description: "Rental: Model A for 3 days",
                    customer: "Juan Dela Cruz",
                    amount: 1500,
                    paid: true
                },
                {
                    number: 1002,
                    date: "2023-06-05",
                    description: "Sale: 1 Model C",
                    customer: "Maria Santos",
                    amount: 20000,
                    paid: true
                },
                {
                    number: 1003,
                    date: "2023-06-10",
                    description: "Rental: Model E for 7 days",
                    customer: "Pedro Bautista",
                    amount: 63000,
                    paid: false
                }
            ],
            rentals: [
                {
                    date: "2023-06-01",
                    customerName: "Juan Dela Cruz",
                    customerContact: "09123456789",
                    model: "Model A",
                    duration: 3,
                    amount: 1500,
                    returned: true
                },
                {
                    date: "2023-06-10",
                    customerName: "Pedro Bautista",
                    customerContact: "09987654321",
                    model: "Model E",
                    duration: 7,
                    amount: 63000,
                    returned: false
                }
            ],
            sales: [
                {
                    date: "2023-06-05",
                    customerName: "Maria Santos",
                    model: "Model C",
                    quantity: 1,
                    amount: 20000
                }
            ],
            currentRental: null,
            revenueData: {
                labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
                data: [120000, 150000, 180000, 140000, 210000, 230000]
            }
        };

        const imagePaths = {
            "Model A": "https://images.unsplash.com/photo-1558981806-ec527fa84c39?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80",
            "Model B": "https://images.unsplash.com/photo-1507035895480-2b3156c31fc8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80",
            "Model C": "https://images.unsplash.com/photo-1485965120184-e220f721d03e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80",
            "Model D": "https://images.unsplash.com/photo-1576435728678-68d0fbf94e91?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1644&q=80",
            "Model E": "https://images.unsplash.com/photo-1511994298241-608e28f14fde?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80"
        };

        function formatDate(date) {
            const d = new Date(date);
            return d.toLocaleDateString('en-US', {
                year: 'numeric',
                month: 'short',
                day: 'numeric'
            });
        }

        function calculateDueDate(days) {
            const dueDate = new Date();
            dueDate.setDate(dueDate.getDate() + parseInt(days));
            return formatDate(dueDate);
        }

        function calculateRevenueLast30Days() {
            const thirtyDaysAgo = new Date();
            thirtyDaysAgo.setDate(thirtyDaysAgo.getDate() - 30);
            
            let revenue = 0;
            
            eBikeStore.rentals.forEach(rental => {
                const rentalDate = new Date(rental.date);
                if (rentalDate >= thirtyDaysAgo) {
                    revenue += rental.amount;
                }
            });
            
            eBikeStore.sales.forEach(sale => {
                const saleDate = new Date(sale.date);
                if (saleDate >= thirtyDaysAgo) {
                    revenue += sale.amount;
                }
            });
            
            return revenue;
        }

        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast-notification');
            toast.className = `toast toast-${type}`;
            toast.querySelector('.toast-message').textContent = message;
            toast.querySelector('i').className = type === 'success' ? 'fas fa-check-circle' : 
                                                type === 'warning' ? 'fas fa-exclamation-triangle' : 
                                                'fas fa-times-circle';
            
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        function openModal(modalId) {
            document.getElementById(modalId).classList.add('active');
            document.body.style.overflow = 'hidden';
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('active');
            document.body.style.overflow = 'auto';
        }

        function updateDashboardStats() {
            let totalBikes = 0;
            for (const model in eBikeStore.inventory) {
                totalBikes += eBikeStore.inventory[model].stock;
            }
            document.getElementById('total-bikes').textContent = totalBikes;
            
            let availableBikes = 0;
            for (const model in eBikeStore.inventory) {
                if (eBikeStore.inventory[model].stock > 0) {
                    availableBikes += eBikeStore.inventory[model].stock;
                }
            }
            document.getElementById('available-bikes').textContent = availableBikes;
            
            const activeRentals = eBikeStore.rentals.filter(r => !r.returned).length;
            document.getElementById('active-rentals').textContent = activeRentals;
            
            const revenue = calculateRevenueLast30Days();
            document.getElementById('month-revenue').textContent = revenue.toLocaleString();
            
            const lowStockModels = [];
            for (const model in eBikeStore.inventory) {
                if (eBikeStore.inventory[model].stock <= 2) {
                    lowStockModels.push(`${model} (${eBikeStore.inventory[model].stock} left)`);
                }
            }
            document.getElementById('low-stock-alert').textContent = lowStockModels.join(', ') || 'None';
        }

        function updateRevenueChart() {
            const ctx = document.getElementById('revenueChart').getContext('2d');
            
            if (window.revenueChart) {
                window.revenueChart.destroy();
            }
            
            window.revenueChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: eBikeStore.revenueData.labels,
                    datasets: [{
                        label: 'Monthly Revenue (₱)',
                        data: eBikeStore.revenueData.data,
                        backgroundColor: 'rgba(52, 152, 219, 0.2)',
                        borderColor: 'rgba(52, 152, 219, 1)',
                        borderWidth: 2,
                        tension: 0.3,
                        fill: true
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    return '₱' + value.toLocaleString();
                                }
                            }
                        }
                    },
                    plugins: {
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return '₱' + context.raw.toLocaleString();
                                }
                            }
                        }
                    }
                }
            });
        }

        function updateInventoryDisplay() {
            const tbody = document.querySelector("#inventory-table tbody");
            tbody.innerHTML = "";

            for (const [model, data] of Object.entries(eBikeStore.inventory)) {
                const status = data.stock === 0 ? 'Out of Stock' : 
                              data.stock <= 2 ? 'Low Stock' : 'In Stock';
                
                const statusClass = data.stock === 0 ? 'badge-danger' : 
                                  data.stock <= 2 ? 'badge-warning' : 'badge-success';
                
                const row = document.createElement("tr");
                row.innerHTML = `
                    <td><strong>${model}</strong></td>
                    <td>${data.stock}</td>
                    <td>₱${data.price.toLocaleString()}</td>
                    <td>₱${data.rentalPrice.toLocaleString()}</td>
                    <td><span class="badge ${statusClass}">${status}</span></td>
                    <td>
                        <button onclick="adjustStock('${model}', -1)" class="btn-sm"><i class="fas fa-minus"></i></button>
                        <button onclick="adjustStock('${model}', 1)" class="btn-sm"><i class="fas fa-plus"></i></button>
                        <button onclick="removeModel('${model}')" class="btn-sm btn-danger"><i class="fas fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(row);
            }
            
            updateDashboardStats();
        }

        function updateAvailableBikesDisplay() {
            const ebikeList = document.getElementById("ebike-list");
            ebikeList.innerHTML = "";

            for (const [model, data] of Object.entries(eBikeStore.inventory)) {
                if (data.stock > 0) {
                    const listItem = document.createElement("li");
                    listItem.className = "ebike-card";
                    listItem.innerHTML = `  
                        <div class="card-img">
                            <img src="${imagePaths[model]}" alt="${model}" onerror="this.src='images/default-bike.jpg'">
                            <span class="card-badge">${data.category === 'premium' ? 'Premium' : 'Standard'}</span>
                        </div>
                        <div class="card-content">
                            <h3 class="card-title">${model}</h3>
                            <div class="card-price">₱${data.rentalPrice.toLocaleString()} <small>/ day</small></div>
                            <p class="card-description">${data.description}</p>
                            <div class="card-meta">
                                <span><i class="fas fa-battery-three-quarters"></i> ${model === 'Model E' ? '120km' : model === 'Model C' ? '80km' : model === 'Model A' ? '50km' : '30km'} range</span>
                                <span><i class="fas fa-box-open"></i> ${data.stock} available</span>
                            </div>
                            <div class="card-actions">
                                <button onclick="quickRentModel('${model}')" class="btn-sm btn-success"><i class="fas fa-bolt"></i> Quick Rent</button>
                                <button onclick="showModelDetails('${model}')" class="btn-sm btn-outline"><i class="fas fa-info-circle"></i> Details</button>
                            </div>
                        </div>
                    `;
                    ebikeList.appendChild(listItem);
                }
            }
            
            updateDashboardStats();
        }

        function updateDropdowns() {
            updateDropdown("rent-model", true);
            updateDropdown("maintenance-model", true);
            updateDropdown("sell-model", false);
            updateDropdown("quick-bike-model", true);
        }

        function updateDropdown(selectId, availableOnly) {
            const select = document.getElementById(selectId);
            select.innerHTML = "";

            for (const [model, data] of Object.entries(eBikeStore.inventory)) {
                if (!availableOnly || data.stock > 0) {
                    const option = document.createElement("option");
                    option.value = model;
                    option.textContent = model;
                    select.appendChild(option);
                }
            }
        }

        function updateMaintenanceDisplay() {
            const tbody = document.getElementById("maintenance-list");
            tbody.innerHTML = "";

            eBikeStore.maintenance.forEach((item, index) => {
                const row = document.createElement("tr");
                row.innerHTML = `
                    <td>${item.model}</td>
                    <td>${formatDate(item.date)}</td>
                    <td>${item.details}</td>
                    <td>
                        <span class="badge ${item.completed ? 'badge-success' : 'badge-warning'}">
                            ${item.completed ? 'Completed' : 'Pending'}
                        </span>
                    </td>
                    <td>
                        <button onclick="toggleMaintenanceStatus(${index})" class="btn-sm ${item.completed ? 'btn-warning' : 'btn-success'}">
                            <i class="fas ${item.completed ? 'fa-undo' : 'fa-check'}"></i> ${item.completed ? 'Reopen' : 'Complete'}
                        </button>
                        <button onclick="deleteMaintenance(${index})" class="btn-sm btn-danger"><i class="fas fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function updateInvoicesDisplay() {
            const tbody = document.getElementById("invoice-list");
            tbody.innerHTML = "";

            eBikeStore.invoices.forEach((invoice, index) => {
                const row = document.createElement("tr");
                row.innerHTML = `
                    <td>#${invoice.number}</td>
                    <td>${formatDate(invoice.date)}</td>
                    <td>${invoice.description}</td>
                    <td>${invoice.customer || 'N/A'}</td>
                    <td>₱${invoice.amount.toLocaleString()}</td>
                    <td>
                        <span class="badge ${invoice.paid ? 'badge-success' : 'badge-warning'}">
                            ${invoice.paid ? 'Paid' : 'Pending'}
                        </span>
                    </td>
                    <td>
                        <button onclick="toggleInvoiceStatus(${index})" class="btn-sm ${invoice.paid ? 'btn-warning' : 'btn-success'}">
                            <i class="fas ${invoice.paid ? 'fa-times' : 'fa-check'}"></i> ${invoice.paid ? 'Unpay' : 'Pay'}
                        </button>
                        <button onclick="printInvoice(${index})" class="btn-sm btn-outline"><i class="fas fa-print"></i></button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function updateRentalHistoryDisplay() {
            const tbody = document.getElementById("summary-list");
            if (!tbody) return;
            
            tbody.innerHTML = "";

            eBikeStore.rentals.forEach(rental => {
                const row = document.createElement("tr");
                row.innerHTML = `
                    <td>${formatDate(rental.date)}</td>
                    <td>${rental.customerName}</td>
                    <td>${rental.model}</td>
                    <td>${rental.duration} days</td>
                    <td>₱${rental.amount.toLocaleString()}</td>
                    <td>
                        <span class="badge ${rental.returned ? 'badge-primary' : 'badge-success'}">
                            ${rental.returned ? 'Returned' : 'Active'}
                        </span>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function updateSellSection() {
            const model = document.getElementById("sell-model").value;
            const quantity = parseInt(document.getElementById("sell-quantity").value) || 1;
            const modelData = eBikeStore.inventory[model];
            
            if (modelData) {
                document.getElementById("sell-bike-model").textContent = model;
                document.getElementById("sell-bike-price").textContent = modelData.price.toLocaleString();
                document.getElementById("sell-bike-stock").textContent = modelData.stock;
                document.getElementById("total-sale-amount").textContent = (modelData.price * quantity).toLocaleString();
            }
        }

        function adjustStock(model, change) {
            if (eBikeStore.inventory[model]) {
                const newStock = eBikeStore.inventory[model].stock + change;
                if (newStock >= 0) {
                    eBikeStore.inventory[model].stock = newStock;
                    updateInventoryDisplay();
                    updateAvailableBikesDisplay();
                    updateDropdowns();
                    updateSellSection();
                    showToast(`Stock updated for ${model}`, 'success');
                } else {
                    showToast("Stock cannot be negative", 'warning');
                }
            }
        }

        function addNewModel() {
            const name = document.getElementById("new-model-name").value.trim();
            const price = parseFloat(document.getElementById("new-model-price").value);
            const rentalPrice = parseFloat(document.getElementById("new-rental-price").value);
            const quantity = parseInt(document.getElementById("new-model-quantity").value);
            const category = document.getElementById("new-model-category").value;
            const description = document.getElementById("new-model-description").value.trim();

            if (!name || isNaN(price) || isNaN(rentalPrice) || isNaN(quantity)) {
                showToast("Please fill in all required fields with valid values", 'warning');
                return;
            }

            if (eBikeStore.inventory[name]) {
                showToast("This model already exists in inventory", 'warning');
                return;
            }

            eBikeStore.inventory[name] = {
                stock: quantity,
                price: price,
                rentalPrice: rentalPrice,
                category: category,
                description: description
            };

            document.getElementById("new-model-name").value = "";
            document.getElementById("new-model-price").value = "";
            document.getElementById("new-rental-price").value = "";
            document.getElementById("new-model-quantity").value = "";
            document.getElementById("new-model-description").value = "";

            updateInventoryDisplay();
            updateAvailableBikesDisplay();
            updateDropdowns();
            closeModal('add-model-modal');
            showToast(`New model "${name}" added successfully!`, 'success');
        }

        function removeModel(model) {
            if (confirm(`Are you sure you want to remove ${model} from inventory? This action cannot be undone.`)) {
                delete eBikeStore.inventory[model];
                updateInventoryDisplay();
                updateAvailableBikesDisplay();
                updateDropdowns();
                showToast(`Model ${model} removed from inventory`, 'success');
            }
        }

        function rentEbike() {
            const customerName = document.getElementById("customer-name").value.trim();
            const contact = document.getElementById("customer-contact").value.trim();
            const model = document.getElementById("rent-model").value;
            const duration = parseInt(document.getElementById("rent-duration").value);
            const insurance = document.getElementById("insurance").value;
            const notes = document.getElementById("rent-notes").value.trim();

            if (!customerName || !contact || !model || isNaN(duration) || duration < 1) {
                showToast("Please fill in all required fields with valid values", 'warning');
                return;
            }

            const bikeData = eBikeStore.inventory[model];
            if (!bikeData || bikeData.stock < 1) {
                showToast("Selected E-Bike is not available for rent", 'warning');
                return;
            }

            bikeData.stock--;
            let amount = bikeData.rentalPrice * duration;
            
            if (insurance === 'basic') {
                amount += 200;
            } else if (insurance === 'premium') {
                amount += 500;
            }
            
            const today = new Date();
            const dueDate = calculateDueDate(duration);

            const rental = {
                date: today,
                customerName,
                customerContact: contact,
                model,
                duration,
                amount,
                insurance,
                notes,
                returned: false
            };

            eBikeStore.rentals.push(rental);
            eBikeStore.currentRental = rental;

            const invoiceNumber = eBikeStore.invoices.length + 1000;
            eBikeStore.invoices.push({
                number: invoiceNumber,
                date: today,
                description: `Rental: ${model} for ${duration} days${insurance !== 'none' ? ` (${insurance} insurance)` : ''}`,
                customer: customerName,
                amount,
                paid: false
            });

            updateInventoryDisplay();
            updateAvailableBikesDisplay();
            updateDropdowns();
            updateInvoicesDisplay();
            updateRentalHistoryDisplay();

            document.getElementById("confirmed-customer-name").textContent = customerName;
            document.getElementById("rented-bike-model").textContent = model;
            document.getElementById("rented-duration").textContent = duration;
            document.getElementById("rental-cost").textContent = amount.toLocaleString();
            document.getElementById("due-date").textContent = formatDate(dueDate);
            document.getElementById("rent-confirmation").style.display = "flex";
            document.getElementById("return-btn").style.display = "inline-block";

            document.getElementById("customer-name").value = "";
            document.getElementById("customer-contact").value = "";
            document.getElementById("rent-duration").value = "1";
            document.getElementById("rent-notes").value = "";

            showToast(`E-Bike rented successfully! Invoice #${invoiceNumber} created.`, 'success');
        }

        function quickRentModel(model) {
            document.getElementById('quick-bike-model').value = model;
            openModal('quick-rent-modal');
        }

        function processQuickRent() {
            const phone = document.getElementById("quick-customer-phone").value.trim();
            const model = document.getElementById("quick-bike-model").value;
            const duration = parseInt(document.querySelector(".duration-option.active").dataset.duration);

            if (!phone || !model || isNaN(duration)) {
                showToast("Please fill in all required fields", 'warning');
                return;
            }

            const bikeData = eBikeStore.inventory[model];
            if (!bikeData || bikeData.stock < 1) {
                showToast("Selected E-Bike is not available for rent", 'warning');
                return;
            }

            bikeData.stock--;
            const amount = bikeData.rentalPrice * duration;
            const today = new Date();
            const dueDate = calculateDueDate(duration);

            const rental = {
                date: today,
                customerName: "Walk-in Customer",
                customerContact: phone,
                model,
                duration,
                amount,
                returned: false
            };

            eBikeStore.rentals.push(rental);
            eBikeStore.currentRental = rental;

            const invoiceNumber = eBikeStore.invoices.length + 1000;
            eBikeStore.invoices.push({
                number: invoiceNumber,
                date: today,
                description: `Quick Rental: ${model} for ${duration} days`,
                customer: "Walk-in Customer",
                amount,
                paid: false
            });

            updateInventoryDisplay();
            updateAvailableBikesDisplay();
            updateDropdowns();
            updateInvoicesDisplay();
            updateRentalHistoryDisplay();

            document.getElementById("quick-customer-phone").value = "";

            closeModal('quick-rent-modal');
            showToast(`Quick rental processed! Invoice #${invoiceNumber} created.`, 'success');
        }

        function returnEbike() {
            if (!eBikeStore.currentRental) {
                showToast("No E-Bike is currently rented", 'warning');
                return;
            }

            const rental = eBikeStore.currentRental;
            rental.returned = true;
            eBikeStore.inventory[rental.model].stock++;
            eBikeStore.currentRental = null;

            updateInventoryDisplay();
            updateAvailableBikesDisplay();
            updateDropdowns();
            updateRentalHistoryDisplay();

            document.getElementById("return-btn").style.display = "none";
            document.getElementById("rent-confirmation").style.display = "none";

            showToast("E-Bike returned successfully. Thank you!", 'success');
        }

        function addMaintenance() {
            const model = document.getElementById("maintenance-model").value;
            const date = document.getElementById("maintenance-date").value;
            const details = document.getElementById("maintenance-details").value.trim();

            if (!model || !date || !details) {
                showToast("Please fill in all fields", 'warning');
                return;
            }

            eBikeStore.maintenance.push({
                model,
                date,
                details,
                completed: false
            });

            updateMaintenanceDisplay();

            document.getElementById("maintenance-details").value = "";

            showToast("Maintenance scheduled successfully!", 'success');
        }

        function toggleMaintenanceStatus(index) {
            eBikeStore.maintenance[index].completed = !eBikeStore.maintenance[index].completed;
            updateMaintenanceDisplay();
            showToast(`Maintenance marked as ${eBikeStore.maintenance[index].completed ? 'completed' : 'pending'}`, 'success');
        }

        function deleteMaintenance(index) {
            if (confirm("Are you sure you want to delete this maintenance record?")) {
                eBikeStore.maintenance.splice(index, 1);
                updateMaintenanceDisplay();
                showToast("Maintenance record deleted", 'success');
            }
        }

        function toggleInvoiceStatus(index) {
            eBikeStore.invoices[index].paid = !eBikeStore.invoices[index].paid;
            updateInvoicesDisplay();
            showToast(`Invoice #${eBikeStore.invoices[index].number} marked as ${eBikeStore.invoices[index].paid ? 'paid' : 'unpaid'}`, 'success');
        }

        function printInvoice(index) {
            showToast(`Printing invoice #${eBikeStore.invoices[index].number}`, 'success');
        }

        function sellEbike() {
            const customerName = document.getElementById("sell-customer-name").value.trim();
            const email = document.getElementById("sell-customer-email").value.trim();
            const model = document.getElementById("sell-model").value;
            const quantity = parseInt(document.getElementById("sell-quantity").value);
            const paymentMethod = document.getElementById("payment-method").value;

            if (!customerName || !model || isNaN(quantity) || quantity < 1) {
                showToast("Please fill in all required fields with valid values", 'warning');
                return;
            }

            const bikeData = eBikeStore.inventory[model];
            if (!bikeData || bikeData.stock < quantity) {
                showToast(`Not enough stock! Only ${bikeData ? bikeData.stock : 0} available.`, 'warning');
                return;
            }

            bikeData.stock -= quantity;
            const amount = bikeData.price * quantity;
            const today = new Date();

            eBikeStore.sales.push({
                date: today,
                customerName,
                customerEmail: email,
                model,
                quantity,
                amount,
                paymentMethod
            });

            const invoiceNumber = eBikeStore.invoices.length + 1000;
            eBikeStore.invoices.push({
                number: invoiceNumber,
                date: today,
                description: `Sale: ${quantity} ${model} (${paymentMethod})`,
                customer: customerName,
                amount,
                paid: true
            });

            updateInventoryDisplay();
            updateAvailableBikesDisplay();
            updateDropdowns();
            updateInvoicesDisplay();
            updateSellSection();
            updateDashboardStats();

            document.getElementById("sell-customer-name").value = "";
            document.getElementById("sell-customer-email").value = "";
            document.getElementById("sell-quantity").value = "1";

            showToast(`${quantity} ${model} E-Bike(s) sold for ₱${amount.toLocaleString()}. Invoice #${invoiceNumber} created.`, 'success');
        }

        function showModelDetails(model) {
            const bikeData = eBikeStore.inventory[model];
            if (!bikeData) return;
            
            alert(`Model: ${model}\n\n` +
                  `Description: ${bikeData.description}\n\n` +
                  `Purchase Price: ₱${bikeData.price.toLocaleString()}\n` +
                  `Rental Price: ₱${bikeData.rentalPrice.toLocaleString()} per day\n` +
                  `Available Stock: ${bikeData.stock}\n` +
                  `Category: ${bikeData.category === 'premium' ? 'Premium' : 'Standard'}`);
        }

        document.getElementById("add-model-btn").addEventListener("click", () => openModal('add-model-modal'));
        document.getElementById("confirm-add-model").addEventListener("click", addNewModel);
        document.getElementById("rent-btn").addEventListener("click", rentEbike);
        document.getElementById("return-btn").addEventListener("click", returnEbike);
        document.getElementById("add-maintenance-btn").addEventListener("click", addMaintenance);
        document.getElementById("sell-btn").addEventListener("click", sellEbike);
        document.getElementById("quick-rent-btn").addEventListener("click", () => openModal('quick-rent-modal'));
        document.getElementById("confirm-quick-rent").addEventListener("click", processQuickRent);

        document.getElementById("sell-model").addEventListener("change", updateSellSection);
        document.getElementById("sell-quantity").addEventListener("input", function() {
            const quantity = parseInt(this.value) || 1;
            this.value = quantity > 0 ? quantity : 1;
            updateSellSection();
        });

        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', function() {
                const tabId = this.getAttribute('data-tab');
                
                document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                this.classList.add('active');
                
                document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
                document.getElementById(`tab-${tabId}`).classList.add('active');
            });
        });

        document.querySelectorAll('.duration-option').forEach(option => {
            option.addEventListener('click', function() {
                document.querySelectorAll('.duration-option').forEach(opt => opt.classList.remove('active'));
                this.classList.add('active');
            });
        });

        document.querySelectorAll('.modal-close').forEach(btn => {
            btn.addEventListener('click', function() {
                const modal = this.closest('.modal');
                closeModal(modal.id);
            });
        });

        document.querySelectorAll('.modal').forEach(modal => {
            modal.addEventListener('click', function(e) {
                if (e.target === this) {
                    closeModal(this.id);
                }
            });
        });

        window.onload = function() {
            updateDashboardStats();
            updateRevenueChart();
            updateInventoryDisplay();
            updateAvailableBikesDisplay();
            updateDropdowns();
            updateMaintenanceDisplay();
            updateInvoicesDisplay();
            updateRentalHistoryDisplay();
            updateSellSection();
            
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('rent-date').value = today;
            document.getElementById('maintenance-date').value = today;
            
            setTimeout(() => {
                showToast('Welcome to E-Bike Management System!', 'success');
            }, 1000);
        };
    </script>
</body>
</html>
