# Local-Board-Hubs
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Auckland Local Board Hubs Dashboard</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: #0f1419;
            color: #e2e8f0;
            overflow-x: hidden;
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%);
            padding: 1.5rem 2rem;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
            animation: pulse 3s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); opacity: 0.5; }
            50% { transform: scale(1.1); opacity: 0.8; }
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            position: relative;
            z-index: 1;
        }

        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        /* Main Container */
        .container {
            max-width: 1600px;
            margin: 0 auto;
            padding: 2rem;
        }

        /* Dashboard Grid */
        .dashboard-grid {
            display: grid;
            grid-template-columns: 300px 1fr;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        /* Control Panel */
        .control-panel {
            background: #1a202c;
            border-radius: 16px;
            padding: 1.5rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            border: 1px solid #2d3748;
        }

        .control-section {
            margin-bottom: 2rem;
        }

        .control-section h3 {
            font-size: 1.2rem;
            margin-bottom: 1rem;
            color: #60a5fa;
        }

        .control-group {
            margin-bottom: 1rem;
        }

        .control-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-size: 0.9rem;
            color: #94a3b8;
        }

        select, input[type="range"], input[type="number"] {
            width: 100%;
            padding: 0.5rem;
            background: #2d3748;
            border: 1px solid #4a5568;
            border-radius: 8px;
            color: #e2e8f0;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }

        select:hover, input:hover {
            border-color: #60a5fa;
            background: #374151;
        }

        select:focus, input:focus {
            outline: none;
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }

        .range-value {
            text-align: center;
            margin-top: 0.5rem;
            font-size: 1.2rem;
            color: #60a5fa;
            font-weight: 600;
        }

        .btn {
            background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 8px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            margin-top: 0.5rem;
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }

        .btn:hover::before {
            width: 300px;
            height: 300px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(59, 130, 246, 0.4);
        }

        /* Main Content Area */
        .main-content {
            background: #1a202c;
            border-radius: 16px;
            padding: 2rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            border: 1px solid #2d3748;
        }

        /* Tabs */
        .tabs {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
            border-bottom: 2px solid #2d3748;
            padding-bottom: 1rem;
        }

        .tab {
            padding: 0.75rem 1.5rem;
            background: #2d3748;
            border-radius: 8px 8px 0 0;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .tab.active {
            background: #3b82f6;
            transform: translateY(-2px);
        }

        .tab:hover:not(.active) {
            background: #374151;
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Map Container */
        .map-container {
            background: #0f1419;
            border-radius: 12px;
            padding: 2rem;
            height: 600px;
            position: relative;
            overflow: hidden;
            border: 2px solid #2d3748;
        }

        .hub-map {
            position: relative;
            width: 100%;
            height: 100%;
        }

        .hub-region {
            position: absolute;
            background: rgba(59, 130, 246, 0.2);
            border: 2px solid #3b82f6;
            border-radius: 12px;
            padding: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(5px);
        }

        .hub-region:hover {
            background: rgba(59, 130, 246, 0.4);
            transform: scale(1.05);
            box-shadow: 0 10px 30px rgba(59, 130, 246, 0.5);
            z-index: 10;
        }

        .hub-region h4 {
            font-size: 1.1rem;
            margin-bottom: 0.5rem;
            color: #60a5fa;
        }

        .hub-stats {
            font-size: 0.9rem;
            color: #94a3b8;
        }

        /* Statistics Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: #2d3748;
            border-radius: 12px;
            padding: 1.5rem;
            border: 1px solid #4a5568;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(90deg, #3b82f6, #60a5fa);
            transform: scaleX(0);
            transform-origin: left;
            transition: transform 0.3s ease;
        }

        .stat-card:hover::before {
            transform: scaleX(1);
        }

        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
            border-color: #60a5fa;
        }

        .stat-label {
            font-size: 0.9rem;
            color: #94a3b8;
            margin-bottom: 0.5rem;
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 600;
            color: #60a5fa;
            margin-bottom: 0.5rem;
        }

        .stat-change {
            font-size: 0.8rem;
            color: #10b981;
        }

        .stat-change.negative {
            color: #ef4444;
        }

        /* Analysis Table */
        .analysis-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 1rem;
        }

        .analysis-table th,
        .analysis-table td {
            padding: 1rem;
            text-align: left;
            border-bottom: 1px solid #2d3748;
        }

        .analysis-table th {
            background: #2d3748;
            color: #60a5fa;
            font-weight: 600;
            position: sticky;
            top: 0;
        }

        .analysis-table tr:hover {
            background: #374151;
        }

        /* Charts Container */
        .charts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }

        .chart-container {
            background: #2d3748;
            border-radius: 12px;
            padding: 1.5rem;
            border: 1px solid #4a5568;
        }

        .chart-container h4 {
            margin-bottom: 1rem;
            color: #60a5fa;
        }

        /* Loading Animation */
        .loading {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 1000;
        }

        .loading.active {
            display: block;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border: 3px solid #2d3748;
            border-top-color: #3b82f6;
            border-radius: 50%;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Responsive Design */
        @media (max-width: 1024px) {
            .dashboard-grid {
                grid-template-columns: 1fr;
            }

            .control-panel {
                position: sticky;
                top: 1rem;
                z-index: 100;
            }
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 1.8rem;
            }

            .tabs {
                flex-wrap: wrap;
            }

            .stats-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- Loading Spinner -->
    <div class="loading" id="loading">
        <div class="spinner"></div>
    </div>

    <!-- Header -->
    <header class="header">
        <h1>Auckland Local Board Hubs Dashboard</h1>
        <p>Strategic Planning & Analysis Tool for Operational Hub Implementation</p>
    </header>

    <!-- Main Container -->
    <div class="container">
        <div class="dashboard-grid">
            <!-- Control Panel -->
            <aside class="control-panel">
                <div class="control-section">
                    <h3>Hub Configuration</h3>
                    <div class="control-group">
                        <label for="hubCount">Number of Hubs</label>
                        <input type="range" id="hubCount" min="4" max="8" value="6" oninput="updateHubCount(this.value)">
                        <div class="range-value" id="hubCountValue">6</div>
                    </div>
                    <div class="control-group">
                        <label for="scenario">Scenario Model</label>
                        <select id="scenario" onchange="loadScenario(this.value)">
                            <option value="geographic">Geographic Proximity</option>
                            <option value="population">Population Balance</option>
                            <option value="economic">Economic Clusters</option>
                            <option value="transport">Transport Corridors</option>
                            <option value="custom">Custom Configuration</option>
                        </select>
                    </div>
                </div>

                <div class="control-section">
                    <h3>Analysis Parameters</h3>
                    <div class="control-group">
                        <label for="fundingModel">Funding Model</label>
                        <select id="fundingModel">
                            <option value="population">Population-based</option>
                            <option value="needs">Needs-based</option>
                            <option value="hybrid">Hybrid (50/50)</option>
                            <option value="performance">Performance-based</option>
                        </select>
                    </div>
                    <div class="control-group">
                        <label for="implementationSpeed">Implementation Timeline</label>
                        <select id="implementationSpeed">
                            <option value="rapid">Rapid (6-12 months)</option>
                            <option value="standard">Standard (12-18 months)</option>
                            <option value="phased">Phased (18-24 months)</option>
                            <option value="legislative">Legislative (24+ months)</option>
                        </select>
                    </div>
                </div>

                <div class="control-section">
                    <h3>Financial Parameters</h3>
                    <div class="control-group">
                        <label for="totalBudget">Total Budget (NZ$ millions)</label>
                        <input type="number" id="totalBudget" value="2000" min="1000" max="5000" step="100">
                    </div>
                    <div class="control-group">
                        <label for="borrowingCapacity">Borrowing Capacity (%)</label>
                        <input type="range" id="borrowingCapacity" min="0" max="50" value="20" oninput="updateBorrowingCapacity(this.value)">
                        <div class="range-value" id="borrowingValue">20%</div>
                    </div>
                </div>

                <button class="btn" onclick="runAnalysis()">Run Analysis</button>
                <button class="btn" onclick="exportReport()">Export Report</button>
            </aside>

            <!-- Main Content Area -->
            <main class="main-content">
                <!-- Tabs -->
                <div class="tabs">
                    <div class="tab active" onclick="switchTab('overview')">Overview</div>
                    <div class="tab" onclick="switchTab('demographics')">Demographics</div>
                    <div class="tab" onclick="switchTab('financial')">Financial Analysis</div>
                    <div class="tab" onclick="switchTab('implementation')">Implementation</div>
                    <div class="tab" onclick="switchTab('performance')">Performance Metrics</div>
                </div>

                <!-- Tab Contents -->
                <div id="overview" class="tab-content active">
                    <h2>Hub Configuration Overview</h2>
                    <div class="map-container">
                        <div class="hub-map" id="hubMap">
                            <!-- Hub regions will be dynamically generated -->
                        </div>
                    </div>
                    
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-label">Total Population</div>
                            <div class="stat-value" id="totalPopulation">1,717,500</div>
                            <div class="stat-change">+2.3% from 2018</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-label">Average Hub Size</div>
                            <div class="stat-value" id="avgHubSize">286,250</div>
                            <div class="stat-change">Balanced distribution</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-label">Cost Efficiency</div>
                            <div class="stat-value" id="costEfficiency">89%</div>
                            <div class="stat-change">+12% vs current</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-label">Service Coverage</div>
                            <div class="stat-value" id="serviceCoverage">94%</div>
                            <div class="stat-change">+8% improvement</div>
                        </div>
                    </div>
                </div>

                <div id="demographics" class="tab-content">
                    <h2>Demographic Analysis</h2>
                    <table class="analysis-table">
                        <thead>
                            <tr>
                                <th>Hub</th>
                                <th>Population</th>
                                <th>Growth Rate</th>
                                <th>Median Age</th>
                                <th>Diversity Index</th>
                                <th>Service Needs</th>
                            </tr>
                        </thead>
                        <tbody id="demographicsTable">
                            <!-- Table rows will be dynamically generated -->
                        </tbody>
                    </table>
                    
                    <div class="charts-grid">
                        <div class="chart-container">
                            <h4>Population Distribution</h4>
                            <canvas id="populationChart"></canvas>
                        </div>
                        <div class="chart-container">
                            <h4>Ethnic Diversity</h4>
                            <canvas id="diversityChart"></canvas>
                        </div>
                    </div>
                </div>

                <div id="financial" class="tab-content">
                    <h2>Financial Analysis</h2>
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-label">Total Investment Required</div>
                            <div class="stat-value" id="totalInvestment">$2.4B</div>
                            <div class="stat-change">Over 10 years</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-label">Annual Operating Cost</div>
                            <div class="stat-value" id="annualCost">$180M</div>
                            <div class="stat-change">Per hub: $30M</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-label">ROI Projection</div>
                            <div class="stat-value" id="roiProjection">3.2x</div>
                            <div class="stat-change">10-year horizon</div>
                        </div>
                    </div>

                    <table class="analysis-table">
                        <thead>
                            <tr>
                                <th>Hub</th>
                                <th>Budget Allocation</th>
                                <th>Capital Requirements</th>
                                <th>Operating Costs</th>
                                <th>Revenue Potential</th>
                                <th>Debt Capacity</th>
                            </tr>
                        </thead>
                        <tbody id="financialTable">
                            <!-- Table rows will be dynamically generated -->
                        </tbody>
                    </table>
                </div>

                <div id="implementation" class="tab-content">
                    <h2>Implementation Roadmap</h2>
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-label">Phase 1 - Setup</div>
                            <div class="stat-value">Q1-Q2 2025</div>
                            <div class="stat-change">Legal framework</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-label">Phase 2 - Pilot</div>
                            <div class="stat-value">Q3-Q4 2025</div>
                            <div class="stat-change">2 hub pilots</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-label">Phase 3 - Rollout</div>
                            <div class="stat-value">2026</div>
                            <div class="stat-change">Full deployment</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-label">Phase 4 - Optimize</div>
                            <div class="stat-value">2027+</div>
                            <div class="stat-change">Continuous improvement</div>
                        </div>
                    </div>

                    <table class="analysis-table">
                        <thead>
                            <tr>
                                <th>Milestone</th>
                                <th>Timeline</th>
                                <th>Dependencies</th>
                                <th>Risk Level</th>
                                <th>Budget Impact</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody id="implementationTable">
                            <!-- Table rows will be dynamically generated -->
                        </tbody>
                    </table>
                </div>

                <div id="performance" class="tab-content">
                    <h2>Performance Metrics</h2>
                    <div class="charts-grid">
                        <div class="chart-container">
                            <h4>Service Delivery Efficiency</h4>
                            <canvas id="efficiencyChart"></canvas>
                        </div>
                        <div class="chart-container">
                            <h4>Community Satisfaction Projections</h4>
                            <canvas id="satisfactionChart"></canvas>
                        </div>
                    </div>

                    <table class="analysis-table">
                        <thead>
                            <tr>
                                <th>Hub</th>
                                <th>Efficiency Score</th>
                                <th>Service Quality</th>
                                <th>Response Time</th>
                                <th>Cost per Capita</th>
                                <th>Overall Rating</th>
                            </tr>
                        </thead>
                        <tbody id="performanceTable">
                            <!-- Table rows will be dynamically generated -->
                        </tbody>
                    </table>
                </div>
            </main>
        </div>
    </div>

    <script>
        // Hub configuration data
        const localBoards = [
            'Albert-Eden', 'Devonport-Takapuna', 'Franklin', 'Great Barrier',
            'Henderson-Massey', 'Hibiscus and Bays', 'Howick', 'Kaipātiki',
            'Māngere-Ōtāhuhu', 'Manurewa', 'Maungakiekie-Tāmaki', 'Ōrākei',
            'Ōtara-Papatoetoe', 'Papakura', 'Puketāpapa', 'Rodney',
            'Upper Harbour', 'Waiheke', 'Waitākere Ranges', 'Waitematā', 'Whau'
        ];

        const hubConfigurations = {
            geographic: {
                'Central Auckland': ['Albert-Eden', 'Maungakiekie-Tāmaki', 'Puketāpapa', 'Waitematā'],
                'Eastern Suburbs': ['Howick', 'Ōrākei', 'Ōtara-Papatoetoe'],
                'North Shore': ['Devonport-Takapuna', 'Hibiscus and Bays', 'Kaipātiki', 'Upper Harbour'],
                'West Auckland': ['Henderson-Massey', 'Rodney', 'Waitākere Ranges', 'Whau'],
                'South Auckland': ['Franklin', 'Manurewa', 'Māngere-Ōtāhuhu', 'Papakura'],
                'Hauraki Gulf Islands': ['Great Barrier', 'Waiheke']
            },
            population: {
                'Metro North': ['Devonport-Takapuna', 'Hibiscus and Bays', 'Kaipātiki', 'Upper Harbour', 'Rodney'],
                'Metro Central': ['Albert-Eden', 'Waitematā', 'Ōrākei', 'Maungakiekie-Tāmaki'],
                'Metro West': ['Henderson-Massey', 'Waitākere Ranges', 'Whau', 'Puketāpapa'],
                'Metro East': ['Howick', 'Ōtara-Papatoetoe'],
                'Metro South': ['Manurewa', 'Māngere-Ōtāhuhu', 'Papakura', 'Franklin'],
                'Islands': ['Great Barrier', 'Waiheke']
            }
        };

        let currentScenario = 'geographic';
        let currentHubCount = 6;

        // Initialize dashboard
        function initializeDashboard() {
            loadScenario('geographic');
            updateHubMap();
            populateTables();
        }

        // Update hub count display
        function updateHubCount(value) {
            document.getElementById('hubCountValue').textContent = value;
            currentHubCount = parseInt(value);
            updateHubMap();
        }

        // Update borrowing capacity display
        function updateBorrowingCapacity(value) {
            document.getElementById('borrowingValue').textContent = value + '%';
        }

        // Load scenario
        function loadScenario(scenario) {
            currentScenario = scenario;
            showLoading();
            setTimeout(() => {
                updateHubMap();
                populateTables();
                updateStatistics();
                hideLoading();
            }, 500);
        }

        // Switch tabs
        function switchTab(tabName) {
            // Update tab buttons
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            event.target.classList.add('active');

            // Update tab content
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            document.getElementById(tabName).classList.add('active');
        }

        // Update hub map visualization
        function updateHubMap() {
            const hubMap = document.getElementById('hubMap');
            hubMap.innerHTML = '';

            const hubs = hubConfigurations[currentScenario] || hubConfigurations.geographic;
            const hubNames = Object.keys(hubs);
            
            // Create hub regions with different positions
            const positions = [
                { top: '10%', left: '40%', width: '200px', height: '120px' },
                { top: '5%', right: '10%', width: '220px', height: '130px' },
                { top: '35%', left: '5%', width: '210px', height: '125px' },
                { top: '35%', right: '8%', width: '200px', height: '120px' },
                { top: '65%', left: '25%', width: '230px', height: '135px' },
                { top: '70%', right: '20%', width: '180px', height: '110px' }
            ];

            hubNames.forEach((hubName, index) => {
                if (index < positions.length) {
                    const hubDiv = document.createElement('div');
                    hubDiv.className = 'hub-region';
                    hubDiv.style.top = positions[index].top;
                    hubDiv.style.left = positions[index].left;
                    hubDiv.style.right = positions[index].right;
                    hubDiv.style.width = positions[index].width;
                    hubDiv.style.height = positions[index].height;
                    
                    const population = Math.floor(Math.random() * 100000 + 250000);
                    const boards = hubs[hubName].length;
                    
                    hubDiv.innerHTML = `
                        <h4>${hubName}</h4>
                        <div class="hub-stats">
                            <div>Population: ${population.toLocaleString()}</div>
                            <div>Local Boards: ${boards}</div>
                        </div>
                    `;
                    
                    hubDiv.onclick = () => showHubDetails(hubName);
                    hubMap.appendChild(hubDiv);
                }
            });
        }

        // Populate tables with data
        function populateTables() {
            populateDemographicsTable();
            populateFinancialTable();
            populateImplementationTable();
            populatePerformanceTable();
        }

        function populateDemographicsTable() {
            const tbody = document.getElementById('demographicsTable');
            tbody.innerHTML = '';
            
            const hubs = hubConfigurations[currentScenario] || hubConfigurations.geographic;
            
            Object.keys(hubs).forEach(hubName => {
                const row = tbody.insertRow();
                const population = Math.floor(Math.random() * 100000 + 250000);
                const growthRate = (Math.random() * 4 - 1).toFixed(1);
                const medianAge = Math.floor(Math.random() * 10 + 35);
                const diversityIndex = (Math.random() * 30 + 60).toFixed(0);
                const serviceNeeds = ['High', 'Medium', 'Low'][Math.floor(Math.random() * 3)];
                
                row.innerHTML = `
                    <td>${hubName}</td>
                    <td>${population.toLocaleString()}</td>
                    <td>${growthRate}%</td>
                    <td>${medianAge}</td>
                    <td>${diversityIndex}%</td>
                    <td>${serviceNeeds}</td>
                `;
            });
        }

        function populateFinancialTable() {
            const tbody = document.getElementById('financialTable');
            tbody.innerHTML = '';
            
            const hubs = hubConfigurations[currentScenario] || hubConfigurations.geographic;
            const totalBudget = parseInt(document.getElementById('totalBudget').value);
            
            Object.keys(hubs).forEach(hubName => {
                const row = tbody.insertRow();
                const allocation = Math.floor(totalBudget / Object.keys(hubs).length);
                const capital = Math.floor(allocation * 0.6);
                const operating = Math.floor(allocation * 0.4);
                const revenue = Math.floor(allocation * 0.15);
                const debtCapacity = Math.floor(allocation * parseFloat(document.getElementById('borrowingCapacity').value) / 100);
                
                row.innerHTML = `
                    <td>${hubName}</td>
                    <td>$${allocation}M</td>
                    <td>$${capital}M</td>
                    <td>$${operating}M</td>
                    <td>$${revenue}M</td>
                    <td>$${debtCapacity}M</td>
                `;
            });
        }

        function populateImplementationTable() {
            const tbody = document.getElementById('implementationTable');
            tbody.innerHTML = '';
            
            const milestones = [
                { name: 'Legal Framework', timeline: 'Q1 2025', dependencies: 'Council approval', risk: 'Medium', budget: '$2M', status: 'Planning' },
                { name: 'Hub Boundaries', timeline: 'Q2 2025', dependencies: 'Community consultation', risk: 'High', budget: '$1M', status: 'Draft' },
                { name: 'Pilot Launch', timeline: 'Q3 2025', dependencies: 'Staff recruitment', risk: 'Medium', budget: '$50M', status: 'Pending' },
                { name: 'Full Rollout', timeline: 'Q1 2026', dependencies: 'Pilot success', risk: 'Low', budget: '$200M', status: 'Planned' },
                { name: 'Optimization', timeline: 'Q3 2026', dependencies: 'Performance data', risk: 'Low', budget: '$20M', status: 'Future' }
            ];
            
            milestones.forEach(milestone => {
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>${milestone.name}</td>
                    <td>${milestone.timeline}</td>
                    <td>${milestone.dependencies}</td>
                    <td>${milestone.risk}</td>
                    <td>${milestone.budget}</td>
                    <td>${milestone.status}</td>
                `;
            });
        }

        function populatePerformanceTable() {
            const tbody = document.getElementById('performanceTable');
            tbody.innerHTML = '';
            
            const hubs = hubConfigurations[currentScenario] || hubConfigurations.geographic;
            
            Object.keys(hubs).forEach(hubName => {
                const row = tbody.insertRow();
                const efficiency = Math.floor(Math.random() * 20 + 80);
                const quality = Math.floor(Math.random() * 15 + 85);
                const responseTime = Math.floor(Math.random() * 5 + 2);
                const costPerCapita = Math.floor(Math.random() * 100 + 150);
                const overallRating = ((efficiency + quality) / 2).toFixed(0);
                
                row.innerHTML = `
                    <td>${hubName}</td>
                    <td>${efficiency}%</td>
                    <td>${quality}%</td>
                    <td>${responseTime} days</td>
                    <td>$${costPerCapita}</td>
                    <td>${overallRating}%</td>
                `;
            });
        }

        // Update statistics
        function updateStatistics() {
            const hubs = hubConfigurations[currentScenario] || hubConfigurations.geographic;
            const hubCount = Object.keys(hubs).length;
            
            // Update overview statistics
            document.getElementById('avgHubSize').textContent = Math.floor(1717500 / hubCount).toLocaleString();
            document.getElementById('costEfficiency').textContent = Math.floor(Math.random() * 10 + 85) + '%';
            document.getElementById('serviceCoverage').textContent = Math.floor(Math.random() * 8 + 90) + '%';
            
            // Update financial statistics
            const totalBudget = parseInt(document.getElementById('totalBudget').value);
            document.getElementById('totalInvestment').textContent = '$' + (totalBudget * 1.2 / 1000).toFixed(1) + 'B';
            document.getElementById('annualCost').textContent = '$' + Math.floor(totalBudget * 0.09) + 'M';
            document.getElementById('roiProjection').textContent = (Math.random() * 2 + 2).toFixed(1) + 'x';
        }

        // Show hub details
        function showHubDetails(hubName) {
            alert(`Detailed view for ${hubName} hub - This would show comprehensive analytics including:\n\n• Local board composition\n• Demographic breakdown\n• Service delivery metrics\n• Financial projections\n• Implementation timeline`);
        }

        // Run analysis
        function runAnalysis() {
            showLoading();
            setTimeout(() => {
                updateStatistics();
                populateTables();
                hideLoading();
                alert('Analysis complete! Results have been updated across all dashboard sections.');
            }, 1500);
        }

        // Export report
        function exportReport() {
            alert('Report export initiated. A comprehensive PDF report including all current configurations, analysis results, and implementation recommendations would be generated.');
        }

        // Loading functions
        function showLoading() {
            document.getElementById('loading').classList.add('active');
        }

        function hideLoading() {
            document.getElementById('loading').classList.remove('active');
        }

        // Initialize on load
        window.onload = initializeDashboard;
    </script>
</body>
</html>
