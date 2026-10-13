# 🏨 Hotel Booking Cancellation Prediction
### Otel Rezervasyon İptal Tahmini

**ATM​​ACA Team | BIL545 – Veri Madenciliği Projesi**

## 📌 Proje Hakkında

Bu proje, **BIL545 – Veri Madenciliği** dersi kapsamında, otel rezervasyonlarının iptal edilme durumlarını veri madenciliği ve makine öğrenmesi yöntemleriyle analiz etmek ve tahmin etmek amacıyla hazırlanmıştır.

Çalışmada **Hotel Booking Demand** veri seti kullanılmaktadır. Rezervasyonlara ilişkin çeşitli özellikler incelenerek iptal davranışlarıyla ilişkili değişkenlerin belirlenmesi ve rezervasyon iptallerini tahmin edebilen sınıflandırma modellerinin geliştirilmesi hedeflenmektedir.

Proje, birbirini tamamlayan **Proje 1** ve **Proje 2** olmak üzere iki aşamadan oluşmaktadır.

## 🎯 Projenin Amaçları

- Otel rezervasyon verilerini incelemek ve veri setinin yapısını anlamak.
- Eksik, hatalı ve tutarsız verileri tespit etmek.
- Veri ön işleme ve kategorik değişken kodlama yöntemlerini değerlendirmek.
- Veri sızıntısı (Data Leakage) risklerini belirlemek ve önlemek.
- Sınıflandırma modelleri geliştirerek rezervasyon iptallerini tahmin etmek.
- Modelleri çapraz doğrulama (Cross-Validation) yöntemiyle değerlendirmek.
- Accuracy, Precision, Recall ve F1-Score gibi performans metriklerini karşılaştırmak.
- Elde edilen sonuçları yorumlamak ve model performansını iyileştirmeye yönelik çalışmalar gerçekleştirmek.

## 📊 Kullanılan Veri Seti

**Veri seti:** Hotel Booking Demand

| Özellik | Açıklama |
|---|---|
| Toplam kayıt sayısı | 119.390 |
| Değişken sayısı | 32 |
| Hedef değişken | `is_canceled` |
| Problem türü | İkili sınıflandırma |
| Otel türleri | City Hotel ve Resort Hotel |

Hedef değişken olan `is_canceled`, rezervasyonun iptal edilip edilmediğini göstermektedir:

- **0:** Rezervasyon iptal edilmemiştir.
- **1:** Rezervasyon iptal edilmiştir.

## 📂 Proje Yapısı

```text
hotel-booking-cancellation/
│
├── Proje1/
│   ├── README.md
│   ├── Proje1.ipynb
│   ├── data/
│   ├── references/
│   └── weka_results/
│
├── Proje2/
│   ├── README.md
│   ├── data/
│   └── references/
│
├── .gitignore
└── README.md
```

*Not: Klasör yapısı proje ilerledikçe güncellenebilir.*

## 🔬 Proje Aşamaları

### Proje 1 – Veri Analizi, Ön İşleme ve Başlangıç Modelleri

Proje 1 kapsamında veri setinin incelenmesi, veri kalitesi kontrolleri, eksik değer analizi, kategorik değişkenlerin kodlanması ve veri sızıntısı risklerinin değerlendirilmesi gerçekleştirilmektedir.

Ayrıca temel sınıflandırma modelleri oluşturularak performansları karşılaştırılmakta ve Weka üzerinden bağımsız doğrulama çalışmaları yapılmaktadır.

Bu aşamanın temel çıktıları:

- Veri seti analizi ve veri künyesi
- Veri ön işleme çalışmaları
- Veri sızıntısı kontrolleri
- Değerlendirme hattı (Pipeline)
- Başlangıç modelleri ve performans sonuçları
- Weka doğrulama sonuçları

### Proje 2 – İleri Modelleme ve Performans Değerlendirmesi

Proje 2, Proje 1 kapsamında gerçekleştirilen çalışmaların devamı niteliğindedir.

Bu aşamada sınıflandırma modellerinin geliştirilmesi, performanslarının iyileştirilmesi ve elde edilen sonuçların daha kapsamlı şekilde değerlendirilmesi hedeflenmektedir.

Proje 2'ye ilişkin yöntemler, deneyler ve sonuçlar çalışmalar ilerledikçe ilgili klasörde belgelenecektir.

## 🛠️ Kullanılan Teknolojiler ve Araçlar

- **Python:** Veri analizi ve makine öğrenmesi
- **Google Colab:** Kod geliştirme ve deney ortamı
- **Pandas ve NumPy:** Veri işleme
- **Scikit-learn:** Makine öğrenmesi ve model değerlendirme
- **Matplotlib:** Veri görselleştirme
- **Weka:** Bağımsız model doğrulama
- **GitHub:** Proje dosyalarının yönetimi ve sürüm kontrolü

## 👥 Proje Ekibi

**ATM​​ACA Team**

## 🎓 Akademik Bilgiler

**Ders:** BIL545 – Veri Madenciliği

**Proje konusu:** Otel Rezervasyonlarında İptal Tahmini

**Veri seti:** Hotel Booking Demand

---

*Bu çalışma akademik ve eğitim amaçlı hazırlanmıştır.*
