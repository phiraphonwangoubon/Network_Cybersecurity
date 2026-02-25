# lab02_install and connected wazuh from windows and Linux

❇️ knowledge

    - Wazuh

    Wazuh ซึ่งเป็นโซลูชัน SIEM (Security Information and Event Management) แบบโอเพ่นซอร์สที่ทรงพลัง ในยุคดิจิทัลที่มีความซับซ้อนในปัจจุบัน การปกป้องระบบและข้อมูลของคุณจึงเป็นสิ่งสำคัญยิ่ง 

    Wazuh มอบแพลตฟอร์มที่แข็งแกร่งสำหรับการตรวจจับภัยคุกคาม การตอบสนองต่อเหตุการณ์ และการจัดการด้านการปฏิบัติตามข้อกำหนด 
    
    ไม่ว่าคุณจะเป็นผู้เชี่ยวชาญด้านความมั่นคงปลอดภัยไซเบอร์หรือผู้ที่สนใจเรียนรู้ คู่มือการติดตั้งทีละขั้นตอนนี้จะช่วยนำทางคุณตลอดกระบวนการอย่างง่ายดาย ครอบคลุมทุกระดับทักษะ


## 📌 1 )how to install wazuh ( ฝั่ง wazuh server หรือ wazuh manager )

1.1 ) update packages 

    command : sudo apt-get update
    command : sudo su

1.2 ) การติดตั้ง wazuh อย่างรวดเร็ว

    command : curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
    command : sudo bash ./wazuh-install.sh -a -o

1.3 ) จะได้ user and password มาหลังจากนั้นเข้าไปที่ https://[your_ipserver] นำไป login

<img width="928" height="60" alt="image" src="https://github.com/user-attachments/assets/925b004f-de4f-4a14-8996-48aeae548540" />

1.4 ) หน้า dashboard

<img width="1917" height="865" alt="image" src="https://github.com/user-attachments/assets/3d575a67-6344-4d06-afe3-356ae0ad1a4d" />

## 📌 2 ) how to install wazuh ( ฝั่ง wazuh agent windows )

2.1 ) ดาวน์โหลดและติดตั้ง Wazuh Agent จากเว็บไซต์

- Installing Wazuh agents on Windows endpoints - Wazuh agent

ทำการเลือกเวอร์ชั่น Agent ให้ตรงกับ Wazuh ที่ทำการติดตั้ง


2.2 ) ใส่ ip ของ wazuh manager และ auth key

📌 หาได้จาก 

command : sudo var/ossec/bin/manage_agents

<img width="447" height="366" alt="image" src="https://github.com/user-attachments/assets/2386be46-b45e-4e67-ac32-d4faf6c20959" />

<img width="660" height="223" alt="image" src="https://github.com/user-attachments/assets/d2e089ac-d138-417c-aa25-5e78c04715df" />

<img width="806" height="241" alt="image" src="https://github.com/user-attachments/assets/208fadd1-c989-4b14-ac30-450c8507c695" />

## 📌 3 ) Wazuh agents Linux endpoints

3.1 ) ติดตั้ง GPG Key

    command : curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg

3.2 ) เพิ่มแหล่งแพ็กเกจ (Repository)

      command : echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list

3.3 ) Update the package information:

    command : apt-get update

3.4 ) ติดตั้ง Wazuh Agent

เพื่อปรับใช้ (deploy) Wazuh agent บนเครื่องปลายทาง (endpoint) ให้คุณเลือกตัวจัดการแพ็กเกจที่เหมาะสม และแก้ไขตัวแปร WAZUH_MANAGER ให้ใส่เป็น IP หรือชื่อโฮสต์ของเครื่อง Wazuh Manager
    
    command : WAZUH_MANAGER="[ip_server_wazuh]" apt-get install wazuh-agent=version_wazuh

    คำสั่ง : sudo rm -f /var/ossec/etc/ossec.conf

3.5 ) ลบไฟล์เก่าทิ้ง

    command : sudo rm -f /var/ossec/etc/ossec.conf

3.6 ) สร้างใหม่

    command : sudo nano /var/ossec/etc/ossec.conf

จากนั้นให้คุณ วางทั้งหมดนี้ลงไป
            
              
          
      <ossec_config>
      <client>
        <server>
          <address>[ip_wazuhserver]</address>
          <port>[port_wazuh_server]</port>
          <protocol>tcp</protocol>
        </server>
      </client>
    
      <logging>
        <log_format>plain</log_format>
      </logging>
    </ossec_config>









