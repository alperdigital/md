# Admin Panel Kurulum Rehberi

## 🚀 Anında Yayınlama Özelliği

Admin panelinden yapılan değişiklikler **anında GitHub'a push edilir** ve **1-2 dakika içinde** canlı sitede görünür hale gelir.

## 📋 Kurulum Adımları

### 1. GitHub Personal Access Token Oluşturma

1. GitHub'a giriş yapın: https://github.com
2. Sağ üst köşedeki profil fotoğrafınıza tıklayın
3. **Settings** (Ayarlar) seçeneğine tıklayın
4. Sol menüden **Developer settings** seçeneğine tıklayın
5. **Personal access tokens** > **Tokens (classic)** seçeneğine tıklayın
6. **Generate new token** > **Generate new token (classic)** butonuna tıklayın
7. Token için bir isim verin (örn: "Admin Panel Token")
8. **Expiration** (Süre) seçin (önerilen: 90 gün veya daha uzun)
9. Aşağıdaki **scopes** (izinler) seçin:
   - ✅ `repo` (Full control of private repositories)
     - Bu, tüm repo izinlerini içerir (read, write, workflow hariç)
10. **Generate token** butonuna tıklayın
11. **ÖNEMLİ:** Token'ı kopyalayın ve güvenli bir yere kaydedin (bir daha gösterilmeyecek!)

### 2. Admin Config Dosyasını Güncelleme

1. `admin-config.js` dosyasını açın
2. `githubToken` alanına oluşturduğunuz token'ı yapıştırın:

```javascript
const ADMIN_CONFIG = {
    password: 'admin123', // Şifrenizi değiştirin!
    githubToken: 'ghp_your_token_here', // Token'ınızı buraya yapıştırın
    githubRepo: 'alperdigital/md',
    githubBranch: 'master'
};
```

3. Dosyayı kaydedin

### 3. GitHub Pages Ayarları

GitHub Pages otomatik olarak çalışıyor olmalı. Kontrol etmek için:

1. GitHub repository'nize gidin: https://github.com/alperdigital/md
2. **Settings** sekmesine tıklayın
3. Sol menüden **Pages** seçeneğine tıklayın
4. **Source** bölümünde **Deploy from a branch** seçili olmalı
5. **Branch** olarak **master** seçili olmalı
6. **Save** butonuna tıklayın

## ✅ Test Etme

1. Admin paneline gidin: `http://localhost:8602/admin.html`
2. Şifre ile giriş yapın: `admin123`
3. Herhangi bir sayfayı düzenleyin veya haber/karar ekleyin
4. Kaydet butonuna tıklayın
5. Başarı mesajını görün
6. 1-2 dakika sonra canlı siteyi kontrol edin: https://alperdigital.github.io

## 🔄 Nasıl Çalışıyor?

1. **Admin Panelden Değişiklik:** Kullanıcı admin panelinden içerik ekler/düzenler
2. **GitHub API:** Değişiklikler GitHub API üzerinden doğrudan repository'ye push edilir
3. **Otomatik Build:** GitHub Pages, push'u algılar ve otomatik olarak siteyi yeniden build eder
4. **Canlı Yayın:** 1-2 dakika içinde değişiklikler canlı sitede görünür

## ⚠️ Önemli Notlar

- **Token Güvenliği:** `admin-config.js` dosyasını asla GitHub'a commit etmeyin! (Zaten .gitignore'da olmalı)
- **Build Süresi:** GitHub Pages build işlemi genellikle 1-2 dakika sürer
- **Build Durumu:** Build durumunu kontrol etmek için repository'nin **Actions** sekmesine bakabilirsiniz
- **Hata Durumu:** Eğer build başarısız olursa, GitHub repository'nizde **Settings > Pages** bölümünden hata mesajını görebilirsiniz

## 🛠️ Sorun Giderme

### Token çalışmıyor
- Token'ın `repo` scope'una sahip olduğundan emin olun
- Token'ın süresinin dolmadığından emin olun
- Token'ın doğru kopyalandığından emin olun (boşluk olmamalı)

### Değişiklikler sitede görünmüyor
- GitHub Pages build durumunu kontrol edin (Actions sekmesi)
- Build başarısız olmuşsa hata mesajını okuyun
- Repository'nin public olduğundan emin olun (GitHub Pages ücretsiz plan için)

### Build çok uzun sürüyor
- Normal build süresi 1-2 dakikadır
- İlk build daha uzun sürebilir (5-10 dakika)
- Repository büyükse build süresi artabilir

## 📞 Destek

Sorun yaşarsanız:
1. Browser console'u açın (F12) ve hata mesajlarını kontrol edin
2. GitHub repository'nin Actions sekmesinde build loglarını kontrol edin
3. `admin-config.js` dosyasındaki ayarları tekrar kontrol edin

