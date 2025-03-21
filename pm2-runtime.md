การใช้งาน `pm2-runtime` ใน Dockerfile สำหรับแอป Node.js เป็นวิธีที่ดีในการจัดการ process ภายใน container โดยเฉพาะถ้าเราต้องการใช้ความสามารถของ PM2 ในการจัดการ lifecycle ของแอป เช่น auto-restart, log management ฯลฯ

ด้านล่างนี้คือตัวอย่างการใช้งาน `pm2-runtime` ใน `Dockerfile` สำหรับ Node.js:

---

### ✅ **ตัวอย่าง `Dockerfile`**

```Dockerfile
# เลือก base image ที่มี Node.js
FROM node:18-alpine

# ติดตั้ง PM2 แบบ global
RUN npm install pm2 -g

# ตั้ง working directory
WORKDIR /app

# คัดลอกไฟล์ต่างๆ ไปยัง container
COPY package*.json ./
RUN npm install

COPY . .

# Expose port ที่แอปใช้งาน
EXPOSE 3000

# ใช้ pm2-runtime เพื่อรันแอป
CMD ["pm2-runtime", "start", "ecosystem.config.js"]
```

---

### ✅ **ตัวอย่าง `ecosystem.config.js`**

```js
module.exports = {
  apps: [
    {
      name: "my-node-app",
      script: "index.js", // หรือ main.js แล้วแต่โปรเจกต์
      instances: 1,       // หรือ "max" เพื่อใช้ multi-core
      exec_mode: "fork",  // หรือ "cluster" ถ้าต้องการ clustering
      env: {
        NODE_ENV: "production",
      },
    },
  ],
};
```

---

### ✅ หรือถ้าไม่มี `ecosystem.config.js`

คุณสามารถรันตรงๆ แบบนี้ได้เลย:

```Dockerfile
CMD ["pm2-runtime", "index.js"]
```

---

### ✨ ข้อดีของ `pm2-runtime`:

- ทำให้ container ไม่จบ process หลังจาก Node หยุดชั่วคราว
- รองรับการ log อัตโนมัติ
- ใช้ได้กับ cluster mode ง่ายๆ
- ควบคุม process management ได้ดีใน production

---

ถ้ามีโค้ดหรือโครงสร้างโปรเจกต์ที่ใช้อยู่แล้ว บอกได้นะ จะได้ช่วยเขียนให้แม่นยำขึ้น 😄
