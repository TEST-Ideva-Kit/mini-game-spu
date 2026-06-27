🎮  GAME  SPECIFICATION  &amp;  PROJECT  
PROPOSAL
 
PROJECT  NAME:  Music  Mania  (2026  Modernized  Edition)  STUDIO  POSITIONING:  Enterprise  
AI-Assisted
 
Co-Production
 
(Digital
 
Media
 
Faculty
 
Pilot)
 
FRAMEWORK:
 
Spec-Driven
 
Development
 
(SDD)
 
via
 
Promptzone
 
Architectural
 
Command
 
Center
 
🏗  มิติ ที่  1:  สถาปัตยกรรม ระบบ หลัง บ้าน และ การ วาง ระบบ  
(Technical
 
Architecture)
 
เพื่อ ความ เป็น สากล และ สามารถ แสดง ผล บน  Promptzone  Website  ได้ ทันที ผ่านแท็ก    ตัว เกม จะ
ถูก
สร้าง
ขึ้น
ด้วย
สถาปัตยกรรม
ดังนี้
:
 
1.  Audio-Clock  Synchronizer  (Conductor.cs)  
●  กฎ เหล็ก เชิง ระบบ  (System  Rule):  ห้าม ใช้  Time.time  ใน การ คํานวณ การ เคลื่อนที่ ของ โน้ต ดนตรี
โดย
เด็ดขาด
 ●  ตรรกะ แกน หลัก :  ตัว เกม ต้อง คํานวณ ตําแหน่ง จังหวะ ผ่าน ระบบ เวลา  Audio  Hardware  ของ  Unity  
โดย
ใช้
สูตร
:
 
\text{secPerBeat}
 
=
 
\frac{60.0f}{\text{bpm}}
 
\text{songPosition}
 
=
 
(\text{AudioSettings.dspTime}
 
-
 
\text{dspSongTime})
 
-
 
\text{startDelay}
 
\text{songPositionInBeats}
 
=
 
\frac{\text{songPosition}}{\text{secPerBeat}}
 ●  Quality  Gate:  ระบบ  Parity  Gate  ของ  Promptzone  จะ ทํา การ รัน สค ริ ปต์ทดสอบ  (Unit  Test)  บน  
Local
 
Machine
 
ของ
นักศึกษา
เพื่อ
ตรวจ
จับ
อัตรา
การ
หลุด
จังหวะ
 
(Audio
 
Drift)
 
ก่อน
อนุญาต
ให้
 
Commit
 
2.  Sandbox  Build  &amp;  Deployment  Specs  
●  Build  Target:  Unity  6  WebGL  (Headless  /  Batchmode  Build  via  Railway)  ●  Deployment  Pipeline:  เมื่อ  Conductor  Agent  ส่ง สัญญาณ  Socket  จาก เครื่อง นักศึกษา  
แพลตฟอร์ม
จะ
สั่ง
รัน
 
Docker
 
Image
 
บน
 
Railway
 
เพื่อ
คอม
ไพล์โป
ร
เจ
กต์เป็นไฟล์
 
Static
 
Web
 
แล้ว
ผลัก
ขึ้น
 
Vercel
 
เพื่อ
นํา
ลิง
ก์มา
ฝัง
บน
 
Web
 
UI
 
ทันที
 
🎭  มิติ ที่  2:  เมท ริก ซ์การ ออก แบบ ตัว ละคร และ ระบบสกิล  
(Character
 
Design
 
&amp;
 
Ability
 
Specs)
 
อ้างอิง จาก คลัง ตัว ละคร ดั้งเดิม ในไฟล์  Monomania_Musicmania_noDS.pdf  เรา จะ แปลง ลักษณะ ทาง
ศิลปะ
 
(Artistic
 
Persona)
 
ให้
กลาย
เป็น
 
ตรรกะ
เชิง
ระบบ
 
(Game
 
Mechanics)
 
เพื่อให้
 
AI
 
และ
นักศึกษา
นํา
ไป
เขียน
โปรแกรม
ร่วม
กับ
ระบบ
 
Event-Driven
 
System
 
ได้
อย่าง
แม่นยํา
:
                           [BaseCharacter]  
                                 
│
 
         
┌───────────────────────┼───────────────────────┐
 
         
▼
                       
▼
                       
▼
 
   
(Turntable
 
Bee)
          
(Aqua
 
Girl)
             
(DJ
 
Puff)
 
   
[Score
 
Enhancer]
     
[Shield
 
&amp;
 
Recovery]
     
