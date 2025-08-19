# create_jwt.py README

Bu script, MindSphere cihaz entegrasyonlarında kullanılmak üzere, X.509 sertifikalarıyla imzalanmış JWT token oluşturur.

## Kullanım

Script’i çalıştırmak için aşağıdaki yapıyı takip edin:

python create_jwt.py <device_name> <tenant_name>

**Parametreler:**
- `<device_name>` : Cihaz adınızı belirtin. (Aynı isimde `.pem` ve `.key` dosyası olmalı)
- `<tenant_name>` : Tenant adınızı belirtin. (Aynı isimde `.pem` dosyası olmalı)

## Gerekli Dosyalar

Script’in düzgün çalışması için dizinde aşağıdaki dosyaların bulunması gerekir:
- `<device_name>.pem` : Cihaza ait X.509 sertifikası (PEM formatında)
- `<tenant_name>.pem` : Tenant’a ait X.509 sertifikası (PEM formatında)
- `<device_name>.key` : Cihaza ait özel anahtar dosyası (PEM formatında)

## Script’in Yaptıkları

1. Komut satırından cihaz ve tenant ismini alır.
2. İlgili sertifika dosyalarını okuyarak base64 olarak JWT `x5c` header’ına ekler.
3. JWT payload’unu hazırlar (jti, iss, sub, aud, iat, exp, schemas, ten gibi alanlar içerir).
4. Özel anahtarı kullanarak JWT’yi RS256 algoritmasıyla imzalar.
5. İmzalanmış JWT’yi ekrana basar.

## Bağımlılıklar

Aşağıdaki Python paketlerinin kurulu olması gerekir:
- `PyJWT`
- `cryptography`

Kurulum için:
```bash
pip install pyjwt cryptography

Örnek Çalıştırma

python create_jwt.py myDevice myTenant

Başarılı çalışmada çıktınız JWT token olacaktır.
Notlar

    Sertifika dosyalarınızın başlangıç ve bitiş satırları (-----BEGIN CERTIFICATE----- / -----END CERTIFICATE-----) kaldırılır, yalnızca base64 verisi kullanılır.
    Token’in geçerlilik süresi 1 saattir (exp).
    Gizli anahtar dosyanız şifresiz olmalı veya şifre alanını uyarlamalısınız.
