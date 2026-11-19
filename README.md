# MALA Patient Registry

ต้นแบบหน้าจอบันทึกผู้ป่วย MALA ตามภาพอ้างอิง ครบ 5 ส่วนและข้อ 1–21 เปิด `index.html` ด้วยเว็บเบราว์เซอร์ได้โดยตรง

## ไฟล์ในโฟลเดอร์

- `index.html` — แบบฟอร์มแบ่ง 5 ส่วน พร้อมตัวเลือกหลายค่า ค้นหาไม่จำเป็น บันทึกในอุปกรณ์ และดาวน์โหลด CSV
- `mala_database_template.xlsx` — แม่แบบฐานข้อมูล มีชีต `Meat_Records` และ `Data_Dictionary`

## Google Sheets

อัปโหลดไฟล์ Excel ไปยัง Google Drive แล้วเปิดด้วย Google Sheets ได้ แต่หน้าฟอร์มนี้ยังไม่ได้เชื่อมต่อหรือส่งข้อมูลไป Google Sheets โดยตรง การเชื่อมต่อภายหลังต้องตั้งค่า Apps Script/API และสิทธิ์เข้าถึงก่อน

หนึ่งแถวแทนผู้ป่วยหนึ่งราย ชื่อคอลัมน์ภาษาอังกฤษใช้เป็น schema สำหรับฐานข้อมูล ตัวเลือกโรคประจำตัวและปัจจัยเสี่ยงหลายค่าถูกส่งออก CSV โดยคั่นด้วย `;`

## Deploy ด้วย GitHub Pages

มี workflow ที่ `.github/workflows/deploy.yml` แล้ว เมื่อ push ไปที่ branch `main` จะเผยแพร่เว็บ static นี้ด้วย GitHub Pages อัตโนมัติ

1. สร้าง repository ใหม่บน GitHub
2. ไปที่ **Settings → Pages** แล้วตั้ง **Build and deployment → Source** เป็น **GitHub Actions**
3. จาก PowerShell ในโฟลเดอร์โปรเจกต์ รันคำสั่งต่อไปนี้ แล้วแทน `YOUR-USERNAME` และ `YOUR-REPOSITORY` ให้ตรงกับบัญชีและ repository ของคุณ:

```powershell
git init
git add index.html README.md mala_database_template.xlsx .github/workflows/deploy.yml
git commit -m "Initial MALA registry site"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

4. เปิดแท็บ **Actions** รอ workflow สำเร็จ จากนั้นดู URL ที่ **Settings → Pages** (รูปแบบทั่วไป `https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/`)

## ข้อมูลผู้ป่วยและการเผยแพร่

GitHub Pages เผยแพร่เว็บไซต์ให้เข้าถึงได้สาธารณะ แม้ source repository จะเป็น private ในแผนที่รองรับ ดังนั้นเว็บนี้เหมาะกับการสาธิตด้วยข้อมูลสมมติเท่านั้น อย่ากรอกหรือเผยแพร่ข้อมูลผู้ป่วยจริงผ่านต้นแบบนี้ ข้อมูลใน Local Storage ยังอยู่ในเบราว์เซอร์ และไม่มีระบบล็อกอิน/ควบคุมสิทธิ์หรือฐานข้อมูลที่ปลอดภัย สำหรับใช้งานจริงให้ใช้ระบบและ hosting ที่หน่วยงานอนุมัติ พร้อม backend และการควบคุมสิทธิ์ที่เหมาะสม

## ข้อจำกัดของต้นแบบ

- ข้อมูลที่กรอกถูกเก็บใน Local Storage ของเบราว์เซอร์บนเครื่องนี้ และดาวน์โหลดเป็น CSV ได้; ยังไม่มีการยืนยันตัวตนหรือการสำรองข้อมูล
- ไฟล์ Excel เป็นแม่แบบว่าง ไม่ได้บรรจุข้อมูลผู้ป่วย
- มีตารางเกณฑ์ประกอบข้อ 16 ตามภาพอ้างอิง พร้อมลิงก์เอกสารต้นทาง; ให้หน่วยงานตรวจรับรองก่อนใช้งานทางคลินิก
- หมายเลขข้อ 3 ใช้กับ Refer Case ตามลำดับที่อนุมานจากภาพ ซึ่งแสดงหัวข้อวันที่ Admit เป็นข้อ 4