[Mechanic
 
Tweaker]
 

 
1.  Turntable  Bee  ( ตัว ต่อ สี เหลือง สวม หู ฟัง ดี เจ )  
●  สาย งาน :  Score  Enhancer  ( สาย เน้น ทํา คะแนน ระดับ สูง )  ●  คํา อธิบาย พฤติกรรมสกิล  (C#  Data  Structure):  ○  ดัก จับ สถานะ ผ่าน อิน เทอร์เฟซ  ICharacterAbility  ○  เมื่อ ตัวแปร  currentCombo  &gt;=  50  ระบบ จะ เปิด ใช้ งาน สถานะ  Overdrive  ○  สูตร คํานวณ คะแนน :  ใน ขณะ ที่ สถานะ นี้ ทํา งาน  โน้ต ที่ กด ได้  Perfect  จะ ถูก คํานวณ ใหม่ เป็น :  
\text{NoteScore}
 
=
 
300
 
\times
 
1.10
 
\times
 
(\text{ComboMultiplier})
 ●  Animation  State  Triggers:  สั่ง งาน ผ่าน สค ริปต์  CharacterAnimationController  ให้ เปลี่ยน
สถานะ
ใน
 
Animator
 
ไป
ที่
ท
ริก
เกอร์
 
OnOverdriveActive
 
เพื่อ
เปิด
เอฟ
เฟกต์แสง
ไฟ
ดิสโก้รอบ
ตัว
ละคร
 
2.  Aqua  Girl  ( ตัว ละคร ธาตุ นํ้า สี ฟ้า สวม แว่นโกเกิ้ล )  
●  สาย งาน :  Shield  &amp;  Recovery  ( สาย ป้องกัน สําหรับ ผู้ เล่น เริ่ม ต้น )  ●  คํา อธิบาย พฤติกรรมสกิล  (C#  Data  Structure):  ○  กําหนด ตัวแปร  int  shieldCount  =  3  เมื่อ เริ่ม ต้น เพลง  ○  เมื่อ ระบบ  PlayerInput.cs  ส่ง สัญญาณ  Event  onNoteMiss  ให้ ทํา การ ดัก จับ  (Intercept)  
สัญญาณ
ก่อน
คลา
ส
คํานวณ
คะแนน
หลัก
จะ
รับ
รู้
 ○  เงื่อนไข :  หาก  shieldCount  &gt;  0  ให้ ทํา ลด ค่า  shieldCount--  และ บังคับ ส่ง สถานะ หลอก  
(Fake
 
State)
 
เป็น
 
Good
 
แทน
 
เพื่อ
รักษา
เส้น
สะสม
 
Combo
 
ของ
ผู้
เล่น
ไม่
ให้
กลาย
เป็น
 
0
 ●  Animation  State  Triggers:  เล่น อ นิ เม ชัน ท่า  OnGuardShield  พร้อม ทํา เอฟ เฟกต์ฟอง สบู่ แตก
กระจาย
บน
จอ
 
3.  DJ  Puff  ( ตัว ละคร แปด แขน สี ส้ม สวม หน้ากาก แก๊ส ลําโพง )  
●  สาย งาน :  Mechanic  Tweaker  ( สาย ปรับ แต่ง โครงสร้าง เกม เชิง เวลา )  ●  คํา อธิบาย พฤติกรรมสกิล  (C#  Data  Structure):  ○  มี หลอด สะสม ค่า พลังงาน  FeverBar  ( รับ ค่าเพิ่ม ขึ้น  +1\%  ทุก ครั้ง ที่ กด จังหวะ  Perfect)  ○  เมื่อ หลอด พลังงาน เต็ม  ผู้ เล่น สามารถ กด ปุ่ม  Spacebar  เพื่อ เปิด ใช้ งาน  Fever  Mode  เป็น
เวลา
 
5
 
วินาที
 ○  พฤติกรรม เชิง ระบบ :  ระบบ จะ เปลี่ยน ค่าตัว แปรก รอบ เวลา การก ด จังหวะ  (Hit  Window  
Offset)
 
ใน
สค
ริปต์
 
PlayerInput.cs
 
จาก
เดิม
 
0.1\text{s}
 
ขยาย
เป็น
 
0.115\text{s}
 
(+15\%)
 
ชั่วคราว
 
เพื่อ
เพิ่ม
โอกาส
การก
ด
 
Perfect
 
ใน
จังหวะ
เพลง
เร็ว
 ●  Animation  State  Triggers:  ท ริก เก อร์อ นิ เม ชัน ท่า  FeverDance  และ เปลี่ยน แถบ สี ของ ลู่ กด โน้ต
ทั้ง
 
4
 
เลน
เป็น
สี
ทอง
สว่าง
 
🗺  มิติ ที่  3:  ระบบ ด่าน และ กรอบ ความ ปลอดภัย  (Level  
Design
 
&amp;
 
Security
 
Rules)
 
ตัว เกม จะ ประกอบ ไป ด้วย  5  โซ น ตาม ภาพ แผนที่ โลก ต้นฉบับ  ซึ่ง ระบบ  Beatmap  Recorder  จะ ต้อง แปลง
ผลลัพธ์
ออก
มา
เป็น
โครงสร้าง
ข้อมูล
มาตรฐาน
 
เพื่อ
ส่ง
ขึ้น
ไป
โฮ
สต์และ
รี
วิ
ว
บน
หน้า
เว็บ
คอม
มูนิตี้ของ
 
Promptzone:
 

1.  โครงสร้าง ไฟล์ข้อมูล ด่าน  (Beatmap  JSON  Schema)  
AI  Worker  และ สค ริ ปต์เขียน ไฟล์จะ ต้อง ส่ง ออก ข้อมูล สอดคล้อง ตาม โครงสร้าง นี้ เท่านั้น  เพื่อ ผ่าน ด่าน  
Security
 
Gate
 
(
ตรวจ
สอบ
การ
แฝง
โค้ดอันตราย
หรือ
 
System
 
Path
 
หลุด
รอด
):
 {  
  
"beatmapId":
 
"musicmania_zone1_pub",
 
  
"songName":
 
"To
 
Be
 
Star",
 
  
"bpm":
 
128.0,
 
  
"noteCount":
 
420,
 
  
"levelZone":
 
"PinkPubDistrict",
 
  
"notes":
 
[
 
    
{
 
"beat":
 
4.0,
 
"lane":
 
0
 
},
 
    
{
 
"beat":
 
4.5,
 
"lane":
 
2
 
},
 
    
{
 
"beat":
 
5.0,
 
"lane":
 
1
 
},
 
    
{
 
"beat":
 
5.0,
 
"lane":
 
3
 
}
 
  
]
 
}
 
 
2.  Shift-Left  Security  &amp;  STRIDE  Mapping  
●  Spoofing  &amp;  Tampering  Protection:  สค ริ ปต์ระบบ คะแนน และ การ ส่ง ข้อมูล  Leaderboard  ไป ยัง
หน้า
เว็บ
จะ
ต้อง
วิ่ง
ผ่าน
กลไก
การ
เข้ารหัส
 
Hash
 
แบบ
 
SHA-256
 
ผูก
กับ
รหัส
นักศึกษา
 
เพื่อ
ป้องกัน
ไม่
ให้
นักศึกษา
แอบ
ใช้
วิธี
ส่ง
ข้อมูล
คะแนน
ปลอม
เข้า
 
API
 
เว็บก
ลาง
 
🤖  มิติ ที่  4:  พิมพ์เขียว สั่ง การ ระบบ  Multi-Agent  AI  
(Promptzone
 
Configuration)
 
เพื่อให้ นักศึกษา ทํา งาน แบบ  Strategic  Architect  (Agent  Boss)  ควบคุม  AI  ไม่ ให้ เกิด  Spaghetti  Code  
ให้
เรา
เขียน
ค่า
กําหนด
 
(Configurations)
 
นี้
ตั้ง
ไว้
บน
แพลตฟอร์ม
:
 promptzone_config:  
  
ai_tier_policy:
 
    
cloud_platform_ai:
 
"Stateless
 
(Haiku-class)
 
for
 
Task
 
breakdown
 
&amp;
 
API
 
routing"
 
    
local_agent_ai:
 
"Stateful
 
(Claude-class)
 
inside
 
student
 
machine
 
via
 
Conductor
 
daemon"
 
  
code_merge_policy:
 
    
engine:
 
"Hash-Anchored
 
Edits
 
Enabled"
 
    
conflict_resolution:
 
"Identify
 
stable-line
 
anchors
 
before
 
merging
 
player/score/conductor
 
branches"
 
  
autonomy_dial:
 
    
core_logic_scripts:
 
"Suggest-Only
 
(Requires
 
student
 
review
 
&amp;
 
emoji
 
confirmation)"
 
    
ui_vfx_assets:
 
"Semi-Autonomous
 
(AI
 
writes
 
boilerplate,
 
student
 
tweaks
 
parameters)"
 
 

หน้าที่ บน บอร์ด งาน  (Kanban  Assignment  Framework):  
●  Agent  1  (Orchestrator):  ส แกน ส เปก ตัว ละคร  3  ตัว ข้าง ต้น  แล้ว ทํา การ แตก งาน สร้าง ไฟล์คลา ส
หลัก
 
เช่น
 
ICharacterAbility.cs,
 
CharacterBase.cs
 
ลง
ลู่
บอร์ด
งาน
ของ
โปรแกรม
เมอร์
 ●  Agent  2  (VFX/UI  Worker):  รับหน้า ส เปก เรื่อง ของ เอฟ เฟกต์ฟอง สบู่  เพื่อ ไป เจน คําสั่ง
ระเบิดพาร์ทิเคิล
 
(Particle
 
System)
 
ให้
ฝั่ง
 
Technical
 
Artist
 
นํา
ไป
สวม
ใน
 
Unity
 
เอน
จิ
น
ทันที