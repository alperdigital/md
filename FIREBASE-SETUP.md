# Firebase Kurulum Rehberi

Bu rehber, admin panelinden yapılan değişikliklerin **tüm kullanıcılar tarafından anında görülmesi** için Firebase Realtime Database kurulumunu açıklar.

## 🎯 Neden Firebase?

- ✅ **GitHub token gerektirmez** - Daha basit kurulum
- ✅ **Anında yayınlama** - Değişiklikler 1-2 saniye içinde tüm kullanıcılara ulaşır
- ✅ **Ücretsiz plan** - Küçük-orta ölçekli siteler için yeterli
- ✅ **Gerçek zamanlı** - Veriler anında senkronize olur

## 📋 Adım 1: Firebase Projesi Oluşturma

1. [Firebase Console](https://console.firebase.google.com/) adresine gidin
2. "Add project" (Proje Ekle) butonuna tıklayın
3. Proje adını girin (örn: `simdi-onlar-manset`)
4. Google Analytics'i isteğe bağlı olarak etkinleştirin
5. "Create project" (Proje Oluştur) butonuna tıklayın

## 📋 Adım 2: Realtime Database Oluşturma

1. Firebase Console'da sol menüden **"Realtime Database"** seçin
2. **"Create Database"** butonuna tıklayın
3. **"Start in test mode"** seçeneğini seçin (güvenlik kurallarını sonra ayarlayacağız)
4. Bölge seçin (örn: `europe-west1` - Türkiye'ye yakın)
5. **"Enable"** butonuna tıklayın

## 📋 Adım 3: Güvenlik Kurallarını Ayarlama

1. Realtime Database sayfasında **"Rules"** sekmesine gidin
2. Aşağıdaki kuralları yapıştırın:

```json
{
  "rules": {
    "haberler": {
      ".read": true,
      ".write": false
    },
    "kararlar": {
      ".read": true,
      ".write": false
    }
  }
}
```

3. **"Publish"** butonuna tıklayın

> ⚠️ **Not:** Bu kurallar herkesin okuyabileceği, ancak sadece admin panelinden (Firebase Admin SDK ile) yazılabileceği anlamına gelir. Admin paneli için özel bir yazma yöntemi kullanacağız.

## 📋 Adım 4: Web App Oluşturma

1. Firebase Console'da sol menüden **⚙️ Project Settings** (Proje Ayarları) seçin
2. Aşağı kaydırın ve **"Your apps"** bölümünde **</>** (Web) ikonuna tıklayın
3. App nickname girin (örn: `Web App`)
4. **"Register app"** butonuna tıklayın
5. **Firebase SDK snippet** bölümünden **"Config"** seçeneğini seçin
6. Aşağıdaki gibi bir config göreceksiniz:

```javascript
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project-default-rtdb.firebaseio.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

## 📋 Adım 5: Firebase Config Dosyasını Güncelleme

1. Projenizdeki `firebase-config.js` dosyasını açın
2. Firebase Console'dan aldığınız config bilgilerini yapıştırın:

```javascript
const FIREBASE_CONFIG = {
    apiKey: "AIza...",  // Firebase'den aldığınız
    authDomain: "your-project.firebaseapp.com",
    databaseURL: "https://your-project-default-rtdb.firebaseio.com",
    projectId: "your-project",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123"
};

// Firebase'i aktif et
const USE_FIREBASE = true;  // false'dan true'ya değiştirin
```

3. Dosyayı kaydedin

## 📋 Adım 6: Realtime Database Yazma İzni

Admin panelinden yazma yapabilmek için Firebase Authentication veya özel bir yöntem kullanmamız gerekiyor. En basit yöntem:

### Yöntem 1: Anonymous Authentication (Önerilen)

1. Firebase Console > **Authentication** > **Sign-in method**
2. **Anonymous** seçeneğini etkinleştirin
3. `admin.html` dosyasına anonymous auth ekleyin (otomatik eklenecek)

### Yöntem 2: Database Rules'ı Geçici Olarak Açma (Sadece Test İçin)

⚠️ **Dikkat:** Bu yöntem sadece test için kullanılmalıdır. Production'da kullanmayın!

1. Realtime Database > **Rules** sekmesine gidin
2. Geçici olarak yazma izni verin:

```json
{
  "rules": {
    "haberler": {
      ".read": true,
      ".write": true
    },
    "kararlar": {
      ".read": true,
      ".write": true
    }
  }
}
```

3. **"Publish"** butonuna tıklayın

> ⚠️ **Önemli:** Bu kurallar herkesin yazabilmesine izin verir. Sadece test için kullanın ve sonra daha güvenli kurallara geçin.

## 📋 Adım 7: Test Etme

1. Admin panelini açın (`/admin.html`)
2. **MANŞET** veya **KARARLAR** sayfasına gidin
3. Yeni bir haber veya karar ekleyin
4. Kaydet butonuna tıklayın
5. Başarı mesajında **"🔥 Firebase'e kaydedildi"** yazısını görmelisiniz
6. Başka bir tarayıcıda veya gizli modda siteyi açın
7. MANŞET veya KARARLAR sayfasında yeni eklediğiniz içeriği görmelisiniz

## 🔒 Güvenlik Notları

1. **API Key Güvenliği:** Firebase API key'leri public olabilir, ancak güvenlik kuralları ile korunur
2. **Database Rules:** Mutlaka uygun güvenlik kuralları ayarlayın
3. **Rate Limiting:** Firebase ücretsiz planında günlük okuma/yazma limitleri vardır
4. **Authentication:** Production'da mutlaka authentication kullanın

## 🆘 Sorun Giderme

### Firebase'e yazılamıyor
- Database Rules'ı kontrol edin
- Anonymous Authentication'ın açık olduğundan emin olun
- Browser console'da hata mesajlarını kontrol edin

### Veriler görünmüyor
- `USE_FIREBASE = true` olduğundan emin olun
- Firebase config bilgilerinin doğru olduğunu kontrol edin
- Browser console'da Firebase bağlantısını kontrol edin

### "Permission denied" hatası
- Database Rules'da yazma izni olduğundan emin olun
- Anonymous Authentication'ın aktif olduğunu kontrol edin

## 📚 Daha Fazla Bilgi

- [Firebase Realtime Database Dokümantasyonu](https://firebase.google.com/docs/database)
- [Firebase Güvenlik Kuralları](https://firebase.google.com/docs/database/security)
- [Firebase Ücretsiz Plan Limitleri](https://firebase.google.com/pricing)

## ✅ Kurulum Tamamlandı!

Artık admin panelinden yaptığınız değişiklikler **tüm kullanıcılar tarafından anında görünecek**! 🎉

