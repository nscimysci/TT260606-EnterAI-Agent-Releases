# Enter AI Agent

Public download host สำหรับ **Enter AI local agent** (เก็บเฉพาะไฟล์ติดตั้ง — ซอร์สโค้ดอยู่ใน repo ส่วนตัว)

👉 **[ดาวน์โหลดเวอร์ชันล่าสุด](../../releases/latest)**

> ตั้งแต่ v1.26.9.23.1 เปลี่ยนชื่อจาก **AI Builder Agent** เป็น **Enter AI** — รุ่นก่อนหน้าอัปเดตเองไม่ได้ ให้โหลดตัวใหม่ไปลง 1 ครั้ง (release เก่ายังใช้ชื่อไฟล์ `ai-builder-agent-*`)

## เลือกไฟล์ให้ตรงเครื่อง

| เครื่อง | ไฟล์ |
|---|---|
| Mac (M1/M2/M3/M4) | `enter-ai-agent-darwin-arm64.app.zip` |
| Windows | `enter-ai-agent-win32-x64-setup.exe` |
| Windows (ไม่ติดตั้ง) | `enter-ai-agent-win32-x64.zip` |

`enter-ai-agent-win32-x64.zip` คือชุดเดียวกันแบบ **portable** — แตกไฟล์แล้วดับเบิลคลิก `run.cmd` ได้เลย ไม่ต้องติดตั้ง

> **Mac Intel ไม่รองรับแล้ว** — แจกเฉพาะ Apple Silicon (M1 ขึ้นไป) ไม่แน่ใจว่าเครื่องรุ่นไหน เปิด terminal พิมพ์ `uname -m` → `arm64` = Apple Silicon

## macOS — ครั้งแรกจะโดน Gatekeeper บล็อก

แอปยังไม่ได้ notarize กับ Apple จะขึ้นว่า *"Apple ไม่สามารถตรวจสอบยืนยันว่า … ไม่มีมัลแวร์"*
กด **เสร็จสิ้น** (⚠️ ห้ามกด "ย้ายไปยังถังขยะ") แล้วทำอย่างใดอย่างหนึ่ง:

### วิธีที่ 1 — terminal (เร็วสุด)

unzip แล้วลากแอปไปไว้ `/Applications` ก่อน จากนั้น:

```bash
xattr -dr com.apple.quarantine "/Applications/Enter AI.app"
open "/Applications/Enter AI.app"
```

ถ้าวางแอปไว้ที่อื่น ให้พิมพ์ `xattr -dr com.apple.quarantine ` **เว้นวรรค 1 เคาะ** แล้ว**ลากไอคอนแอปจาก Finder มาวางในหน้าต่าง terminal** — path จะเติมให้เองอัตโนมัติ แล้วค่อยกด Enter

### วิธีที่ 2 — ไม่แตะ terminal

เปิดแอป 1 ครั้งให้โดนบล็อกก่อน → **การตั้งค่าระบบ → ความเป็นส่วนตัวและความปลอดภัย** → เลื่อนลงล่างสุดจะเจอปุ่ม **"เปิดใช้งานต่อไป"** (Open Anyway)

> ต้องทำใหม่ทุกครั้งที่ดาวน์โหลดเวอร์ชันใหม่ เพราะ macOS ติดแฟล็ก `com.apple.quarantine` ให้ทุกไฟล์ที่โหลดมาจากอินเทอร์เน็ต

## Windows — SmartScreen จะเตือน

ตัวติดตั้งยังไม่ได้เซ็นด้วย code-signing certificate จะขึ้นจอน้ำเงิน *"Windows protected your PC"*
→ กด **More info** → **Run anyway**

## ตรวจสอบไฟล์ (ถ้าต้องการ)

ทุก asset มี `sha256` แสดงอยู่ในหน้า release เทียบกับของจริงได้ด้วย:

```bash
shasum -a 256 enter-ai-agent-darwin-arm64.app.zip   # macOS / Linux
certutil -hashfile enter-ai-agent-win32-x64-setup.exe SHA256   # Windows
```
