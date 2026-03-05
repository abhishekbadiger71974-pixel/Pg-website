<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Retail Demand Forecasting & Inventory Management</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <!-- Navigation Header -->
        <header class="header">
            <div class="logo">
                <h1>📦 RetailForecast</h1>
                <p>Demand Forecasting & Inventory Management System</p>
            </div>
            <nav class="nav-menu">
                <button class="nav-btn active" data-section="dashboard">Dashboard</button>
                <button class="nav-btn" data-section="products">Products</button>
                <button class="nav-btn" data-section="sales">Sales Data</button>
                <button class="nav-btn" data-section="forecasting">Forecasting</button>
                <button class="nav-btn" data-section="inventory">Inventory</button>
                <button class="nav-btn" data-section="alerts">Alerts</button>
                <button class="nav-btn" data-section="reports">Reports</button>
            </nav>
        </header>

        <!-- Main Content Area -->
        <main class="main-content">

            <!-- DASHBOARD SECTION -->
            <section id="dashboard" class="section active">
                <h2>Dashboard Overview</h2>
                <div class="dashboard-grid">
                    <div class="card metric-card">
                        <h3>Total Products</h3>
                        <p class="metric-value" id="totalProducts">0</p>
                        <p class="metric-label">in inventory</p>
                    </div>
                    <div class="card metric-card">
                        <h3>Total Sales (30 days)</h3>
                        <p class="metric-value" id="totalSales">0</p>
                        <p class="metric-label">units sold</p>
                    </div>
                    <div class="card metric-card">
                        <h3>Stock Health</h3>
                        <p class="metric-value" id="stockHealth">85%</p>
                        <p class="metric-label">optimal level</p>
                    </div>
                    <div class="card metric-card">
                        <h3>Accuracy Rate</h3>
                        <p class="metric-value" id="accuracyRate">92%</p>
                        <p class="metric-label">forecast accuracy</p>
                    </div>
                </div>

                <div class="dashboard-charts">
                    <div class="card chart-card">
                        <h3>Sales Trend (Last 30 Days)</h3>
                        <canvas id="salesTrendChart"></canvas>
                    </div>
                    <div class="card chart-card">
                        <h3>Inventory Distribution</h3>
                        <canvas id="inventoryDistChart"></canvas>
                    </div>
                </div>

                <div class="alerts-preview">
                    <h3>Active Alerts</h3>
                    <div id="alertsPreview" class="alerts-list"></div>
                </div>
            </section>

            <!-- PRODUCTS SECTION -->
            <section id="products" class="section">
                <h2>Product & Sales Data Management</h2>
                
                <div class="form-container">
                    <div class="card">
                        <h3>Add New Product</h3>
                        <form id="productForm">
                            <div class="form-group">
                                <label for="productName">Product Name:</label>
                                <input type="text" id="productName" required>
                            </div>
                            <div class="form-group">
                                <label for="productCategory">Category:</label>
                                <select id="productCategory" required>
                                    <option>Electronics</option>
                                    <option>Clothing</option>
                                    <option>Groceries</option>
                                    <option>Home & Garden</option>
                                    <option>Sports</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="initialStock">Initial Stock:</label>
                                <input type="number" id="initialStock" min="0" required>
                            </div>
                            <div class="form-group">
                                <label for="minThreshold">Min Stock Threshold:</label>
                                <input type="number" id="minThreshold" min="0" required>
                            </div>
                            <div class="form-group">
                                <label for="maxThreshold">Max Stock Threshold:</label>
                                <input type="number" id="maxThreshold" min="0" required>
                            </div>
                            <div class="form-group">
                                <label for="unitPrice">Unit Price ($):</label>
                                <input type="number" id="unitPrice" min="0" step="0.01" required>
                            </div>
                            <button type="submit" class="btn btn-primary">Add Product</button>
                        </form>
                    </div>
                </div>

                <div class="card">
                    <h3>Products List</h3>
                    <div class="search-filter">
                        <input type="text" id="productSearch" placeholder="Search products...">
                        <select id="categoryFilter">
                            <option value="">All Categories</option>
                            <option>Electronics</option>
                            <option>Clothing</option>
                            <option>Groceries</option>
                            <option>Home & Garden</option>
                            <option>Sports</option>
                        </select>
                    </div>
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>Product ID</th>
                                <th>Name</th>
                                <th>Category</th>
                                <th>Current Stock</th>
                                <th>Min Threshold</th>
                                <th>Max Threshold</th>
                                <th>Unit Price</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody id="productsTableBody">
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- SALES DATA SECTION -->
            <section id="sales" class="section">
                <h2>Sales Data Management</h2>
                
                <div class="form-container">
                    <div class="card">
                        <h3>Record Sales Transaction</h3>
                        <form id="salesForm">
                            <div class="form-group">
                                <label for="saleProductId">Product:</label>
                                <select id="saleProductId" required></select>
                            </div>
                            <div class="form-group">
                                <label for="saleQuantity">Quantity Sold:</label>
                                <input type="number" id="saleQuantity" min="1" required>
                            </div>
                            <div class="form-group">
                                <label for="saleDate">Sale Date:</label>
                                <input type="date" id="saleDate" required>
                            </div>
                            <div class="form-group">
                                <label for="salePrice">Sale Price ($):</label>
                                <input type="number" id="salePrice" min="0" step="0.01" required>
                            </div>
                            <button type="submit" class="btn btn-primary">Record Sale</button>
                        </form>
                    </div>
                </div>

                <div class="card">
                    <h3>Sales History</h3>
                    <div class="search-filter">
                        <input type="text" id="salesSearch" placeholder="Search sales...">
                        <input type="date" id="startDate">
                        <input type="date" id="endDate">
                        <button class="btn btn-secondary" id="filterSalesBtn">Filter</button>
                    </div>
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>Sale ID</th>
                                <th>Product</th>
                                <th>Quantity</th>
                                <th>Sale Date</th>
                                <th>Price</th>
                                <th>Total</th>
                            </tr>
                        </thead>
                        <tbody id="salesTableBody">
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- FORECASTING SECTION -->
            <section id="forecasting" class="section">
                <h2>AI-Based Demand Forecasting</h2>
                
                <div class="card">
                    <h3>Forecast Settings</h3>
                    <div class="form-group">
                        <label for="forecastDays">Forecast Period (days):</label>
                        <input type="number" id="forecastDays" min="7" max="365" value="30">
                        <button class="btn btn-primary" id="generateForecastBtn">Generate Forecast</button>
                    </div>
                </div>

                <div class="card">
                    <h3>Demand Forecast Results</h3>
                    <div id="forecastStatus" class="status-message"></div>
                    <canvas id="forecastChart"></canvas>
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>Product</th>
                                <th>Average Daily Demand</th>
                                <th>Predicted 30-Day Demand</th>
                                <th>Trend</th>
                                <th>Confidence</th>
                            </tr>
                        </thead>
                        <tbody id="forecastTableBody">
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- INVENTORY SECTION -->
            <section id="inventory" class="section">
                <h2>Inventory Level Monitoring</h2>
                
                <div class="inventory-summary">
                    <div class="card summary-card">
                        <h4>Total Inventory Value</h4>
                        <p class="large-number" id="totalInventoryValue">$0</p>
                    </div>
                    <div class="card summary-card">
                        <h4>Low Stock Items</h4>
                        <p class="large-number" id="lowStockCount">0</p>
                    </div>
                    <div class="card summary-card">
                        <h4>Over Stock Items</h4>
                        <p class="large-number" id="overStockCount">0</p>
                    </div>
                    <div class="card summary-card">
                        <h4>Optimal Stock Items</h4>
                        <p class="large-number" id="optimalStockCount">0</p>
                    </div>
                </div>

                <div class="card">
                    <h3>Inventory Status by Product</h3>
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>Product</th>
                                <th>Current Stock</th>
                                <th>Min Threshold</th>
                                <th>Max Threshold</th>
                                <th>Status</th>
                                <th>Inventory Value</th>
                                <th>Days to Stockout</th>
                            </tr>
                        </thead>
                        <tbody id="inventoryTableBody">
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- ALERTS SECTION -->
            <section id="alerts" class="section">
                <h2>Stock Alerts & Notifications</h2>
                
                <div class="alerts-controls">
                    <button class="btn btn-secondary" id="clearAlertsBtn">Clear All Alerts</button>
                    <div class="alert-filters">
                        <label>
                            <input type="checkbox" id="filterLowStock" checked> Low Stock
                        </label>
                        <label>
                            <input type="checkbox" id="filterOverStock" checked> Over Stock
                        </label>
                        <label>
                            <input type="checkbox" id="filterStockOut" checked> Stock Out
                        </label>
                    </div>
                </div>

                <div id="alertsContainer" class="alerts-container">
                </div>
            </section>

            <!-- REPORTS SECTION -->
            <section id="reports" class="section">
                <h2>Sales & Demand Visualization Reports</h2>
                
                <div class="report-controls">
                    <div class="form-group">
                        <label for="reportType">Report Type:</label>
                        <select id="reportType">
                            <option value="sales-trend">Sales Trend</option>
                            <option value="demand-forecast">Demand Forecast</option>
                            <option value="inventory-analysis">Inventory Analysis</option>
                            <option value="category-performance">Category Performance</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="reportPeriod">Period:</label>
                        <select id="reportPeriod">
                            <option value="7">Last 7 Days</option>
                            <option value="30" selected>Last 30 Days</option>
                            <option value="90">Last 90 Days</option>
                            <option value="365">Last Year</option>
                        </select>
                    </div>
                    <button class="btn btn-primary" id="generateReportBtn">Generate Report</button>
                    <button class="btn btn-secondary" id="exportReportBtn">Export as CSV</button>
                </div>

                <div class="card">
                    <h3>Report Visualization</h3>
                    <canvas id="reportChart"></canvas>
                </div>

                <div class="card">
                    <h3>Detailed Report Data</h3>
                    <table class="data-table">
                        <thead id="reportTableHead">
                        </thead>
                        <tbody id="reportTableBody">
                        </tbody>
                    </table>
                </div>
            </section>

        </main>

        <!-- Footer -->
        <footer class="footer">
            <p>&copy; 2026 RetailForecast - Intelligent Inventory Management System</p>
        </footer>
    </div>

    <!-- Chart.js Library -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@3.9.1/dist/chart.min.js"></script>
    <!-- Main Application Script -->
    <script src="script.js"></script>
