<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trading Journal - Validasi & Entry</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 15px;
            font-weight: 700;
        }

        .session-info {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-top: 15px;
        }

        .info-item {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .info-item input[type="date"] {
            padding: 10px 16px;
            border: 2px solid rgba(255,255,255,0.3);
            background: rgba(255,255,255,0.1);
            color: white;
            border-radius: 8px;
            font-size: 16px;
            min-width: 160px;
        }

        .info-item input::placeholder {
            color: rgba(255,255,255,0.7);
        }

        .content {
            padding: 30px;
        }

        .section {
            margin-bottom: 30px;
            border: 2px solid #e0e0e0;
            border-radius: 15px;
            padding: 20px;
            transition: all 0.3s;
        }

        .section:hover {
            border-color: #667eea;
            box-shadow: 0 5px 15px rgba(102,126,234,0.2);
        }

        .section-title {
            font-size: 18px;
            font-weight: 700;
            color: #1e3c72;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 3px solid #667eea;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .badge {
            background: #667eea;
            color: white;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
        }

        .checklist-item {
            display: flex;
            align-items: flex-start;
            gap: 12px;
            padding: 12px;
            margin-bottom: 10px;
            border-radius: 10px;
            transition: all 0.3s;
            cursor: pointer;
        }

        .checklist-item:hover {
            background: #f5f7ff;
        }

        .checklist-item.checked {
            background: #e8f5e9;
        }

        .checkbox {
            width: 24px;
            height: 24px;
            border: 2px solid #667eea;
            border-radius: 6px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            transition: all 0.3s;
        }

        .checkbox.checked {
            background: #4caf50;
            border-color: #4caf50;
        }

        .checkbox.checked::after {
            content: '✓';
            color: white;
            font-weight: bold;
            font-size: 16px;
        }

        .item-text {
            flex: 1;
            line-height: 1.6;
        }

        .item-label {
            font-weight: 600;
            color: #333;
        }

        .item-description {
            color: #666;
            font-size: 14px;
            margin-top: 4px;
        }

        .method-card {
            background: #f8f9fa;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 15px;
            border-left: 4px solid #667eea;
        }

        .method-title {
            font-weight: 700;
            color: #1e3c72;
            margin-bottom: 12px;
            font-size: 16px;
        }

        .result-section {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 25px;
            border-radius: 15px;
            margin-top: 20px;
        }

        .save-btn {
            width: 100%;
            padding: 15px;
            background: #4caf50;
            border: none;
            color: white;
            border-radius: 10px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 700;
            margin-top: 15px;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .save-btn:hover {
            background: #45a049;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(76, 175, 80, 0.4);
        }

        .save-btn:active {
            transform: translateY(0);
        }

        .history-section {
            margin-top: 30px;
            padding: 25px;
            background: #f8f9fa;
            border-radius: 15px;
        }

        .history-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .history-title {
            font-size: 20px;
            font-weight: 700;
            color: #1e3c72;
        }

        .clear-history-btn {
            padding: 8px 16px;
            background: #f44336;
            border: none;
            color: white;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.3s;
        }

        .clear-history-btn:hover {
            background: #da190b;
        }

        .history-list {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .history-item {
            background: white;
            padding: 20px;
            border-radius: 12px;
            border-left: 5px solid #667eea;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            transition: all 0.3s;
        }

        .history-item:hover {
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            transform: translateX(5px);
        }

        .history-item.profit {
            border-left-color: #4caf50;
        }

        .history-item.loss {
            border-left-color: #f44336;
        }

        .history-date {
            font-size: 14px;
            color: #666;
            margin-bottom: 8px;
        }

        .history-result {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 10px;
        }

        .history-result.profit {
            color: #4caf50;
        }

        .history-result.loss {
            color: #f44336;
        }

        .history-stats {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            margin-bottom: 10px;
        }

        .stat-item {
            display: flex;
            align-items: center;
            gap: 5px;
            font-size: 13px;
            color: #666;
        }

        .history-notes {
            font-size: 14px;
            color: #444;
            font-style: italic;
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid #e0e0e0;
        }

        .delete-btn {
            float: right;
            padding: 6px 12px;
            background: #ff5252;
            border: none;
            color: white;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
            transition: all 0.3s;
        }

        .delete-btn:hover {
            background: #ff1744;
        }

        .empty-history {
            text-align: center;
            padding: 40px;
            color: #999;
            font-size: 16px;
        }

        .stats-summary {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .summary-card {
            background: white;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .summary-value {
            font-size: 24px;
            font-weight: 700;
            color: #1e3c72;
        }

        .summary-label {
            font-size: 12px;
            color: #666;
            margin-top: 5px;
        }

        .summary-card.profit .summary-value {
            color: #4caf50;
        }

        .summary-card.loss .summary-value {
            color: #f44336;
        }

        .result-buttons {
            display: flex;
            gap: 15px;
            margin: 15px 0;
            flex-wrap: wrap;
        }

        .result-btn {
            flex: 1;
            padding: 15px;
            border: 2px solid white;
            background: transparent;
            color: white;
            border-radius: 10px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s;
            min-width: 120px;
        }

        .result-btn.profit {
            border-color: #4caf50;
        }

        .result-btn.profit.active {
            background: #4caf50;
            border-color: #4caf50;
        }

        .result-btn.loss {
            border-color: #f44336;
        }

        .result-btn.loss.active {
            background: #f44336;
            border-color: #f44336;
        }

        textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid rgba(255,255,255,0.3);
            background: rgba(255,255,255,0.1);
            color: white;
            border-radius: 10px;
            font-size: 14px;
            min-height: 80px;
            resize: vertical;
            font-family: inherit;
        }

        textarea::placeholder {
            color: rgba(255,255,255,0.7);
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin: 20px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            border-radius: 10px;
            transition: width 0.3s;
        }

        .progress-text {
            text-align: center;
            color: #666;
            font-size: 14px;
            margin-top: 8px;
        }

        @media (max-width: 600px) {
            .session-info {
                flex-direction: column;
            }
            
            .result-buttons {
                flex-direction: column;
            }

            .result-btn {
                min-width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📊 TRADING JOURNAL</h1>
            <div class="session-info">
                <div class="info-item">
                    <span>📅</span>
                    <input type="date" id="dateInput">
                </div>
            </div>
        </div>

        <div class="content">
            <div class="progress-bar">
                <div class="progress-fill" id="progressBar"></div>
            </div>
            <div class="progress-text" id="progressText">0% Completed (0/5 Validasi + 0/1 Metode)</div>

            <div class="section">
                <div class="section-title">
                    <span>1️⃣</span>
                    GERBANG VALIDASI UNIVERSAL
                    <span class="badge">WAJIB 100%</span>
                </div>
                
                <div class="checklist-item" data-check="struktur">
                    <div class="checkbox"></div>
                    <div class="item-text">
                        <div class="item-label">STRUKTUR</div>
                        <div class="item-description">Hierarki Candle (2, 1, A, B) Sempurna & Tanpa Cacat</div>
                    </div>
                </div>

                <div class="checklist-item" data-check="snr">
                    <div class="checkbox"></div>
                    <div class="item-text">
                        <div class="item-label">SNR VALID</div>
                        <div class="item-description">Harga bereaksi di SnR M10 / M15</div>
                    </div>
                </div>

                <div class="checklist-item" data-check="warna">
                    <div class="checkbox"></div>
                    <div class="item-text">
                        <div class="item-label">WARNA</div>
                        <div class="item-description">Keselarasan warna Candle Pivot & Konfirmasi 100% Konsisten</div>
                    </div>
                </div>

                <div class="checklist-item" data-check="news">
                    <div class="checkbox"></div>
                    <div class="item-text">
                        <div class="item-label">NEWS FILTER</div>
                        <div class="item-description">Tidak ada High Impact News (News Clear)</div>
                    </div>
                </div>

                <div class="checklist-item" data-check="risk">
                    <div class="checkbox"></div>
                    <div class="item-text">
                        <div class="item-label">RISK</div>
                        <div class="item-description">SL 12 Poin & TP 35 Poin sudah terpasang</div>
                    </div>
                </div>
            </div>

            <div class="section">
                <div class="section-title">
                    <span>2️⃣</span>
                    METODE ENTRY
                    <span class="badge">PILIH SALAH SATU</span>
                </div>

                <div class="method-card">
                    <div class="method-title">📍 METODE 1: RETEST FVG</div>
                    <div class="checklist-item" data-check="m1-fibo">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Tarik Fibo: Body B ke Wick A</div>
                        </div>
                    </div>
                    <div class="checklist-item" data-check="m1-area">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Area Entry: Level Fibo 0.60 - 0.70</div>
                        </div>
                    </div>
                    <div class="checklist-item" data-check="m1-exec">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Eksekusi: Limit/Market saat Retest ke Zona</div>
                        </div>
                    </div>
                </div>

                <div class="method-card">
                    <div class="method-title">⚡ METODE 2: DIRECT ENTRY</div>
                    <div class="checklist-item" data-check="m2-proporsi">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Proporsi: Body Candle 2, 1, A, B Seimbang/Seragam</div>
                        </div>
                    </div>
                    <div class="checklist-item" data-check="m2-kondisi">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Kondisi: C1 Doji / Ekor A & B Pendek (Gundul)</div>
                        </div>
                    </div>
                    <div class="checklist-item" data-check="m2-exec">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Eksekusi: Instant saat Close Candle B</div>
                        </div>
                    </div>
                </div>

                <div class="method-card">
                    <div class="method-title">🔄 METODE 3: EXTENDED LINE</div>
                    <div class="checklist-item" data-check="m3-kondisi">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Kondisi: Metode 1 & 2 Tidak Valid/Gagal</div>
                        </div>
                    </div>
                    <div class="checklist-item" data-check="m3-validasi">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Validasi: First Touch garis C2 (Maks 1 Hari)</div>
                        </div>
                    </div>
                    <div class="checklist-item" data-check="m3-entry">
                        <div class="checkbox"></div>
                        <div class="item-text">
                            <div class="item-description">Entry: Retest Fibo 60%-70% (Merah: Close-Wick | Hijau: Open-Close)</div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="result-section">
                <div class="section-title" style="color: white; border-color: white;">
                    <span>3️⃣</span>
                    RESULT
                </div>
                <div class="result-buttons">
                    <button class="result-btn profit" id="btnProfit">✅ PROFIT (+35)</button>
                    <button class="result-btn loss" id="btnLoss">❌ LOSS (-12)</button>
                </div>
                <textarea id="notesInput" placeholder="Notes: Tulis catatan trading Anda di sini..."></textarea>
                <button class="save-btn" id="saveBtn">💾 SIMPAN RIWAYAT</button>
            </div>

            <div class="history-section" id="historySection">
                <div class="history-header">
                    <div class="history-title">📊 RIWAYAT TRADING</div>
                    <button class="clear-history-btn" id="clearHistoryBtn">🗑️ Hapus Semua</button>
                </div>
                
                <div class="stats-summary" id="statsSummary"></div>
                
                <div class="history-list" id="historyList">
                    <div class="empty-history">Belum ada riwayat trading</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const state = {
            date: '',
            checks: {},
            result: '',
            notes: '',
            history: []
        };

        // Load history from localStorage
        function loadHistory() {
            const saved = localStorage.getItem('tradingHistory');
            if (saved) {
                state.history = JSON.parse(saved);
                displayHistory();
            }
        }

        // Save history to localStorage
        function saveHistory() {
            localStorage.setItem('tradingHistory', JSON.stringify(state.history));
        }

        // Display history
        function displayHistory() {
            const historyList = document.getElementById('historyList');
            const statsSummary = document.getElementById('statsSummary');
            
            if (state.history.length === 0) {
                historyList.innerHTML = '<div class="empty-history">Belum ada riwayat trading</div>';
                statsSummary.innerHTML = '';
                return;
            }

            // Calculate statistics
            const totalTrades = state.history.length;
            const profits = state.history.filter(h => h.result === 'PROFIT').length;
            const losses = state.history.filter(h => h.result === 'LOSS').length;
            const winRate = totalTrades > 0 ? Math.round((profits / totalTrades) * 100) : 0;
            const totalPnL = (profits * 35) - (losses * 12);

            // Display summary stats
            statsSummary.innerHTML = `
                <div class="summary-card">
                    <div class="summary-value">${totalTrades}</div>
                    <div class="summary-label">Total Trades</div>
                </div>
                <div class="summary-card profit">
                    <div class="summary-value">${profits}</div>
                    <div class="summary-label">Profit</div>
                </div>
                <div class="summary-card loss">
                    <div class="summary-value">${losses}</div>
                    <div class="summary-label">Loss</div>
                </div>
                <div class="summary-card">
                    <div class="summary-value">${winRate}%</div>
                    <div class="summary-label">Win Rate</div>
                </div>
                <div class="summary-card ${totalPnL >= 0 ? 'profit' : 'loss'}">
                    <div class="summary-value">${totalPnL > 0 ? '+' : ''}${totalPnL}</div>
                    <div class="summary-label">Total P&L</div>
                </div>
            `;

            // Clear history list
            historyList.innerHTML = '';
            
            // Create history items (reverse to show newest first)
            const reversedHistory = [...state.history].reverse();
            
            reversedHistory.forEach((item, displayIndex) => {
                const actualIndex = state.history.length - 1 - displayIndex;
                const validationComplete = item.validationCount === 5;
                const methodUsed = item.method || 'N/A';
                
                const itemDiv = document.createElement('div');
                itemDiv.className = `history-item ${item.result.toLowerCase()}`;
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'delete-btn';
                deleteBtn.textContent = '❌';
                deleteBtn.onclick = function() {
                    deleteHistoryItem(actualIndex);
                };
                
                const dateDiv = document.createElement('div');
                dateDiv.className = 'history-date';
                dateDiv.textContent = `📅 ${item.date || 'Tanggal tidak tersedia'}`;
                
                const resultDiv = document.createElement('div');
                resultDiv.className = `history-result ${item.result.toLowerCase()}`;
                resultDiv.textContent = item.result === 'PROFIT' ? '✅ PROFIT (+35)' : '❌ LOSS (-12)';
                
                const statsDiv = document.createElement('div');
                statsDiv.className = 'history-stats';
                statsDiv.innerHTML = `
                    <div class="stat-item">
                        <span>📋</span>
                        <span>Validasi: ${item.validationCount}/5 ${validationComplete ? '✅' : '⚠️'}</span>
                    </div>
                    <div class="stat-item">
                        <span>🎯</span>
                        <span>Metode: ${methodUsed}</span>
                    </div>
                    <div class="stat-item">
                        <span>✓</span>
                        <span>Checklist: ${item.totalChecked}/${item.totalItems}</span>
                    </div>
                `;
                
                itemDiv.appendChild(deleteBtn);
                itemDiv.appendChild(dateDiv);
                itemDiv.appendChild(resultDiv);
                itemDiv.appendChild(statsDiv);
                
                if (item.notes) {
                    const notesDiv = document.createElement('div');
                    notesDiv.className = 'history-notes';
                    notesDiv.textContent = `📝 ${item.notes}`;
                    itemDiv.appendChild(notesDiv);
                }
                
                historyList.appendChild(itemDiv);
            });
        }

        // Delete single history item
        function deleteHistoryItem(index) {
            if (confirm('Hapus riwayat trading ini?')) {
                state.history.splice(index, 1);
                saveHistory();
                displayHistory();
            }
        }

        // Set today's date
        document.getElementById('dateInput').valueAsDate = new Date();

        // Load history on page load
        loadHistory();

        // Save button
        document.getElementById('saveBtn').addEventListener('click', function() {
            // Validation
            if (!state.result) {
                alert('⚠️ Pilih hasil trading (PROFIT/LOSS) terlebih dahulu!');
                return;
            }

            const date = document.getElementById('dateInput').value;
            if (!date) {
                alert('⚠️ Pilih tanggal trading terlebih dahulu!');
                return;
            }

            // Calculate validation and method completion
            const validationChecks = ['struktur', 'snr', 'warna', 'news', 'risk'];
            const validationChecked = validationChecks.filter(id => state.checks[id]).length;
            
            const method1Checks = ['m1-fibo', 'm1-area', 'm1-exec'];
            const method2Checks = ['m2-proporsi', 'm2-kondisi', 'm2-exec'];
            const method3Checks = ['m3-kondisi', 'm3-validasi', 'm3-entry'];
            
            const method1Complete = method1Checks.every(id => state.checks[id]);
            const method2Complete = method2Checks.every(id => state.checks[id]);
            const method3Complete = method3Checks.every(id => state.checks[id]);
            
            let methodUsed = 'Tidak Ada';
            if (method1Complete) methodUsed = 'Metode 1 (Retest FVG)';
            else if (method2Complete) methodUsed = 'Metode 2 (Direct Entry)';
            else if (method3Complete) methodUsed = 'Metode 3 (Extended Line)';

            const totalChecked = Object.values(state.checks).filter(v => v).length;
            const totalItems = document.querySelectorAll('.checklist-item').length;

            // Create history entry
            const historyEntry = {
                date: date,
                result: state.result,
                notes: state.notes,
                validationCount: validationChecked,
                method: methodUsed,
                totalChecked: totalChecked,
                totalItems: totalItems,
                timestamp: new Date().getTime()
            };

            // Add to history
            state.history.push(historyEntry);
            saveHistory();
            displayHistory();

            // Reset form
            if (confirm('✅ Riwayat berhasil disimpan!\n\nReset form untuk trading baru?')) {
                resetForm();
            }
        });

        // Clear all history
        const clearHistoryBtn = document.getElementById('clearHistoryBtn');
        if (clearHistoryBtn) {
            clearHistoryBtn.onclick = function() {
                if (confirm('⚠️ Hapus semua riwayat trading?\n\nTindakan ini tidak dapat dibatalkan!')) {
                    state.history = [];
                    saveHistory();
                    displayHistory();
                    alert('✅ Semua riwayat berhasil dihapus!');
                }
            };
        }

        // Reset form function
        function resetForm() {
            // Reset checks
            document.querySelectorAll('.checkbox').forEach(cb => cb.classList.remove('checked'));
            document.querySelectorAll('.checklist-item').forEach(item => item.classList.remove('checked'));
            state.checks = {};

            // Reset result buttons
            document.getElementById('btnProfit').classList.remove('active');
            document.getElementById('btnLoss').classList.remove('active');
            state.result = '';

            // Reset notes
            document.getElementById('notesInput').value = '';
            state.notes = '';

            // Reset progress
            updateProgress();
        }

        // Result buttons
        document.getElementById('btnProfit').addEventListener('click', function() {
            this.classList.toggle('active');
            document.getElementById('btnLoss').classList.remove('active');
            state.result = this.classList.contains('active') ? 'PROFIT' : '';
        });

        document.getElementById('btnLoss').addEventListener('click', function() {
            this.classList.toggle('active');
            document.getElementById('btnProfit').classList.remove('active');
            state.result = this.classList.contains('active') ? 'LOSS' : '';
        });

        // Checklist items
        document.querySelectorAll('.checklist-item').forEach(item => {
            item.addEventListener('click', function() {
                const checkbox = this.querySelector('.checkbox');
                const checkId = this.getAttribute('data-check');
                
                checkbox.classList.toggle('checked');
                this.classList.toggle('checked');
                
                state.checks[checkId] = checkbox.classList.contains('checked');
                updateProgress();
            });
        });

        function updateProgress() {
            // Validasi Universal (5 items - wajib semua)
            const validationChecks = ['struktur', 'snr', 'warna', 'news', 'risk'];
            const validationChecked = validationChecks.filter(id => state.checks[id]).length;
            
            // Metode 1 (3 items)
            const method1Checks = ['m1-fibo', 'm1-area', 'm1-exec'];
            const method1Checked = method1Checks.filter(id => state.checks[id]).length;
            const method1Complete = method1Checked === 3;
            
            // Metode 2 (3 items)
            const method2Checks = ['m2-proporsi', 'm2-kondisi', 'm2-exec'];
            const method2Checked = method2Checks.filter(id => state.checks[id]).length;
            const method2Complete = method2Checked === 3;
            
            // Metode 3 (3 items)
            const method3Checks = ['m3-kondisi', 'm3-validasi', 'm3-entry'];
            const method3Checked = method3Checks.filter(id => state.checks[id]).length;
            const method3Complete = method3Checked === 3;
            
            // Hitung progress: 5 validasi + minimal 1 metode lengkap
            const methodComplete = method1Complete || method2Complete || method3Complete ? 1 : 0;
            const totalRequired = 6; // 5 validasi + 1 metode
            const completed = validationChecked + methodComplete;
            
            const percentage = Math.round((completed / totalRequired) * 100);
            
            document.getElementById('progressBar').style.width = percentage + '%';
            document.getElementById('progressText').textContent = percentage + '% Completed (' + validationChecked + '/5 Validasi + ' + (methodComplete ? '1/1 Metode' : '0/1 Metode') + ')';
        }

        // Save inputs
        document.getElementById('dateInput').addEventListener('change', e => state.date = e.target.value);
        document.getElementById('notesInput').addEventListener('input', e => state.notes = e.target.value);
    </script>
</body>
</html>
