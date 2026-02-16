<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Consultant Timesheet Manager - Cloud Ready</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600;700&family=JetBrains+Mono:wght@400;600&display=swap');
        
        :root {
            --primary: #0f172a;
            --primary-light: #1e293b;
            --accent: #3b82f6;
            --accent-hover: #2563eb;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --bg: #f8fafc;
            --card: #ffffff;
            --border: #e2e8f0;
            --text: #0f172a;
            --text-secondary: #64748b;
            --shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
            --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'IBM Plex Sans', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: var(--text);
            line-height: 1.6;
            min-height: 100vh;
            padding: 2rem;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }
        
        .header {
            background: var(--card);
            padding: 2rem;
            border-radius: 16px;
            box-shadow: var(--shadow-lg);
            margin-bottom: 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 1rem;
        }
        
        .header h1 {
            font-size: 2rem;
            font-weight: 700;
            color: var(--primary);
        }
        
        .header-actions {
            display: flex;
            gap: 1rem;
            align-items: center;
            flex-wrap: wrap;
        }
        
        .auto-save-status {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.5rem 1rem;
            background: var(--bg);
            border-radius: 8px;
            font-size: 0.875rem;
            color: var(--text-secondary);
        }
        
        .save-indicator {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--success);
            animation: pulse 2s ease-in-out infinite;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .tabs {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 2rem;
            background: var(--card);
            padding: 0.5rem;
            border-radius: 12px;
            box-shadow: var(--shadow);
            flex-wrap: wrap;
        }
        
        .tab {
            flex: 1;
            min-width: 150px;
            padding: 1rem;
            background: transparent;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.95rem;
            color: var(--text-secondary);
            transition: all 0.2s;
        }
        
        .tab:hover {
            background: var(--bg);
        }
        
        .tab.active {
            background: var(--accent);
            color: white;
            box-shadow: var(--shadow);
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
            animation: fadeIn 0.3s ease-in-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .card {
            background: var(--card);
            padding: 2rem;
            border-radius: 12px;
            box-shadow: var(--shadow);
            margin-bottom: 1.5rem;
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            padding-bottom: 1rem;
            border-bottom: 2px solid var(--border);
            flex-wrap: wrap;
            gap: 1rem;
        }
        
        .card-title {
            font-size: 1.25rem;
            font-weight: 700;
            color: var(--primary);
        }
        
        .btn {
            padding: 0.625rem 1.25rem;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            font-size: 0.875rem;
            cursor: pointer;
            transition: all 0.2s;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            white-space: nowrap;
        }
        
        .btn-primary {
            background: var(--accent);
            color: white;
        }
        
        .btn-primary:hover {
            background: var(--accent-hover);
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }
        
        .btn-success {
            background: var(--success);
            color: white;
        }
        
        .btn-danger {
            background: var(--danger);
            color: white;
        }
        
        .btn-secondary {
            background: var(--bg);
            color: var(--text);
        }
        
        .btn-secondary:hover {
            background: var(--border);
        }
        
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.25rem;
            margin-bottom: 1.5rem;
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }
        
        .form-label {
            font-weight: 600;
            font-size: 0.875rem;
            color: var(--text);
        }
        
        .form-input, .form-select, .form-textarea {
            padding: 0.75rem;
            border: 2px solid var(--border);
            border-radius: 8px;
            font-size: 0.95rem;
            font-family: inherit;
            transition: all 0.2s;
            background: var(--card);
        }
        
        .form-input:focus, .form-select:focus, .form-textarea:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }
        
        .consultant-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1rem;
        }
        
        .consultant-card {
            background: var(--bg);
            padding: 1.5rem;
            border-radius: 12px;
            border: 2px solid var(--border);
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .consultant-card:hover {
            border-color: var(--accent);
            box-shadow: var(--shadow-lg);
            transform: translateY(-2px);
        }
        
        .consultant-card.selected {
            border-color: var(--accent);
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.1) 0%, rgba(59, 130, 246, 0.05) 100%);
        }
        
        .consultant-name {
            font-weight: 700;
            font-size: 1.1rem;
            margin-bottom: 0.5rem;
            color: var(--primary);
        }
        
        .consultant-info {
            font-size: 0.875rem;
            color: var(--text-secondary);
            margin-bottom: 0.25rem;
        }
        
        .consultant-actions {
            display: flex;
            gap: 0.5rem;
            margin-top: 1rem;
            flex-wrap: wrap;
        }
        
        .timesheet-grid {
            overflow-x: auto;
        }
        
        .timesheet-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.875rem;
        }
        
        .timesheet-table th {
            background: var(--primary);
            color: white;
            padding: 1rem;
            text-align: left;
            font-weight: 600;
            white-space: nowrap;
        }
        
        .timesheet-table td {
            padding: 0.75rem;
            border-bottom: 1px solid var(--border);
        }
        
        .timesheet-table tr:hover {
            background: var(--bg);
        }
        
        .property-entry {
            background: var(--bg);
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 0.75rem;
            border: 2px solid var(--border);
        }
        
        .property-entry-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.75rem;
            flex-wrap: wrap;
            gap: 0.5rem;
        }
        
        .property-entry-fields {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 0.75rem;
        }
        
        .add-property-btn {
            width: 100%;
            padding: 0.75rem;
            background: var(--bg);
            border: 2px dashed var(--border);
            border-radius: 8px;
            color: var(--text-secondary);
            cursor: pointer;
            font-weight: 600;
            transition: all 0.2s;
        }
        
        .add-property-btn:hover {
            border-color: var(--accent);
            color: var(--accent);
            background: rgba(59, 130, 246, 0.05);
        }
        
        .summary-card {
            background: linear-gradient(135deg, var(--accent) 0%, var(--accent-hover) 100%);
            color: white;
            padding: 2rem;
            border-radius: 12px;
            margin-bottom: 1rem;
        }
        
        .summary-value {
            font-size: 2.5rem;
            font-weight: 700;
            margin-top: 0.5rem;
        }
        
        .summary-label {
            font-size: 0.875rem;
            opacity: 0.9;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }
        
        .stat-card {
            background: var(--bg);
            padding: 1.5rem;
            border-radius: 12px;
            border-left: 4px solid var(--accent);
        }
        
        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--primary);
            margin-top: 0.5rem;
        }
        
        .stat-label {
            font-size: 0.875rem;
            color: var(--text-secondary);
            font-weight: 600;
        }
        
        .export-buttons {
            display: flex;
            gap: 1rem;
            margin-top: 1.5rem;
            flex-wrap: wrap;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }
        
        .modal.active {
            display: flex;
        }
        
        .modal-content {
            background: var(--card);
            padding: 2rem;
            border-radius: 16px;
            max-width: 600px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: var(--shadow-lg);
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }
        
        .modal-close {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-secondary);
        }
        
        .total-row {
            font-weight: 700;
            background: var(--primary-light) !important;
            color: white;
        }
        
        .total-row td {
            border-top: 2px solid var(--primary);
        }
        
        .badge {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            border-radius: 12px;
            font-size: 0.75rem;
            font-weight: 600;
        }
        
        .badge-success {
            background: #d1fae5;
            color: #065f46;
        }
        
        .badge-warning {
            background: #fef3c7;
            color: #92400e;
        }
        
        .badge-info {
            background: #dbeafe;
            color: #1e40af;
        }
        
        .alert {
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }
        
        .alert-success {
            background: #d1fae5;
            color: #065f46;
            border: 2px solid #10b981;
        }
        
        .alert-info {
            background: #dbeafe;
            color: #1e40af;
            border: 2px solid #3b82f6;
        }
        
        @media print {
            body {
                background: white;
                padding: 0;
            }
            
            .header, .tabs, .btn, .consultant-actions, .header-actions {
                display: none !important;
            }
            
            .card {
                box-shadow: none;
                page-break-inside: avoid;
            }
        }
        
        @media (max-width: 768px) {
            body {
                padding: 1rem;
            }
            
            .header {
                padding: 1rem;
            }
            
            .header h1 {
                font-size: 1.5rem;
            }
            
            .card {
                padding: 1rem;
            }
            
            .form-grid {
                grid-template-columns: 1fr;
            }
            
            .property-entry-fields {
                grid-template-columns: 1fr;
            }
            
            .consultant-list {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📊 Consultant Timesheet Manager</h1>
            <div class="header-actions">
                <div class="auto-save-status">
                    <div class="save-indicator"></div>
                    <span id="saveStatus">Auto-saved</span>
                </div>
                <button class="btn btn-success" onclick="exportAllData()">💾 Export Data</button>
                <button class="btn btn-primary" onclick="importData()">📥 Import Data</button>
            </div>
        </div>
        
        <div class="tabs">
            <button class="tab active" onclick="switchTab('consultants')">👤 Consultants</button>
            <button class="tab" onclick="switchTab('timesheet')">⏰ Timesheet</button>
            <button class="tab" onclick="switchTab('summary')">📈 Summary</button>
            <button class="tab" onclick="switchTab('analysis')">📊 Analysis</button>
        </div>
        
        <!-- Consultants Tab -->
        <div id="consultants" class="tab-content active">
            <div class="alert alert-info">
                <span style="font-size: 1.5rem;">💡</span>
                <div>
                    <strong>Collaboration Tip:</strong> Click "Export Data" to save your timesheet data, then share the JSON file with colleagues. 
                    They can use "Import Data" to load it into their system.
                </div>
            </div>
            
            <div class="card">
                <div class="card-header">
                    <h2 class="card-title">Consultant Management</h2>
                    <button class="btn btn-primary" onclick="openAddConsultantModal()">+ Add Consultant</button>
                </div>
                <div id="consultantsList" class="consultant-list"></div>
            </div>
        </div>
        
        <!-- Monthly Timesheet Tab -->
        <div id="timesheet" class="tab-content">
            <div class="card">
                <div class="card-header">
                    <h2 class="card-title">Monthly Timesheet Entry</h2>
                    <div style="display: flex; gap: 1rem; flex-wrap: wrap;">
                        <select id="timesheetConsultant" class="form-select" onchange="updateTimesheetDisplay()">
                            <option value="">Select Consultant</option>
                        </select>
                        <input type="month" id="timesheetMonth" class="form-input" onchange="updateTimesheetDisplay()">
                    </div>
                </div>
                
                <div id="timesheetContent"></div>
            </div>
        </div>
        
        <!-- Monthly Summary Tab -->
        <div id="summary" class="tab-content">
            <div class="card">
                <div class="card-header">
                    <h2 class="card-title">Monthly Summary</h2>
                    <div style="display: flex; gap: 1rem; flex-wrap: wrap;">
                        <select id="summaryConsultant" class="form-select" onchange="updateSummaryDisplay()">
                            <option value="">Select Consultant</option>
                        </select>
                        <input type="month" id="summaryMonth" class="form-input" onchange="updateSummaryDisplay()">
                        <button class="btn btn-primary" onclick="window.print()">📄 Print/PDF</button>
                    </div>
                </div>
                <div id="summaryContent"></div>
            </div>
        </div>
        
        <!-- Analysis Tab -->
        <div id="analysis" class="tab-content">
            <div class="card">
                <div class="card-header">
                    <h2 class="card-title">Analysis & Reports</h2>
                    <input type="month" id="analysisMonth" class="form-input" onchange="updateAnalysisDisplay()">
                </div>
                
                <div class="stats-grid" id="statsGrid"></div>
                
                <div class="card">
                    <h3 class="card-title">Consultant Performance</h3>
                    <div id="consultantPerformance"></div>
                </div>
                
                <div class="card">
                    <h3 class="card-title">Property Cost Breakdown</h3>
                    <div id="propertyCostBreakdown"></div>
                </div>
                
                <div class="card">
                    <h3 class="card-title">Payment Tracking</h3>
                    <div id="paymentTracking"></div>
                </div>
                
                <div class="export-buttons">
                    <button class="btn btn-secondary" onclick="exportAnalysisCSV()">💾 Export CSV</button>
                    <button class="btn btn-primary" onclick="window.print()">📄 Print Report</button>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Add/Edit Consultant Modal -->
    <div id="consultantModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="card-title" id="modalTitle">Add Consultant</h2>
                <button class="modal-close" onclick="closeConsultantModal()">×</button>
            </div>
            
            <div class="form-grid">
                <div class="form-group">
                    <label class="form-label">Full Name *</label>
                    <input type="text" id="consultantName" class="form-input" required>
                </div>
                <div class="form-group">
                    <label class="form-label">Email Address *</label>
                    <input type="email" id="consultantEmail" class="form-input" required>
                </div>
                <div class="form-group">
                    <label class="form-label">Telephone Number</label>
                    <input type="tel" id="consultantPhone" class="form-input">
                </div>
                <div class="form-group">
                    <label class="form-label">Invoice Number</label>
                    <input type="text" id="consultantInvoice" class="form-input">
                </div>
                <div class="form-group">
                    <label class="form-label">Standard Hourly Rate (£) *</label>
                    <input type="number" id="consultantRate" class="form-input" step="0.01" required>
                </div>
                <div class="form-group">
                    <label class="form-label">Overtime Hourly Rate (£)</label>
                    <input type="number" id="consultantOTRate" class="form-input" step="0.01">
                </div>
                <div class="form-group">
                    <label class="form-label">Travel Expenses (£)</label>
                    <input type="number" id="consultantTravel" class="form-input" step="0.01" value="0">
                </div>
                <div class="form-group">
                    <label class="form-label">Bonus Payment (£)</label>
                    <input type="number" id="consultantBonus" class="form-input" step="0.01" value="0">
                </div>
                <div class="form-group">
                    <label class="form-label">Other Amounts (£)</label>
                    <input type="number" id="consultantOther" class="form-input" step="0.01" value="0">
                </div>
                <div class="form-group">
                    <label class="form-label">Client Company</label>
                    <input type="text" id="consultantClient" class="form-input">
                </div>
            </div>
            
            <div class="form-grid" style="margin-top: 1.5rem;">
                <div class="form-group">
                    <label class="form-label">Payment Status</label>
                    <select id="consultantPaidStatus" class="form-select">
                        <option value="unpaid">Unpaid</option>
                        <option value="partial">Partially Paid</option>
                        <option value="paid">Paid</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="form-label">Payment Date</label>
                    <input type="date" id="consultantPaidDate" class="form-input">
                </div>
                <div class="form-group">
                    <label class="form-label">Payment Amount (£)</label>
                    <input type="number" id="consultantPaidAmount" class="form-input" step="0.01" value="0">
                </div>
            </div>
            
            <div style="display: flex; gap: 1rem; margin-top: 2rem; flex-wrap: wrap;">
                <button class="btn btn-primary" onclick="saveConsultant()">Save Consultant</button>
                <button class="btn btn-secondary" onclick="closeConsultantModal()">Cancel</button>
            </div>
        </div>
    </div>
    
    <!-- Import Data Modal -->
    <input type="file" id="importFileInput" accept=".json" style="display: none;" onchange="handleImportFile(event)">
    
    <script>
        // Data Storage
        let consultants = [];
        let timesheets = [];
        let currentEditingId = null;
        
        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            loadData();
            initializeDefaults();
            updateConsultantsList();
            updateAllDisplays();
            showWelcomeMessage();
        });
        
        function showWelcomeMessage() {
            if (consultants.length === 0) {
                console.log('Welcome! Start by adding consultants.');
            }
        }
        
        // Auto-save functionality
        function saveData() {
            const data = {
                consultants: consultants,
                timesheets: timesheets,
                lastSaved: new Date().toISOString(),
                version: '2.0'
            };
            localStorage.setItem('consultantTimesheetData', JSON.stringify(data));
            updateSaveStatus();
        }
        
        function loadData() {
            const saved = localStorage.getItem('consultantTimesheetData');
            if (saved) {
                try {
                    const data = JSON.parse(saved);
                    consultants = data.consultants || [];
                    timesheets = data.timesheets || [];
                } catch (e) {
                    console.error('Error loading data:', e);
                }
            }
        }
        
        function updateSaveStatus() {
            const status = document.getElementById('saveStatus');
            status.textContent = 'Saving...';
            setTimeout(() => {
                status.textContent = 'Auto-saved';
            }, 500);
        }
        
        // Export/Import functionality
        function exportAllData() {
            const data = {
                consultants: consultants,
                timesheets: timesheets,
                exportDate: new Date().toISOString(),
                version: '2.0'
            };
            
            const dataStr = JSON.stringify(data, null, 2);
            const blob = new Blob([dataStr], { type: 'application/json' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `timesheet-data-${new Date().toISOString().split('T')[0]}.json`;
            a.click();
            window.URL.revokeObjectURL(url);
            
            showNotification('Data exported successfully! Share this file with your colleagues.', 'success');
        }
        
        function importData() {
            document.getElementById('importFileInput').click();
        }
        
        function handleImportFile(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = JSON.parse(e.target.result);
                    
                    if (confirm('This will replace your current data. Continue?')) {
                        consultants = data.consultants || [];
                        timesheets = data.timesheets || [];
                        saveData();
                        updateConsultantsList();
                        updateAllDisplays();
                        showNotification('Data imported successfully!', 'success');
                    }
                } catch (error) {
                    alert('Error importing file. Please ensure it\'s a valid timesheet data file.');
                }
            };
            reader.readAsText(file);
            
            // Reset file input
            event.target.value = '';
        }
        
        function showNotification(message, type) {
            const alertDiv = document.createElement('div');
            alertDiv.className = `alert alert-${type}`;
            alertDiv.innerHTML = `
                <span style="font-size: 1.5rem;">${type === 'success' ? '✅' : '💡'}</span>
                <div>${message}</div>
            `;
            
            const container = document.querySelector('.container');
            container.insertBefore(alertDiv, container.firstChild);
            
            setTimeout(() => {
                alertDiv.remove();
            }, 5000);
        }
        
        // Initialize defaults
        function initializeDefaults() {
            const now = new Date();
            const monthStr = `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, '0')}`;
            document.getElementById('timesheetMonth').value = monthStr;
            document.getElementById('summaryMonth').value = monthStr;
            document.getElementById('analysisMonth').value = monthStr;
        }
        
        // Tab switching
        function switchTab(tabName) {
            document.querySelectorAll('.tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            
            event.target.classList.add('active');
            document.getElementById(tabName).classList.add('active');
            
            if (tabName === 'timesheet') updateTimesheetDisplay();
            if (tabName === 'summary') updateSummaryDisplay();
            if (tabName === 'analysis') updateAnalysisDisplay();
        }
        
        // Consultant Management
        function openAddConsultantModal() {
            currentEditingId = null;
            document.getElementById('modalTitle').textContent = 'Add Consultant';
            document.getElementById('consultantModal').classList.add('active');
            clearConsultantForm();
        }
        
        function openEditConsultantModal(id) {
            currentEditingId = id;
            const consultant = consultants.find(c => c.id === id);
            if (!consultant) return;
            
            document.getElementById('modalTitle').textContent = 'Edit Consultant';
            document.getElementById('consultantName').value = consultant.name;
            document.getElementById('consultantEmail').value = consultant.email;
            document.getElementById('consultantPhone').value = consultant.phone || '';
            document.getElementById('consultantInvoice').value = consultant.invoiceNumber || '';
            document.getElementById('consultantRate').value = consultant.standardRate;
            document.getElementById('consultantOTRate').value = consultant.overtimeRate || '';
            document.getElementById('consultantTravel').value = consultant.travelExpenses || 0;
            document.getElementById('consultantBonus').value = consultant.bonusPayment || 0;
            document.getElementById('consultantOther').value = consultant.otherAmounts || 0;
            document.getElementById('consultantClient').value = consultant.clientCompany || '';
            document.getElementById('consultantPaidStatus').value = consultant.paidStatus || 'unpaid';
            document.getElementById('consultantPaidDate').value = consultant.paidDate || '';
            document.getElementById('consultantPaidAmount').value = consultant.paidAmount || 0;
            
            document.getElementById('consultantModal').classList.add('active');
        }
        
        function closeConsultantModal() {
            document.getElementById('consultantModal').classList.remove('active');
            clearConsultantForm();
        }
        
        function clearConsultantForm() {
            document.getElementById('consultantName').value = '';
            document.getElementById('consultantEmail').value = '';
            document.getElementById('consultantPhone').value = '';
            document.getElementById('consultantInvoice').value = '';
            document.getElementById('consultantRate').value = '';
            document.getElementById('consultantOTRate').value = '';
            document.getElementById('consultantTravel').value = '0';
            document.getElementById('consultantBonus').value = '0';
            document.getElementById('consultantOther').value = '0';
            document.getElementById('consultantClient').value = '';
            document.getElementById('consultantPaidStatus').value = 'unpaid';
            document.getElementById('consultantPaidDate').value = '';
            document.getElementById('consultantPaidAmount').value = '0';
        }
        
        function saveConsultant() {
            const name = document.getElementById('consultantName').value;
            const email = document.getElementById('consultantEmail').value;
            const rate = parseFloat(document.getElementById('consultantRate').value);
            
            if (!name || !email || !rate) {
                alert('Please fill in all required fields');
                return;
            }
            
            const consultant = {
                id: currentEditingId || Date.now().toString(),
                name: name,
                email: email,
                phone: document.getElementById('consultantPhone').value,
                invoiceNumber: document.getElementById('consultantInvoice').value,
                standardRate: rate,
                overtimeRate: parseFloat(document.getElementById('consultantOTRate').value) || rate * 1.5,
                travelExpenses: parseFloat(document.getElementById('consultantTravel').value) || 0,
                bonusPayment: parseFloat(document.getElementById('consultantBonus').value) || 0,
                otherAmounts: parseFloat(document.getElementById('consultantOther').value) || 0,
                clientCompany: document.getElementById('consultantClient').value,
                paidStatus: document.getElementById('consultantPaidStatus').value,
                paidDate: document.getElementById('consultantPaidDate').value,
                paidAmount: parseFloat(document.getElementById('consultantPaidAmount').value) || 0
            };
            
            if (currentEditingId) {
                const index = consultants.findIndex(c => c.id === currentEditingId);
                consultants[index] = consultant;
            } else {
                consultants.push(consultant);
            }
            
            saveData();
            updateConsultantsList();
            updateAllDropdowns();
            closeConsultantModal();
        }
        
        function deleteConsultant(id) {
            if (!confirm('Are you sure you want to delete this consultant? This will also delete all their timesheet data.')) {
                return;
            }
            
            consultants = consultants.filter(c => c.id !== id);
            timesheets = timesheets.filter(t => t.consultantId !== id);
            saveData();
            updateConsultantsList();
            updateAllDropdowns();
        }
        
        function updateConsultantsList() {
            const container = document.getElementById('consultantsList');
            if (consultants.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: var(--text-secondary); padding: 2rem;">No consultants added yet. Click "Add Consultant" to get started.</p>';
                return;
            }
            
            container.innerHTML = consultants.map(consultant => {
                const statusBadge = consultant.paidStatus === 'paid' ? 'badge-success' : 
                                   consultant.paidStatus === 'partial' ? 'badge-warning' : 'badge-info';
                
                return `
                    <div class="consultant-card">
                        <div class="consultant-name">${consultant.name}</div>
                        <div class="consultant-info">📧 ${consultant.email}</div>
                        ${consultant.phone ? `<div class="consultant-info">📞 ${consultant.phone}</div>` : ''}
                        <div class="consultant-info">💰 £${consultant.standardRate}/hr (Standard)</div>
                        ${consultant.clientCompany ? `<div class="consultant-info">🏢 ${consultant.clientCompany}</div>` : ''}
                        <div style="margin-top: 0.75rem;">
                            <span class="badge ${statusBadge}">${consultant.paidStatus ? consultant.paidStatus.toUpperCase() : 'UNPAID'}</span>
                        </div>
                        <div class="consultant-actions">
                            <button class="btn btn-primary" onclick="openEditConsultantModal('${consultant.id}')">Edit</button>
                            <button class="btn btn-danger" onclick="deleteConsultant('${consultant.id}')">Delete</button>
                        </div>
                    </div>
                `;
            }).join('');
        }
        
        function updateAllDropdowns() {
            const timesheetSelect = document.getElementById('timesheetConsultant');
            const summarySelect = document.getElementById('summaryConsultant');
            
            const options = '<option value="">Select Consultant</option>' + 
                consultants.map(c => `<option value="${c.id}">${c.name}</option>`).join('');
            
            timesheetSelect.innerHTML = options;
            summarySelect.innerHTML = options;
        }
        
        // Timesheet Management
        function updateTimesheetDisplay() {
            const consultantId = document.getElementById('timesheetConsultant').value;
            const month = document.getElementById('timesheetMonth').value;
            const container = document.getElementById('timesheetContent');
            
            if (!consultantId || !month) {
                container.innerHTML = '<p style="text-align: center; color: var(--text-secondary); padding: 2rem;">Please select a consultant and month to view timesheet.</p>';
                return;
            }
            
            const consultant = consultants.find(c => c.id === consultantId);
            const [year, monthNum] = month.split('-').map(Number);
            const daysInMonth = new Date(year, monthNum, 0).getDate();
            
            let html = '<div class="timesheet-grid">';
            
            for (let day = 1; day <= daysInMonth; day++) {
                const date = new Date(year, monthNum - 1, day);
                const dateStr = date.toISOString().split('T')[0];
                const dayName = date.toLocaleDateString('en-US', { weekday: 'short' });
                const isWeekend = dayName === 'Sat' || dayName === 'Sun';
                
                let dayData = timesheets.find(t => t.consultantId === consultantId && t.date === dateStr);
                if (!dayData) {
                    dayData = {
                        consultantId: consultantId,
                        date: dateStr,
                        properties: []
                    };
                    timesheets.push(dayData);
                }
                
                html += `
                    <div class="card" style="margin-bottom: 1rem; ${isWeekend ? 'opacity: 0.6;' : ''}">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; flex-wrap: wrap; gap: 1rem;">
                            <h3 style="margin: 0;">
                                ${dayName}, ${date.toLocaleDateString('en-US', { month: 'long', day: 'numeric', year: 'numeric' })}
                                ${isWeekend ? '<span class="badge badge-info" style="margin-left: 0.5rem;">Weekend</span>' : ''}
                            </h3>
                            <div style="font-weight: 700; font-size: 1.25rem; color: var(--accent);">
                                Total: ${calculateDayTotal(dayData, consultant).hours.toFixed(2)} hrs | £${calculateDayTotal(dayData, consultant).cost.toFixed(2)}
                            </div>
                        </div>
                        
                        <div id="properties-${dateStr}">
                            ${renderPropertyEntries(dayData, consultant, dateStr)}
                        </div>
                        
                        ${dayData.properties.length < 6 ? `
                        <button class="add-property-btn" onclick="addPropertyEntry('${dateStr}', '${consultantId}')">
                            + Add Property Entry (${dayData.properties.length}/6)
                        </button>
                        ` : '<p style="text-align: center; color: var(--text-secondary); padding: 1rem;">Maximum 6 entries reached</p>'}
                    </div>
                `;
                
                if (dayName === 'Sun' || day === daysInMonth) {
                    const weekStart = new Date(date);
                    weekStart.setDate(date.getDate() - date.getDay());
                    const weekEnd = new Date(weekStart);
                    weekEnd.setDate(weekStart.getDate() + 6);
                    
                    const weekTotal = calculateWeekTotal(consultantId, weekStart, weekEnd, consultant);
                    
                    html += `
                        <div class="summary-card" style="margin-bottom: 2rem;">
                            <div class="summary-label">Week Total (${weekStart.toLocaleDateString()} - ${weekEnd.toLocaleDateString()})</div>
                            <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem;">
                                <div class="summary-value">${weekTotal.hours.toFixed(2)} hours</div>
                                <div class="summary-value">£${weekTotal.cost.toFixed(2)}</div>
                            </div>
                        </div>
                    `;
                }
            }
            
            const monthTotal = calculateMonthTotal(consultantId, year, monthNum, consultant);
            html += `
                <div class="summary-card" style="background: linear-gradient(135deg, #10b981 0%, #059669 100%);">
                    <div class="summary-label">MONTH TOTAL</div>
                    <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem;">
                        <div class="summary-value">${monthTotal.hours.toFixed(2)} hours</div>
                        <div class="summary-value">£${monthTotal.cost.toFixed(2)}</div>
                    </div>
                </div>
            `;
            
            html += '</div>';
            container.innerHTML = html;
        }
        
        function renderPropertyEntries(dayData, consultant, dateStr) {
            if (!dayData.properties || dayData.properties.length === 0) {
                return '<p style="text-align: center; color: var(--text-secondary); padding: 1rem;">No entries for this day</p>';
            }
            
            return dayData.properties.map((prop, index) => {
                const hours = calculateHours(prop.startTime, prop.endTime);
                const cost = hours * consultant.standardRate;
                
                return `
                    <div class="property-entry">
                        <div class="property-entry-header">
                            <span style="font-weight: 600;">Entry ${index + 1}</span>
                            <div style="display: flex; align-items: center; gap: 1rem; flex-wrap: wrap;">
                                <span style="color: var(--accent); font-weight: 700;">
                                    ${hours.toFixed(2)} hrs | £${cost.toFixed(2)}
                                </span>
                                <button class="btn btn-danger" style="padding: 0.25rem 0.75rem; font-size: 0.75rem;" 
                                        onclick="removePropertyEntry('${dateStr}', ${index})">Remove</button>
                            </div>
                        </div>
                        <div class="property-entry-fields">
                            <div class="form-group">
                                <label class="form-label">Property Code</label>
                                <input type="text" class="form-input" value="${prop.propertyCode || ''}" 
                                       onchange="updatePropertyField('${dateStr}', ${index}, 'propertyCode', this.value)">
                            </div>
                            <div class="form-group">
                                <label class="form-label">Start Time</label>
                                <input type="time" class="form-input" value="${prop.startTime || ''}" 
                                       onchange="updatePropertyField('${dateStr}', ${index}, 'startTime', this.value)">
                            </div>
                            <div class="form-group">
                                <label class="form-label">End Time</label>
                                <input type="time" class="form-input" value="${prop.endTime || ''}" 
                                       onchange="updatePropertyField('${dateStr}', ${index}, 'endTime', this.value)">
                            </div>
                        </div>
                        <div class="form-group" style="margin-top: 0.75rem;">
                            <label class="form-label">Notes</label>
                            <textarea class="form-input" rows="2" 
                                      onchange="updatePropertyField('${dateStr}', ${index}, 'notes', this.value)">${prop.notes || ''}</textarea>
                        </div>
                    </div>
                `;
            }).join('');
        }
        
        function addPropertyEntry(dateStr, consultantId) {
            const dayData = timesheets.find(t => t.consultantId === consultantId && t.date === dateStr);
            
            if (dayData.properties.length >= 6) {
                alert('Maximum 6 property entries per day');
                return;
            }
            
            dayData.properties.push({
                propertyCode: '',
                startTime: '',
                endTime: '',
                notes: ''
            });
            
            saveData();
            updateTimesheetDisplay();
        }
        
        function removePropertyEntry(dateStr, index) {
            const consultantId = document.getElementById('timesheetConsultant').value;
            const dayData = timesheets.find(t => t.consultantId === consultantId && t.date === dateStr);
            
            dayData.properties.splice(index, 1);
            saveData();
            updateTimesheetDisplay();
        }
        
        function updatePropertyField(dateStr, index, field, value) {
            const consultantId = document.getElementById('timesheetConsultant').value;
            const dayData = timesheets.find(t => t.consultantId === consultantId && t.date === dateStr);
            
            dayData.properties[index][field] = value;
            saveData();
            updateTimesheetDisplay();
        }
        
        function calculateHours(startTime, endTime) {
            if (!startTime || !endTime) return 0;
            
            const start = new Date(`2000-01-01T${startTime}`);
            const end = new Date(`2000-01-01T${endTime}`);
            
            if (end < start) {
                end.setDate(end.getDate() + 1);
            }
            
            return (end - start) / (1000 * 60 * 60);
        }
        
        function calculateDayTotal(dayData, consultant) {
            let totalHours = 0;
            let totalCost = 0;
            
            if (dayData.properties) {
                dayData.properties.forEach(prop => {
                    const hours = calculateHours(prop.startTime, prop.endTime);
                    totalHours += hours;
                    totalCost += hours * consultant.standardRate;
                });
            }
            
            return { hours: totalHours, cost: totalCost };
        }
        
        function calculateWeekTotal(consultantId, weekStart, weekEnd, consultant) {
            let totalHours = 0;
            let totalCost = 0;
            
            timesheets.filter(t => {
                if (t.consultantId !== consultantId) return false;
                const date = new Date(t.date);
                return date >= weekStart && date <= weekEnd;
            }).forEach(dayData => {
                const dayTotal = calculateDayTotal(dayData, consultant);
                totalHours += dayTotal.hours;
                totalCost += dayTotal.cost;
            });
            
            return { hours: totalHours, cost: totalCost };
        }
        
        function calculateMonthTotal(consultantId, year, month, consultant) {
            let totalHours = 0;
            let totalCost = 0;
            
            timesheets.filter(t => {
                if (t.consultantId !== consultantId) return false;
                const date = new Date(t.date);
                return date.getFullYear() === year && date.getMonth() === month - 1;
            }).forEach(dayData => {
                const dayTotal = calculateDayTotal(dayData, consultant);
                totalHours += dayTotal.hours;
                totalCost += dayTotal.cost;
            });
            
            return { hours: totalHours, cost: totalCost };
        }
        
        // Summary Display
        function updateSummaryDisplay() {
            const consultantId = document.getElementById('summaryConsultant').value;
            const month = document.getElementById('summaryMonth').value;
            const container = document.getElementById('summaryContent');
            
            if (!consultantId || !month) {
                container.innerHTML = '<p style="text-align: center; color: var(--text-secondary); padding: 2rem;">Please select a consultant and month to view summary.</p>';
                return;
            }
            
            const consultant = consultants.find(c => c.id === consultantId);
            const [year, monthNum] = month.split('-').map(Number);
            
            const monthData = timesheets.filter(t => {
                if (t.consultantId !== consultantId) return false;
                const date = new Date(t.date);
                return date.getFullYear() === year && date.getMonth() === monthNum - 1;
            });
            
            const propertyTotals = {};
            let grandTotalHours = 0;
            let grandTotalCost = 0;
            
            monthData.forEach(dayData => {
                if (dayData.properties) {
                    dayData.properties.forEach(prop => {
                        const hours = calculateHours(prop.startTime, prop.endTime);
                        const cost = hours * consultant.standardRate;
                        
                        if (!propertyTotals[prop.propertyCode]) {
                            propertyTotals[prop.propertyCode] = { hours: 0, cost: 0, days: 0 };
                        }
                        
                        propertyTotals[prop.propertyCode].hours += hours;
                        propertyTotals[prop.propertyCode].cost += cost;
                        propertyTotals[prop.propertyCode].days++;
                        
                        grandTotalHours += hours;
                        grandTotalCost += cost;
                    });
                }
            });
            
            const additionalCosts = (consultant.travelExpenses || 0) + 
                                   (consultant.bonusPayment || 0) + 
                                   (consultant.otherAmounts || 0);
            const finalTotal = grandTotalCost + additionalCosts;
            
            let html = `
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-label">Total Hours</div>
                        <div class="stat-value">${grandTotalHours.toFixed(2)}</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Work Cost</div>
                        <div class="stat-value">£${grandTotalCost.toFixed(2)}</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Additional Costs</div>
                        <div class="stat-value">£${additionalCosts.toFixed(2)}</div>
                    </div>
                    <div class="stat-card" style="border-left-color: var(--success);">
                        <div class="stat-label">Total Amount Due</div>
                        <div class="stat-value">£${finalTotal.toFixed(2)}</div>
                    </div>
                </div>
                
                <div class="card">
                    <h3 class="card-title">Property Breakdown</h3>
                    <div style="overflow-x: auto;">
                        <table class="timesheet-table">
                            <thead>
                                <tr>
                                    <th>Property Code</th>
                                    <th>Days Worked</th>
                                    <th>Total Hours</th>
                                    <th>Total Cost</th>
                                </tr>
                            </thead>
                            <tbody>
            `;
            
            Object.entries(propertyTotals).forEach(([code, data]) => {
                html += `
                    <tr>
                        <td><strong>${code || 'Not specified'}</strong></td>
                        <td>${data.days}</td>
                        <td>${data.hours.toFixed(2)} hrs</td>
                        <td>£${data.cost.toFixed(2)}</td>
                    </tr>
                `;
            });
            
            html += `
                            </tbody>
                        </table>
                    </div>
                </div>
                
                <div class="card">
                    <h3 class="card-title">Additional Costs</h3>
                    <table class="timesheet-table">
                        <tbody>
                            <tr>
                                <td><strong>Travel Expenses</strong></td>
                                <td>£${(consultant.travelExpenses || 0).toFixed(2)}</td>
                            </tr>
                            <tr>
                                <td><strong>Bonus Payment</strong></td>
                                <td>£${(consultant.bonusPayment || 0).toFixed(2)}</td>
                            </tr>
                            <tr>
                                <td><strong>Other Amounts</strong></td>
                                <td>£${(consultant.otherAmounts || 0).toFixed(2)}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                
                <div class="summary-card" style="background: linear-gradient(135deg, #10b981 0%, #059669 100%);">
                    <div class="summary-label">INVOICE SUMMARY</div>
                    <div style="margin-top: 1rem;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 0.5rem;">
                            <span>Invoice Number:</span>
                            <strong>${consultant.invoiceNumber || 'N/A'}</strong>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin-bottom: 0.5rem;">
                            <span>Client Company:</span>
                            <strong>${consultant.clientCompany || 'N/A'}</strong>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin-bottom: 0.5rem;">
                            <span>Payment Status:</span>
                            <strong>${consultant.paidStatus ? consultant.paidStatus.toUpperCase() : 'UNPAID'}</strong>
                        </div>
                        ${consultant.paidDate ? `
                            <div style="display: flex; justify-content: space-between; margin-bottom: 0.5rem;">
                                <span>Payment Date:</span>
                                <strong>${new Date(consultant.paidDate).toLocaleDateString()}</strong>
                            </div>
                        ` : ''}
                        ${consultant.paidAmount ? `
                            <div style="display: flex; justify-content: space-between;">
                                <span>Amount Paid:</span>
                                <strong>£${consultant.paidAmount.toFixed(2)}</strong>
                            </div>
                        ` : ''}
                    </div>
                </div>
            `;
            
            container.innerHTML = html;
        }
        
        // Analysis Display
        function updateAnalysisDisplay() {
            const month = document.getElementById('analysisMonth').value;
            if (!month) return;
            
            const [year, monthNum] = month.split('-').map(Number);
            
            const monthTimesheets = timesheets.filter(t => {
                const date = new Date(t.date);
                return date.getFullYear() === year && date.getMonth() === monthNum - 1;
            });
            
            let totalRevenue = 0;
            let totalHours = 0;
            let uniqueProperties = new Set();
            let paidInvoices = 0;
            let unpaidInvoices = 0;
            
            consultants.forEach(consultant => {
                const consultantTimesheets = monthTimesheets.filter(t => t.consultantId === consultant.id);
                consultantTimesheets.forEach(day => {
                    if (day.properties) {
                        day.properties.forEach(prop => {
                            const hours = calculateHours(prop.startTime, prop.endTime);
                            totalHours += hours;
                            totalRevenue += hours * consultant.standardRate;
                            if (prop.propertyCode) uniqueProperties.add(prop.propertyCode);
                        });
                    }
                });
                
                if (consultant.paidStatus === 'paid') paidInvoices++;
                else unpaidInvoices++;
            });
            
            const statsGrid = document.getElementById('statsGrid');
            statsGrid.innerHTML = `
                <div class="stat-card">
                    <div class="stat-label">Total Revenue</div>
                    <div class="stat-value">£${totalRevenue.toFixed(2)}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Total Hours</div>
                    <div class="stat-value">${totalHours.toFixed(0)}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Active Consultants</div>
                    <div class="stat-value">${consultants.length}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Properties Served</div>
                    <div class="stat-value">${uniqueProperties.size}</div>
                </div>
                <div class="stat-card" style="border-left-color: var(--success);">
                    <div class="stat-label">Paid Invoices</div>
                    <div class="stat-value">${paidInvoices}</div>
                </div>
                <div class="stat-card" style="border-left-color: var(--danger);">
                    <div class="stat-label">Unpaid Invoices</div>
                    <div class="stat-value">${unpaidInvoices}</div>
                </div>
            `;
            
            const performanceContainer = document.getElementById('consultantPerformance');
            let performanceHtml = '<div style="overflow-x: auto;"><table class="timesheet-table"><thead><tr><th>Consultant</th><th>Hours Worked</th><th>Revenue Generated</th><th>Payment Status</th></tr></thead><tbody>';
            
            consultants.forEach(consultant => {
                let consultantHours = 0;
                let consultantRevenue = 0;
                
                monthTimesheets.filter(t => t.consultantId === consultant.id).forEach(day => {
                    if (day.properties) {
                        day.properties.forEach(prop => {
                            const hours = calculateHours(prop.startTime, prop.endTime);
                            consultantHours += hours;
                            consultantRevenue += hours * consultant.standardRate;
                        });
                    }
                });
                
                const statusBadge = consultant.paidStatus === 'paid' ? 'badge-success' : 
                                   consultant.paidStatus === 'partial' ? 'badge-warning' : 'badge-info';
                
                performanceHtml += `
                    <tr>
                        <td><strong>${consultant.name}</strong></td>
                        <td>${consultantHours.toFixed(2)} hrs</td>
                        <td>£${consultantRevenue.toFixed(2)}</td>
                        <td><span class="badge ${statusBadge}">${consultant.paidStatus || 'unpaid'}</span></td>
                    </tr>
                `;
            });
            
            performanceHtml += '</tbody></table></div>';
            performanceContainer.innerHTML = performanceHtml;
            
            const propertyContainer = document.getElementById('propertyCostBreakdown');
            const propertyTotals = {};
            
            monthTimesheets.forEach(day => {
                const consultant = consultants.find(c => c.id === day.consultantId);
                if (day.properties && consultant) {
                    day.properties.forEach(prop => {
                        if (!prop.propertyCode) return;
                        
                        if (!propertyTotals[prop.propertyCode]) {
                            propertyTotals[prop.propertyCode] = { hours: 0, cost: 0, consultants: new Set() };
                        }
                        
                        const hours = calculateHours(prop.startTime, prop.endTime);
                        propertyTotals[prop.propertyCode].hours += hours;
                        propertyTotals[prop.propertyCode].cost += hours * consultant.standardRate;
                        propertyTotals[prop.propertyCode].consultants.add(consultant.name);
                    });
                }
            });
            
            let propertyHtml = '<div style="overflow-x: auto;"><table class="timesheet-table"><thead><tr><th>Property Code</th><th>Total Hours</th><th>Total Cost</th><th>Consultants</th></tr></thead><tbody>';
            
            Object.entries(propertyTotals).forEach(([code, data]) => {
                propertyHtml += `
                    <tr>
                        <td><strong>${code}</strong></td>
                        <td>${data.hours.toFixed(2)} hrs</td>
                        <td>£${data.cost.toFixed(2)}</td>
                        <td>${Array.from(data.consultants).join(', ')}</td>
                    </tr>
                `;
            });
            
            propertyHtml += '</tbody></table></div>';
            propertyContainer.innerHTML = propertyHtml;
            
            const paymentContainer = document.getElementById('paymentTracking');
            let paymentHtml = '<div style="overflow-x: auto;"><table class="timesheet-table"><thead><tr><th>Consultant</th><th>Invoice #</th><th>Amount</th><th>Client</th><th>Status</th><th>Payment Date</th></tr></thead><tbody>';
            
            consultants.forEach(consultant => {
                let amount = 0;
                monthTimesheets.filter(t => t.consultantId === consultant.id).forEach(day => {
                    if (day.properties) {
                        day.properties.forEach(prop => {
                            const hours = calculateHours(prop.startTime, prop.endTime);
                            amount += hours * consultant.standardRate;
                        });
                    }
                });
                
                amount += (consultant.travelExpenses || 0) + (consultant.bonusPayment || 0) + (consultant.otherAmounts || 0);
                
                const statusBadge = consultant.paidStatus === 'paid' ? 'badge-success' : 
                                   consultant.paidStatus === 'partial' ? 'badge-warning' : 'badge-info';
                
                paymentHtml += `
                    <tr>
                        <td><strong>${consultant.name}</strong></td>
                        <td>${consultant.invoiceNumber || 'N/A'}</td>
                        <td>£${amount.toFixed(2)}</td>
                        <td>${consultant.clientCompany || 'N/A'}</td>
                        <td><span class="badge ${statusBadge}">${consultant.paidStatus || 'unpaid'}</span></td>
                        <td>${consultant.paidDate ? new Date(consultant.paidDate).toLocaleDateString() : 'N/A'}</td>
                    </tr>
                `;
            });
            
            paymentHtml += '</tbody></table></div>';
            paymentContainer.innerHTML = paymentHtml;
        }
        
        function exportAnalysisCSV() {
            const month = document.getElementById('analysisMonth').value;
            const [year, monthNum] = month.split('-').map(Number);
            
            let csv = 'Consultant,Date,Property Code,Start Time,End Time,Hours,Cost\n';
            
            timesheets.forEach(day => {
                const date = new Date(day.date);
                if (date.getFullYear() === year && date.getMonth() === monthNum - 1) {
                    const consultant = consultants.find(c => c.id === day.consultantId);
                    if (day.properties && consultant) {
                        day.properties.forEach(prop => {
                            const hours = calculateHours(prop.startTime, prop.endTime);
                            const cost = hours * consultant.standardRate;
                            csv += `"${consultant.name}","${day.date}","${prop.propertyCode || ''}","${prop.startTime}","${prop.endTime}",${hours.toFixed(2)},${cost.toFixed(2)}\n`;
                        });
                    }
                }
            });
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `timesheet-analysis-${month}.csv`;
            a.click();
            window.URL.revokeObjectURL(url);
        }
        
        function updateAllDisplays() {
            updateAllDropdowns();
            updateTimesheetDisplay();
            updateSummaryDisplay();
            updateAnalysisDisplay();
        }
    </script>
</body>
</html>
