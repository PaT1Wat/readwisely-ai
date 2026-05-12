# 📚 BookRec

BookRec คือเว็บแนะนำหนังสือ มังงะ และไลท์โนเวล ที่ใช้ระบบ AI และ Recommendation System เพื่อช่วยผู้ใช้ค้นหาหนังสือที่ตรงกับความสนใจ

---

# ✨ Features

- 🔍 ค้นหาหนังสือ
- ❤️ ระบบ Favorite
- 🤖 AI Chatbot (BookBot) ด้วย Gemini AI
- 📖 แนะนำหนังสืออัตโนมัติ
- 🎯 Recommendation System ด้วย LightFM
- 🏷️ ระบบแท็กและหมวดหมู่
- 👤 Authentication ด้วย Supabase
- 🛠️ Admin Panel สำหรับจัดการหนังสือ

---

# 🧠 Tech Stack

## Frontend
- React
- TypeScript
- Vite
- TailwindCSS
- React Router
- TanStack Query

## Backend
- FastAPI
- Python
- LightFM
- Gemini API

## Database
- Supabase

---

# 📂 Project Structure

```bash
BookRec/
│
├── backend/
│   ├── main.py
│   ├── recommend.py
│   └── requirements.txt
│
├── src/
│   ├── components/
│   ├── context/
│   ├── pages/
│   ├── hooks/
│   └── integrations/
│
├── public/
├── package.json
└── README.md
-------------------------------------------------------------------------------------------------------------
⚙️ Installation

1. Clone Project
git clone https://github.com/PaT1Wat/BookRec.git
cd BookRec

🚀 Frontend Setup

Install dependencies
npm install

Create .env
VITE_SUPABASE_URL=YOUR_SUPABASE_URL
VITE_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY
VITE_API_URL=http://localhost:8000

Run Frontend
npm run dev

Frontend:
http://localhost:8080

🐍 Backend Setup

Create venv
python -m venv venv

Activate venv
Windows
venv\Scripts\activate

Mac/Linux
source venv/bin/activate

Install packages
pip install -r requirements.txt

Create .env
Inside backend/.env
SUPABASE_URL=YOUR_SUPABASE_URL
SUPABASE_KEY=YOUR_SUPABASE_SERVICE_ROLE
GEMINI_API_KEY=YOUR_GEMINI_API_KEY

▶️ Run Backend
uvicorn main:app --reload

Backend:
http://127.0.0.1:8000
--------------------------------------------------------------------------------------------------------------
🤖 AI Chatbot

BookBot ใช้ Gemini AI สำหรับ:
แนะนำหนังสือ
วิเคราะห์แนวหนังสือ
ค้นหาหนังสือจาก tags
ตอบคำถามเกี่ยวกับหนังสือ

Supported Types:
มังงะ
นิยาย
ไลท์โนเวล

Supported Tags:
แอ็กชัน
ผจญภัย
แฟนตาซี
โรแมนติก
ดราม่า
คอมเมดี้
สยองขวัญ
สืบสวน
ไซไฟ
ชีวิตประจำวัน
BL ( Boy Love )
GL ( Girl Love )
-------------------------------------------------------------------------------------------------------------
🧩 Recommendation System

ใช้ LightFM สำหรับ:
Personalized Recommendation
Collaborative Filtering
Genre-based Recommendation

Train model:
POST /admin/retrain

📡 API Routes
Chat AI
POST /chat

Recommendation
GET /recommend/{user_id}

Retrain Model
POST /admin/retrain
-------------------------------------------------------------------------------------------------------------
# 🧠 Algorithms & Methods

## 🎯 Recommendation System: LightFM

ระบบแนะนำหนังสือใช้วิธี **Hybrid Recommendation System** โดยใช้ไลบรารี **LightFM**

LightFM เป็นอัลกอริทึมที่ผสมแนวคิด 2 แบบเข้าด้วยกัน คือ

1. **Collaborative Filtering**  
   วิเคราะห์พฤติกรรมของผู้ใช้ เช่น การกดถูกใจ การรีวิว หรือการมีปฏิสัมพันธ์กับหนังสือ เพื่อหาว่าผู้ใช้ที่มีพฤติกรรมคล้ายกันมักสนใจหนังสือประเภทใด

2. **Content-based Filtering**  
   วิเคราะห์ข้อมูลของหนังสือ เช่น ประเภทหนังสือ แท็ก ผู้แต่ง หรือแนวหนังสือ เพื่อแนะนำหนังสือที่มีลักษณะใกล้เคียงกับความสนใจของผู้ใช้

หลักการทำงานคือ ระบบจะสร้าง **user embedding** และ **item embedding** เพื่อแทนผู้ใช้และหนังสือในรูปแบบเวกเตอร์ จากนั้นคำนวณคะแนนความเหมาะสมระหว่างผู้ใช้กับหนังสือแต่ละเล่ม แล้วเรียงลำดับหนังสือที่มีคะแนนสูงที่สุดมาแสดงเป็นรายการแนะนำ

ระบบนี้เหมาะกับ BookRec เพราะสามารถใช้ได้ทั้งข้อมูลพฤติกรรมผู้ใช้และข้อมูลเนื้อหาของหนังสือ ทำให้แนะนำหนังสือได้แม่นยำกว่าการสุ่มหรือแสดงเฉพาะหนังสือยอดนิยม

---

## 🤖 AI Chatbot: BookBot

BookBot ใช้ **Gemini API** เป็น Large Language Model (LLM) สำหรับตอบคำถามและช่วยแนะนำหนังสือผ่านรูปแบบแชท

หลักการทำงานของ Chatbot คือ

1. ผู้ใช้พิมพ์คำถาม เช่น “แนะนำมังงะแนวดราม่า”
2. ระบบ frontend วิเคราะห์คำสำคัญจากคำถาม เช่น ประเภทหนังสือและแท็ก
3. ระบบคัดหนังสือที่เกี่ยวข้องจากฐานข้อมูล เช่น `type = manga` และ `tag = ดราม่า`
4. ส่งข้อมูลหนังสือที่เกี่ยวข้องไปยัง backend
5. backend สร้าง prompt ให้ Gemini วิเคราะห์
6. Gemini ตอบกลับเป็น JSON ที่มีข้อความตอบกลับและรายชื่อหนังสือแนะนำ
7. frontend แสดงผลเป็นข้อความและการ์ดหนังสือในหน้าแชท

แนวคิดที่ใช้คือ **Retrieval-Augmented Generation (RAG)** แบบเบื้องต้น โดยระบบไม่ได้ให้ AI แต่งข้อมูลเองทั้งหมด แต่จะส่งข้อมูลหนังสือจริงจากฐานข้อมูลไปให้ AI ใช้ประกอบการตอบ

กฎของ BookBot คือ:
- ใช้เฉพาะข้อมูลหนังสือที่มีอยู่ในระบบ
- ไม่แต่งข้อมูลหนังสือที่ไม่มีในฐานข้อมูล
- ตอบกลับเป็น JSON
- แนะนำหนังสือพร้อมเหตุผลสั้น ๆ

วิธีนี้ช่วยให้ Chatbot ตอบได้เป็นธรรมชาติ แต่ยังอ้างอิงจากข้อมูลจริงในระบบ BookRec