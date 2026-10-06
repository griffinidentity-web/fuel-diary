# ⛽ Fuel Receipt Diary

แอปจดบันทึกบิลน้ำมัน (ภาษาอังกฤษ, สกุลเงิน £) สำหรับใช้บน iPhone / iPad
ไฟล์เดียว (`index.html`) ไม่มีเซิร์ฟเวอร์ — **ข้อมูลทั้งหมดเก็บในเครื่องของคุณ** (IndexedDB ของ Safari)

## ทำอะไรได้บ้าง

- วางข้อความบิลที่ copy จาก LINE → กด **Read Receipt** → แอปดึงข้อมูลลงฟอร์มให้อัตโนมัติ
- กรอก **Odometer (miles)** เอง
- คำนวณ Trip miles, MPG (UK) และ £/mile ให้ทุกครั้งที่เติม
- สรุปรายเดือนปฏิทิน และ **Export เป็น Excel (.xlsx)** เพื่อส่งบัญชีเบิกเงิน
- **Backup / Restore** เพื่อย้ายข้อมูลระหว่าง iPhone กับ iPad

> บันทึกเฉพาะ **ยอดก่อนหักส่วนลด** (ส่วนลดไม่ถูกเก็บ)

## ข้อมูลที่ดึงจากบิล

| ฟิลด์ | ตัวอย่าง |
|---|---|
| Date & time | 25/09/2026 11:21 |
| Amount (£, ก่อนหักส่วนลด) | 74.69 |
| Litres / Price per litre | 42.22 L / £1.769 |
| Fuel type, Pump | FS Unleaded, 5 |
| Brand, Location, Postcode, Station No | Shell, Stanground Peterborough, PE2 8SH, 2438 |
| Payment, Terminal ID, Receipt No, Transaction No | Amex, 05243801, 000231, 000231 |

ฟิลด์ที่อ่านไม่ได้จะเว้นว่างและมีแถบเตือนสีเหลือง ตรวจและแก้ไขก่อนกด Save เสมอ เพราะ OCR อาจอ่านตัวเลขผิด

## การติดตั้ง (GitHub Pages)

1. สร้าง repository แบบ **Public** บน [github.com](https://github.com) (เช่นชื่อ `fuel-diary`)
2. อัปโหลดไฟล์ **`index.html` และ `apple-touch-icon.png`** (ไอคอนแอป) พร้อมกัน แล้วกด **Commit changes**
3. ไปที่ **Settings → Pages** → Branch: `main`, โฟลเดอร์ `/ (root)` → **Save**
4. รอ 1–2 นาที จะได้ลิงก์ `https://<ชื่อผู้ใช้>.github.io/fuel-diary/`

อัปเดตแอปภายหลัง: อัปโหลด `index.html` ใหม่ทับของเดิม (ข้อมูลในเครื่องไม่หาย)

## การใช้งานบน iPhone / iPad

1. เปิดลิงก์ใน **Safari** → **Share → Add to Home Screen**
2. เปิดแอปจากไอคอนบนหน้าจอหลักทุกครั้ง (iOS เก็บข้อมูลได้ดีกว่าเปิดผ่านแท็บ)

### การเพิ่มบิล

1. แท็บ **Add** → วางข้อความจาก LINE → **✨ Read Receipt**
2. ตรวจข้อมูล และกรอก **Odometer (miles)** (ช่องสีชมพู)
3. กด **💾 Save**

### สรุปยอดและส่งบัญชีสิ้นเดือน

1. แท็บ **Report** → เลือกเดือน
2. กด **📗 Export Excel for Accounts** → เลือก Save to Files / AirDrop / ส่งอีเมล
3. ไฟล์ `Fuel-Expenses-YYYY-MM.xlsx` มี 2 ชีต: **Summary** (สรุปยอด) และ **Receipts** (รายการทุกบิล + แถว TOTAL)

### Backup ทุก 1–2 สัปดาห์

1. แท็บ **Backup** → **📤 Backup** → เลือก Save to Files (iCloud Drive) หรือ AirDrop ไป iPad
2. บน iPad: เปิดแอปเดียวกัน → แท็บ **Backup** → **📂 Choose backup file**
3. Restore เป็นการ **รวมข้อมูล (merge)** ไม่ใช่ทับ — นำเข้าหลายไฟล์ต่อกันได้ รายการซ้ำจะไม่ซ้อน
4. แอปเตือนเมื่อไม่ได้ Backup เกิน 7 วัน

## การคำนวณ

- **Trip miles** = เลขไมล์ครั้งนี้ − เลขไมล์ครั้งก่อนหน้า (รวมข้ามเดือน)
- **MPG (UK)** = Trip miles ÷ (ลิตร ÷ 4.54609) — สมมติว่าเติมเต็มถังทุกครั้ง
- **£/mile** = ยอด ÷ Trip miles
- **Miles ของเดือน** = ผลรวม Trip miles ของบิลในเดือนนั้น

## ข้อควรรู้

- ต้องมีอินเทอร์เน็ตตอนเปิดแอป (โหลด Tailwind และตัวสร้าง Excel จาก CDN)
- ข้อมูลผูกกับ **ลิงก์ที่ใช้เปิด** ถ้าเปลี่ยนชื่อ repo / บัญชี ลิงก์จะเปลี่ยนและข้อมูลไม่ตามไป ให้ Backup ก่อนเสมอ
- ถ้าล้างข้อมูลเว็บไซต์ใน Safari ข้อมูลจะหาย — Backup ไว้สม่ำเสมอ
- ห้ามใช้ Private Browsing (เก็บข้อมูลไม่ได้)
- repo สาธารณะเห็นแค่โค้ดของแอป ไม่มีข้อมูลบิลของคุณ

## ไฟล์ในโปรเจกต์

| ไฟล์ | หน้าที่ |
|---|---|
| `index.html` | แอปหลัก (อัปโหลดไฟล์นี้ขึ้น GitHub Pages) |
| `apple-touch-icon.png` | ไอคอนแอปบนหน้าจอหลัก (อัปโหลดคู่กับ index.html) |
| `make_icon.py` | สคริปต์สร้างไอคอน (ไม่ต้องอัปโหลด) |
| `app.py` | เวอร์ชัน Flask + SQLite รุ่นแรก (ไม่ได้ใช้แล้ว) |