</body>
</html>



#script js

// ========================================
// RETAIL DEMAND FORECASTING & INVENTORY MANAGEMENT SYSTEM
// ========================================

// ========== DATA MANAGEMENT ==========
const DataManager = {
    products: [],
    sales: [],
    forecasts: [],
    alerts: [],

    // Initialize demo data
    initializeDemoData() {
        this.products = [
            { id: 'P001', name: 'Laptop Pro', category: 'Electronics', stock: 45, minThreshold: 20, maxThreshold: 100, unitPrice: 1299 },
            { id: 'P002', name: 'Wireless Mouse', category: 'Electronics', stock: 150, minThreshold: 50, maxThreshold: 300, unitPrice: 29.99 },
            { id: 'P003', name: 'USB-C Cable', category: 'Electronics', stock: 80, minThreshold: 100, maxThreshold: 500, unitPrice: 12.99 },
            { id: 'P004', name: 'Winter Jacket', category: 'Clothing', stock: 35, minThreshold: 25, maxThreshold: 150, unitPrice: 89.99 },
            { id: 'P005', name: 'Running Shoes', category: 'Clothing', stock: 120, minThreshold: 40, maxThreshold: 200, unitPrice: 129.99 },
            { id: 'P006', name: 'Organic Coffee', category: 'Groceries', stock: 200, minThreshold: 100, maxThreshold: 500, unitPrice: 9.99 },
        ];

        // Generate 90 days of sales data
        const today = new Date();
        for (let i = 90; i >= 0; i--) {
            const date = new Date(today);
            date.setDate(date.getDate() - i);
            
            this.products.forEach(product => {
                const dailySales = Math.floor(Math.random() * 50) + 5;
                for (let j = 0; j < dailySales; j++) {
                    this.sales.push({
                        id: `S${this.sales.length + 1}`,
                        productId: product.id,
                        quantity: Math.floor(Math.random() * 3) + 1,
                        date: date.toISOString().split('T')[0],
                        price: product.unitPrice
                    });
                }
            });
        }

        this.generateAlerts();
    },

    addProduct(product) {
        const newProduct = {
            id: `P${String(this.products.length + 1).padStart(3, '0')}`,
            ...product
        };
        this.products.push(newProduct);
        return newProduct;
    },

    recordSale(saleData) {
        const newSale = {
            id: `S${String(this.sales.length + 1).padStart(6, '0')}`,
            ...saleData
        };
        this.sales.push(newSale);

        // Update product stock
        const product = this.products.find(p => p.id === saleData.productId);
        if (product) {
            product.stock -= parseInt(saleData.quantity);
        }

        return newSale;
    },

    generateAlerts() {
        this.alerts = [];
        
        this.products.forEach(product => {
            if (product.stock <= product.minThreshold) {
                this.alerts.push({
                    type: 'low-stock',
                    severity: product.stock === 0 ? 'critical' : 'warning',
                    productId: product.id,
                    productName: product.name,
                    message: product.stock === 0 
                        ? `${product.name} is out of stock!` 
                        : `${product.name} stock is below minimum threshold (${product.stock}/${product.minThreshold})`,
                    timestamp: new Date()
                });
            } else if (product.stock >= product.maxThreshold) {
                this.alerts.push({
                    type: 'overstock',
                    severity: 'info',
                    productId: product.id,
                    productName: product.name,
                    message: `${product.name} stock exceeds maximum threshold (${product.stock}/${product.maxThreshold})`,
                    timestamp: new Date()
                });
            }
        });
    },

    getProductSalesHistory(productId, days = 30) {
        const cutoffDate = new Date();
        cutoffDate.setDate(cutoffDate.getDate() - days);
        
        return this.sales.filter(sale => 
            sale.productId === productId && 
            new Date(sale.date) >= cutoffDate
        );
    },

    getDailySalesData(days = 30) {
        const cutoffDate = new Date();
        cutoffDate.setDate(cutoffDate.getDate() - days);
        
        const dailyData = {};
        
        this.sales.forEach(sale => {
            if (new Date(sale.date) >= cutoffDate) {
                if (!dailyData[sale.date]) {
                    dailyData[sale.date] = 0;
                }
                dailyData[sale.date] += sale.quantity;
            }
        });

        return Object.keys(dailyData).sort().map(date => ({
            date,
            quantity: dailyData[date]
        }));
    }
};

