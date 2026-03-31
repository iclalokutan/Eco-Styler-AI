# Eco-Styler AI - Urun Gereksinim Dokumani (PRD)

## 1) Urun Vizyonu

Kullanicilarin gardiroplarindaki parcalari daha verimli kullanmasini saglayarak "giyecek bir seyim yok" stresini azaltmak ve gereksiz hizli moda tuketimini dusurmek.

Eco-Styler AI, her kullanicinin cebindeki kisisel stil danismani ve surdurulebilirlik asistani olarak konumlanir.

## 2) Hedef Kitle

- **Universite ogrencileri:** Kisıtlı butceyle eldeki kiyafetlerden maksimum kombin uretmek isteyenler.
- **Surdurulebilir yasam destekcileri:** Az parcayla cok secenek (capsule wardrobe) yaratmak isteyen kullanicilar.
- **Zamani kisitli profesyoneller:** Sabah karar yorgunlugu yasamadan hizli hazirlanmak isteyenler.

## 3) MVP Ozellikleri

### A. Dijital Gardirop Yonetimi

- **Fotograf analizi (AI):** Kullanici kiyafet fotografi yuklediginde sistem turu (tisort, pantolon vb.), rengi ve kategoriyi (ust/alt/dis giyim) otomatik belirler.
- **Envanter listesi:** Tum kiyafetler dijital gardiropta listelenir ve aranabilir olur.

### B. Akilli Kombin Algoritmasi

- **Hava durumu entegrasyonu:** Konuma gore anlik sicaklik ve yagis bilgisi alinir.
- **Mod (mood) secimi:** Kullanici "Resmi", "Rahat", "Enerjik" gibi seceneklerden birini secer.
- **Kombin onerici:** Hava durumu + mood + renk uyumu kurallarini birlestirerek oneriler sunar.

### C. Unutulanlari Canlandir (Sustainability Feature)

- **Takip:** Her kiyafet icin `last_worn_date` bilgisi tutulur.
- **Onceliklendirme:** 30 gunden uzun suredir giyilmeyen parcalar kombin onerilerinde ust siralara cikarilir.
- **Bildirim:** Kullaniciya "Bu parcayi degerlendirmek ister misin?" onerisi gosterilir.

## 4) Teknik Mimari (Tech Stack)

| Katman | Teknoloji | Gorev |
|---|---|---|
| Frontend | Streamlit (Python tabanli) | Kullanici arayuzu ve web sayfasi |
| Backend | Python (FastAPI / Flask) | Uygulama mantigi ve API yonetimi |
| Yapay Zeka | OpenCV & Hugging Face | Goruntu isleme ve siniflandirma |
| Veritabani | SQLite | Kiyafet ve kullanim verilerini saklama |
| Dis Servis | OpenWeather API | Anlik hava durumu verisi cekme |

## 5) UX Akisi

1. **Yukleme:** Kullanici yeni veya mevcut bir kiyafeti fotograflar.
2. **Onay:** AI etiketleri onerir (ornek: "Mavi Kazak"), kullanici duzenler/onaylar.
3. **Talep:** Ana ekranda "Bugun ne giyeyim?" butonuna basilir, mood secilir.
4. **Secim:** AI tarafindan sunulan 3 kombin arasindan biri secilir ve "Bunu Giydim" denir.
5. **Guncelleme:** Secilen parcalarin `last_worn_date` alani guncellenir.

## 6) Basari Kriterleri (KPI)

- Kullanicinin sabah kombin secme suresi 1 dakikanin altina iner.
- Gardiroptaki parcalarin ortalama kullanim sikligi en az %20 artar.
- Kullanicinin yeni kiyafet alma ihtiyaci olculebilir bicimde ertelenir.

## 7) MVP Disi Fikirler (Gelecek Asama)

- Takvim entegrasyonu (etkinlik turune gore kombin onerisi)
- Kiyafetler arasi otomatik kapsul gardirop analizi
- Karbon ayak izi tahmini ve surdurulebilirlik skoru
