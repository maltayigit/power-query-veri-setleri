# TeknoSepet — Power Query Veri Setleri

Kurgusal **TeknoSepet** perakende şirketinin 2025 yılı verileriyle hazırlanmış, Excel / Power BI **Power Query** uygulamaları için veri seti koleksiyonu.

Veri setleri; farklı kaynaklardan veri alma, sorguları birleştirme, kirli veriyi temizleme ve tabloyu yeniden şekillendirme (unpivot / pivot) gibi gerçek hayatta sık karşılaşılan veri hazırlama senaryolarını kapsar. Her senaryo için doğrulanabilir **kontrol rakamları** verilmiştir.

> Tüm kişi, kurum ve rakamlar kurgusaldır; gerçek kişi veya kurum verisi içermez.

## İçerik

| Klasör | Konu | Dosyalar | Öne çıkan beceri |
|---|---|---|---|
| `01_Ilk_Sorgu` | İlk sorgu | `Siparisler_2025.xlsx` (6.004 satır), `Yenileme_Testi_5_Satir.xlsx` | Tablodan sorgu oluşturma, yenileme |
| `02_Veri_Alma` | Veri alma | Excel, CSV (`;`), sekme ayraçlı TXT, Access `.mdb`, SQL Server kurulum betiği | Farklı kaynak türlerine bağlanma |
| `03_Birlestirme` | Birleştirme | 4 çeyrek tablosu, 12 aylık CSV, iade tablosu | Ekleme (append), klasörden birleştirme, birleştirme türleri (merge / anti join) |
| `04_Temizleme` | Temizleme | Kirli CRM dışa aktarımı, ERP rapor dökümü | Başlık/boş satır temizliği, tip dönüşümü, tekilleştirme, metin düzenleme |
| `05_Sekillendirme` | Şekillendirme | Geniş format hedefler, uzun format personel, iki başlıklı bütçe | Unpivot, pivot, çok satırlı başlıkları düzleştirme |

Dosya bazında ayrıntılı açıklama: [`docs/VERI_SETLERI_README.md`](docs/VERI_SETLERI_README.md)

## Veri modeli

Satış verisi yıldız şemaya uygun şekilde tasarlanmıştır:

- **Olgu tablosu:** Siparişler — `SatisID, SiparisNo, Tarih, MusteriID, UrunID, MagazaID, KanalID, Adet, BirimFiyat, IndirimOrani, IadeMi, OdemeTipi`
- **Boyutlar:** Müşteriler (500), Ürünler (48) ve Kategoriler (6), Mağazalar (12), Kanallar, Tedarikçiler
- **Ek tablolar:** İadeler (278), Mağaza × ay hedefleri (144), Bölge bütçesi

`Net tutar = Adet × BirimFiyat × (1 − IndirimOrani)`

## Bilinçli "tuzaklar"

Veri setleri, gerçek projelerdeki sorunları canlandırmak için bilerek hatalı kurgulanmış bölümler içerir:

- Q3 tablosunda `Adet` yerine `Miktar`, Q4'te fazladan `Not` sütunu (sütun adı uyumsuzluğu)
- Aylık CSV klasörüne kopyalandığında klasörden birleştirmeyi bozan yabancı dosya (`Aylik_CSV_Tuzak`)
- Sistemde karşılığı olmayan 15 iade kaydı (sağ karşıt birleşim alıştırması)
- 5 farklı telefon biçimi, metin olarak saklanmış tarih ve tutarlar, hata hücreleri, yinelenen kayıtlar
- Her sayfada tekrar eden başlıklar içeren ERP rapor dökümü

## Kontrol rakamları

| Kontrol | Beklenen değer |
|---|---|
| Net tutar (iadeler dahil) | 126.792.200,85 |
| İadesiz net satış | 121.192.322,30 |
| İadesiz sipariş sayısı | 3.467 |
| İadesiz brüt kâr | 34.050.130,30 |
| Hedef gerçekleşme | yaklaşık %97,4 |
| Temizlenmiş müşteri listesi | 240 müşteri |
| Temizlenmiş ERP dökümü | 360 satır · 777 adet · 7.673.143,20 TL |
| Hedefler (unpivot sonrası) | 144 satır · toplam 124.367.000 |
| Bölge bütçesi (uzun format) | 56 satır · toplam 232.300.000 |

## Kullanım

1. Repoyu indirin (**Code → Download ZIP**) veya klonlayın.
2. Klasörü örneğin `C:\PQ_Egitim\Veri_Setleri\` konumuna kopyalayın.
3. Excel'de **Veri → Veri Al** ya da Power BI Desktop'ta **Veri al** ile ilgili dosyaya bağlanın.
4. SQL Server örneği için `02_Veri_Alma/TeknoSepetDB_SQLServer_Kurulum.sql` dosyasını SSMS'te açıp çalıştırın (SQL Server 2016+ / Express / LocalDB).

## Kullanılan araçlar

Excel · Power Query (M) · Power BI · SQL Server · Microsoft Access