// ========== FORECASTING ENGINE ==========
const ForecastingEngine = {
    // Simple Moving Average
    calculateMovingAverage(data, period = 7) {
        const result = [];
        for (let i = 0; i < data.length - period + 1; i++) {
            const sum = data.slice(i, i + period).reduce((a, b) => a + b, 0);
            result.push(sum / period);
        }
        return result;
    },

    // Exponential Smoothing
    exponentialSmoothing(data, alpha = 0.3) {
        if (data.length === 0) return [];
        
        const result = [data[0]];
        for (let i = 1; i < data.length; i++) {
            const forecast = alpha * data[i - 1] + (1 - alpha) * result[i - 1];
            result.push(forecast);
        }
        return result;
    },

    // Linear regression trend
    calculateTrend(data) {
        const n = data.length;
        let sumX = 0, sumY = 0, sumXY = 0, sumX2 = 0;

        for (let i = 0; i < n; i++) {
            sumX += i;
            sumY += data[i];
            sumXY += i * data[i];
            sumX2 += i * i;
        }

        const slope = (n * sumXY - sumX * sumY) / (n * sumX2 - sumX * sumX);
        const intercept = (sumY - slope * sumX) / n;

        return { slope, intercept };
    },

    forecastDemand(productId, days = 30) {
        const salesHistory = DataManager.getProductSalesHistory(productId, 90);
        
        if (salesHistory.length === 0) {
            return {
                productId,
                dailyDemand: 0,
                totalDemand: 0,
                trend: 'stable',
                confidence: 0
            };
        }

        // Aggregate by date
        const dailyData = {};
        salesHistory.forEach(sale => {
            dailyData[sale.date] = (dailyData[sale.date] || 0) + sale.quantity;
        });

        const quantities = Object.values(dailyData).sort((a, b) => new Date(Object.keys(dailyData).find(k => dailyData[k] === a)) - new Date(Object.keys(dailyData).find(k => dailyData[k] === b)));

        // Calculate metrics
        const avgDaily = quantities.reduce((a, b) => a + b) / quantities.length;
        const trend = this.calculateTrend(quantities);
        const forecast = this.exponentialSmoothing(quantities);
        const lastForecast = forecast[forecast.length - 1];

        // Determine trend direction
        let trendDirection = 'stable';
        if (trend.slope > 0.5) trendDirection = 'increasing';
        else if (trend.slope < -0.5) trendDirection = 'decreasing';

        // Calculate confidence (based on data consistency)
        const variance = quantities.reduce((sum, val) => sum + Math.pow(val - avgDaily, 2), 0) / quantities.length;
        const stdDev = Math.sqrt(variance);
        const cv = stdDev / avgDaily; // Coefficient of variation
        const confidence = Math.max(60, Math.min(99, 100 - (cv * 30)));

        return {
            productId,
            dailyDemand: Math.round(lastForecast),
            totalDemand: Math.round(lastForecast * days),
            trend: trendDirection,
            confidence: Math.round(confidence)
        };
    },

    forecastAllProducts(days = 30) {
        return DataManager.products.map(product => {
            const forecast = this.forecastDemand(product.id, days);
            return {
                ...forecast,
                productName: product.name
            };
        });
    }
};

