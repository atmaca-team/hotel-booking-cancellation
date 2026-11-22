# 🏨 **ATM​​ACA Team | BIL545 – İleri Veri Madenciliği Projesi**

# Otel Rezervasyonlarında İptal Riski: Rezervasyon Anında Öngörülebilir mi?

> BIL545 · Veri Madenciliğinde İleri Konular · 2026–2027 Güz · Üsküdar Üniversitesi
> Bu dosya Atmaca grubunun GitHub deposunun ana sayfasıdır ve her proje tesliminde güncellenir.

## Grup

| Üye | Öğrenci no |
|---|---|
| Melike Duygu YILDIRIM | 264312005 |
| Vildan ÇAP | [no] |
| Melisa LOTFIAZAR | [no] |
| WAIL ABDULRAQEB MOHAMMED NOMAN | [no] |

- **Grup adı:** ATM​​ACA Team
- **İletişim sorumlusu:** Melike Duygu YILDIRIM -melikedyg@gmail.com
- **Grup tipi:** 4 kişi (+ Ek paket 1)

## Soru

Bir otel rezervasyonunun iptal edilip edilmeyeceği (iptal veya No-Show), rezervasyonun oluşturulduğu anda bilinen bilgilerle öngörülebilir mi? Bu soru, otelin fazla rezervasyon (overbooking), oda planlaması ve gelir yönetimi kararlarına yarar.

## Veri

| | |
|---|---|
| **Veri kümesi** | Hotel Booking Demand (Antonio, Almeida ve Nunes, 2019) |
| **Kaynak** | Makale: https://doi.org/10.1016/j.dib.2018.11.126 · Kullandığımız birleşik dosya (H1 + H2, TidyTuesday kopyası): https://raw.githubusercontent.com/rfordatascience/tidytuesday/main/data/2020/2020-02-11/hotels.csv |
| **Lisans** | CC BY 4.0 |
| **Boyut** | 119.390 satır × 32 sütun (Resort Hotel 40.060, City Hotel 79.330; varış tarihi 1 Temmuz 2015 – 31 Ağustos 2017) |
| **Hedef değişken** | `is_canceled` (1 = iptal edildi veya No-Show, 0 = gerçekleşti); iptal oranı %37,04 |

**Verinin indirilmesi:** Veri bu depoda yoktur. Defter, veriyi yukarıdaki TidyTuesday adresinden `pd.read_csv(url)` ile her çalıştırmada kendisi indirir; ayrıca bir yükleme adımı gerekmez. Colab'ın internet erişimi olmalıdır.

## Depo yapısı

```
.
├── README.md
├── proje1/
│   ├── BIL545_Proje1_Atmaca.ipynb
│   └── weka/
│       ├── 1.7_ZeroR_J48_cikti.txt
│       ├── 3.4_weka_output.txt
│       └── ekran_goruntuleri/
└── proje2/
    └── BIL545_Proje2_Atmaca.ipynb
```

Defterin ürettiği dosyalar (`HotelBooking_Weka.arff`, `bolum3_islemler.arff`, `bolum3_weka_apriori.txt`, `proje2_aktarim/`) defter çalıştırılınca yeniden oluşur. Veri içerdikleri için ARFF dosyaları ve `proje2_aktarim/p1_temiz_veri.csv` depoya konmamıştır.

## Çalıştırma

