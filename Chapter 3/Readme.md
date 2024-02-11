# Chapter 3 Log Collection/ Server
## Log collection คือ 
การรวบรวมบันทึก log file จากแหล่งที่มาต่างๆ มารวมไว้ในที่เดียว

## ทำไมถึงต้องมี log collection 
เพราะ การรวมบันทึก log ไว้ในที่เดียวจะชวยให้เราทำงานได้ง่ายขึ้น เช่น
* ทำให้แก้ไขปัญหาได้ง่ายขึ้นและเร็วขึ้น การทำ log collection จะทำให้เราค้นหาได้เร็วมากขึ้น ปัญหาหนึ่งของ log file คือมันมักจะมีขนาดใหญ่ ซึ่งทำให้การค้นหาค่อนข้างยุ่งยาก การใช้ grep และ regex แจช่วยได้ แต่ก็ไม่เพียงพอเมื่อพูดถึงข้อมูลจำนวนมหาศาล เครื่องมือพิเศษที่ใช้ทำ log collection มักจะมีความสามารถในการค้นหาที่รวดเร็ว
* การวิเคราะห์  การเก็บ log file ในที่ต่างๆอาจแตกต่างกันทั้งรูปแบบทั้งเวลา ดังนั้น log collection จะมีเครื่องมือที่ช่วยในการบันทึก ทำให้การแก้ปัญหาและการจัดการรวดเร็วและง่ายยิ่งขึ้น

การเก็บ log collection ต้องปฏิบัติตามหลักเกณฑ์การเก็บรักษาข้อมูลจราจรทางคอมพิวเตอร์ของผู้ให้บริการ ตามพระราชบัญญัติว่าด้วยการกระทำความผิดเกี่ยวกับคอมพิวเตอร์ พ.ศ. 2560 และพระราชบัญญัติคุ้มครองข้อมูลส่วนบุคคล พ.ศ. 2562

## Log collection บน linux 
เป็นกระบวนการรวบรวม log file จากที่ต่างๆบนระบบ linux และส่งไปยังตำแหน่งศูนย์กลาง(central location) เพื่อสำหรับการวิเคราะห์และจัดเก็บ บน linux มี log file หลายประเภทเช่น application log, service log and audio log ในการรวบรวม log file จากระบบ linux จึงต้องมี log collection tool ช่วย 

## Syslog server คือ
เซิร์ฟเวอร์ที่ใช้รับและจัดเก็บ log file จากอุปกรณ์หรือแอปพลิเคชันต่างๆ ในเครือข่าย โดยใช้โปรโตคอล Syslog ซึ่งเป็นมาตรฐานที่แพร่หลายสำหรับการส่งข้อมูลบันทึกผ่าน UDP พอร์ต 514 
Syslog server ช่วยให้เราสามารถรวบรวมและวิเคราะห์ log file จากแหล่งต่างๆ ได้ในที่เดียว ซึ่งมีประโยชน์ในการแก้ไขปัญหา ตรวจสอบประสิทธิภาพ และรักษาความปลอดภัยของระบบ

### ประโยชน์ของ syslog
* เก็บรักษา log file ในรูปแบบของ database หรือ cloud
* สามารถแสดง log file เป็นตาราง กราฟ หรือ แผนภูมิได้
* สามารถ filter ในการค้นหาได้
* จัดหมวดหมู log file ได้
* ช่วยป้องกันการศูนย์หาย การเปลี่ยนแปลง หรือ การเข้าถึง log file โดยไม่ได้รับ อนุญาต

## ตัวอย่างโปรแกรมที่ใช้บันทึก log collection
### Syslogd
เป็นโปรแกรมที่ใช้บ่อยในระบบปฏิบัติการ linux และ Unix
syslogd daemon ช่วยจัดการข้อความจากเซิร์ฟเวอร์และโปรแกรม syslogd มีวิธีการจัดการไฟล์และบันทึกแบบครบวงจร ยอมรับ log จากเซิร์ฟเวอร์และโปรแกรมแล้วนำไป log file อย่างเหมาะสม ซึ่งสามารถช่วยให้รวบรวมข้อความจากแหล่งต่างๆ ไว้ใน log file ได้ง่ายขึ้น

* syslogd daemon จะอ่าน datagram socket และส่งขอความแต่ละบรรทัดไปยังปลายทาง /etc/syslog.conf 
* syslogd daemon อ่าน configuration file เมื่อ activated
* syslogd daemon จะสร้างไฟล์ /etc/syslog.pd ซึ่งเป็นบรรทัดเดียวที่มี command process ID ใช้เพื่อนสิ้นสุดหรือกำหนด syslogd daemon ใหม่ 
* เมื่อ terminate signal ส่งไปที่ syslogd daemon จะสิ้นสุดและ syslogd daemon จะบันทึกข้อมูล end signal และสิ้นสุดทันที

####การติดตั้ง
* sudo apt-get update<br>
  ![image](![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/109953502/baf463c1-cbba-4b94-88d5-f30c538b7f66)
)<br>)

* sudo apt-get install inetutils-syslogs
เพื่อติดตั้ง syslogd หลังจาดติดตั้งแล้วจะเริ่มเก็บ log ทันที

#### Option
-a = ใช้ระบุเพิ่มเติมจากที่ syslogd ต้องรับฟังได้
-d = เปิด debug mode เขียนข้อมูล debug ลง tty
-f = ปรับแต่งไฟล์ ระบุไฟล์ที่กำหนดค่าสำรองแทน /etc/syslog.conf ที่เป็นค่าเริ่มต้น
-h = ทำให้ log daemon ส่งข้อความระยะไกลไปยัง host ได้ (ค่าเริ่มต้น syslogd ไม่ส่งข้อความไป host ระยะไกล)	
-l = ระบุชื่อ host ที่จะบันทึก (ใช้ “:” คั่นเมื่อมีหลาย host)
-m = บันทึก timestamp (ตั้งค่าช่วงเวลาเป็นศูนย์จะปิดทำงานโดยสิ้นเชิง)
-p = ใช้ระบุ uinx domain socket สำรองแทน /dev/log
-r = ช่วยในการรับข้อความจากเครือข่ายโดยใช้ internet domain socket
-s = ระบุชื่อโดเมนที่ควรถอดออกก่อนเข้าสู่ระบบ
-v = แสดง version และออก
-x = ปอดใช้งานค้นหาชื่อเมื่อได้รับข้อความระยะไกล (วิธีนี้จะหลีกเลี่ยงไม่ให้เกิด deadlocks)

# Other Chapter
- 🛠 [**Introduction Monitoring and Logging Tools**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/README.md)
- 🛠 [**Chapter 1 Monitoring and Logging Tools**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%201/Readme.md)
- 📈 [**Chapter 2 Log Reader and Analysis**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%202/Readme.md)
- 📚 [**Chapter 4 Log Files**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%204/Readme.md)
- 📩 [**Chapter 5 Working with Texts**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%205/Readme.md)

# Source
- [Reference Log Collection and Server](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Reference/Chapter%203.md)
