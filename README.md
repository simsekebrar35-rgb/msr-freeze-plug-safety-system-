# ⚛️ Ergimiş Tuz Reaktörlerinde Freeze Plug Pasif Güvenlik Mekanizması İçin Sensör Tabanlı İzleme ve Karar Destek Sistemi

[![TEKNOFEST 2026](https://img.shields.io/badge/TEKNOFEST-2026-blue.svg)](https://teknofest.org)
[![Kategori](https://img.shields.io/badge/Kategori-Pasif%20G%C3%BCvenlik%20Sistemi%20Tasar%C4%B1m%C4%B1-orange.svg)](#)
[![Takım](https://img.shields.io/badge/Tak%C4%B1m-ALTIORA-green.svg)](#)
[![Durum](https://img.shields.io/badge/FDR-Tamamland%C4%B1%20(Temmuz%202026)-success.svg)](#)

Bu depo, **TEKNOFEST 2026 Nükleer Enerji Teknolojileri Tasarım Yarışması (Alt Kategoriler Sistem Geliştirme)** kapsamında **ALTIORA** takımı tarafından geliştirilen; ergimiş tuz reaktörlerinde (MSR) kullanılan Freeze Plug pasif güvenlik mekanizmasının gerçek zamanlı izlenmesine yönelik sensör füzyonu, veri doğrulama ve Açıklanabilir Yapay Zekâ (XAI) tabanlı karar destek mimarisini içermektedir.

---

## 📌 Proje Özeti

Ergimiş tuz reaktörlerinde (MSR) kullanılan Freeze Plug, acil durumlarda harici güç kaynağına ihtiyaç duymadan eriyerek yakıt tuzunun Drain Tank'a tahliyesini sağlayan kritik bir pasif güvenlik elemanıdır.

**ALTIORA projesinin temel amacı:**
Mevcut pasif güvenlik mekanizmasının doğal fiziksel işleyişine ve reaktör kontrol sistemine **hiçbir aktif müdahalede bulunmadan**, Freeze Plug bölgesindeki termal-hidrolik süreçleri çoklu sensör füzyonu ile izlemek, ölçüm tutarlılığını doğrulamak ve olası anormallikleri operatöre **Açıklanabilir Yapay Zekâ (XAI)** destekli erken uyarılarla sunmaktır.

* **Referans Reaktör:** Oak Ridge National Laboratory (ORNL) - Molten Salt Reactor Experiment (MSRE, 8 MWth)
* **Temel Felsefe:** IAEA *Defence in Depth* (Derinlemesine Savunma) prensipleriyle tam uyumlu bağımsız dijital izleme katmanı.

---

## ⏱️ Proje İş-Zaman Takvimi (Bahar - Yaz 2026)

Proje faaliyetleri, yarışma takvimi doğrultusunda 8 iş paketi (WP) halinde yürütülmüştür:

| Dönem / Tarih | Aşama / İş Paketi | Kapsam ve Faaliyetler |
| :--- | :--- | :--- |
| **Nisan 2026** | **WP-1, WP-2, WP-3** | Takım organizasyonu, IAEA/ORNL standartları literatür taraması ve MSRE referans sistem gereksinimleri analizi. |
| **Mayıs 2026** | **WP-7 (ÖDR Aşaması)** | **Ön Değerlendirme Raporu (ÖDR)** başarıyla tamamlandı ve onaylandı. Pasif Güvenlik Sistemi Tasarımı alt kategorisine geçiş sağlandı. |
| **Mayıs – Haziran 2026** | **WP-4 & WP-5** | Sensör seçimi, SolidWorks kavramsal mekanik modeli, DAQ altyapısı, Modbus TCP/IP ve OPC UA haberleşme mimarisi tasarımı. |
| **Haziran – Temmuz 2026**| **WP-6** | Python ile sentetik veri setleri üzerinden sıcaklık, basınç ve debi analizleri; alarm eşiklerinin belirlenmesi, SHAP & LIME açıklanabilirlik modelleri ve FMEA risk analizleri. |
| **17 Temmuz 2026** | **WP-8 (FDR Teslimi)** | Kapsamlı mühendislik hesaplamaları, blok diyagramlar ve sistem mimarisini içeren **Final Değerlendirme Raporu (FDR)** jüriye resmi olarak teslim edildi. |

---

## 🏗️ Fonksiyonel Sistem Mimarisi

Sistem, sahadaki fiziksel ölçümden operatör arayüzüne kadar modüler bir katman yapısıyla tasarlanmıştır:

```text
[Primer Çevrim / Freeze Plug Bölgesi]
        │
        ├── Tip N Termokupl (Sıcaklık: ~650°C, Eşik: 660°C)
        ├── Rosemount 3051S Remote Seal (Basınç: 0.30 MPa)
        └── Venturi Debimetre (Kütlesel Debi: ~170 kg/s, ISO 5167-4)
        │
        ▼
[Sinyal Koşullandırma & Merkezi DAQ]
        │ (Zaman Damgalı Veri Kaydı)
        ▼
[Veri Doğrulama Katmanı]
        │ ├── Fiziksel Limit Kontrolü
        │ ├── Zaman Sürekliliği Kontrolü
        │ └── Sensörler Arası Çapraz Tutarlılık
        ▼
[Endüstriyel Haberleşme (Modbus TCP/IP & OPC UA)]
        ▼
[Merkezi İşleme: Çoklu Sensör Füzyonu & XAI Karar Destek]
        │ (SHAP & LIME Özellik Katkı Analizi)
        ▼
[Operatör Arayüzü (HMI)] ── Açıklanabilir Alarm & Durumsal Farkındalık

```
---

## 🔬 Teknik Özellikler ve Enstrümantasyon 
* **Sıcaklık Ölçümü:** 2 adet yedekli, mineral yalıtımlı (MI) Tip N (Nicrosil-Nisil) termokupl (IEC 60584-1 Class 1, ±1.5°C). Yüksek sıcaklık kararlılığı ve düşük drift oranı.
* **Basınç Ölçümü:** Emerson Rosemount 3051S Remote Seal diyafram tipi diferansiyel/gösterge basınç transmitteri (±%0.025 Span doğruluğu, 100 ms tepki süresi).
* **Debi Ölçümü:** Venturi Tipi Diferansiyel Basınç Debimetresi (ISO 5167-4 standardı, ±%0.5 doğruluk, düşük kalıcı basınç kaybı, hareketli parçasız yapı).
* **Yapısal Malzeme Uyumu:** Yüksek sıcaklık ve erimiş florür tuzu korozyon dayanımı için Hastelloy-N alaşımı referans alınmıştır.
* **Güvenilirlik & Risk Yönetimi**: Fail-safe yaklaşımıyla gerçekleştirilen ön FMEA (Hata Türleri ve Etkileri Analizi) kapsamında tüm hata modlarında RPN değerleri 12–18 bandında (Düşük Risk) tutulmuştur.

  
🧠 Karar Destek ve Açıklanabilir Yapay Zekâ (XAI) Klasik izleme sistemleri yalnızca eşik aşımında ikili (0/1) alarm üretirken, ALTIORA karar destek mekanizması:  * **Sensör Füzyonu:** Sıcaklık, basınç ve debi verilerini korelasyonlu biçimde değerlendirerek tekil sensör sapmalarından kaynaklı asılsız alarmları engeller.
* **XAI Açıklanabilirliği:** Olası bir anormallikte SHAP ve LIME metodolojileriyle operatöre alarmın hangi parametreden kaynaklandığını şeffaf olarak raporlar (Örn: "Artan sıcaklık eğilimi ve primer debi azalması nedeniyle Freeze Plug durumu incelenmelidir").
* **👥 Takım:** ALTIORA Proje, disiplinlerarası sistem mühendisliği yaklaşımıyla yürütülmüştür:
* **Bilgisayar Mühendisliği:** Karar destek yazılım mimarisi, sensör veri ön işleme/doğrulama algoritmaları, XAI (SHAP/LIME) açıklanabilirlik yöntemlerinin analizi.
* **Elektrik-Elektronik Mühendisliği:** Sensör seçimi, DAQ mimarisi, sinyal koşullandırma ve endüstriyel haberleşme altyapısı (Modbus/OPC UA).
* **Uzay ve Havacılık Mühendisliği:** MSRE referans sistem analizi, termal-hidrolik değerlendirmeler, SolidWorks kavramsal mekanik tasarımı.
* **Not:** Bu proje TEKNOFEST 2026 Nükleer Enerji Teknolojileri Tasarım Yarışması kapsamında kavramsal bir Ar-Ge ve detaylı sistem mühendisliği tasarımı olarak tamamlanmış ve 17 Temmuz 2026'da FDR teslimi gerçekleştirilmiştir.   