1. Defteri Colab'da açın: [Proje 1 Colab bağlantısı]
2. Veri ilk hücrelerde internetten otomatik indirilir; ek bir adım gerekmez.
3. **Çalışma Zamanı → Tümünü çalıştır.** Kütüphane sürümleri defterin ilk hücresinde yazdırılır; `mlxtend` 0.25.0 sürümüyle kurulur. Tüm defterin çalışması standart Colab makinesinde yaklaşık [süre] sürer (en uzun adım 2.1'deki model karşılaştırması).
4. 1.7 ve 3.4'teki ARFF dosyaları Colab'dan indirilir ve Weka 3.8 Explorer'da açılır; 3.4'te Weka Apriori ayrıca komut satırından da çalıştırılır.

## Sonuç özeti

Bütün sonuçlar katmanlı 5 kat × 5 tekrar çapraz doğrulamadan (25 bölme), ortalama ± standart sapma olarak verilmiştir; ana ölçüt iptal sınıfının F1 değeridir.

### Proje 1 (vize)
- **Baseline:** Hep "iptal değil" diyen Dummy: F1 0,0000 ± 0,0000 (doğruluk 0,6296 ± 0,0000); hep "iptal" diyen Dummy: F1 0,5406 ± 0,0000. İlk model (lojistik regresyon): F1 0,6275 ± 0,0046.
- **En iyi model:** Rastgele orman (100 ağaç, `min_samples_leaf=2`, nadir One-Hot ön işleme, tek `Pipeline`): F1 0,7166 ± 0,0043, ROC-AUC 0,8890 ± 0,0020. k-NN'den farkı McNemar (p ≈ 1,6·10⁻³⁵) ve 5×2 ÇD t-testinde (p ≈ 3,7·10⁻⁵) anlamlı çıktı.
- **Sızıntı deneyi:** Doğru kurulum (ön işleme ve öznitelik seçimi `Pipeline` içinde) F1 0,4676 ± 0,0056; yanlış kurulum (bütün veride) F1 0,4664 ± 0,0053. Bu veride fark küçük çıktı, ama yanlış kurulumdaki skor test bilgisi içerdiği için geçerli kabul edilmedi.
- **Önemli bulgular:**
  - Satırların %26,80'i (31.994) başka bir satırın birebir kopyası. Kopyalar çıkarılınca rastgele ormanın F1'i 0,7163'ten 0,4571'e, ROC-AUC'si 0,8893'ten 0,7939'a düşüyor; bu yüzden raporlanan skorları yeni rezervasyonlar için iyimser bir üst sınır olarak görüyoruz.
  - `reservation_status` ve `reservation_status_date` kesin sızıntı olduğu için, `booking_changes`, `assigned_room_type`, `days_in_waiting_list` ise rezervasyondan sonra oluştuğu için modele alınmadı. Rezervasyon anında bilinip bilinmediği şüpheli `deposit_type` ve `country` eklenince F1 0,7769'a çıkıyor; tahmin anını korumak için bu sütunları kullanmadık.
  - Birliktelik analizinde (Seçenek B) sonucu iptal olan 121 kural bulundu; Weka Apriori aynı eşiklerde aynı 121 kuralı aynı sayımlarla verdi. Veri küpünde City Hotel'in yüksek iptal oranının büyük kısmı acente (TA/TO) kanalından geliyor; 9 yıl × kanal alt grubunun 2'sinde otel farkının yönü tersine dönüyor.

### Proje 2 (final)
- **Proje 1'den düzeltilenler:** [Proje 2 tesliminde doldurulacak]
- **Bölüm bulguları:** [Proje 2 tesliminde doldurulacak]
- **Sınırlılıklar:** [Proje 2 tesliminde doldurulacak]

## Katkı beyanı

| Üye | Çalıştığı alt başlıklar ve işler | Sunumda anlattığı alt başlık |
|---|---|---|
| Melike Duygu YILDIRIM | [ | [ ] |
| Vildan ÇAP | [ ] | [ ] |
| Melisa LOTFIAZAR | [ ] | [ ] |
| WAIL ABDULRAQEB MOHAMMED NOMAN | [ ] | [ ] |

## Yapay zekâ beyanı

Projede ChatGPT (OpenAI) ve Claude (Anthropic) kullanıldı: kod taslaklarını hazırlamak ve düzenlemek, defteri hatalara karşı gözden geçirmek, yöntemleri yönergeyle karşılaştırmak, açıklamaları daha anlaşılır yazmak ve sunuma hazırlanmak için. Yöntem kararları (tahmin anı, sızıntı riskli sütunlar, ölçüt, model seçim kuralı) grubumuza aittir; defter tarafımızdan çalıştırıldı ve Weka sonuçları tarafımızdan üretildi.

## Kaynaklar

- Antonio, N., de Almeida, A. ve Nunes, L. (2019). Hotel booking demand datasets. *Data in Brief*, 22, 41–49. https://doi.org/10.1016/j.dib.2018.11.126
- TidyTuesday (2020-02-11). Hotels veri dosyası. https://github.com/rfordatascience/tidytuesday/tree/main/data/2020/2020-02-11
- Kaufman, S., Rosset, S., Perlich, C. ve Stitelman, O. (2012). Leakage in data mining: Formulation, detection, and avoidance. *ACM Transactions on Knowledge Discovery from Data*, 6(4), Article 15. https://doi.org/10.1145/2382577.2382579
- Dietterich, T. G. (1998). Approximate statistical tests for comparing supervised classification learning algorithms. *Neural Computation*, 10(7), 1895–1923. https://doi.org/10.1162/089976698300017197
- Wu, T., Chen, Y. ve Han, J. (2010). Re-examination of interestingness measures in pattern mining: A unified framework. *Data Mining and Knowledge Discovery*, 21(3), 371–397. https://doi.org/10.1007/s10618-009-0161-2
- Han, J., Kamber, M. ve Pei, J. (2012). *Data Mining: Concepts and Techniques* (3. baskı). Morgan Kaufmann.
- Pedregosa, F. vd. (2011). Scikit-learn: Machine learning in Python. *Journal of Machine Learning Research*, 12, 2825–2830.
- Raschka, S. (2018). MLxtend. *Journal of Open Source Software*, 3(24), 638. https://doi.org/10.21105/joss.00638
- Frank, E., Hall, M. A. ve Witten, I. H. (2016). *The WEKA Workbench*. Online Appendix for "Data Mining: Practical Machine Learning Tools and Techniques" (4. baskı). Morgan Kaufmann.
