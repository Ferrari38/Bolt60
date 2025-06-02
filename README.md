<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sum Inputs</title>
    <style>
        body {
            background-color: #2a2a2a;
            color: #f1f1f1;
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
        }
        form {
            background-color: #333333;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
            width: 100%;
            max-width: 400px;
            color: #ffffff;
        }
        .section {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-top: 10px;
            margin-bottom: 5px;
            font-weight: bold;
            text-align: left;
        }
        .input-group {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        input {
            padding: 5px;
            border: none;
            border-radius: 5px;
            background-color: #444444;
            color: #ffffff;
        }
        .highlight {
            border: 2px solid #4CAF50;
            padding: 10px;
            background-color: #333333;
            width: fit-content;
            border-radius: 5px;
            margin: 20px auto 0;
            text-align: left;
            display: none;
        }
        #calculationDetails {
            color: #b0f2b4;
            margin-top: 10px;
            white-space: pre-line;
            font-size: 12px;
        }
        #totalSum, #distanceUsed, #ratePerKm {
            color: #FFD700;
            font-size: 24px;
        }
        .button-container {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
        }
        button {
            padding: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 48%;
        }
        #calculateButton {
            background-color: #4CAF50;
            color: white;
        }
        #resetButton {
            background-color: #f44336;
            color: white;
        }
        #calculateButton:hover {
            background-color: #45a049;
        }
        #resetButton:hover {
            background-color: #e53935;
        }
        .compact-input-group {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        .compact-input-group label {
            margin: 0;
            width: 30%;
            text-align: right;
        }
        .compact-input-group input {
            width: 50%;
        }
        #dateSelector {
            margin-bottom: 20px;
        }
        #dateSelector label {
            font-size: 18px;
            font-weight: bold;
        }
        #dateSelector input {
            padding: 5px;
            border: none;
            border-radius: 5px;
            background-color: #444444;
            color: #ffffff;
        }
        #imageOutput {
            display: none;
            margin-top: 20px;
            text-align: center;
        }
        #canvasOutput {
            border: 2px solid #4CAF50; /* เส้นขอบสีเขียว */
            border-radius: 10px; /* มุมโค้ง */
            background-color: #f0f0f0; /* พื้นหลังสีขาวเทา */
            width: 100%;
            max-width: 380px;
            height: auto; /* ปรับความสูงอัตโนมัติ */
        }
        #copyButton {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
            width: 100%;
        }
        #copyButton:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <form id="sumForm">
        <div id="dateSelector">
            <h3>60:40</h3>
            <h3>แนะนำให้เปิดใน browser</h3>
            <h3>เช่น google chrome, safari</h3>
            <h3>(เพื่อบันทึกรูป)</h3>
            <label for="selectedDate">ยอดวันที่:</label>
            <input type="date" id="selectedDate" onchange="updateDate()">
        </div>

        <div class="section">
            <h2>รายรับ</h2>
            <div class="input-group">
                <label for="grab">GRAB:</label>
                <input type="number" id="grab" name="GRAB" placeholder="กรอกจำนวนเงิน" oninput="resetCalculation()">
            </div>
            <div class="input-group">
                <label for="bolt">BOLT:</label>
                <input type="number" id="bolt" name="BOLT" placeholder="กรอกจำนวนเงิน" oninput="resetCalculation()">
            </div>
            <div class="input-group">
                <label for="indriver">INDRIVER:</label>
                <input type="number" id="indriver" name="INDRIVER" placeholder="กรอกจำนวนเงิน" oninput="resetCalculation()">
            </div>
            <div class="input-group">
                <label for="maxim">MAXIM:</label>
                <input type="number" id="maxim" name="MAXIM" placeholder="กรอกจำนวนเงิน" oninput="resetCalculation()">
            </div>
            <div class="input-group">
                <label for="lineman">LINEMAN:</label>
                <input type="number" id="lineman" name="LINEMAN" placeholder="กรอกจำนวนเงิน" oninput="resetCalculation()">
            </div>
            <div class="input-group">
                <label for="others">งานนอก:</label>
                <input type="number" id="others" name="OTHERS" placeholder="กรอกจำนวนเงิน" oninput="resetCalculation()">
            </div>
        </div>

        <div class="section">
            <h2>รายจ่าย</h2>
            <div class="input-group">
                <label for="electricity">ค่าไฟ:</label>
                <input type="number" id="electricity" name="ELECTRICITY" placeholder="กรอกจำนวนเงิน" oninput="resetCalculation()">
            </div>
            <div class="input-group">
                <label for="otherExpenses">รายจ่ายอื่นๆ:</label>
                <input type="number" id="otherExpenses" name="OTHER_EXPENSES" placeholder="กรอกจำนวนเงิน" oninput="resetCalculation()">
            </div>
        </div>

        <div class="section">
            <h2>เลขไมล์รถ</h2> 
            <h4>ขับกะเช้า (ขับรถไม่ข้ามวัน)</h4> 
            <div class="compact-input-group">
                <label for="startday1">เริ่มงาน</label>
                <input type="number" id="startday1" name="startday1" placeholder="กรอกระยะทาง #1" oninput="resetCalculation()">
            </div>
            <div class="compact-input-group">
                <label for="endday1">จบงาน</label>
                <input type="number" id="endday1" name="endday1" placeholder="กรอกระยะทาง #1" oninput="resetCalculation()">
            </div>
            <h4>ขับกะกลางคืน (ขับข้ามวัน)</h4>
            <h5>ใส่ยอดตั้งแต่เที่ยงคืนเมื่อวาน-เที่ยงคืนวันนี้</h5>
            <h5>ยอดหลังเที่ยงคืนคิดในวันถัดไป</h5>
            <h5>เช่น 0.00-8.00น. ช่วง1 และ 20.00-24.00น. ช่วง2</h5>
            <div class="compact-input-group">
                <label for="startnight1">เมื่อวาน 0.00น.</label>
                <input type="number" id="startnight1" name="startnight1" placeholder="กรอกระยะทาง #1" oninput="resetCalculation()">
            </div>
            <div class="compact-input-group">
                <label for="endnight1">จบงานเมื่อวานตอนเช้า</label>
                <input type="number" id="endnight1" name="endnight1" placeholder="กรอกระยะทาง #1" oninput="resetCalculation()">
            </div>
            <div class="compact-input-group">
                <label for="startnight2">เริ่มงานเมื่อวานตอนเย็น</label>
                <input type="number" id="startnight2" name="startnight2" placeholder="กรอกระยะทาง #2" oninput="resetCalculation()">
            </div>
            <div class="compact-input-group">
                <label for="endnight2">เมื่อวาน 24.00น./ วันนี้ 0.00น.</label>
                <input type="number" id="endnight2" name="endnight2" placeholder="กรอกระยะทาง #2" oninput="resetCalculation()">
            </div>
        </div>

        <!-- ซ่อน calculationBox -->
        <div class="highlight" id="calculationBox" style="display: none;">
            <div id="calculationDetails"></div>
            <h2 id="totalSum">รวมยอดที่ต้องโอน: 0 บาท</h2>
            <h2 id="distanceUsed">ระยะทางที่ใช้: 0 กม.</h2>
            <h2 id="ratePerKm">บาทต่อกิโลเมตร: 0.00 บาท/กม.</h2>
            <div id="dateTime"></div>
        </div>

        <div class="button-container">
            <button type="button" id="resetButton" onclick="confirmReset()">รีเซ็ต</button>
            <button type="button" id="calculateButton" onclick="calculateAndShow()">คำนวณ</button>
        </div>

        <!-- แสดงผลรูปภาพสรุปผล -->
        <div id="imageOutput">
            <h3>สรุปผล</h3>
            <canvas id="canvasOutput" width="400" height="300"></canvas>
            <button type="button" id="copyButton" onclick="saveImage()">บันทึกรูปภาพ</button>
        </div>
    </form>

    <script>
        let isCalculated = false;
        let lastSelectedDate = "";

        function updateDate() {
            lastSelectedDate = document.getElementById('selectedDate').value;
            generateImage(); // สร้างรูปภาพใหม่เมื่อเปลี่ยนวันที่
        }

        function calculateAndShow() {
            calculateSum();
            generateImage();
            document.getElementById('imageOutput').style.display = 'block';
            isCalculated = true;
            
            // อัปเดตเวลาแบบเรียลไทม์ทุก 1 วินาที
            if (window.updateInterval) {
                clearInterval(window.updateInterval);
            }
            window.updateInterval = setInterval(() => {
                if (isCalculated) {
                    generateImage();
                }
            }, 1000);
        }

        function calculateSum() {
            let grab = parseFloat(document.getElementById('grab').value) || 0;
            let bolt = parseFloat(document.getElementById('bolt').value) || 0;
            let indriver = parseFloat(document.getElementById('indriver').value) || 0;
            let maxim = parseFloat(document.getElementById('maxim').value) || 0;
            let lineman = parseFloat(document.getElementById('lineman').value) || 0;
            let others = parseFloat(document.getElementById('others').value) || 0;
            let electricity = parseFloat(document.getElementById('electricity').value) || 0;
            let otherExpenses = parseFloat(document.getElementById('otherExpenses').value) || 0;

            let incomeSum = grab + bolt + indriver + maxim + others + lineman;
            let maintenanceFee = incomeSum * 0.1;
            let remainingIncome = incomeSum - maintenanceFee;
            let remainingAfterExpenses = remainingIncome - electricity;
            let half = remainingAfterExpenses * 0.6;
            let totalToTransfer = half + maintenanceFee;

            let calculationText = '';

            if (grab > 0) calculationText += `GRAB: ${grab} บาท\n`;
            if (bolt > 0) calculationText += `BOLT: ${bolt} บาท\n`;
            if (indriver > 0) calculationText += `INDRIVER: ${indriver} บาท\n`;
            if (maxim > 0) calculationText += `MAXIM: ${maxim} บาท\n`;
            if (lineman > 0) calculationText += `LINEMAN: ${lineman} บาท\n`;
            if (others > 0) calculationText += `งานนอก: ${others} บาท\n`;
            calculationText += `รวมยอดรายรับ = ${incomeSum.toFixed(2)} บาท\n`;
            calculationText += `maintenance (10%) = ${maintenanceFee.toFixed(2)} บาท\n`;
            calculationText += `ค่าไฟ: ${electricity} บาท\n`;
            calculationText += `รายจ่ายอื่นๆ: ${otherExpenses} บาท\n`;
            calculationText += `รวมรายจ่าย = ${maintenanceFee.toFixed(2)} + ${electricity} + ${otherExpenses} = ${(maintenanceFee + electricity + otherExpenses).toFixed(2)} บาท\n`;
            calculationText += `60% = (${incomeSum.toFixed(2)} - ${(maintenanceFee + electricity + otherExpenses).toFixed(2)}) = ${half.toFixed(2) - otherExpenses*0.6} บาท\n`;
            calculationText += `60%+บำรุง 10% = ${half.toFixed(2) - otherExpenses*0.6} + ${maintenanceFee.toFixed(2)} = ${totalToTransfer.toFixed(2) - otherExpenses*0.6} บาท\n`;

            let startday1 = parseFloat(document.getElementById('startday1').value) || 0;
            let endday1 = parseFloat(document.getElementById('endday1').value) || 0;
            let startnight1 = parseFloat(document.getElementById('startnight1').value) || 0;
            let endnight1 = parseFloat(document.getElementById('endnight1').value) || 0;
            let startnight2 = parseFloat(document.getElementById('startnight2').value) || 0;
            let endnight2 = parseFloat(document.getElementById('endnight2').value) || 0;

            let distance1 = Math.abs(endday1 - startday1);
            let distance2 = Math.abs(endnight1 - startnight1);
            let distance3 = Math.abs(endnight2 - startnight2);
            let totalDistance = distance1 + distance2 + distance3;
            
            if (startday1 > 0) calculationText += `เริ่มกะเช้า : ${startday1} KM\n`;
            if (endday1 > 0) calculationText += `จบกะเช้า : ${endday1} KM\n`;
            if (startnight1 > 0) calculationText += `0.00 กะกลางคืน : ${startnight1} KM\n`;
            if (endnight1 > 0) calculationText += `จบงานกะกลางคืน : ${endnight1} KM\n`;
            if (startnight2 > 0) calculationText += `เริ่มงานกะกลางคืน : ${startnight2} KM\n`;
            if (endnight2 > 0) calculationText += `24.00 กะกลางคืน : ${endnight2} KM\n`;
            
            let percentBonus = 0;
            let bonus = 0;
            let bamlaws = 0;

            if (totalDistance > 0) {
                percentBonus = (incomeSum / totalDistance) - 10;
                bamlaws = Math.abs(((((incomeSum / totalDistance) - 10)) / 10) * ((totalDistance / 2) * 10));
                if (percentBonus < 20) {
                    bonus = (percentBonus / 100) * 1.5 * bamlaws;
                    calculationText += `โบนัสรถใหญ่: ${bonus.toFixed(2)} บาท\n`;
                } else {
                    bonus = (20 / 100) * 1.5 * bamlaws;
                    calculationText += `โบนัสรถใหญ่: ${bonus.toFixed(2)} บาท\n`;
                }
            } else {
                calculationText += `โบนัสรถใหญ่: คำนวณไม่ได้เนื่องจากระยะทางรวมเป็นศูนย์\n`;
            }

            let percentBonusSM = 0;
            let bonusSM = 0;

            if (totalDistance > 0) {
                percentBonusSM = (incomeSum / totalDistance) - 10 ;
                if (percentBonusSM < 10 ) {
                    bonusSM = (percentBonusSM / 100)* 3 * bamlaws;
                    calculationText += `โบนัสรถเล็ก: ${bonusSM.toFixed(2)} บาท\n`;
                } else {
                    bonusSM = (10 / 100)* 3 * bamlaws;
                    calculationText += `โบนัสรถเล็ก: ${bonusSM.toFixed(2)} บาท\n`;
                }
            } else {
                calculationText += `โบนัสรถเล็ก: คำนวณไม่ได้เนื่องจากระยะทางรวมเป็นศูนย์\n`;
            }
            let ratePerKm = (incomeSum / totalDistance).toFixed(2) || 0;
            document.getElementById('calculationDetails').textContent = calculationText;
            document.getElementById('totalSum').textContent = `รวมยอดที่ต้องโอน: ${totalToTransfer.toFixed(2) - otherExpenses*0.6} บาท`;
            document.getElementById('distanceUsed').textContent = `ระยะทางที่ใช้: ${totalDistance} กม.`;
            document.getElementById('ratePerKm').textContent = `บาทต่อกิโลเมตร: ${ratePerKm} บาท/กม.`;
        }
        function resetCalculation() {
            document.getElementById('calculationBox').style.display = 'none';
            document.getElementById('imageOutput').style.display = 'none';
            isCalculated = false;
            if (window.updateInterval) {
                clearInterval(window.updateInterval);
            }
        }

        function confirmReset() {
            if (confirm("คุณแน่ใจว่าจะรีเซ็ตข้อมูลทั้งหมด?")) {
                document.getElementById('sumForm').reset();
                resetCalculation();
            }
        }

        function generateImage() {
            const canvas = document.getElementById('canvasOutput');
            const ctx = canvas.getContext('2d');

            // ตั้งค่า Scale Factor เพื่อเพิ่มความคมชัด
            const scaleFactor = 2;
            const baseWidth = 400; // ความกว้างฐานของ Canvas (ไม่รวม Scale)
            const baseHeight = 300; // ความสูงฐานขั้นต่ำ

            // คำนวณขอบ 10%
            const leftPadding = baseWidth * 0.1; // ขอบซ้าย 10% ของความกว้าง
            let topPadding; // ขอบบน 10% ของความสูง (จะคำนวณทีหลัง)

            // ดึงข้อมูลจาก UI
            const details = document.getElementById('calculationDetails').textContent;
            const totalSum = document.getElementById('totalSum').textContent;
            const distanceUsed = document.getElementById('distanceUsed').textContent;
            const ratePerKm = document.getElementById('ratePerKm').textContent;

            // แยกข้อมูลเป็นบรรทัด
            const detailsLines = details.split('\n').filter(line => line.trim() !== '');
            const summaryLines = [totalSum, distanceUsed, ratePerKm];

            // ตั้งค่าขนาดตัวอักษรและระยะห่าง
            const dateFont = '24px Arial';
            const detailsFont = '12px Arial';
            const summaryFont = '24px Arial';
            const lineHeight = 20; // ระยะห่างระหว่างบรรทัดในรายละเอียด
            const summaryLineHeight = 30; // ระยะห่างระหว่างบรรทัดสรุป
            const sectionGap = 20; // ระยะห่างระหว่างส่วน

            // 1. คำนวณความสูงของเนื้อหา
            let contentHeight = 30;
            
            // ส่วนวันที่ (ใช้ฟอนต์ 28px)
            ctx.font = dateFont;
            contentHeight += 35; // ความสูงของส่วนวันที่
            
            // ส่วนรายละเอียด (ใช้ฟอนต์ 24px)
            ctx.font = detailsFont;
            contentHeight += detailsLines.length * lineHeight;
            
            // ระยะห่างก่อนส่วนสรุป
            contentHeight += sectionGap;
            
            // ส่วนสรุป (ใช้ฟอนต์ 48px)
            ctx.font = summaryFont;
            contentHeight += summaryLines.length * summaryLineHeight;

            // 2. คำนวณความสูงรวม (รวม 10% ขอบบน)
            // สูตร: totalHeight = contentHeight / 0.9
            let totalHeight = Math.max(contentHeight / 0.9, baseHeight); // ไม่ต่ำกว่า 300px
            
            // 3. ตั้งค่าขนาด Canvas
            canvas.width = baseWidth * scaleFactor;
            canvas.height = totalHeight * scaleFactor;
            canvas.style.width = `${baseWidth}px`;
            canvas.style.height = `${totalHeight}px`;
            ctx.scale(scaleFactor, scaleFactor);

            // 4. คำนวณขอบบนใหม่จาก totalHeight
            topPadding = totalHeight * 0.1; // 10% ของความสูงรวม

            // ล้าง Canvas และตั้งค่าพื้นหลัง
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#f0f0f0';
            ctx.fillRect(0, 0, baseWidth, totalHeight);

            // วาดเส้นขอบ
            ctx.strokeStyle = '#4CAF50';
            ctx.lineWidth = 2;
            ctx.strokeRect(0, 0, baseWidth, totalHeight);

            // วาดวันที่
            ctx.fillStyle = '#0a7e07';
            ctx.font = dateFont;
            ctx.fillText(`ยอดวันที่: ${lastSelectedDate}`, leftPadding, topPadding);

            // วาดรายละเอียด
            ctx.fillStyle = '#000000';
            ctx.font = detailsFont;
            let y = topPadding + 35; // เริ่มจากใต้ส่วนวันที่
            detailsLines.forEach((line) => {
                ctx.fillText(line, leftPadding, y);
                y += lineHeight;
            });

            // วาดส่วนสรุป
            ctx.fillStyle = '#0a7e07';
            y += sectionGap;
            ctx.font = summaryFont;
            summaryLines.forEach((line) => {
                ctx.fillText(line, leftPadding, y);
                y += summaryLineHeight;
            });
            const now = new Date();
            const thaiDate = now.toLocaleDateString('th-TH', {
                year: 'numeric',
                month: 'long',
                day: 'numeric',
                weekday: 'long'
            });
            const thaiTime = now.toLocaleTimeString('th-TH');
            const dateTimeText = `อัปเดตล่าสุด: ${thaiDate} ${thaiTime} น.`;

            // เพิ่มความสูงส่วนวันที่และเวลา
            const dateTimeFont = '14px Arial';
            ctx.font = dateTimeFont;
            contentHeight += 30; // เพิ่มความสูงสำหรับบรรทัดวันที่

            // ... โค้ดเดิมที่คำนวณความสูง ...

            // วาดวันที่และเวลาด้านล่าง
            ctx.fillStyle = '#666666';
            ctx.font = dateTimeFont;
            ctx.textAlign = 'right';
            ctx.fillText(dateTimeText, baseWidth - leftPadding, totalHeight - 20);
            ctx.textAlign = 'left'; // รีเซ็ตการจัดตำแหน่ง
        }
        // ฟังก์ชันคัดลอกรูปภาพไปยังคลิปบอร์ด
        function saveImage() {
            const canvas = document.getElementById('canvasOutput');
            const dataURL = canvas.toDataURL('image/png');
            const link = document.createElement('a');
            link.download = `สรุปผล-${lastSelectedDate}.png`;
            link.href = dataURL;
            link.click();
        }
        setInterval(function() {
            const now = new Date();
            const dateTimeStr = `${now.toLocaleDateString('th-TH')} ${now.toLocaleTimeString('th-TH')}`;
            document.getElementById('dateTime').innerText = dateTimeStr;
        }, 1000);
        // เพิ่มการอัปเดตวันที่เริ่มต้น
        window.onload = function() {
            const dateInput = document.getElementById('selectedDate');
            const now = new Date();
            
            // แก้ไขเวลาตาม timezone ให้ถูกต้อง
            const timezoneOffset = now.getTimezoneOffset() * 60000; // แปลงเป็นมิลลิวินาที
            const localDate = new Date(now - timezoneOffset);
            
            const today = localDate.toISOString().split('T')[0];
            dateInput.value = today;
            lastSelectedDate = today;
        };
    </script>
</body>
</html> 
