# Chapter 2 Log Reader/Analysis
## Log Reader/Analysis มันคืออะไร?
   **Log Analysis**  เป็นกระบวนการตรวจสอบ วิเคราะห์การบันทึก(logs) เพื่อตรวจดูพฤติกรรมของโปรแกรม และคาดการณ์ปัญหาที่อาจจะเกิดขึ้นจากการใช้งาน

## คำสั่งพื้นฐานสำหรับ Log Analysis
   **Journalctl** - เป็นส่วนหนึ่งของชุดยูทิลิตี้ systemd และใช้เพื่อค้นหาและแสดงข้อความบันทึกจาก Systemd Journal(ระบบการบันทึกแบบรวมศูนย์ที่รวบรวมและจัดเก็บข้อมูลบันทึกจากแหล่งต่างๆ รวมถึงบริการของระบบ เหตุการณ์เคอร์เนล และแอปพลิเคชันผู้ใช้)

### Syntax ของคำสั่ง journalctl
	journalctl [options] [unit]

### ตัวอย่างเมื่อใช้คำสั่ง journalctl
<div>
  <img align="right" width="100%" src="image/journalctl.png">
  <p>&nbsp;</p>
</div>

### Option ทั้งหมดของคำสั่ง journalctl
<div align="center" style="width: 100%; margin: auto;">
<table style="width: 100%; border-collapse: collapse;">

| Options                 | Description                | Example   | Result |
| :---------------:  | :---------------------: | :-----------------: | :----------------: |
| --system           | แสดงข้อความจาก service ของระบบ     | journalctl --system |  |
| --user           | แสดงข้อความจาก service ของผู้ใช้ | journalctl --user |       |
| -M, --machine=CONTAINER           | แสดงข้อความจาก machine หรือ container นั้นๆ | journalctl -M CONTAINER_NAME |       |
| -S, --since=DATE           | แสดงข้อความตั้งแต่เวลาที่กำหนด | journalctl --since "2024-02-04 10:00:00" |       |
| -U, --until=DATE          | แสดงข้อความจนถึงเวลาที่กำหนด | journalctl --until "2024-02-10 10:00:00" |       |
| -c, --cursor=CURSOR           | แสดงบันทึกตามตำแหน่งที่กำหนด | journalctl -c <cursor_value> |       |
| --after-cursor=CURSOR           | แสดงบันทึกที่เกิดขึ้นหลังจากตำแหน่งที่กำหนด | journalctl --after-cursor=<cursor_value> |       |
</table>
</div>
