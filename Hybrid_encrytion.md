
----------------------
#** Hybrid encrytion **
การเข้ารหัสแบบผสม
การเข้ารหัสแบบไฮบริดแบบดั้งเดิมจะรวมประสิทธิภาพของการเข้ารหัสแบบสมมาตรเข้ากับการใช้วิทยาการเข้ารหัสคีย์สาธารณะ (แบบอสมมาตร) เพื่อความสะดวก ทุกคนสามารถเข้ารหัสข้อมูลโดยใช้คีย์สาธารณะได้ แต่เฉพาะผู้ใช้ที่มีคีย์ส่วนตัวเท่านั้นที่จะถอดรหัสข้อมูลได้

สำหรับการเข้ารหัสแบบผสม ผู้ส่งจะสร้างคีย์สมมาตรใหม่เพื่อเข้ารหัสข้อความธรรมดาของแต่ละข้อความเพื่อสร้างข้อความเข้ารหัส คีย์แบบสมมาตรนั้นจะมีการรวมไว้กับคีย์สาธารณะของผู้รับ สำหรับการถอดรหัสแบบไฮบริด ผู้รับจะถอดรหัสคีย์แบบสมมาตร จากนั้นใช้ในการถอดรหัสข้อความเข้ารหัสเพื่อกู้คืนข้อความธรรมดาต้นฉบับ ดูรายละเอียดเกี่ยวกับวิธีจัดเก็บหรือส่งข้อความเข้ารหัสพร้อมกับการห่อหุ้มคีย์ได้ที่รูปแบบสายการเข้ารหัส Tink Hybrid

การเข้ารหัสแบบผสมมีคุณสมบัติดังต่อไปนี้

การปกปิดข้อมูล: ไม่มีใครรับข้อมูลใดๆ เกี่ยวกับข้อความธรรมดาที่เข้ารหัสได้ (ยกเว้นความยาว) เว้นแต่จะมีสิทธิ์เข้าถึงคีย์ส่วนตัว
ความไม่สมมาตร: การเข้ารหัสข้อความเข้ารหัสสามารถทำได้ด้วยคีย์สาธารณะ แต่ต้องใช้คีย์ส่วนตัวในการถอดรหัส
การสุ่ม: การเข้ารหัสจะเป็นแบบสุ่ม ข้อความ 2 รายการที่มีข้อความธรรมดาเดียวกันจะไม่ได้รับข้อความเข้ารหัสเดียวกัน เพื่อป้องกันไม่ให้ผู้โจมตีทราบว่า ข้อความเข้ารหัสใดตรงกับข้อความธรรมดา
การเข้ารหัสแบบไฮบริดแสดงด้วย Tink เป็นคู่ของค่าดั้งเดิมดังนี้

HybridEncrypt สำหรับการเข้ารหัส
HybridDecrypt สำหรับการถอดรหัส
พารามิเตอร์ข้อมูลบริบท
นอกเหนือจากข้อความธรรมดาแล้ว การเข้ารหัสแบบผสมยังยอมรับพารามิเตอร์เพิ่มเติมคือ context_info ซึ่งปกติแล้วจะเป็นข้อมูลสาธารณะโดยนัยจากบริบท แต่ควรเชื่อมโยงกับข้อความเข้ารหัสที่ได้ ซึ่งหมายความว่าข้อความเข้ารหัสช่วยให้คุณยืนยันความถูกต้องของข้อมูลบริบทได้ แต่ไม่รับประกันว่าข้อมูลจะปลอดภัยหรือถูกต้อง ข้อมูลบริบทจริงอาจว่างเปล่าหรือไม่มีข้อมูลก็ได้ แต่เพื่อให้แน่ใจว่าการถอดรหัสข้อความเข้ารหัสที่ได้นั้นถูกต้อง คุณจะต้องระบุค่าข้อมูลบริบทเดียวกันสำหรับการถอดรหัส

การใช้งานการเข้ารหัสแบบผสมอย่างเป็นรูปธรรมสามารถเชื่อมโยงข้อมูลบริบทกับข้อความเข้ารหัสได้หลายวิธี ตัวอย่างเช่น

ใช้ context_info เป็นอินพุตข้อมูลที่เกี่ยวข้องสำหรับการเข้ารหัสแบบสมมาตร AEAD (cf. RFC 5116)
ใช้ context_info เป็นอินพุต "CtxInfo" สำหรับ HKDF (หากการใช้งานใช้ HKDF เป็นฟังก์ชันที่มาของคีย์, cf. RFC 5869)
เลือกประเภทคีย์
เราขอแนะนำให้ใช้ประเภทคีย์ DHKEM_X25519_HKDF_SHA256_HKDF_SHA256_AES_256_GCM สำหรับกรณีการใช้งานส่วนใหญ่ คีย์ประเภทนี้ใช้มาตรฐานการเข้ารหัสคีย์สาธารณะแบบไฮบริด (HPKE) ตามที่ระบุไว้ใน RFC 9180 HPKE ประกอบด้วยกลไกการห่อหุ้มคีย์ (KEM) ฟังก์ชันการถอดรหัสคีย์ (KDF) และอัลกอริทึมการเข้ารหัสที่มีการตรวจสอบสิทธิ์ด้วยข้อมูลที่เกี่ยวข้อง (AEAD)