// ========== UI MANAGER ==========
const UIManager = {
    currentSection: 'dashboard',
    charts: {},

    init() {
        this.setupEventListeners();
        this.displayDashboard();
    },

    setupEventListeners() {
        // Navigation
        document.querySelectorAll('.nav-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                this.switchSection(e.target.dataset.section);
            });
        });

        // Product Form
        document.getElementById('productForm').addEventListener('submit', (e) => {
            e.preventDefault();
            this.handleAddProduct();
        });

        // Sales Form
        document.getElementById('salesForm').addEventListener('submit', (e) => {
            e.preventDefault();
            this.handleRecordSale();
        });

        // Forecasting
        document.getElementById('generateForecastBtn').addEventListener('click', () => {
            this.displayForecasting();
        });

        // Alerts
        document.getElementById('clearAlertsBtn').addEventListener('click', () => {
            DataManager.alerts = [];
            this.displayAlerts();
        });

        document.querySelectorAll('.alert-filters input[type="checkbox"]').forEach(checkbox => {
            checkbox.addEventListener('change', () => this.displayAlerts());
        });

        // Reports
        document.getElementById('generateReportBtn').addEventListener('click', () => {
            this.generateReport();
        });

        document.getElementById('exportReportBtn').addEventListener('click', () => {
            this.exportReportAsCSV();
        });

        // Search and filter
        document.getElementById('productSearch').addEventListener('input', () => {
            this.displayProducts();
        });

        document.getElementById('categoryFilter').addEventListener('change', () => {
            this.displayProducts();
        });

        document.getElementById('filterSalesBtn').addEventListener('click', () => {
            this.displaySalesData();
        });
    },

    switchSection(section) {
        // Hide all sections
        document.querySelectorAll('.section').forEach(sec => {
            sec.classList.remove('active');
        });

        // Remove active from all nav buttons
        document.querySelectorAll('.nav-btn').forEach(btn => {
            btn.classList.remove('active');
        });

        // Show selected section
        document.getElementById(section).classList.add('active');
        document.querySelector(`[data-section="${section}"]`).classList.add('active');

        this.currentSection = section;

        // Display appropriate content
        switch(section) {
            case 'dashboard':
                this.displayDashboard();
                break;
            case 'products':
                this.displayProducts();
                break;
            case 'sales':
                this.displaySalesData();
                break;
            case 'forecasting':
                this.displayForecasting();
                break;
            case 'inventory':
                this.displayInventory();
                break;
            case 'alerts':
                this.displayAlerts();
                break;
            case 'reports':
                this.displayReports();
                break;
        }
    },

    displayDashboard() {
        // Update metrics
        document.getElementById('totalProducts').textContent = DataManager.products.length;
        
        const last30Days = DataManager.getDailySalesData(30);
        const totalSales = last30Days.reduce((sum, d) => sum + d.quantity, 0);
        document.getElementById('totalSales').textContent = totalSales;

        // Stock health calculation
        const healthyStock = DataManager.products.filter(p => 
            p.stock > p.minThreshold && p.stock < p.maxThreshold
        ).length;
        const stockHealth = Math.round((healthyStock / DataManager.products.length) * 100);
        document.getElementById('stockHealth').textContent = stockHealth + '%';

        // Draw sales trend chart
        this.drawSalesTrendChart();

        // Draw inventory distribution chart
        this.drawInventoryDistributionChart();

        // Display alerts preview
        this.displayAlertsPreview();
    },

    displayProducts() {
        const searchTerm = document.getElementById('productSearch').value.toLowerCase();
        const categoryFilter = document.getElementById('categoryFilter').value;

        // Update product form select for sales
        const saleProductSelect = document.getElementById('saleProductId');
        saleProductSelect.innerHTML = DataManager.products
            .map(p => `<option value="${p.id}">${p.name}</option>`)
            .join('');

        // Filter and display products
        let filteredProducts = DataManager.products;

        if (searchTerm) {
            filteredProducts = filteredProducts.filter(p =>
                p.name.toLowerCase().includes(searchTerm) ||
                p.id.toLowerCase().includes(searchTerm)
            );
        }

        if (categoryFilter) {
            filteredProducts = filteredProducts.filter(p => p.category === categoryFilter);
        }

        const tableBody = document.getElementById('productsTableBody');
        tableBody.innerHTML = filteredProducts.map(product => `
            <tr>
                <td>${product.id}</td>
                <td>${product.name}</td>
                <td>${product.category}</td>
                <td>${product.stock}</td>
                <td>${product.minThreshold}</td>
                <td>${product.maxThreshold}</td>
                <td>$${product.unitPrice.toFixed(2)}</td>
                <td>
                    <button class="btn btn-secondary table-action-btn" onclick="UIManager.editProduct('${product.id}')">Edit</button>
                </td>
            </tr>
        `).join('');
    },

    handleAddProduct() {
        const product = {
            name: document.getElementById('productName').value,
            category: document.getElementById('productCategory').value,
            stock: parseInt(document.getElementById('initialStock').value),
            minThreshold: parseInt(document.getElementById('minThreshold').value),
            maxThreshold: parseInt(document.getElementById('maxThreshold').value),
            unitPrice: parseFloat(document.getElementById('unitPrice').value)
        };

        DataManager.addProduct(product);
        DataManager.generateAlerts();

        // Reset form
        document.getElementById('productForm').reset();

        // Show success message
        this.showMessage('Product added successfully!', 'success');

        this.displayProducts();
    },

    displaySalesData() {
        const startDate = document.getElementById('startDate').value;
        const endDate = document.getElementById('endDate').value;
        const searchTerm = document.getElementById('salesSearch').value.toLowerCase();

        let filteredSales = DataManager.sales;

        if (startDate) {
            filteredSales = filteredSales.filter(s => new Date(s.date) >= new Date(startDate));
        }

        if (endDate) {
            filteredSales = filteredSales.filter(s => new Date(s.date) <= new Date(endDate));
        }

        if (searchTerm) {
            filteredSales = filteredSales.filter(s => {
                const product = DataManager.products.find(p => p.id === s.productId);
                return s.id.toLowerCase().includes(searchTerm) || 
                       (product && product.name.toLowerCase().includes(searchTerm));
            });
        }

        const tableBody = document.getElementById('salesTableBody');
        tableBody.innerHTML = filteredSales.slice(-100).map(sale => {
            const product = DataManager.products.find(p => p.id === sale.productId);
            const total = sale.quantity * sale.price;
            return `
                <tr>
                    <td>${sale.id}</td>
                    <td>${product ? product.name : 'Unknown'}</td>
                    <td>${sale.quantity}</td>
                    <td>${sale.date}</td>
                    <td>$${sale.price.toFixed(2)}</td>
                    <td>$${total.toFixed(2)}</td>
                </tr>
            `;
        }).join('');
    },

    handleRecordSale() {
        const sale = {
            productId: document.getElementById('saleProductId').value,
            quantity: parseInt(document.getElementById('saleQuantity').value),
            date: document.getElementById('saleDate').value,
            price: parseFloat(document.getElementById('salePrice').value)
        };

        DataManager.recordSale(sale);
        DataManager.generateAlerts();

        // Reset form
        document.getElementById('salesForm').reset();

        this.showMessage('Sale recorded successfully!', 'success');
        this.displaySalesData();
        this.displayDashboard();
    },

    displayForecasting() {
        const forecastDays = parseInt(document.getElementById('forecastDays').value) || 30;
        
        const statusEl = document.getElementById('forecastStatus');
        statusEl.classList.add('info');
        statusEl.textContent = `Generating forecast for ${forecastDays} days...`;

        setTimeout(() => {
            const forecasts = ForecastingEngine.forecastAllProducts(forecastDays);
            DataManager.forecasts = forecasts;

            statusEl.classList.remove('info');
            statusEl.classList.add('success');
            statusEl.textContent = `Forecast generated successfully with average ${Math.round(forecasts.reduce((sum, f) => sum + f.confidence, 0) / forecasts.length)}% confidence!`;

            this.drawForecastChart(forecasts, forecastDays);
            this.displayForecastTable(forecasts);
        }, 500);
    },

    displayInventory() {
        // Calculate summary metrics
        const totalValue = DataManager.products.reduce((sum, p) => sum + (p.stock * p.unitPrice), 0);
        document.getElementById('totalInventoryValue').textContent = `$${totalValue.toFixed(2)}`;

        const lowStockItems = DataManager.products.filter(p => p.stock <= p.minThreshold).length;
        document.getElementById('lowStockCount').textContent = lowStockItems;

        const overStockItems = DataManager.products.filter(p => p.stock >= p.maxThreshold).length;
        document.getElementById('overStockCount').textContent = overStockItems;

        const optimalItems = DataManager.products.filter(p => 
            p.stock > p.minThreshold && p.stock < p.maxThreshold
        ).length;
        document.getElementById('optimalStockCount').textContent = optimalItems;

        // Display inventory table
        const tableBody = document.getElementById('inventoryTableBody');
        tableBody.innerHTML = DataManager.products.map(product => {
            let status = 'Optimal';
            let statusClass = 'status-optimal';

            if (product.stock <= product.minThreshold) {
                status = product.stock === 0 ? 'Out of Stock' : 'Low Stock';
                statusClass = 'status-critical';
            } else if (product.stock >= product.maxThreshold) {
                status = 'Over Stock';
                statusClass = 'status-overstock';
            }

            // Calculate days to stockout
            const dailySales = ForecastingEngine.forecastDemand(product.id);
            const daysToStockout = dailySales.dailyDemand > 0 
                ? Math.ceil(product.stock / dailySales.dailyDemand)
                : 999;

            const inventoryValue = (product.stock * product.unitPrice).toFixed(2);

            return `
                <tr>
                    <td>${product.name}</td>
                    <td>${product.stock}</td>
                    <td>${product.minThreshold}</td>
                    <td>${product.maxThreshold}</td>
                    <td class="${statusClass}">${status}</td>
                    <td>$${inventoryValue}</td>
                    <td>${daysToStockout === 999 ? '∞' : daysToStockout} days</td>
                </tr>
            `;
        }).join('');
    },

    displayAlerts() {
        DataManager.generateAlerts();

        const filterLowStock = document.getElementById('filterLowStock').checked;
        const filterOverStock = document.getElementById('filterOverStock').checked;
        const filterStockOut = document.getElementById('filterStockOut').checked;

        let filteredAlerts = DataManager.alerts;

        if (filterLowStock || filterOverStock || filterStockOut) {
            filteredAlerts = filteredAlerts.filter(alert => {
                if (alert.type === 'low-stock' && alert.severity === 'critical' && !filterStockOut) return false;
                if (alert.type === 'low-stock' && alert.severity === 'warning' && !filterLowStock) return false;
                if (alert.type === 'overstock' && !filterOverStock) return false;
                return true;
            });
        }

        const container = document.getElementById('alertsContainer');
        container.innerHTML = filteredAlerts.map(alert => {
            const alertClass = alert.type === 'low-stock' 
                ? (alert.severity === 'critical' ? 'alert-stockout' : 'alert-low-stock')
                : 'alert-overstock';

            return `
                <div class="alert-item ${alertClass}">
                    <h4>${alert.productName}</h4>
                    <p>${alert.message}</p>
                    <small>${new Date(alert.timestamp).toLocaleString()}</small>
                </div>
            `;
        }).join('');

        if (filteredAlerts.length === 0) {
            container.innerHTML = '<p style="text-align: center; color: var(--text-light);">No alerts at this time. Great job!</p>';
        }
    },

    displayAlertsPreview() {
        DataManager.generateAlerts();
        const preview = document.getElementById('alertsPreview');
        const alerts = DataManager.alerts.slice(0, 3);

        preview.innerHTML = alerts.map(alert => {
            const alertClass = alert.type === 'low-stock' ? 'alert-low-stock' : 'alert-overstock';
            return `
                <div class="alert-item ${alertClass}">
                    <h4>${alert.productName}</h4>
                    <p>${alert.message}</p>
                </div>
            `;
        }).join('');

        if (alerts.length === 0) {
            preview.innerHTML = '<p style="color: var(--text-light);">No alerts. All inventory levels are healthy!</p>';
        }
    },

    displayReports() {
        this.generateReport();
    },

    generateReport() {
        const reportType = document.getElementById('reportType').value;
        const period = parseInt(document.getElementById('reportPeriod').value);

        let data, labels, title;

        switch(reportType) {
            case 'sales-trend':
                data = DataManager.getDailySalesData(period);
                labels = data.map(d => d.date);
                title = `Sales Trend - Last ${period} Days`;
                this.drawReportChart(labels, [data.map(d => d.quantity)], title, 'Sales Volume');
                this.displaySalesReportTable(data);
                break;

            case 'demand-forecast':
                const forecasts = ForecastingEngine.forecastAllProducts(30);
                labels = forecasts.map(f => f.productName);
                title = 'Demand Forecast - 30 Days';
                this.drawReportChart(labels, [forecasts.map(f => f.totalDemand)], title, 'Forecasted Units');
                this.displayForecastReportTable(forecasts);
                break;

            case 'inventory-analysis':
                labels = DataManager.products.map(p => p.name);
                title = 'Current Inventory Levels';
                this.drawReportChart(labels, [DataManager.products.map(p => p.stock)], title, 'Stock Units');
                this.displayInventoryReportTable();
                break;

            case 'category-performance':
                const categories = [...new Set(DataManager.products.map(p => p.category))];
                labels = categories;
                const categoryData = categories.map(cat => {
                    const products = DataManager.products.filter(p => p.category === cat);
                    const categoryValue = products.reduce((sum, p) => sum + (p.stock * p.unitPrice), 0);
                    return categoryValue;
                });
                title = 'Inventory Value by Category';
                this.drawReportChart(labels, [categoryData], title, 'Inventory Value ($)');
                this.displayCategoryReportTable(categories, categoryData);
                break;
        }
    },

    drawSalesTrendChart() {
        const data = DataManager.getDailySalesData(30);
        const ctx = document.getElementById('salesTrendChart').getContext('2d');

        if (this.charts.salesTrend) {
            this.charts.salesTrend.destroy();
        }

        this.charts.salesTrend = new Chart(ctx, {
            type: 'line',
            data: {
                labels: data.map(d => d.date),
                datasets: [{
                    label: 'Daily Sales',
                    data: data.map(d => d.quantity),
                    borderColor: '#2563eb',
                    backgroundColor: 'rgba(37, 99, 235, 0.1)',
                    tension: 0.4,
                    fill: true
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: true }
                },
                scales: {
                    y: { beginAtZero: true }
                }
            }
        });
    },

    drawInventoryDistributionChart() {
        const products = DataManager.products.slice(0, 6);
        const ctx = document.getElementById('inventoryDistChart').getContext('2d');

        if (this.charts.inventoryDist) {
            this.charts.inventoryDist.destroy();
        }

        this.charts.inventoryDist = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: products.map(p => p.name),
                datasets: [{
                    label: 'Current Stock',
                    data: products.map(p => p.stock),
                    backgroundColor: '#10b981'
                },
                {
                    label: 'Min Threshold',
                    data: products.map(p => p.minThreshold),
                    backgroundColor: '#f59e0b'
                },
                {
                    label: 'Max Threshold',
                    data: products.map(p => p.maxThreshold),
                    backgroundColor: '#3b82f6'
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: true }
                },
                scales: {
                    y: { beginAtZero: true }
                }
            }
        });
    },

    drawForecastChart(forecasts, days) {
        const ctx = document.getElementById('forecastChart').getContext('2d');

        if (this.charts.forecast) {
            this.charts.forecast.destroy();
        }

        this.charts.forecast = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: forecasts.map(f => f.productName),
                datasets: [{
                    label: `${days}-Day Forecast`,
                    data: forecasts.map(f => f.totalDemand),
                    backgroundColor: '#3b82f6',
                    borderColor: '#1e40af',
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: true }
                },
                scales: {
                    y: { beginAtZero: true }
                }
            }
        });
    },

    drawReportChart(labels, datasets, title, yAxisLabel) {
        const ctx = document.getElementById('reportChart').getContext('2d');

        if (this.charts.report) {
            this.charts.report.destroy();
        }

        const colors = ['#2563eb', '#10b981', '#f59e0b', '#ef4444'];

        this.charts.report = new Chart(ctx, {
            type: 'bar',
            data: {
                labels,
                datasets: datasets.map((data, idx) => ({
                    label: `Dataset ${idx + 1}`,
                    data,
                    backgroundColor: colors[idx % colors.length],
                    borderColor: colors[idx % colors.length],
                    borderWidth: 1
                }))
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    title: { display: true, text: title },
                    legend: { display: true }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        title: { display: true, text: yAxisLabel }
                    }
                }
            }
        });
    },

    displayForecastTable(forecasts) {
        const tableBody = document.getElementById('forecastTableBody');
        tableBody.innerHTML = forecasts.map(forecast => `
            <tr>
                <td>${forecast.productName}</td>
                <td>${forecast.dailyDemand}</td>
                <td>${forecast.totalDemand}</td>
                <td>${forecast.trend}</td>
                <td>${forecast.confidence}%</td>
            </tr>
        `).join('');
    },

    displaySalesReportTable(data) {
        const tableHead = document.getElementById('reportTableHead');
        tableHead.innerHTML = `
            <tr>
                <th>Date</th>
                <th>Units Sold</th>
            </tr>
        `;

        const tableBody = document.getElementById('reportTableBody');
        tableBody.innerHTML = data.map(item => `
            <tr>
                <td>${item.date}</td>
                <td>${item.quantity}</td>
            </tr>
        `).join('');
    },

    displayForecastReportTable(forecasts) {
        const tableHead = document.getElementById('reportTableHead');
        tableHead.innerHTML = `
            <tr>
                <th>Product</th>
                <th>Daily Demand</th>
                <th>30-Day Forecast</th>
                <th>Trend</th>
                <th>Confidence</th>
            </tr>
        `;

        const tableBody = document.getElementById('reportTableBody');
        tableBody.innerHTML = forecasts.map(forecast => `
            <tr>
                <td>${forecast.productName}</td>
                <td>${forecast.dailyDemand}</td>
                <td>${forecast.totalDemand}</td>
                <td>${forecast.trend}</td>
                <td>${forecast.confidence}%</td>
            </tr>
        `).join('');
    },

    displayInventoryReportTable() {
        const tableHead = document.getElementById('reportTableHead');
        tableHead.innerHTML = `
            <tr>
                <th>Product</th>
                <th>Current Stock</th>
                <th>Min Threshold</th>
                <th>Max Threshold</th>
                <th>Inventory Value</th>
            </tr>
        `;

        const tableBody = document.getElementById('reportTableBody');
        tableBody.innerHTML = DataManager.products.map(product => `
            <tr>
                <td>${product.name}</td>
                <td>${product.stock}</td>
                <td>${product.minThreshold}</td>
                <td>${product.maxThreshold}</td>
                <td>$${(product.stock * product.unitPrice).toFixed(2)}</td>
            </tr>
        `).join('');
    },

    displayCategoryReportTable(categories, values) {
        const tableHead = document.getElementById('reportTableHead');
        tableHead.innerHTML = `
            <tr>
                <th>Category</th>
                <th>Inventory Value</th>
            </tr>
        `;

        const tableBody = document.getElementById('reportTableBody');
        tableBody.innerHTML = categories.map((cat, idx) => `
            <tr>
                <td>${cat}</td>
                <td>$${values[idx].toFixed(2)}</td>
            </tr>
        `).join('');
    },

    editProduct(productId) {
        this.showMessage('Edit feature coming soon!', 'info');
    },

    showMessage(message, type) {
        const statusEl = document.getElementById('forecastStatus') || document.createElement('div');
        statusEl.className = `status-message ${type}`;
        statusEl.textContent = message;
        statusEl.style.display = 'block';

        setTimeout(() => {
            statusEl.style.display = 'none';
        }, 3000);
    },

    exportReportAsCSV() {
        const reportType = document.getElementById('reportType').value;
        const tableBody = document.getElementById('reportTableBody');
        const rows = tableBody.querySelectorAll('tr');

        if (rows.length === 0) {
            this.showMessage('No data to export!', 'error');
            return;
        }

        let csv = [];
        const headers = Array.from(document.getElementById('reportTableHead').querySelectorAll('th'))
            .map(th => th.textContent);
        csv.push(headers.join(','));

        rows.forEach(row => {
            const values = Array.from(row.querySelectorAll('td'))
                .map(td => {
                    let value = td.textContent;
                    if (value.includes(',')) {
                        value = `"${value}"`;
                    }
                    return value;
                });
            csv.push(values.join(','));
        });

        const csvContent = csv.join('\n');
        const blob = new Blob([csvContent], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `report-${reportType}-${new Date().toISOString().split('T')[0]}.csv`;
        document.body.appendChild(a);
        a.click();
        window.URL.revokeObjectURL(url);
        document.body.removeChild(a);

        this.showMessage('Report exported successfully!', 'success');
    }
};

