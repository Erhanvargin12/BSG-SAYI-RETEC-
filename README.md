# Unique Collatz Random Number Generator (RNG)

Bu proje, matematiksel **Collatz Sanısı** (3n+1 problemi) mantığını temel alan, sistem entropisiyle güçlendirilmiş özgün bir rastgele sayı üretme algoritmasıdır. Standart kütüphanelerden bağımsız olarak, sayısal kaos ve bit manipülasyonu ile benzersiz sonuçlar üretir.

---

## 🛠 Algoritma Mimarisi

Algoritma, deterministik bir matematiksel süreci (Collatz), sistemden gelen rastgelelik (Entropy) ile birleştirir. Süreç şu adımlardan oluşur:

### 1. Benzersiz Tohumlama (Unique Seeding)
Sıradan üreteçlerin aksine, tohum değeri sadece zamana bağlı değildir:
* **Nanosaniye Hassasiyeti:** `time.perf_counter_ns()` ile en küçük zaman birimi alınır.
* **Sistem Kimliği (PID):** İşletim sistemi tarafından atanan Process ID (İşlem Kimliği) kullanılır.
* **XOR İşlemi:** Bu iki değer XOR'lanarak aynı saniye içinde çalışan farklı işlemlerin aynı sonucu üretmesi engellenir.

### 2. Dinamik Aralık Belirleme
Algoritma sadece sayı üretmez, her çalışmada çıktıların bulunacağı **[Min, Max]** aralığını da başlangıçtaki tohum değerine bağlı olarak dinamik bir şekilde yeniden hesaplar.

### 3. Collatz Motoru ve Bit Hasadı
Her sayı üretimi için 16 adımlık bir döngü kurulur:
* Sayı **Tek** ise: $3n + 1$
* Sayı **Çift** ise: $n / 2$ işlemi uygulanır.



Bu işlemler sırasında oluşan tek/çift durumu, bir **Bit Havuzu (Bit Pool)** içinde toplanır. Bu yöntem, sayının matematiksel geçmişini bir "parmak izi" olarak saklayarak sonucu belirler.

### 4. Döngü Kırıcı (Loop Breaker)
Collatz dizisi 1'e ulaştığında normalde $4 \to 2 \to 1$ döngüsüne girer. Algoritma bunu tespit ederek `PID` ve `adım sayısı` ile duruma müdahale eder (**Jitter/Sarsıntı**) ve kaosun sürekliliğini sağlar.

### 5. Zincirleme Reaksiyon (State Chaining)
Üretilen her sayı, bir sonraki sayının başlangıç durumunu (state) doğrudan etkiler. Bu sayede üretilen sayılar dizisi arasında karmaşık bir bağımlılık kurulur ve tahmin edilebilirlik en aza indirilir.

---

## 💻 Kullanım Örneği

Sınıfı projenize dahil ettikten sonra aşağıdaki şekilde çağırabilirsiniz:

```python
# Sınıfı başlatma
rng = UniqueCollatzRNG()

# 3 adet analizli sayı üretme
rng.generate(3)
📋 Teknik Detaylar
Dil: Python 3.x

Kütüphaneler: os, time

Bit Genişliği: 16-bit (Havuza dayalı üretim)

Modüler Yapı: Her üretim adımında tam analiz ve loglama imkanı sunar.

👤 Geliştirici
Ad Soyad: Erhan Varğın

Öğrenci No: 230541087


---

Bu README dosyası projenin mantığını hem teknik hem de akademik olarak çok iyi özetleyecektir. 

**İstersen bu algoritmanın çıktılarını bir grafik (scatter plot) üzerinde görselleş
