# Eco-Styler AI - Gelistirme Gorev Listesi

Bu liste `PRD.md` baz alinarak MVP'yi adim adim gelistirmek icin hazirlandi.

## 0) Proje Kurulumu ve Iskelet

- [ ] Python sanal ortamini olustur (`venv`) ve aktif et
- [ ] Temel bagimliliklari ekle: `streamlit`, `fastapi` (veya `flask`), `uvicorn`, `opencv-python`, `transformers`, `torch`, `sqlite3` (builtin), `requests`, `python-dotenv`
- [ ] Klasor yapisini olustur:
  - `app/frontend/` (Streamlit)
  - `app/backend/` (API ve is mantigi)
  - `app/ai/` (goruntu analizi)
  - `app/db/` (veritabani ve sorgular)
  - `data/` (lokal sqlite dosyasi)
- [ ] `.env.example` olustur (`OPENWEATHER_API_KEY`, `DEFAULT_CITY`)
- [ ] Baslangic README yaz (kurulum + calistirma adimlari)

## 1) Veritabani Tasarimi (SQLite)

- [ ] SQLite baglantisi ve migration/initialization scripti yaz
- [ ] `items` tablosunu olustur:
  - `id`, `name`, `type`, `category`, `color`, `image_path`, `created_at`, `last_worn_date`
- [ ] `outfits` tablosunu olustur:
  - `id`, `mood`, `weather_summary`, `created_at`
- [ ] `outfit_items` iliski tablosunu olustur:
  - `outfit_id`, `item_id`
- [ ] Temel CRUD fonksiyonlarini yaz (ekle, listele, guncelle, sil)
- [ ] Test verisi (seed) ekleme scripti hazirla

## 2) Backend API (FastAPI/Flask)

- [ ] API uygulama giris dosyasini olustur
- [ ] Endpoint: `POST /items` (kiyafet ekleme)
- [ ] Endpoint: `GET /items` (envanter listeleme)
- [ ] Endpoint: `POST /analyze-image` (AI etiketleme)
- [ ] Endpoint: `POST /outfit/suggest` (kombin onerisi uretme)
- [ ] Endpoint: `POST /outfit/worn` ("Bunu Giydim" ile `last_worn_date` guncelleme)
- [ ] Endpoint: `GET /items/forgotten` (30+ gun giyilmeyenler)
- [ ] Temel hata yonetimi ve dogrulama (eksik alan, gecersiz dosya vb.)

## 3) AI Fotograf Analizi (OpenCV + Hugging Face)

- [ ] Gorsel yukleme ve dosya kaydetme akisini yaz
- [ ] OpenCV ile temel on-isleme (boyutlandirma, normalize)
- [ ] HF modeli ile kiyafet turu tahmini (tisort, pantolon, dis giyim vb.)
- [ ] Renk cikarimi (baskin renk tespiti) fonksiyonu yaz
- [ ] Kategori esleme kurallari yaz (`ust`, `alt`, `dis`)
- [ ] Cikti formatini standardize et:
  - `type`, `category`, `color`, `confidence`
- [ ] Dusuk confidence durumunda kullanici onayi zorunlu akisi ekle

## 4) Hava Durumu Entegrasyonu (OpenWeather)

- [ ] OpenWeather servis istemcisini yaz
- [ ] Sehir/konuma gore anlik sicaklik + yagis verisi cek
- [ ] API hata ve timeout durumlarini ele al
- [ ] Hava durumunu kombin kurallarinda kullanilacak sade formata donustur:
  - `cold/mild/hot`, `rain/no-rain`
- [ ] Son hava verisi icin kisa sureli cache ekle (opsiyonel ama onerilir)

## 5) Kombin Oneri Motoru (MVP Kural Bazli)

- [ ] Mood seceneklerini tanimla: `Resmi`, `Rahat`, `Enerjik`
- [ ] Renk uyumu kurallarini tanimla (uyumlu/kontrast basit kurallar)
- [ ] Hava durumuna gore parca filtreleme kurallari yaz
- [ ] `last_worn_date` bazli oncelik skoru ekle (30+ gun giyilmeyenlere boost)
- [ ] Envanterden 3 farkli kombin ureten fonksiyon yaz
- [ ] Oneri sonucuna aciklama metni ekle ("Yagis ihtimali nedeniyle dis giyim eklendi" vb.)

## 6) Streamlit Arayuzu (UX Akisina Gore)

- [ ] Sayfa 1: Kiyafet yukleme (fotograf yukle + AI etiketlerini goster)
- [ ] Sayfa 2: Etiket onay/duzenleme ve kaydetme
- [ ] Sayfa 3: Dijital gardirop listesi (filtre + arama)
- [ ] Sayfa 4: "Bugun ne giyeyim?" (mood secimi + kombin getir)
- [ ] Sayfa 5: 3 kombin karti gosterimi
- [ ] "Bunu Giydim" butonu ile secilen kombin kaydi ve tarih guncelleme
- [ ] "Unutulanlari Canlandir" alani (30+ gun giyilmeyen parcalar)

## 7) Surdurulebilirlik Ozelligi Detaylari

- [ ] Gunluk kontrol job/fonksiyonu yaz (30+ gun giyilmeyenleri bul)
- [ ] Uygulama icinde bildirim/banner metni goster
- [ ] O parcalari kombin onerilerinde ust siraya tasima dogrulamasi yap
- [ ] Kullanici etkileşimi takibi ekle:
  - "Oneriyi degerlendirdi mi?"
  - "Gercekten giydi mi?"

## 8) Test ve Kalite

- [ ] Unit testler:
  - renk tespiti
  - kategori esleme
  - kombin puanlama
- [ ] API testleri:
  - `POST /items`
  - `POST /outfit/suggest`
  - `POST /outfit/worn`
- [ ] UI smoke test:
  - yukleme -> onay -> oneriler -> "Bunu Giydim" akisi
- [ ] Hata senaryolari testleri (bos gorsel, API key yok, hava servisi kapali)
- [ ] Kod kalitesi: `ruff/flake8` ve `black` ile format/lint

## 9) KPI Olcumleme ve Analitik

- [ ] Kombin secim suresi olcumu ekle (hedef: < 1 dakika)
- [ ] Parca kullanim sikligi metriği hesapla (hedef: +%20)
- [ ] "Yeni kiyafet alma ihtiyaci erteleme" icin basit anket/alarm noktasi ekle
- [ ] Haftalik KPI ozeti olustur (ekran veya rapor dosyasi)

## 10) Yayina Hazirlik

- [ ] Lokal calisma komutlarini netlestir:
  - API: `uvicorn ...`
  - UI: `streamlit run ...`
- [ ] `.env` ve gizli bilgiler kontrolu yap
- [ ] Demo veri seti ile MVP demo senaryosu hazirla
- [ ] Kisa demo rehberi yaz (2-3 dakikada urun gostermi)

## Oncelik Sirasi (Oneri)

1. Proje kurulumu -> Veritabani -> Temel API
2. AI etiketleme -> Streamlit yukleme/onay akisi
3. Hava durumu + kombin motoru
4. "Bunu Giydim" ve `last_worn_date` guncelleme
5. "Unutulanlari Canlandir" ve KPI olcumleme