// ========== APPLICATION INITIALIZATION ==========
document.addEventListener('DOMContentLoaded', () => {
    // Initialize data
    DataManager.initializeDemoData();

    // Initialize UI
    UIManager.init();

    console.log('✅ Retail Demand Forecasting & Inventory Management System Initialized');
    console.log(`📊 Loaded ${DataManager.products.length} products and ${DataManager.sales.length} sales records`);
});



#style jss

 * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root {
    --primary-color: #2563eb;
    --secondary-color: #1e40af;
    --success-color: #10b981;
    --warning-color: #f59e0b;
    --danger-color: #ef4444;
    --info-color: #3b82f6;
    --light-bg: #f3f4f6;
    --dark-bg: #1f2937;
    --border-color: #e5e7eb;
    --text-dark: #111827;
    --text-light: #6b7280;
    --shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: var(--light-bg);
    color: var(--text-dark);
    line-height: 1.6;
}

.container {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

/* HEADER STYLING */
.header {
    background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
    color: white;
    padding: 2rem;
    box-shadow: var(--shadow-lg);
    position: sticky;
    top: 0;
    z-index: 100;
}

.logo {
    margin-bottom: 1.5rem;
}

.logo h1 {
    font-size: 2rem;
    margin-bottom: 0.5rem;
}

.logo p {
    font-size: 0.9rem;
    opacity: 0.9;
}

.nav-menu {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
}

.nav-btn {
    padding: 0.75rem 1.5rem;
    background-color: rgba(255, 255, 255, 0.2);
    border: 2px solid rgba(255, 255, 255, 0.3);
    color: white;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: all 0.3s ease;
    font-weight: 500;
}

.nav-btn:hover {
    background-color: rgba(255, 255, 255, 0.3);
    border-color: rgba(255, 255, 255, 0.5);
}

.nav-btn.active {
    background-color: white;
    color: var(--primary-color);
    border-color: white;
}

/* MAIN CONTENT */
.main-content {
    flex: 1;
    padding: 2rem;
    max-width: 1400px;
    margin: 0 auto;
    width: 100%;
}

.section {
    display: none;
    animation: fadeIn 0.3s ease;
}

.section.active {
    display: block;
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.section h2 {
    margin-bottom: 2rem;
    font-size: 1.8rem;
    color: var(--text-dark);
    border-bottom: 3px solid var(--primary-color);
    padding-bottom: 1rem;
}

/* CARDS */
.card {
    background: white;
    border-radius: 0.75rem;
    padding: 1.5rem;
    box-shadow: var(--shadow);
    margin-bottom: 1.5rem;
    border: 1px solid var(--border-color);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow-lg);
}

.card h3 {
    margin-bottom: 1.5rem;
    color: var(--primary-color);
    font-size: 1.25rem;
}

.card h4 {
    color: var(--text-dark);
    margin-bottom: 0.5rem;
}

/* DASHBOARD GRID */
.dashboard-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
}