DHKEM_X25519_HKDF_SHA256_HKDF_SHA256_AES_256_GCM ว่าจ้างงานต่อไปนี้โดยเฉพาะ

KEM: Diffie–Hellman over Curve25519 พร้อม HKDF-SHA-256 เพื่อเก็บความลับที่แชร์
KDF: HKDF-SHA-256 เพื่อดูบริบทของผู้ส่งและผู้รับ
AEAD: AES-256-GCM พร้อมค่า Nonces 12 ไบต์ที่สร้างขึ้นตามมาตรฐาน HPKE
ประเภทคีย์ HPKE อื่นๆ ที่รองรับรวมถึงแต่ไม่จำกัดเพียงรายการต่อไปนี้

DHKEM_X25519_HKDF_SHA256_HKDF_SHA256_AES_128_GCM
DHKEM_X25519_HKDF_SHA256_HKDF_SHA256_CHACHA20_POLY1305
DHKEM_P256_HKDF_SHA256_HKDF_SHA256_AES_128_GCM
DHKEM_P521_HKDF_SHA512_HKDF_SHA512_AES_256_GCM
ดูรายละเอียดเพิ่มเติมเกี่ยวกับตัวเลือกอัลกอริทึมสำหรับ KEM, KDF และ AEAD ได้ที่ RFC 9180

ถึงแม้จะไม่แนะนำอีกต่อไป แต่ Tink ยังรองรับ ECIES บางรูปแบบตามที่อธิบายไว้ในมาตรฐาน ISO 18033-2 ของ Victor Shoup อีกด้วย ประเภทคีย์ ECIES ที่สนับสนุนบางรายการ แสดงอยู่ด้านล่างนี้

ECIES_P256_HKDF_HMAC_SHA256_AES128_GCM
ECIES_P256_COMPRESSED_HKDF_HMAC_SHA256_AES128_GCM
ECIES_P256_HKDF_HMAC_SHA256_AES128_CTR_HMAC_SHA256
ECIES_P256_COMPRESSED_HKDF_HMAC_SHA256_AES128_CTR_HMAC_SHA256

อ้างอิง https://developers.google.com/tink/hybrid?hl=th#:~:text=The%20Hybrid%20Encryption%20primitive%20combines,key%20can%20decrypt%20the%20data.


------------------------------

What Does Hybrid Encryption Mean?
Hybrid encryption is an approach to encoding and decoding data that blends the speed and convenience of a public asymmetric encryption scheme with the effectiveness of a private symmetric encryption scheme.

In this approach to cryptography, the sender generates a private key, encrypts the key by using a public key algorithm and then encrypts the entire message (including the already-encrypted private key) with the original symmetric key. The encoded cipher can only be decoded if the recipient knows the private key the sender originally generated.

If Bob wants to send an encypted message to Alice in a hybrid cryptosystem, for example, he might do the following:

Request Alice’s public key.
Generate a new symmetric (private) key and use it to encrypt a message.
Use Alice’s public key to encrypt the new symmetric (private) key and the message.
Send the entire cipher to Alice.
Alice will then be able to use her own private key to decrypt the sender’s private key and decode the rest of the message.

Security researchers are looking at ways hybrid encryption can be used as an alternative in quantum computing to more traditional encryption schemes. Until standards have been put in place, however, a hybrid approach can be accompanied by an increased risk of implementation flaws that can negate the encryption scheme’s usefulness.

Techopedia Explains Hybrid Encryption
A hybrid encryption scheme is one that blends the convenience of an asymmetric encryption scheme with the effectiveness of a symmetric encryption scheme.

How Hybrid Encryption Works
Hybrid encryption is achieved through data transfer using unique session keys along with symmetrical encryption. Public key encryption is implemented for random symmetric key encryption. The recipient then uses the public key encryption method to decrypt the symmetric key. Once the symmetric key is recovered, it is then used to decrypt the message.

Advantages and Disadvantages of Hybrid Encryption
The combination of encryption methods has various advantages. One is that a connection channel is established between two users’ sets of equipment. Users then have the ability to communicate through hybrid encryption.

Asymmetric encryption can slow down the encryption process, but with the simultaneous use of symmetric encryption, both forms of encryption are enhanced. The result is the added security of the transmittal process along with overall improved system performance.

อ้างอิง https://www.techopedia.com/definition/1779/hybrid-encryption