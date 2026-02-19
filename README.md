<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حساب عمر الطفل - إدارة تعليم نجران</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        * { box-sizing: border-box; }
        
        body {
            font-family: 'Segoe UI', Tahoma, sans-serif;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f0f9ff;
            background-image: linear-gradient(rgba(255, 255, 255, 0.6), rgba(255, 255, 255, 0.6)), 
                              url('https://images.unsplash.com/photo-1503454537195-1dcabb73ffb9?auto=format&fit=crop&q=80&w=1000');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            background-repeat: no-repeat;
        }

        .main-card {
            background: rgba(255, 255, 255, 0.98);
            padding: 30px;
            border-radius: 30px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
            width: 100%;
            max-width: 500px;
            text-align: center;
            border: 4px solid #FFD700;
        }

        .header-section img {
            width: 140px;
            margin-bottom: 15px;
        }

        .header-section h2 { color: #2E7D32; margin: 5px 0; font-size: 1.5em; }
        .header-section h3 { color: #1565C0; margin: 5px 0; font-size: 1.2em; }

        h1 { color: #D81B60; font-size: 1.7em; margin: 20px 0; }

        .input-group {
            background: #fffbe6;
            padding: 20px;
            border-radius: 20px;
            border: 2px dashed #FFCA28;
            margin-bottom: 25px;
        }

        input[type="date"] {
            width: 100%;
            padding: 12px;
            border: 2px solid #FFCA28;
            border-radius: 12px;
            font-size: 18px;
            text-align: center;
            outline: none;
        }

        .btn-container { display: flex; gap: 12px; }
        button {
            flex: 1;
            padding: 14px;
            font-size: 17px;
            font-weight: bold;
            border-radius: 15px;
            border: none;
            cursor: pointer;
            transition: 0.3s;
            color: white;
        }

        .calc-btn { background: linear-gradient(45deg, #4CAF50, #2E7D32); }
        .print-btn { background: linear-gradient(45deg, #2196F3, #1565C0); }

        /* صندوق النتيجة */
        #result-box {
            margin-top: 25px;
            padding: 20px;
            background: #e1f5fe;
            border-radius: 20px;
            display: none;
            border: 2px solid #03a9f4;
        }

        /* صندوق المتطلبات الجديد */
        #requirements-box {
            margin-top: 20px;
            padding: 20px;
            background: #FFF3E0;
            border-radius: 20px;
            border: 2px solid #FF9800;
            text-align: right;
            display: none; /* يظهر فقط عند القبول */
            animation: fadeIn 0.8s;
        }

        .req-title {
            color: #E65100;
            font-weight: bold;
            font-size: 1.2em;
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }

        .req-title i { margin-left: 10px; font-size: 1.4em; }

        ul.req-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        ul.req-list li {
            padding: 8px 0;
            border-bottom: 1px solid #FFE0B2;
            color: #4E342E;
            font-size: 1.05em;
        }

        ul.req-list li:last-child { border-bottom: none; }

        .age-text { color: #E64A19; font-size: 1.1em; font-weight: bold; display: block; }
        .stage-text { color: #2E7D32; font-size: 1.2em; font-weight: bold; margin-top: 5px; display: block; }

        .footer-section { margin-top: 35px; border-top: 1px solid #eee; padding-top: 20px; }
        .footer-section strong { color: #C2185B; font-size: 1.2em; display: block; }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        @media print {
            body { background: white !important; }
            button { display: none; }
            #requirements-box { display: block !important; } /* يظهر دائماً في الطباعة إذا كان مفعلاً */
        }
    </style>
</head>
<body>

<div class="main-card">
    <div class="header-section">
        <img src="https://upload.wikimedia.org/wikipedia/ar/thumb/2/29/Ministry_of_Education_%28Saudi_Arabia%29_Logo.svg/1200px-Ministry_of_Education_%28Saudi_Arabia_Logo.svg.png" alt="شعار الوزارة">
        <h2>وزارة التعليم</h2>
        <h3>إدارة التعليم بنجران</h3>
    </div>

    <h1>حساب عمر الطفل 🎒</h1>
    
    <div class="input-group">
        <label>يرجى اختيار تاريخ الميلاد ✨</label>
        <input type="date" id="birthDate">
    </div>

    <div class="btn-container">
        <button class="calc-btn" onclick="processResult()">عرض النتيجة 🎉</button>
        <button class="print-btn" onclick="window.print()">🖨️ طباعة</button>
    </div>

    <div id="result-box"></div>

    <div id="requirements-box">
        <div class="req-title">📌 المتطلبات عند القبول:</div>
        <ul class="req-list">
            <li>🍱 وجبة صحية للطفل.</li>
            <li>👕 اللباس الموحد (بلون بيج).</li>
            <li>⏰ الالتزام بمواعيد الحضور والانصراف.</li>
        </ul>
    </div>

    <div class="footer-section">
        <p>المديرة ومصممة الموقع:</p>
        <strong>فاطمه صالح آل بحري</strong>
    </div>
</div>

<script>
    function processResult() {
        const input = document.getElementById('birthDate').value;
        const resBox = document.getElementById('result-box');
        const reqBox = document.getElementById('requirements-box');
        
        if (!input) {
            alert("فضلاً، حدد تاريخ الميلاد أولاً 🎈");
            return;
        }

        confetti({ particleCount: 100, spread: 70, origin: { y: 0.6 } });

        const bDate = new Date(input);
        const today = new Date();
        let y = today.getFullYear() - bDate.getFullYear();
        let m = today.getMonth() - bDate.getMonth();

        if (m < 0 || (m === 0 && today.getDate() < bDate.getDate())) {
            y--;
            m += 12;
        }

        let stage = "";
        let isAccepted = false;

        if (y < 3) {
            stage = "لم يبلغ سن القبول بعد 👶";
        } else if (y >= 3 && y <= 5) {
            isAccepted = true;
            if (y == 3) stage = "مستعد للمستوى الأول (روضة 1) 🎨";
            else if (y == 4) stage = "مستعد للمستوى الثاني (روضة 2) 🧩";
            else if (y == 5) stage = "مستعد للمستوى الثالث (روضة 3) 📚";
        } else {
            stage = "بطلنا مستعد للمرحلة الابتدائية! 🏫";
        }

        resBox.style.display = "block";
        resBox.innerHTML = `
            <span class="age-text">عمر الطفل: ${y} سنوات و ${m} أشهر</span>
            <span class="stage-text">${stage}</span>
        `;

        // إظهار قائمة الطلبات فقط في حال كان الطفل في سن الروضة
        if (isAccepted) {
            reqBox.style.display = "block";
        } else {
            reqBox.style.display = "none";
        }
    }
</script>

</body>
</html>