.metric-card {
    text-align: center;
    border-left: 5px solid var(--primary-color);
}

.metric-card h3 {
    font-size: 0.9rem;
    margin-bottom: 0.5rem;
    color: var(--text-light);
    font-weight: 600;
}

.metric-value {
    font-size: 2rem;
    font-weight: bold;
    color: var(--primary-color);
    margin-bottom: 0.5rem;
}

.metric-label {
    font-size: 0.85rem;
    color: var(--text-light);
}

/* CHARTS */
.dashboard-charts {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
}

.chart-card {
    min-height: 350px;
}

canvas {
    max-height: 300px;
}

/* FORMS */
.form-container {
    margin-bottom: 2rem;
}

.form-group {
    margin-bottom: 1.5rem;
}

.form-group label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 600;
    color: var(--text-dark);
}

.form-group input,
.form-group select,
.form-group textarea {
    width: 100%;
    padding: 0.75rem;
    border: 1px solid var(--border-color);
    border-radius: 0.5rem;
    font-size: 1rem;
    font-family: inherit;
    transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

form {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
}

#productForm {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

#productForm .form-group:last-child {
    grid-column: 1 / -1;
}

/* BUTTONS */
.btn {
    padding: 0.75rem 1.5rem;
    border: none;
    border-radius: 0.5rem;
    cursor: pointer;
    font-size: 1rem;
    font-weight: 600;
    transition: all 0.3s ease;
    display: inline-block;
}

