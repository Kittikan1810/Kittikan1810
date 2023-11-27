
-------------------------

#** Decrytion **

Encryption/Decryption คืออะไร
Encryption คือ  การเข้ารหัส หรือการแปลงข้อมูลให้เป็นรหัสลับ ไม่ให้ข้อมูลความลับนี้ถูกอ่านได้ โดยบุคคลอื่น แต่ให้ถูกอ่านได้โดยบุคคลที่เราต้องการให้อ่านได้เท่านั้น โดยการนำเอาข้อความเดิมที่สามารถอ่านได้ (Plain text,Clear Text) มาทำการเข้ารหัสก่อน เพื่อเปลี่ยนแปลงข้อความเดิมให้ไปเป็นข้อความที่เราเข้ารหัส (Ciphertext) ก่อนที่จะส่งต่อไปให้บุคคลที่เราต้องการที่จะติดต่อด้วย เพื่อป้องกันไม่ให้บุคคลอื่นสามารถที่จะแอบอ่านข้อความที่ส่งมาโดยที่ข้อ ความที่เราเข้ารหัสแล้ว ซึ่งทำได้โดยใช้โปรแกรม เช่น 

Decryption คือ การถอดรหัสข้อมูล อย่างข้อมูลที่ถูกใส่รหัสไว้ ซึ่งข้อมูลนี้เป็นข้อมูลที่ไม่สามารถอ่านได้ ดังนั้น จึงจำเป็นต้องนำข้อมูลเหล่านั้นมาถอดรหัส เพื่อให้สามารถอ่านได้

ประโยชน์ของการเข้ารหัส
1.เราสามารถที่จะระบุตัวตนของผู้ที่เราต้องการให้เข้าถึงข้อมูลของเราได้
2.รักษาความลับที่ไม่ให้ผู้อื่นที่ไม่มีสิทธิ์เข้าถึงข้อมูลได้
3.สามารถรักษาความถูกต้องและสมบูรณ์ของข้อมูล

นอกการเข้ารหัสแบบ Encryption แล้วยังมีการเข้ารหัสแบบอื่นอีก เช่น MD5

ข้อมูลอ้างอิง
http://www.nextproject.net
http://www.kateep.com

--------------------------

Decryption is a cryptographic primitive: it transforms a ciphertext message into plaintext using a cryptographic algorithm called a cipher. Like encryption, decryption in modern ciphers is performed using a specific algorithm and a secret, called the key. Since the algorithm is often public, the key must stay secret if the encryption stays secure.


![Image](img/decryption.png)

Decryption is the reverse of encryption and if the key stays secret, decryption without knowing the specific secret, decryption is mathematically hard to perform. How hard depends on the security of the cryptographic algorithm chosen and evolves with the progress of cryptanalysis.



ข้อมูลอ้างอิง
https://developer.mozilla.org/en-US/docs/Glossary/Decryption
