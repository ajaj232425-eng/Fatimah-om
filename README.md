# Fatimah-om <!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حساب عمر الطفل - إدارة تعليم نجران</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(rgba(255, 255, 255, 0.6), rgba(255, 255, 255, 0.6)), 
                        url('https://cdn.pixabay.com/photo/2016/11/29/05/07/child-1867451_1280.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
        }

        .main-card {
            background: rgba(255, 255, 255, 0.98);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.2);
            width: 90%;
            max-width: 480px;
            text-align: center;
            border: 4px solid #FFD700; /* إطار ذهبي جميل */
        }

        /* رأس الصفحة ملون */
        .header-section h2 {
            color: #2E7D32; /* أخضر غامق للوزارة */
            margin: 5px 0;
            font-size: 1.6em;
        }

        .header-section h3 {
            color: #1565C0; /* أزرق لإدارة نجران */
            margin: 5px 0;
            font-size: 1.3em;
        }

        .header-section img {
            width: 150px;
            margin-bottom: 15px;
        }

        h1 {
            color: #D81B60; /* وردي غامق للعنوان الرئيسي */
            font-size: 1.8em;
            text-shadow: 1px 1px 2px #eee;
        }

        .input-group label {
            color: #4527A0; /* بنفسجي للسؤال */
            font-weight: bold;
            font-size: 1.1em;
        }

        input[type="date"] {
            width: 100%;
            padding: 12px;
            border: 3px solid #FFCA28; /* حدود صفراء زاهية */
            border-radius: 15px;
            font-size: 18px;
            color: #333;
            text-align: center;
        }

        /* الأزرار */
        .btn-container {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }

        button {
            flex: 1;
            padding: 15px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 15px;
            border: none;
            cursor: pointer;
            transition: 0.3s;
            color: white;
        }

        .calc-btn { background: linear-gradient(45deg, #4CAF50, #81C784); }
        .calc-btn:hover { transform: scale(1.05); box-shadow: 0 5px 15px rgba(76, 175, 80, 0.4); }
        
        .print-btn { background: linear-gradient(45deg, #2196F3, #64B5F6); }
        .print-btn:hover { transform: scale(1.05); box-shadow: 0 5px 15px rgba(33, 150, 243, 0.4); }

        /* نتيجة ملونة ومبهجة */
        #result-box {
            margin-top: 25px;
            padding: 20px;
            background: #FFF9C4;
            border-radius: 20px;
            display: none;
            border: 3px dashed #FF8F00;
            animation: fadeIn 0.5s ease-in;
        }

        .age-text { color: #E64A19; font-size: 1.2em; font-weight: bold; }
        .stage-text { color: #2E7D32; font-size: 1.4em; display: block; margin-top: 10px; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* التذييل */
        .footer-section {
            margin-top: 40px;
            border-top: 2px solid #f0f0f0;
            padding-top: 20px;
            color: #555;
        }

        .footer-section strong {
            color: #C2185B; /* لون مميز لاسم المصممة */
            font-size: 1.2em;
            display: block;
            margin-top: 8px;
        }

        @media print {
            body { background: white !important; }
            button { display: none; }
            .main-card { box-shadow: none; border: 2px solid #000; }
        }
    </style>
</head>
<body>

<div class="main-card">
    <div class="header-section">
        <img src="https://raw.githubusercontent.com/moe-gov-sa/assets/main/logo.png" 
             onerror="this.src='https://upload.wikimedia.org/wikipedia/ar/thumb/2/29/Ministry_of_Education_%28Saudi_Arabia%29_Logo.svg/1200px-Ministry_of_Education_%28Saudi_Arabia%29_Logo.svg.png'"
             alt="شعار الوزارة">
        <h2>وزارة التعليم</h2>
        <h3>إدارة التعليم بنجران</h3>
    </div>

    <h1>حساب عمر الطفل 🎈</h1>
    
    <div class="input-group">
        <label>متى ولد طفلك الصغير؟</label>
        <input type="date" id="dob">
    </div>

    <div class="btn-container">
        <button class="calc-btn" onclick="celebrate()">عرض النتيجة 🎉</button>
        <button class="print-btn" onclick="window.print()">🖨️ طباعة</button>
    </div>

    <div id="result-box"></div>

    <div class="footer-section">
        المديرة ومصممة الموقع:
        <strong>فاطمه صالح آل بحري</strong>
    </div>
</div>

<script>
    function celebrate() {
        const dateInput = document.getElementById('dob').value;
        const resBox = document.getElementById('result-box');
        
        if (!dateInput) {
            alert("لطفاً، اختر التاريخ أولاً");
            return;
        }

        // إطلاق القصاصات الملونة (Confetti)
        confetti({
            particleCount: 150,
            spread: 70,
            origin: { y: 0.6 },
            colors: ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff']
        });

        // حساب العمر
        const bDate = new Date(dateInput);
        const today = new Date();
        let y = today.getFullYear() - bDate.getFullYear();
        let m = today.getMonth() - bDate.getMonth();

        if (m < 0 || (m === 0 && today.getDate() < bDate.getDate())) {
            y--;
            m += 12;
        }

        let stage = "";
        if (y < 3) stage = "أهلاً بك! الطفل لا يزال صغيراً جداً على الروضة 👶";
        else if (y == 3) stage = "المستوى الأول (روضة 1) 🎨";
        else if (y == 4) stage = "المستوى الثاني (روضة 2) 🧩";
        else if (y == 5) stage = "المستوى الثالث (روضة 3) 📚";
        else stage = "بطلنا مستعد للمدرسة الابتدائية! 🏫";

        resBox.style.display = "block";
        resBox.innerHTML = `
            <span class="age-text">عمر الطفل: ${y} سنوات و ${m} أشهر</span>
            <span class="stage-text">${stage}</span>
        `;
    }
</script>

</body>
</html>