.btn-primary {
    background-color: var(--primary-color);
    color: white;
}

.btn-primary:hover {
    background-color: var(--secondary-color);
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.btn-secondary {
    background-color: var(--text-light);
    color: white;
}

.btn-secondary:hover {
    background-color: var(--text-dark);
}

.btn-success {
    background-color: var(--success-color);
    color: white;
    padding: 0.5rem 1rem;
    font-size: 0.9rem;
}

.btn-success:hover {
    background-color: #059669;
}

.btn-danger {
    background-color: var(--danger-color);
    color: white;
    padding: 0.5rem 1rem;
    font-size: 0.9rem;
}

.btn-danger:hover {
    background-color: #dc2626;
}

/* TABLES */
.data-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.9rem;
}

.data-table thead {
    background-color: var(--light-bg);
    border-bottom: 2px solid var(--border-color);
}

.data-table th {
    padding: 1rem;
    text-align: left;
    font-weight: 600;
    color: var(--text-dark);
}

.data-table td {
    padding: 0.75rem 1rem;
    border-bottom: 1px solid var(--border-color);
}

.data-table tbody tr:hover {
    background-color: var(--light-bg);
}

.table-action-btn {
    padding: 0.4rem 0.8rem;
    margin-right: 0.5rem;
    font-size: 0.8rem;
}

