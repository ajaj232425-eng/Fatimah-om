# Fatimah-om <!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حساب عمر الطفل - إدارة تعليم نجران</title>
    <style>
        /* إعدادات الخلفية - تأكدي من الاتصال بالإنترنت لرؤية الصورة */
        body {
            font-family: 'Segoe UI', Tahoma, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            
            /* تم تغيير رابط الصورة هنا لرابط أكثر استقراراً */
            background: linear-gradient(rgba(255, 255, 255, 0.6), rgba(255, 255, 255, 0.6)), 
                        url('https://images.unsplash.com/photo-1503454537195-1dcabb73ffb9?q=80&w=1000&auto=format&fit=crop');
            
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
        }

        .main-card {
            background: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.3);
            width: 90%;
            max-width: 500px;
            text-align: center;
            border: 3px solid #1a5e37;
        }

        /* الجزء العلوي (الرأس) */
        .header-section {
            margin-bottom: 30px;
            border-bottom: 2px dashed #1a5e37;
            padding-bottom: 20px;
        }
        .header-section img {
            width: 140px;
            height: auto;
            margin-bottom: 15px;
        }
        .header-section h2 {
            color: #1a5e37;
            margin: 5px 0;
            font-size: 1.6em;
        }
        .header-section h3 {
            color: #2c3e50;
            margin: 5px 0;
            font-size: 1.2em;
            font-weight: 500;
        }

        /* مدخلات البيانات */
        .content-section h1 {
            color: #333;
            font-size: 1.8em;
            margin-bottom: 25px;
        }
        .date-input-container {
            margin-bottom: 30px;
        }
        label {
            display: block;
            font-weight: bold;
            margin-bottom: 10px;
            color: #1a5e37;
        }
        input[type="date"] {
            width: 100%;
            padding: 15px;
            border: 2px solid #1a5e37;
            border-radius: 15px;
            font-size: 18px;
            box-sizing: border-box;
            outline: none;
            text-align: center;
        }

        /* الأزرار */
        .buttons {
            display: flex;
            gap: 15px;
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
        }
        .calc-btn { background: #27ae60; color: white; }
        .calc-btn:hover { background: #219150; transform: scale(1.02); }
        .print-btn { background: #2980b9; color: white; }
        .print-btn:hover { background: #2471a3; transform: scale(1.02); }

        /* نتيجة الحساب */
        #result-box {
            margin-top: 25px;
            padding: 20px;
            background: #f0fdf4;
            border-radius: 15px;
            border: 2px solid #27ae60;
            display: none;
            color: #1a5e37;
            font-size: 1.2em;
            line-height: 1.6;
        }

        /* الجزء السفلي (التذييل) */
        .footer-section {
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            font-size: 1.1em;
            color: #444;
        }
        .footer-section strong {
            color: #1a5e37;
            display: block;
            margin-top: 10px;
            font-size: 1.2em;
        }

        /* عند الطباعة */
        @media print {
            body { background: white !important; }
            .main-card { border: 1px solid #000; box-shadow: none; }
            button { display: none; }
        }
    </style>
</head>
<body>

<div class="main-card">
    <div class="header-section">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/11/Ministry_of_Education_Saudi_Arabia_Logo.svg/512px-Ministry_of_Education_Saudi_Arabia_Logo.svg.png" alt="وزارة التعليم">
        <h2>وزارة التعليم</h2>
        <h3>إدارة التعليم بنجران</h3>
    </div>

    <div class="content-section">
        <h1>حساب عمر الطفل</h1>
        
        <div class="date-input-container">
            <label>اختر تاريخ ميلاد الطفل:</label>
            <input type="date" id="dob_input">
        </div>

        <div class="buttons">
            <button class="calc-btn" onclick="processAge()">عرض النتيجة</button>
            <button class="print-btn" onclick="window.print()">طباعة</button>
        </div>

        <div id="result-box"></div>
    </div>

    <div class="footer-section">
        المديرة ومصممة الموقع:
        <strong>فاطمه صالح آل بحري</strong>
    </div>
</div>

<script>
    function processAge() {
        const val = document.getElementById('dob_input').value;
        const res = document.getElementById('result-box');
        
        if (!val) {
            alert("لطفاً، حدد تاريخ الميلاد أولاً");
            return;
        }

        const bDate = new Date(val);
        const today = new Date();
        
        let y = today.getFullYear() - bDate.getFullYear();
        let m = today.getMonth() - bDate.getMonth();

        if (m < 0 || (m === 0 && today.getDate() < bDate.getDate())) {
            y--;
            m += 12;
        }

        let stage = "";
        if (y < 3) stage = "دون سن القبول";
        else if (y == 3) stage = "المستوى الأول (روضة 1)";
        else if (y == 4) stage = "المستوى الثاني (روضة 2)";
        else if (y == 5) stage = "المستوى الثالث (روضة 3)";
        else stage = "مؤهل للقبول بالصف الأول الابتدائي";

        res.style.display = "block";
        res.innerHTML = `عمر الطفل: ${y} سنوات و ${m} شهر<br>المرحلة: <b>${stage}</b>`;
    }
</script>

</body>
</html>
