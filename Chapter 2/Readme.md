# Chapter 2 Log Reader/Analysis
## Log Reader/Analysis มันคืออะไร?
   **Log Analysis**  เป็นกระบวนการตรวจสอบ วิเคราะห์การบันทึก(logs) เพื่อตรวจดูพฤติกรรมของโปรแกรม และคาดการณ์ปัญหาที่อาจจะเกิดขึ้นจากการใช้งาน

## คำสั่งพื้นฐานสำหรับ Log Analysis
### - Journalctl
   **Journalctl** - เป็นส่วนหนึ่งของชุดยูทิลิตี้ systemd และใช้เพื่อค้นหาและแสดงข้อความบันทึกจาก Systemd Journal(ระบบการบันทึกแบบรวมศูนย์ที่รวบรวมและจัดเก็บข้อมูลบันทึกจากแหล่งต่างๆ รวมถึงบริการของระบบ เหตุการณ์เคอร์เนล และแอปพลิเคชันผู้ใช้)

#### Syntax ของคำสั่ง journalctl
	journalctl [options] [unit]

#### ตัวอย่างเมื่อใช้คำสั่ง journalctl
<div>
  <img align="right" width="100%" src="image/journalctl.png">
  <p>&nbsp;</p>
</div>

#### Option และ Command ทั้งหมดของคำสั่ง journalctl