.status-optimal {
    color: var(--success-color);
    font-weight: 600;
}

.status-low {
    color: var(--warning-color);
    font-weight: 600;
}

.status-critical {
    color: var(--danger-color);
    font-weight: 600;
}

.status-overstock {
    color: var(--info-color);
    font-weight: 600;
}

/* SEARCH & FILTER */
.search-filter {
    display: flex;
    gap: 1rem;
    margin-bottom: 1.5rem;
    flex-wrap: wrap;
}

.search-filter input,
.search-filter select {
    padding: 0.75rem;
    border: 1px solid var(--border-color);
    border-radius: 0.5rem;
    flex: 1;
    min-width: 150px;
}

.search-filter input:focus,
.search-filter select:focus {
    outline: none;
    border-color: var(--primary-color);
}

/* ALERTS */
.alerts-list {
    max-height: 300px;
    overflow-y: auto;
}

.alert-item {
    padding: 1rem;
    margin-bottom: 1rem;
    border-left: 4px solid;
    border-radius: 0.5rem;
    background-color: var(--light-bg);
    animation: slideIn 0.3s ease;
}

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateX(-20px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

.alert-low-stock {
    border-left-color: var(--warning-color);
    background-color: rgba(245, 158, 11, 0.1);
}

.alert-overstock {
    border-left-color: var(--info-color);
    background-color: rgba(59, 130, 246, 0.1);
}

.alert-stockout {
    border-left-color: var(--danger-color);
    background-color: rgba(239, 68, 68, 0.1);
}

.alert-item h4 {
    margin-bottom: 0.5rem;
    font-size: 1rem;
}

.alert-item p {
    font-size: 0.9rem;
    color: var(--text-light);
}

.alerts-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
}

.alerts-controls {
    margin-bottom: 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
}

.alert-filters {
    display: flex;
    gap: 1.5rem;
}

.alert-filters label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
}

.alert-filters input[type="checkbox"] {
    cursor: pointer;
}

/* INVENTORY SUMMARY */
.inventory-summary {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
}

.summary-card {
    text-align: center;
    border-top: 4px solid var(--primary-color);
}

.summary-card h4 {
    color: var(--text-light);
    font-size: 0.9rem;
    font-weight: 600;
}

.large-number {
    font-size: 2.5rem;
    font-weight: bold;
    color: var(--primary-color);
    margin: 1rem 0;
}

/* REPORT CONTROLS */
.report-controls {
    display: flex;
    gap: 1rem;
    margin-bottom: 2rem;
    flex-wrap: wrap;
    align-items: flex-end;
}

.report-controls .form-group {
    flex: 1;
    min-width: 150px;
    margin-bottom: 0;
}

.report-controls .form-group label {
    margin-bottom: 0.3rem;
    font-size: 0.9rem;
}

.report-controls select {
    width: 100%;
    padding: 0.75rem;
    border: 1px solid var(--border-color);
    border-radius: 0.5rem;
}

/* STATUS MESSAGE */
.status-message {
    padding: 1rem;
    margin-bottom: 1rem;
    border-radius: 0.5rem;
    display: none;
}

.status-message.success {
    background-color: rgba(16, 185, 129, 0.1);
    color: var(--success-color);
    border: 1px solid var(--success-color);
    display: block;
}

.status-message.error {
    background-color: rgba(239, 68, 68, 0.1);
    color: var(--danger-color);
    border: 1px solid var(--danger-color);
    display: block;
}

.status-message.info {
    background-color: rgba(59, 130, 246, 0.1);
    color: var(--info-color);
    border: 1px solid var(--info-color);
    display: block;
}

/* FOOTER */
.footer {
    background-color: var(--dark-bg);
    color: white;
    text-align: center;
    padding: 2rem;
    margin-top: 2rem;
}

/* RESPONSIVE DESIGN */
@media (max-width: 1024px) {
    .dashboard-charts {
        grid-template-columns: 1fr;
    }

    .nav-menu {
        flex-direction: column;
    }

    .nav-btn {
        width: 100%;
        text-align: center;
    }
}

@media (max-width: 768px) {
    .header {
        padding: 1rem;
    }

    .logo h1 {
        font-size: 1.5rem;
    }

    .main-content {
        padding: 1rem;
    }

    .dashboard-grid {
        grid-template-columns: 1fr;
    }

    .data-table {
        font-size: 0.8rem;
    }

    .data-table th,
    .data-table td {
        padding: 0.5rem;
    }

    form {
        grid-template-columns: 1fr;
    }

    .search-filter {
        flex-direction: column;
    }

    .search-filter input,
    .search-filter select {
        width: 100%;
    }

    .alerts-container {
        grid-template-columns: 1fr;
    }

    .report-controls {
        flex-direction: column;
    }

    .report-controls .form-group {
        width: 100%;
    }
}

@media (max-width: 480px) {
    .header {
        padding: 0.75rem;
    }

    .logo h1 {
        font-size: 1.25rem;
    }

    .logo p {
        font-size: 0.8rem;
    }

    .nav-menu {
        gap: 0.5rem;
    }

    .nav-btn {
        padding: 0.5rem 1rem;
        font-size: 0.9rem;
    }

    .main-content {
        padding: 0.75rem;
    }

    .section h2 {
        font-size: 1.3rem;
        margin-bottom: 1rem;
    }

    .metric-value {
        font-size: 1.5rem;
    }

    .card {
        padding: 1rem;
    }
}
