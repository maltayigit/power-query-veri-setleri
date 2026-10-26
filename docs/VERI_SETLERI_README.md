# Power Query Eğitim Veri Setleri

Bu klasör, 12 saatlik Power Query eğitiminin tüm uygulamalarında kullanılan dosyaları içerir. Klasörü katılımcı bilgisayarlarında `C:\PQ_Egitim\Veri_Setleri\` konumuna kopyalayın.

Tüm veriler kurgusal TeknoSepet perakende senaryosunun 2025 yılına aittir (Power BI eğitimindeki verinin 2025 dilimi). Gerçek kişi veya kurum verisi içermez.

## 01_Ilk_Sorgu (Ders 1)

- `Siparisler_2025.xlsx`: `Siparisler` sayfasında `tblSiparisler` Excel Tablosu. 6.004 satış satırı, 3.518 sipariş, 12 sütun (SatisID, SiparisNo, Tarih, MusteriID, UrunID, MagazaID, KanalID, Adet, BirimFiyat, IndirimOrani, IadeMi, OdemeTipi).
- `Yenileme_Testi_5_Satir.xlsx`: tabloya yapıştırılıp yenilendiğinde satır sayısı 6.009 olur.

## 02_Veri_Alma (Ders 2)

- `Urunler.xlsx`: `tblUrun` (48 ürün), `tblKategori` (6 kategori), veri içermeyen `Notlar` sayfası.
- `Musteriler.csv`: 500 müşteri; ayraç `;`, kodlama UTF-8, tarih biçimi gg.aa.yyyy.
- `Magazalar.txt`: 12 mağaza; sekme ayraçlı.
- `TeknoSepet_Tedarik.mdb`: Access veritabanı. Tablolar: `Kanallar`, `Tedarikciler`, `Marka_Tedarikci`; sorgu: `qry_TedarikciMarkalari`.
- `TeknoSepetDB_SQLServer_Kurulum.sql`: SQL Server'da `TeknoSepetDB` veritabanını oluşturur. `dbo.Siparisler` 6.004 satır, `dbo.vw_AylikSatis` 504 satır. SQL Server LocalDB üzerinde test edilmiştir.
- Web kaynağı (dosya değil): `https://tr.wikipedia.org/wiki/Türkiye'nin_illeri` (81 il tablosu; sayfa içeriği zamanla değişebilir).

## 03_Birlestirme (Ders 3)

- `Ceyrek_Satislari_2025.xlsx`: `tblQ1`–`tblQ4` (1.454 + 1.436 + 1.568 + 1.546 = 6.004 satır). Bilinçli tuzaklar: Q3'te `Adet` yerine `Miktar`, Q4'te fazladan `Not` sütunu.
- `Aylik_CSV/`: 12 aylık CSV (toplam 6.004 satır); `;` ayraç, UTF-8, ondalık virgül.
- `Aylik_CSV_Tuzak/OKU_BENI.txt`: klasöre kopyalandığında birleştirmeyi bozan yabancı dosya demosu.
- `Iadeler_2025.xlsx`: `tblIade` 278 iade kaydı; 15'i sistemde olmayan siparişlere ait (sağ karşıt birleşim alıştırması).

## 04_Temizleme (Ders 4)

- `Musteri_Listesi_Kirli.xlsx`: CRM dışa aktarımı. Başlık satırları, boş satırlar, yinelenen kayıtlar, karışık harf ve boşluklar, 5 farklı telefon biçimi, metin tarihler ve tutarlar, hata hücreleri, birleştirilmiş hücre etkisi (Bölge). Temiz sonuç: 240 müşteri.
- `ERP_Satis_Dokumu_2025Q1.txt`: sayfa başlıkları tekrar eden rapor dökümü. Temiz sonuç: 360 satır, 777 adet, 7.673.143,20 TL.

## 05_Sekillendirme (Ders 5)

- `Hedefler_Genis_2025.xlsx`: 12 mağaza x 12 ay hedef (geniş format). Unpivot sonrası 144 satır; toplam 124.367.000.
- `Personel_Uzun_Format.xlsx`: 30 personel, öznitelik-değer (uzun) format; Pivot alıştırması.
- `Bolge_Butce_Iki_Baslik.xlsx`: iki başlık satırlı bütçe (ileri düzey). Uzun format sonrası 56 satır; toplam 232.300.000.

## Ders 6

Ders 6 yeni dosya kullanmaz; önceki derslerin sorgularını Veri Modeli'ne yükler.

## Kontrol rakamları (özet)

| Kontrol | Değer |
|---|---|
| Net tutar (iadeler dahil) | 126.792.200,85 |
| İadesiz net satış | 121.192.322,30 |
| İadesiz sipariş sayısı | 3.467 |
| İadesiz brüt kâr | 34.050.130,30 |
| Hedef gerçekleşme | yaklaşık %97,4 |

Net tutar = Adet x BirimFiyat x (1 - IndirimOrani).
