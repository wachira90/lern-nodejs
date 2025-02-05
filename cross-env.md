### การใช้งานแพ็กเกจ **cross-env** ใน Node.js

#### **1. cross-env คืออะไร?**
`cross-env` เป็นแพ็กเกจที่ช่วยให้เราสามารถตั้งค่าตัวแปรแวดล้อม (environment variables) ได้อย่างง่ายดายโดยไม่ต้องกังวลเกี่ยวกับความแตกต่างของระบบปฏิบัติการ เช่น Windows, macOS หรือ Linux

โดยปกติแล้ว การตั้งค่าตัวแปรแวดล้อมมีความแตกต่างกัน เช่น:
- บน **Linux/macOS**: `NODE_ENV=production node app.js`
- บน **Windows (cmd)**: `set NODE_ENV=production && node app.js`

`cross-env` แก้ปัญหานี้โดยทำให้คำสั่งเหล่านี้ทำงานได้เหมือนกันในทุกระบบปฏิบัติการ

---

#### **2. การติดตั้ง**
ติดตั้ง `cross-env` ในโครงการของคุณโดยใช้ npm หรือ yarn:

```sh
# ติดตั้งผ่าน npm
npm install --save-dev cross-env

# ติดตั้งผ่าน yarn
yarn add -D cross-env
```

---

#### **3. การใช้งาน**
โดยทั่วไปแล้ว เราจะใช้ `cross-env` ในไฟล์ `package.json` ในส่วนของ `scripts`

**ตัวอย่าง**:
```json
{
  "scripts": {
    "start": "cross-env NODE_ENV=production node app.js",
    "dev": "cross-env NODE_ENV=development nodemon app.js"
  }
}
```

**การใช้งานใน Terminal**:
```sh
npm run start
```
หรือ
```sh
npm run dev
```

---

#### **4. ตัวอย่างโค้ดการอ่านค่าตัวแปรแวดล้อม**
ในโค้ด Node.js ของคุณ (`app.js`):
```js
console.log('Environment:', process.env.NODE_ENV);
```

- ถ้ารัน `npm run start` → จะแสดงผล `Environment: production`
- ถ้ารัน `npm run dev` → จะแสดงผล `Environment: development`

---

#### **5. ใช้ cross-env สำหรับหลายตัวแปร**
คุณสามารถตั้งค่าตัวแปรแวดล้อมหลายตัวพร้อมกันได้ เช่น:
```json
{
  "scripts": {
    "start": "cross-env NODE_ENV=production API_URL=https://api.example.com node app.js"
  }
}
```
แล้วในโค้ดของคุณ:
```js
console.log('Environment:', process.env.NODE_ENV);
console.log('API URL:', process.env.API_URL);
```

---

### **สรุป**
- `cross-env` ทำให้การตั้งค่าตัวแปรแวดล้อมใน Node.js ทำงานได้เหมือนกันทุกระบบ
- ใช้ `cross-env` ใน `package.json` เพื่อกำหนดตัวแปรแวดล้อมใน `scripts`
- สามารถตั้งค่าหลายตัวแปรได้พร้อมกัน
- อ่านค่าตัวแปรแวดล้อมผ่าน `process.env`

✅ **ช่วยให้การพัฒนาแอปพลิเคชัน Node.js เป็นไปอย่างสะดวกและรองรับทุกแพลตฟอร์ม**
