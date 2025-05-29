# AnamnesisGPT Demo Versiyonu

## Proje Hakkında

AnamnesisGPT, sağlık sektöründe hasta-doktor görüşmelerini optimize etmek ve anamnez sürecini iyileştirmek için geliştirilmiş yapay zeka destekli bir uygulamadır. Bu demo versiyonu, sistemin temel özelliklerini ve kullanım alanlarını göstermektedir.

### Amaç ve Hedefler

- Hasta görüşme sürecini standardize etmek
- Doktorların iş yükünü azaltmak
- Hasta verilerinin daha sistematik toplanmasını sağlamak
- Yapay zeka destekli ön tanı önerileri sunmak
- Hasta takibini kolaylaştırmak

### Temel Özellikler

#### Web Arayüzü
- Modern ve kullanıcı dostu Flask tabanlı arayüz
- Responsive tasarım ile mobil uyumluluk
- Güvenli oturum yönetimi
- Rol tabanlı erişim kontrolü (Doktor, Hasta, Yönetici)

#### Yapay Zeka Entegrasyonu
- Google AI API entegrasyonu
- Doğal dil işleme yetenekleri
- Otomatik anamnez form doldurma
- Semptom analizi ve ön tanı önerileri
- Hasta geçmişine dayalı risk analizi

#### Veri Yönetimi
- SQLite veritabanı ile güvenli veri saklama
- Hasta geçmişi ve takibi
- İstatistiksel analiz ve raporlama
- Veri görselleştirme araçları
- Otomatik yedekleme sistemi

## Teknik Detaylar

### Sistem Gereksinimleri

- Python 3.8 veya üzeri
- 4GB RAM (minimum)
- 1GB disk alanı
- İnternet bağlantısı (Google AI API için)

### Bağımlılıklar

```bash
# Web Framework ve Veritabanı
Flask==2.3.3
Werkzeug==2.3.7
Flask-SQLAlchemy==3.1.1
SQLAlchemy==2.0.23

# Çevresel Değişkenler
python-dotenv==0.19.0

# Yapay Zeka ve Veri İşleme
google-generativeai==0.3.2
numpy>=1.26.0
pandas==2.2.1
matplotlib==3.8.3
```

### Veritabanı Şeması

```sql
-- Örnek Veritabanı Yapısı
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT UNIQUE NOT NULL,
    role TEXT NOT NULL
);

CREATE TABLE medical_records (
    id INTEGER PRIMARY KEY,
    patient_id INTEGER,
    doctor_id INTEGER,
    timestamp DATETIME,
    diagnosis TEXT,
    FOREIGN KEY (patient_id) REFERENCES users(id),
    FOREIGN KEY (doctor_id) REFERENCES users(id)
);
```

## Kurulum Kılavuzu

### 1. Sistem Hazırlığı

```bash
# Gerekli sistem paketlerinin kurulumu (Ubuntu/Debian)
sudo apt-get update
sudo apt-get install python3-pip python3-venv git
```

### 2. Proje Kurulumu

```bash
# Projeyi klonlama
git clone https://github.com/kullaniciadi/AnamnesisGPT-Demo-Version.git
cd AnamnesisGPT-Demo-Version

# Sanal ortam oluşturma ve aktifleştirme
python3 -m venv venv
source venv/bin/activate  # Unix/macOS
# veya
.\venv\Scripts\activate  # Windows

# Bağımlılıkların kurulumu
pip install -r requirements.txt
```

### 3. Çevresel Değişkenler

`.env` dosyası oluşturun ve aşağıdaki değişkenleri ekleyin:

```env
FLASK_APP=app.py
FLASK_ENV=development
DATABASE_URL=sqlite:///database.db
GOOGLE_AI_API_KEY=your_api_key_here
SECRET_KEY=your_secret_key_here
```

### 4. Veritabanı Kurulumu

```bash
# Python shell'i açın
python

# Veritabanını oluşturun
from app import db
db.create_all()
exit()
```

## Kullanım Kılavuzu

### Uygulamayı Başlatma

```bash
# Geliştirme sunucusu
python app.py

# Prodüksiyon sunucusu (Gunicorn ile)
gunicorn --bind 0.0.0.0:5000 app:app
```

### API Endpointleri

| Endpoint | Metod | Açıklama |
|----------|--------|-----------|
| /api/login | POST | Kullanıcı girişi |
| /api/patients | GET | Hasta listesi |
| /api/anamnesis | POST | Yeni anamnez kaydı |
| /api/reports | GET | Raporlar |

### Örnek Veriler

Proje `ornek_veriler.csv` dosyası içerisinde test amaçlı örnek veriler içermektedir. Bu veriler:
- Hasta demografik bilgileri
- Örnek anamnez kayıtları
- Test senaryoları
- Performans metrikleri

## Hata Ayıklama ve Sorun Giderme

### Bilinen Sorunlar

1. SQLite eşzamanlılık sınırlamaları
2. Google AI API gecikmesi
3. Büyük veri setlerinde performans sorunları

### Çözüm Önerileri

- SQLite yerine PostgreSQL kullanımı
- API önbellekleme
- Sayfalama implementasyonu

## Geliştirme Kılavuzu

### Kod Standartları

- PEP 8 stil kılavuzuna uyum
- Docstring kullanımı
- Tip belirteçleri (Type hints)
- Unit test coverage minimum %80

### Branching Stratejisi

- main: Kararlı sürüm
- develop: Geliştirme
- feature/*: Yeni özellikler
- bugfix/*: Hata düzeltmeleri

## Test Süreçleri

### Unit Testler

```bash
# Test çalıştırma
python -m pytest tests/

# Coverage raporu
pytest --cov=app tests/
```

### Entegrasyon Testleri

```bash
# Entegrasyon testlerini çalıştırma
python -m pytest tests/integration/
```

## Güvenlik

- SQL Injection koruması
- XSS koruması
- CSRF token implementasyonu
- Rate limiting
- Input validasyonu

## Lisans

Bu proje MIT Lisansı altında lisanslanmıştır. Detaylı bilgi için [LICENSE](LICENSE) dosyasını inceleyiniz.

## İletişim ve Destek

- Hata raporları için: Issues sayfası
- Özellik önerileri için: Pull Requests
- Genel sorular için: Discussions

## Katkıda Bulunma

1. Fork yapın
2. Feature branch oluşturun (`git checkout -b feature/YeniOzellik`)
3. Değişikliklerinizi commit edin (`git commit -am 'Yeni özellik: XYZ eklendi'`)
4. Branch'inizi push edin (`git push origin feature/YeniOzellik`)
5. Pull Request oluşturun

### Pull Request Kontrol Listesi

- [ ] Kod standartlarına uygunluk
- [ ] Test coverage
- [ ] Dokümantasyon güncellemesi
- [ ] Changelog güncellemesi

## Sürüm Geçmişi

### v0.1.0 (Demo)
- İlk demo sürümü
- Temel özellikler
- Flask web arayüzü
- Google AI entegrasyonu 