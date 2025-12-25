# axial-deformation-calculator2<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>軸向變形計算器 - 靜力學</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft JhengHei', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a237e 0%, #4a148c 100%);
            color: #333;
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .container {
            max-width: 900px;
            width: 100%;
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
            margin: 20px 0;
        }
        
        header {
            background: linear-gradient(to right, #0d47a1, #311b92);
            color: white;
            padding: 25px 30px;
            text-align: center;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }
        
        h1 i {
            font-size: 1.8rem;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
            font-weight: normal;
        }
        
        .formula-section {
            background-color: #f8f9fa;
            padding: 20px;
            border-bottom: 2px solid #e0e0e0;
            text-align: center;
        }
        
        .formula-box {
            display: inline-block;
            background-color: white;
            padding: 20px 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            margin-top: 10px;
            border-left: 5px solid #0d47a1;
        }
        
        .formula {
            font-size: 2.2rem;
            font-weight: bold;
            color: #0d47a1;
            margin: 10px 0;
        }
        
        .formula-explanation {
            color: #555;
            font-size: 1rem;
            line-height: 1.5;
            margin-top: 15px;
        }
        
        .content {
            display: flex;
            flex-wrap: wrap;
            padding: 0;
        }
        
        .input-section {
            flex: 1;
            min-width: 300px;
            padding: 30px;
            border-right: 1px solid #e0e0e0;
        }
        
        .result-section {
            flex: 1;
            min-width: 300px;
            padding: 30px;
            background-color: #f9f9f9;
        }
        
        h2 {
            color: #1a237e;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #e0e0e0;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        h2 i {
            color: #0d47a1;
        }
        
        .input-group {
            margin-bottom: 25px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
            font-size: 1.05rem;
        }
        
        .unit {
            color: #666;
            font-size: 0.9rem;
            font-weight: normal;
        }
        
        input, select {
            width: 100%;
            padding: 14px 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1.1rem;
            transition: all 0.3s;
        }
        
        input:focus, select:focus {
            border-color: #0d47a1;
            box-shadow: 0 0 0 3px rgba(13, 71, 161, 0.1);
            outline: none;
        }
        
        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 30px;
        }
        
        button {
            flex: 1;
            padding: 16px;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .calculate-btn {
            background: linear-gradient(to right, #0d47a1, #1a237e);
            color: white;
        }
        
        .calculate-btn:hover {
            background: linear-gradient(to right, #1565c0, #0d47a1);
            transform: translateY(-3px);
            box-shadow: 0 7px 14px rgba(13, 71, 161, 0.2);
        }
        
        .reset-btn {
            background-color: #f5f5f5;
            color: #333;
            border: 2px solid #ddd;
        }
        
        .reset-btn:hover {
            background-color: #e0e0e0;
            transform: translateY(-3px);
        }
        
        .result-card {
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            border-top: 5px solid #0d47a1;
            margin-bottom: 25px;
        }
        
        .result-value {
            font-size: 3rem;
            font-weight: bold;
            color: #0d47a1;
            text-align: center;
            margin: 15px 0;
        }
        
        .result-unit {
            text-align: center;
            font-size: 1.2rem;
            color: #666;
            margin-bottom: 20px;
        }
        
        .result-details {
            margin-top: 20px;
        }
        
        .detail-row {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid #f0f0f0;
        }
        
        .detail-row:last-child {
            border-bottom: none;
        }
        
        .detail-label {
            color: #666;
        }
        
        .detail-value {
            font-weight: 600;
            color: #333;
        }
        
        .visualization {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #e0e0e0;
        }
        
        .bar-container {
            height: 100px;
            width: 100%;
            background-color: #f0f0f0;
            border-radius: 10px;
            position: relative;
            overflow: hidden;
            margin: 20px 0;
        }
        
        .original-bar {
            height: 50px;
            width: 80%;
            background-color: #78909c;
            border-radius: 5px;
            position: absolute;
            top: 25px;
            left: 10%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            transition: width 1s ease;
        }
        
        .deformed-bar {
            height: 50px;
            background-color: #0d47a1;
            border-radius: 5px;
            position: absolute;
            top: 25px;
            left: 10%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            transition: width 1s ease;
        }
        
        .bar-labels {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            font-size: 0.9rem;
            color: #666;
        }
        
        .examples {
            background-color: #e3f2fd;
            padding: 25px 30px;
            border-top: 1px solid #bbdefb;
        }
        
        .examples h3 {
            color: #1a237e;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .example-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 15px;
        }
        
        .example-btn {
            padding: 10px 15px;
            background-color: white;
            border: 1px solid #90caf9;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 0.95rem;
        }
        
        .example-btn:hover {
            background-color: #bbdefb;
            transform: translateY(-2px);
        }
        
        footer {
            text-align: center;
            padding: 20px;
            color: rgba(255, 255, 255, 0.8);
            font-size: 0.95rem;
            margin-top: 10px;
        }
        
        @media (max-width: 768px) {
            .content {
                flex-direction: column;
            }
            
            .input-section {
                border-right: none;
                border-bottom: 1px solid #e0e0e0;
            }
            
            .formula {
                font-size: 1.8rem;
            }
            
            .result-value {
                font-size: 2.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-ruler-combined"></i> 軸向變形計算器</h1>
            <p class="subtitle">用於計算桿件長度變化的互動工具 (δ = PL/AE)</p>
        </header>
        
        <div class="formula-section">
            <h3><i class="fas fa-calculator"></i> 基本公式</h3>
            <div class="formula-box">
                <div class="formula">δ = P × L / (A × E)</div>
                <div class="formula-explanation">
                    <p><strong>δ</strong> = 長度變化 (變形) • <strong>P</strong> = 軸向力 • <strong>L</strong> = 原始長度 • <strong>A</strong> = 截面積 • <strong>E</strong> = 彈性模數</p>
                </div>
            </div>
        </div>
        
        <div class="content">
            <div class="input-section">
                <h2><i class="fas fa-edit"></i> 輸入參數</h2>
                
                <div class="input-group">
                    <label for="force">軸向力 (P) <span class="unit">(N 或 kN)</span></label>
                    <input type="number" id="force" min="0" step="any" value="10000" placeholder="輸入力值">
                </div>
                
                <div class="input-group">
                    <label for="length">原始長度 (L) <span class="unit">(mm, m, 或 cm)</span></label>
                    <input type="number" id="length" min="0" step="any" value="2000" placeholder="輸入原始長度">
                </div>
                
                <div class="input-group">
                    <label for="area">截面積 (A) <span class="unit">(mm², m², 或 cm²)</span></label>
                    <input type="number" id="area" min="0" step="any" value="500" placeholder="輸入截面積">
                </div>
                
                <div class="input-group">
                    <label for="modulus">彈性模數 (E) <span class="unit">(GPa, MPa, 或 N/mm²)</span></label>
                    <input type="number" id="modulus" min="0" step="any" value="200" placeholder="輸入彈性模數">
                </div>
                
                <div class="input-group">
                    <label for="unit-system">單位系統</label>
                    <select id="unit-system">
                        <option value="mm">mm & N & mm² (N/mm²)</option>
                        <option value="m" selected>m & kN & m² (GPa)</option>
                        <option value="cm">cm & N & cm² (N/cm²)</option>
                    </select>
                </div>
                
                <div class="button-group">
                    <button class="calculate-btn" id="calculate-btn">
                        <i class="fas fa-calculator"></i> 計算變形
                    </button>
                    <button class="reset-btn" id="reset-btn">
                        <i class="fas fa-redo"></i> 重置輸入
                    </button>
                </div>
            </div>
            
            <div class="result-section">
                <h2><i class="fas fa-chart-line"></i> 計算結果</h2>
                
                <div class="result-card">
                    <h3>長度變化 (δ)</h3>
                    <div class="result-value" id="result-value">0.000</div>
                    <div class="result-unit" id="result-unit">mm</div>
                    
                    <div class="result-details">
                        <div class="detail-row">
                            <span class="detail-label">變形狀態：</span>
                            <span class="detail-value" id="deformation-status">-</span>
                        </div>
                        <div class="detail-row">
                            <span class="detail-label">應變 (ε)：</span>
                            <span class="detail-value" id="strain-value">0</span>
                        </div>
                        <div class="detail-row">
                            <span class="detail-label">應力 (σ)：</span>
                            <span class="detail-value" id="stress-value">0</span>
                        </div>
                    </div>
                </div>
                
                <div class="visualization">
                    <h3><i class="fas fa-chart-bar"></i> 變形可視化</h3>
                    <p>原始長度 vs 變形後長度的比較：</p>
                    
                    <div class="bar-container">
                        <div class="original-bar" id="original-bar">原始長度</div>
                        <div class="deformed-bar" id="deformed-bar" style="width: 80%;">最終長度</div>
                    </div>
                    
                    <div class="bar-labels">
                        <span id="original-length-label">L = 0 mm</span>
                        <span id="deformed-length-label">L' = 0 mm</span>
                    </div>
                    
                    <p id="deformation-info" style="text-align: center; margin-top: 15px; color: #666;">
                        無變形可視化。
                    </p>
                </div>
            </div>
        </div>
        
        <div class="examples">
            <h3><i class="fas fa-lightbulb"></i> 快速範例 (預設值)</h3>
            <p>選擇一個範例以自動填入輸入值：</p>
            <div class="example-buttons">
                <button class="example-btn" data-force="15000" data-length="3" data-area="0.01" data-modulus="210" data-unit="m">鋼材 (3m, 15kN)</button>
                <button class="example-btn" data-force="5000" data-length="2000" data-area="300" data-modulus="70" data-unit="mm">鋁材 (2m, 5kN)</button>
                <button class="example-btn" data-force="8000" data-length="150" data-area="20" data-modulus="10" data-unit="cm">木材 (1.5m, 8kN)</button>
                <button class="example-btn" data-force="200000" data-length="5" data-area="0.05" data-modulus="200" data-unit="m">橋樑元件 (5m, 200kN)</button>
            </div>
        </div>
    </div>
    
    <footer>
        <p>軸向變形計算器 - 靜力學互動作業 | δ = PL/AE</p>
    </footer>

    <script>
        // 輸入元素
        const forceInput = document.getElementById('force');
        const lengthInput = document.getElementById('length');
        const areaInput = document.getElementById('area');
        const modulusInput = document.getElementById('modulus');
        const unitSystemSelect = document.getElementById('unit-system');
        
        // 結果元素
        const resultValue = document.getElementById('result-value');
        const resultUnit = document.getElementById('result-unit');
        const deformationStatus = document.getElementById('deformation-status');
        const strainValue = document.getElementById('strain-value');
        const stressValue = document.getElementById('stress-value');
        
        // 可視化元素
        const originalBar = document.getElementById('original-bar');
        const deformedBar = document.getElementById('deformed-bar');
        const originalLengthLabel = document.getElementById('original-length-label');
        const deformedLengthLabel = document.getElementById('deformed-length-label');
        const deformationInfo = document.getElementById('deformation-info');
        
        // 按鈕
        const calculateBtn = document.getElementById('calculate-btn');
        const resetBtn = document.getElementById('reset-btn');
        const exampleButtons = document.querySelectorAll('.example-btn');
        
        // 根據選擇的單位配置
        const unitConfig = {
            'mm': { lengthUnit: 'mm', forceUnit: 'N', areaUnit: 'mm²', modulusUnit: 'N/mm²', resultUnit: 'mm' },
            'm': { lengthUnit: 'm', forceUnit: 'kN', areaUnit: 'm²', modulusUnit: 'GPa', resultUnit: 'mm' },
            'cm': { lengthUnit: 'cm', forceUnit: 'N', areaUnit: 'cm²', modulusUnit: 'N/cm²', resultUnit: 'cm' }
        };
        
        // 初始化
        function init() {
            updateUnitLabels();
            calculateDeformation();
        }
        
        // 根據選擇更新單位標籤
        function updateUnitLabels() {
            const selectedUnit = unitSystemSelect.value;
            const units = unitConfig[selectedUnit];
            
            // 更新佔位符文字
            forceInput.placeholder = `輸入力值 (${units.forceUnit})`;
            lengthInput.placeholder = `輸入原始長度 (${units.lengthUnit})`;
            areaInput.placeholder = `輸入截面積 (${units.areaUnit})`;
            modulusInput.placeholder = `輸入彈性模數 (${units.modulusUnit})`;
            
            // 更新結果標籤
            resultUnit.textContent = units.resultUnit;
        }
        
        // 主要計算變形函數
        function calculateDeformation() {
            // 從輸入獲取值
            const force = parseFloat(forceInput.value) || 0;
            const length = parseFloat(lengthInput.value) || 0;
            const area = parseFloat(areaInput.value) || 0;
            const modulus = parseFloat(modulusInput.value) || 0;
            const unitSystem = unitSystemSelect.value;
            
            // 驗證輸入
            if (force <= 0 || length <= 0 || area <= 0 || modulus <= 0) {
                resultValue.textContent = "0.000";
                deformationStatus.textContent = "輸入無效";
                strainValue.textContent = "0";
                stressValue.textContent = "0";
                
                // 重置可視化
                deformedBar.style.width = "80%";
                originalLengthLabel.textContent = `L = 0 ${unitConfig[unitSystem].lengthUnit}`;
                deformedLengthLabel.textContent = `L' = 0 ${unitConfig[unitSystem].lengthUnit}`;
                deformationInfo.textContent = "請輸入有效數值以查看可視化。";
                return;
            }
            
            // 根據單位計算變形
            let deformation;
            let stress;
            
            if (unitSystem === 'mm') {
                // 所有單位為 mm, N, mm²
                deformation = (force * length) / (area * modulus); // 結果為 mm
                stress = force / area; // N/mm²
            } else if (unitSystem === 'm') {
                // 轉換為米制單位
                // 力為 kN，轉換為 N: force * 1000
                // 彈性模數為 GPa，轉換為 N/m²: modulus * 1e9
                const forceN = force * 1000; // kN 轉 N
                const modulusPa = modulus * 1e9; // GPa 轉 N/m²
                deformation = (forceN * length) / (area * modulusPa); // 結果為米
                deformation *= 1000; // 轉換為 mm 顯示
                stress = forceN / area; // N/m²
                stress /= 1e6; // 轉換為 MPa 顯示
            } else { // cm
                deformation = (force * length) / (area * modulus); // 結果為 cm
                stress = force / area; // N/cm²
            }
            
            // 計算應變 (strain)
            const strain = deformation / length;
            
            // 格式化結果
            let formattedDeformation;
            if (Math.abs(deformation) < 0.001 && deformation !== 0) {
                formattedDeformation = deformation.toExponential(3);
            } else {
                formattedDeformation = deformation.toFixed(3);
            }
            
            // 更新結果
            resultValue.textContent = formattedDeformation;
            deformationStatus.textContent = deformation >= 0 ? "伸長 (拉力)" : "縮短 (壓力)";
            
            // 更新應變和應力
            strainValue.textContent = strain.toExponential(3);
            
            if (unitSystem === 'm') {
                stressValue.textContent = stress.toFixed(2) + " MPa";
            } else if (unitSystem === 'mm') {
                stressValue.textContent = stress.toFixed(2) + " N/mm²";
            } else {
                stressValue.textContent = stress.toFixed(2) + " N/cm²";
            }
            
            // 更新可視化
            updateVisualization(length, deformation, unitSystem);
        }
        
        // 更新可視化條形圖
        function updateVisualization(originalLength, deformation, unitSystem) {
            const units = unitConfig[unitSystem];
            
            // 計算新長度
            const newLength = originalLength + deformation;
            
            // 確定條形寬度 (最大100%)
            const maxBarWidth = 80; // 百分比
            const originalWidth = maxBarWidth;
            
            // 計算變形條形寬度 (按比例)
            let deformedWidth = (newLength / originalLength) * maxBarWidth;
            
            // 限制大小以避免過小或過大
            deformedWidth = Math.max(10, Math.min(100, deformedWidth));
            
            // 更新條形顯示
            originalBar.style.width = `${originalWidth}%`;
            deformedBar.style.width = `${deformedWidth}%`;
            
            // 更新標籤
            originalLengthLabel.textContent = `L = ${originalLength.toFixed(2)} ${units.lengthUnit}`;
            deformedLengthLabel.textContent = `L' = ${newLength.toFixed(2)} ${units.lengthUnit}`;
            
            // 更新變形信息
            const deformationPercent = (deformation / originalLength * 100).toFixed(3);
            deformationInfo.textContent = `變形量：${deformation >= 0 ? '+' : ''}${deformation.toFixed(3)} ${units.resultUnit} (${deformationPercent}%)`;
            
            // 根據拉/壓設置顏色
            if (deformation > 0) {
                deformedBar.style.backgroundColor = "#0d47a1"; // 藍色表示拉伸
            } else if (deformation < 0) {
                deformedBar.style.backgroundColor = "#c62828"; // 紅色表示壓縮
            } else {
                deformedBar.style.backgroundColor = "#0d47a1"; // 默認藍色
            }
        }
        
        // 重置所有輸入
        function resetInputs() {
            forceInput.value = "10000";
            lengthInput.value = "2000";
            areaInput.value = "500";
            modulusInput.value = "200";
            unitSystemSelect.value = "m";
            
            updateUnitLabels();
            calculateDeformation();
        }
        
        // 從預設按鈕設置範例
        function setExample(force, length, area, modulus, unit) {
            forceInput.value = force;
            lengthInput.value = length;
            areaInput.value = area;
            modulusInput.value = modulus;
            unitSystemSelect.value = unit;
            
            updateUnitLabels();
            calculateDeformation();
        }
        
        // 事件監聽器
        calculateBtn.addEventListener('click', calculateDeformation);
        resetBtn.addEventListener('click', resetInputs);
        
        unitSystemSelect.addEventListener('change', function() {
            updateUnitLabels();
            calculateDeformation();
        });
        
        // 實時計算輸入
        [forceInput, lengthInput, areaInput, modulusInput].forEach(input => {
            input.addEventListener('input', calculateDeformation);
        });
        
        // 範例預設
        exampleButtons.forEach(button => {
            button.addEventListener('click', function() {
                const force = this.getAttribute('data-force');
                const length = this.getAttribute('data-length');
                const area = this.getAttribute('data-area');
                const modulus = this.getAttribute('data-modulus');
                const unit = this.getAttribute('data-unit');
                
                setExample(force, length, area, modulus, unit);
                
                // 高亮選中的按鈕
                exampleButtons.forEach(btn => btn.style.backgroundColor = "white");
                this.style.backgroundColor = "#bbdefb";
            });
        });
        
        // 頁面載入時初始化
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
