# 📊 Global Satış & Lojistik Operasyonları Performans Analizi (Power BI)

![Dashboard Ekran Görüntüsü](Ekran%20görüntüsü%202026-06-30%20172007.png)

## 🎯 Projenin Amacı ve İş Problemi
Bu proje, dinamik ve ölçeklenebilir bir iş zekası (BI) mimarisi kurgulayarak bir şirketin global satış operasyonlarını, kârlılık sızıntılarını ve tedarik zinciri/lojistik performansını uçtan uca analiz etmek amacıyla geliştirilmiştir. 

Rapor, ham verilerin temizlenmesinden veri modellemeye, gelişmiş DAX hesaplamalarından minimalist UI/UX tasarım ilkelerine (Numerro felsefesi) kadar tüm aşamaları barındıran uçtan uca bir **Executive Dashboard (Yönetici Paneli)** örneğidir.

---

## 🛠️ Teknik Altyapı ve Veri Mühendisliği

### 1. Veri Modelleme (Star Schema)
* Projede performans ve optimizasyon odaklı, analitik sorgulara en hızlı tepkiyi veren **Yıldız Şeması (Star Schema)** mimarisi kurgulanmıştır.
* `Fact_Sales` ana satış tablosu; `Dim_Product`, `Dim_Customer`, `Dim_Geography` ve zaman analitiği için sıfırdan türetilen `Dim_Date` takvim tabloları ile **1-to-Many (Bire Çok)** ilişkiler üzerinden birbirine bağlanmıştır.

### 2. Gelişmiş DAX Katmanı & Zaman Zekası (Time Intelligence)
Zaman serisi analizlerinin tıkır tıkır çalışması için yazılan bazı kritik DAX (Data Analysis Expressions) ölçüleri:
* **Benzersiz Sipariş Takibi:** Satır bazlı tekrarları engellemek ve gerçek paket hacmini bulmak adına tekil sayım yapılmıştır:
  ```dax
  Total Orders = DISTINCTCOUNT(Fact_Sales[Order ID])
