# AI Builder Agent

Public download host สำหรับ **AI Builder local agent** (เก็บเฉพาะไฟล์ติดตั้ง — ซอร์สโค้ดอยู่ใน repo ส่วนตัว)

👉 **[ดาวน์โหลดเวอร์ชันล่าสุด](../../releases/latest)**

## เลือกไฟล์ให้ตรงเครื่อง

| เครื่อง | ไฟล์ |
|---|---|
| Mac (M1/M2/M3/M4) | `ai-builder-agent-darwin-arm64.app.zip` |
| Mac (Intel) | `ai-builder-agent-darwin-x64.app.zip` |
| Windows | `ai-builder-agent-win32-x64.exe` |
| Linux | `ai-builder-agent-linux-x64` |

ไฟล์ที่ไม่มีนามสกุล (`darwin-arm64`, `darwin-x64`) คือ binary CLI เปล่า ๆ สำหรับรันใน terminal — คนทั่วไปใช้ `.app.zip`

ไม่แน่ใจว่า Mac เป็นรุ่นไหน? เปิด terminal พิมพ์ `uname -m` → `arm64` = Apple Silicon, `x86_64` = Intel

## macOS — ครั้งแรกจะโดน Gatekeeper บล็อก

แอปยังไม่ได้ notarize กับ Apple จะขึ้นว่า *"Apple ไม่สามารถตรวจสอบยืนยันว่า … ไม่มีมัลแวร์"*
กด **เสร็จสิ้น** (⚠️ ห้ามกด "ย้ายไปยังถังขยะ") แล้วทำอย่างใดอย่างหนึ่ง:

### วิธีที่ 1 — terminal (เร็วสุด)

unzip แล้วลากแอปไปไว้ `/Applications` ก่อน จากนั้น:

```bash
xattr -dr com.apple.quarantine "/Applications/AI Builder Agent.app"
open "/Applications/AI Builder Agent.app"
```

ถ้าวางแอปไว้ที่อื่น ให้พิมพ์ `xattr -dr com.apple.quarantine ` **เว้นวรรค 1 เคาะ** แล้ว**ลากไอคอนแอปจาก Finder มาวางในหน้าต่าง terminal** — path จะเติมให้เองอัตโนมัติ แล้วค่อยกด Enter

### วิธีที่ 2 — ไม่แตะ terminal

เปิดแอป 1 ครั้งให้โดนบล็อกก่อน → **การตั้งค่าระบบ → ความเป็นส่วนตัวและความปลอดภัย** → เลื่อนลงล่างสุดจะเจอปุ่ม **"เปิดใช้งานต่อไป"** (Open Anyway)

> ต้องทำใหม่ทุกครั้งที่ดาวน์โหลดเวอร์ชันใหม่ เพราะ macOS ติดแฟล็ก `com.apple.quarantine` ให้ทุกไฟล์ที่โหลดมาจากอินเทอร์เน็ต

## Windows — SmartScreen จะเตือน

`.exe` ยังไม่ได้เซ็นด้วย code-signing certificate จะขึ้นจอน้ำเงิน *"Windows protected your PC"*
→ กด **More info** → **Run anyway**

## Linux

```bash
chmod +x ai-builder-agent-linux-x64
./ai-builder-agent-linux-x64
```

## ตรวจสอบไฟล์ (ถ้าต้องการ)

ทุก asset มี `sha256` แสดงอยู่ในหน้า release เทียบกับของจริงได้ด้วย:

```bash
shasum -a 256 ai-builder-agent-darwin-arm64.app.zip   # macOS / Linux
certutil -hashfile ai-builder-agent-win32-x64.exe SHA256   # Windows
```
