# Collatz XOR-Blending Random Number Generator (RNG)

Bu proje, ünlü **Collatz Sanısı ($3n + 1$)** üzerine inşa edilmiş, kriptografik yaklaşımlardan ilham alan  bir rastgele sayı üretme algoritmasıdır.

Standart ve basit yöntemlerin (örn. rakamları metin olarak yan yana dizmek) aksine, bu algoritma sayıları **XOR (Özel Veya)** mantığıyla matematiksel olarak harmanlayarak daha yüksek kaliteli bir rastgelelik (entropi) sağlar.

---

##  Algoritma Özellikleri

* **Dinamik Tohumlama (Seeding):** Sistem saatinin mikrosaniye hassasiyetini kullanarak her çalıştırmada tahmin edilemez benzersiz bir başlangıç noktası belirler.
* **Kaotik Yörünge Analizi:** Collatz sanısının öngörülemez iniş-çıkış yörüngelerini temel entropi kaynağı olarak kullanır.
* **XOR-Blending Tekniği:** Sayı dizilerini bit düzeyinde işleyerek matematiksel bir havuzda harmanlar. Bu, "string birleştirme" yönteminden çok daha profesyoneldir.
* **Döngü Koruması:** Algoritmanın bilinen $4-2-1$ döngüsüne hapsolmasını engelleyen mekanizmalara sahiptir.

---

##  Çalışma Mantığı

Algoritma temel olarak 4 ana adımdan oluşur:

### 1. Başlatma (Initialization)
Sistemden alınan hassas zaman verisiyle bir başlangıç durumu (`state`) oluşturulur ve kullanıcının istediği aralık (`min`, `max`) belirlenir.

### 2. Collatz Döngüsü ve Harmanlama
Belirli bir adım sayısı boyunca (örn. 8 adım) Collatz kuralı uygulanır:
* Sayı çiftse: $n = n / 2$
* Sayı tekse: $n = 3n + 1$

Her adımda elde edilen yeni değer, bir **`xor_sum`** (XOR Toplamı) değişkeni üzerinde **Bitwise XOR** işlemiyle biriktirilir. Bu işlem, önceki sayıların "izlerini" birbirine karıştırır.

### 3. Aralığa Sığdırma (Mapping)
Oluşan karmaşık `xor_sum` değeri, hedeflenen aralığa sığdırılmak için modülo işlemine tabi tutulur:
$$Sonuc = (xor\_sum \pmod{Aralik\_Boyutu}) + Min$$

### 4. Durum Güncelleme
Bir sonraki sayı üretimi için mevcut durum, son üretilen sayıyla harmanlanarak güncellenir (Zincirleme Etki).

---

##  Kullanım (Python Örneği)

```python
# Sınıfı başlat (Örn: 10 ile 250 arasında sayılar üret)
rng = SimpleCollatzRNG(min_val=10, max_val=250)

# Rastgele sayı üret
sayi = rng.generate()
print(f"Üretilen Sayı: {sayi}")
Geliştiren: Erhan Vargin Öğrenci No: 230541087
