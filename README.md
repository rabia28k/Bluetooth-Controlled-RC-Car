# 🚗 Bluetooth Kontrollü Robot Araba (RC Car)

Bu proje, **Arduino Uno** ve **HC-06 Bluetooth modülü** kullanılarak geliştirilmiş, akıllı telefon üzerinden kablosuz olarak kontrol edilebilen 4 tekerlekten çekişli bir robot araba projesidir.

---

## 🛠️ Kullanılan Malzemeler (Hardware Components)

* **Arduino Uno** (Mikrodenetleyici)
* **L298N Motor Sürücüsü** (DC motorların hız ve yön kontrolü için)
* **HC-06 Bluetooth Modülü** (Kablosuz haberleşme için)
* **4 adet DC Motor ve Tekerlek** (4WD şasi)
* **18650 Pil Yuvası ve Piller** (Güç kaynağı)
* Jumper Kablolar ve Breadboard

---

## 📐 Devre Şeması / Bağlantılar

| Bileşen | Arduino Pin / Bağlantı | Açıklama |
| :--- | :--- | :--- |
| **HC-06 TX** | Dijital Pin 0 (RX) | Seri haberleşme (Kod yüklerken sökülmelidir) |
| **HC-06 RX** | Dijital Pin 1 (TX) | Gerilim bölücü ile bağlanması tavsiye edilir |
| **L298NENA** | Dijital Pin 5 (PWM) | Sol motorlar hız kontrolü |
| **L298NIN1** | Dijital Pin 6 | Sol motor yön kontrolü 1 |
| **L298NIN2** | Dijital Pin 7 | Sol motor yön kontrolü 2 |
| **L298NIN3** | Dijital Pin 8 | Sağ motor yön kontrolü 1 |
| **L298NIN4** | Dijital Pin 9 | Sağ motor yön kontrolü 2 |
| **L298NENB** | Dijital Pin 10 (PWM)| Sağ motor hız kontrolü |

---

## ⚙️ Nasıl Çalışır?

1. **Bağlantı:** Sistem enerjilendiğinde HC-06 Bluetooth modülünün üzerindeki LED yanıp söner. Telefonunuzun bluetooth ayarlarından modülle eşleşin (Varsayılan şifre genellikle `1234` veya `0000`'dır).
2. **Uygulama:** Telefonunuza herhangi bir *Bluetooth RC Controller* uygulamasını indirin (örn: *Arduino Bluetooth Car*). Tuş atamalarını yön tuşlarına (`İleri: F`, `Geri: B`, `Sol: L`, `Sağ: R`, `Dur: S`) göre yapılandırın.
3. **Kontrol:** Uygulama üzerinden gönderilen karakterler Bluetooth modülü aracılığıyla Arduino'ya seri port üzerinden ulaşır. Arduino, gelen karaktere göre motor sürücüsüne (`L298N`) sinyal göndererek aracın hareketini sağlar.

---

## 💻 Yazılım (Arduino Kodu)

Projenin kaynak koduna `arduino/` klasöründen ulaşabilir ya da aşağıdaki temel mantığı inceleyebilirsiniz:

```cpp
// Örnek komut yapısı özeti
char komut;

void setup() {
  Serial.begin(9600); // Bluetooth haberleşme hızı
  // Motor pin tanımlamaları...
}

void loop() {
  if (Serial.available() > 0) {
    komut = Serial.read();
    // Gelen komuta göre yönlendirme fonksiyonları
    if (komut == 'F') ileri();
    else if (komut == 'B') geri();
    else if (komut == 'S') dur();
  }
}
