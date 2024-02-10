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
| --system | แสดงข้อความจาก service ของระบบ | journalctl --system | <img align="right" width="100%" src="image/jourSystem.png"> |
| --user | แสดงข้อความจาก service ของผู้ใช้ | journalctl --user | <img align="right" width="100%" src="image/jourUser.png"> |
| -M, --machine=CONTAINER | แสดงข้อความจาก machine หรือ container นั้นๆ | journalctl -M CONTAINER_NAME |  |
| -S, --since=DATE | แสดงข้อความตั้งแต่เวลาที่กำหนด | journalctl --since "2024-02-04 10:00:00" | <img align="right" width="100%" src="image/jourSince.png"> |
| -U, --until=DATE | แสดงข้อความจนถึงเวลาที่กำหนด | journalctl --until "2024-02-10 10:00:00" | <img align="right" width="100%" src="image/jourUntil.png"> |
| -c, --cursor=CURSOR | แสดงบันทึกตามตำแหน่งที่กำหนด | journalctl -c <cursor_value> |  |
| --after-cursor=CURSOR | แสดงบันทึกที่เกิดขึ้นหลังจากตำแหน่งที่กำหนด | journalctl --after-cursor=<cursor_value> |  |
| --show-cursor | แสดง curosr | journalctl --show-cursor | <img align="right" width="100%" src="image/jourShowCursor.png"> |
| --cursor-file=FILE |  |  |  |
| -b [ID][±offset], --boot [=ID][±offset] | แสดงข้อความที่เกี่ยวกับการบูต โดยกำหนดลำดับได้ | journalctl -b [ID][±offset] | <img align="right" width="100%" src="image/jourBoot.png"> |
| --list-boots | แสดงผลบูตแบบ list | journalctl --list-boots | <img align="right" width="100%" src="image/jourListBoot.png"> |
| -k, --dmesg | แสดงบันทึกในระดับ kernel | journalctl -k | <img align="right" width="100%" src="image/jourDmesg.png"> |
| -u, --unit=UNIT | แสดงข้อความเกี่ยวกับ unit ใน system unit | journalctl -u UNIT | <img align="right" width="100%" src="image/jourUnit.png"> |
| --user-unit=UNIT | แสดงข้อความเกี่ยวกับ unit ใน user unit | journalctl --user-unit=UNIT | <img align="right" width="100%" src="image/jourUserUnit.png"> |
| -t, --identifier=STRING | แสดงบันทึกที่เป็นค่า identifier ที่กำหนด | journalctl -t STRING | <img align="right" width="100%" src="image/jourIdentifier.png"> |
| -p, --priority=RANGE | แสดงข้อความตามระดับความสำคัญ (Range=0-7) | journalctl -p RANGE | <img align="right" width="100%" src="image/jourPriority.png"> |
| --facility=FACILITY | กรองและแสดงข้อความตาม facility(0-23) | journalctl --facility=FACILITY | <img align="right" width="100%" src="image/jourFacility.png"> |
| -g, --grep=PATTERN | กรองและแสดงข้อความตาม pattern | journalctl -g PATTERN | <img align="right" width="100%" src="image/jourGrep.png"> |
| --case-sensitive[=BOOL] | เงื่อนไขเพิ่มเติม โดยไม่สนพิมพ์เล็ก-ใหญ่ | journalctl --grep “error ” --case-sensitive | <img align="right" width="100%" src="image/jourCseSensitive.png"> |
| -e, --pager-end | เพื่อเรียกใช้งาน pager | journalctl -e | <img align="right" width="100%" src="image/jourPager.png"> |

</table>
</div>
