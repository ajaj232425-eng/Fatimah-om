<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بوابة التسجيل الذكية - تعليم نجران</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --primary: #006d51;
            --secondary: #1565C0;
            --accent: #D81B60;
            --bg-card: rgba(255, 255, 255, 0.96);
        }

        body {
            font-family: 'Segoe UI', Tahoma, sans-serif;
            margin: 0;
            padding: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(rgba(255, 255, 255, 0.6), rgba(255, 255, 255, 0.6)), 
                        url('https://images.unsplash.com/photo-1503454537195-1dcabb73ffb9?auto=format&fit=crop&q=80&w=1000');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
        }

        /* العداد التنازلي */
        .countdown-timer {
            background: var(--primary);
            color: white;
            padding: 10px 20px;
            border-radius: 50px;
            margin-bottom: 20px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            font-size: 0.9em;
        }

        .main-card {
            background: var(--bg-card);
            padding: 30px;
            border-radius: 30px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
            width: 100%;
            max-width: 550px;
            text-align: center;
            border: 4px solid #FFD700;
        }

        .logo-box img { width: 160px; margin-bottom: 10px; }
        .header-section h2 { color: var(--primary); margin: 5px 0; }
        .header-section h3 { color: var(--secondary); margin: 5px 0; font-size: 1.1em; }

        .input-group {
            background: #fff9e6;
            padding: 20px;
            border-radius: 20px;
            border: 2px dashed #FFCA28;
            margin: 20px 0;
        }

        input[type="text"], input[type="date"] {
            width: 90%;
            padding: 12px;
            margin: 8px 0;
            border: 2px solid #FFCA28;
            border-radius: 12px;
            text-align: center;
            font-size: 16px;
        }

        .btn-container { display: flex; gap: 10px; margin-top: 10px; }
        button {
            flex: 1;
            padding: 14px;
            border-radius: 15px;
            border: none;
            cursor: pointer;
            font-weight: bold;
            color: white;
            transition: 0.3s;
        }
        .calc-btn { background: var(--primary); }
        .print-btn { background: var(--secondary); }

        /* بطاقة التهنئة */
        #congrats-card {
            display: none;
            margin-top: 25px;
            padding: 20px;
            background: linear-gradient(135deg, #fff9c4, #f8bbd0);
            border-radius: 20px;
            border: 3px double #D81B60;
            animation: slideIn 0.5s ease;
        }

        /* دليل الحقيبة */
        .bag-guide {
            margin-top: 25px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
        }
        .bag-item {
            font-size: 0.8em;
            background: white;
            padding: 10px;
            border-radius: 15px;
            border: 1px solid #ddd;
        }

        /* زر الواتساب */
        .whatsapp-float {
            position: fixed;
            bottom: 20px;
            left: 20px;
            background: #25d366;
            color: white;
            width: 60px;
            height: 60px;
            border-radius: 50px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 30px;
            box-shadow: 2px 2px 10px rgba(0,0,0,0.3);
            z-index: 1000;
            text-decoration: none;
        }

        @keyframes slideIn { from { transform: scale(0.8); opacity: 0; } to { transform: scale(1); opacity: 1; } }

        .footer { margin-top: 30px; border-top: 1px solid #eee; padding-top: 15px; }
        .footer strong { color: var(--accent); display: block; margin-top: 5px; }
    </style>
</head>
<body>

    <div class="countdown-timer" id="countdown">جاري حساب موعد العام الدراسي الجديد...</div>

    <div class="main-card">
        <div class="header-section">
            <img src="https://upload.wikimedia.org/wikipedia/commons/1/11/Ministry_of_Education_Saudi_Arabia_Logo.svg" alt="Logo">
            <h2>وزارة التعليم</h2>
            <h3>إدارة التعليم بنجران</h3>
        </div>

        <h1>حساب القبول الذكي 🎈</h1>

        <div class="input-group">
            <label>اسم الطفل المبدع:</label><br>
            <input type="text" id="childName" placeholder="أدخل اسم الطفل"><br>
            <label>تاريخ الميلاد:</label><br>
            <input type="date" id="birthDate">
        </div>

        <div class="btn-container">
            <button class="calc-btn" onclick="processAll()">تحقق من القبول 🎉</button>
            <button class="print-btn" onclick="window.print()">🖨️ طباعة</button>
        </div>

        <div id="congrats-card">
            <h2 id="resTitle" style="color:#D81B60"></h2>
            <p id="resAge" style="font-weight:bold"></p>
            <div id="reqSection" style="text-align:right; font-size: 0.9em; background: rgba(255,255,255,0.5); padding: 10px; border-radius: 10px;">
                <strong>📌 متطلبات هامة:</strong>
                <ul style="margin:5px 0; padding-right:20px;">
                    <li>وجبة صحية يومياً 🍱</li>
                    <li>الزي الموحد (بيج) 👕</li>
                    <li>الحضور 7:15 صباحاً ⏰</li>
                </ul>
            </div>
            <p id="tip" style="font-style:italic; color:#555; margin-top:10px;"></p>
        </div>

        <h4 style="margin-top:25px; color:var(--primary)">🎒 ماذا نضع في حقيبتي؟</h4>
        <div class="bag-guide">
            <div class="bag-item">💧<br>ماء فاتر</div>
            <div class="bag-item">🧼<br>مناديل</div>
            <div class="bag-item">👕<br>ملابس بديلة</div>
        </div>

        <div class="footer">
            المديرة ومصممة الموقع:
            <strong>فاطمه صالح آل بحري</strong>
        </div>
    </div>

    <a href="https://wa.me/966000000000" class="whatsapp-float" target="_blank">
        <i class="fab fa-whatsapp"></i>
    </a>

    <script>
        // 1. العداد التنازلي (افتراضي لبداية سبتمبر 2026)
        function updateCountdown() {
            const schoolDate = new Date("September 1, 2026 07:00:00").getTime();
            const now = new Date().getTime();
            const diff = schoolDate - now;
            
            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            document.getElementById("countdown").innerHTML = `⏳ متبقي ${days} يوم على بداية مغامرة العام الدراسي الجديد!`;
        }
        setInterval(updateCountdown, 1000);

        // 2. معالجة القبول والنتيجة
        function processAll() {
            const name = document.getElementById('childName').value;
            const bDateInput = document.getElementById('birthDate').value;
            const card = document.getElementById('congrats-card');

            if(!name || !bDateInput) {
                alert("لطفاً أدخل الاسم وتاريخ الميلاد ✨");
                return;
            }

            const bDate = new Date(bDateInput);
            const today = new Date();
            let y = today.getFullYear() - bDate.getFullYear();
            let m = today.getMonth() - bDate.getMonth();
            if (m < 0 || (m === 0 && today.getDate() < bDate.getDate())) { y--; m += 12; }

            let stage = "";
            let accepted = false;
            const tips = [
                "نصيحة: عودوا طفلكم على النوم المبكر من الآن 🌙",
                "نصيحة: شجعوا طفلكم على القراءة والرسم يومياً 🎨",
                "نصيحة: تحدثوا مع طفلكم عن جمال الروضة والأصدقاء 😊"
            ];

            if (y >= 3 && y <= 5) {
                accepted = true;
                if(y==3) stage = "روضة 1 (المستوى الأول)";
                else if(y==4) stage = "روضة 2 (المستوى الثاني)";
                else stage = "روضة 3 (المستوى الثالث)";
            } else if (y < 3) {
                stage = "لا يزال صغيراً جداً";
            } else {
                stage = "مؤهل للمرحلة الابتدائية";
            }

            card.style.display = "block";
            document.getElementById('resTitle').innerHTML = accepted ? `مبارك القبول يا ${name}! 🎉` : "نتيجة الحساب";
            document.getElementById('resAge').innerHTML = `العمر: ${y} سنوات و ${m} شهر <br> الفئة: ${stage}`;
            document.getElementById('tip').innerHTML = tips[Math.floor(Math.random()*tips.length)];
            document.getElementById('reqSection').style.display = accepted ? "block" : "none";

            if(accepted) confetti({ particleCount: 150, spread: 70, origin: { y: 0.6 } });
        }
    </script>
</body>
</html>
