# Jekyll GitHub Pages Sitesi

Bu repository, Jekyll kullanılarak oluşturulmuş ve GitHub Pages üzerinde barındırılan bir web sitesidir.

## Özellikler

- ✅ Modern ve temiz tasarım
- ✅ Mobil uyumlu
- ✅ Hızlı yükleme
- ✅ SEO dostu
- ✅ GitHub Pages entegrasyonu
- ✅ Türkçe dil desteği

## Kurulum

### Gereksinimler

- Ruby 2.7 veya üzeri
- Bundler gem

### Adımlar

1. Repository'yi klonlayın:
```bash
git clone https://github.com/alperdigital/md.git
cd md
```

2. Bağımlılıkları yükleyin:
```bash
bundle install
```

3. Jekyll sunucusunu başlatın:
```bash
bundle exec jekyll serve
```

4. Tarayıcınızda `http://localhost:4000` adresini açın.

## GitHub Pages'te Yayınlama

1. Repository ayarlarına gidin (Settings)
2. "Pages" bölümüne gidin
3. Source olarak "Deploy from a branch" seçin
4. Branch olarak "master" (veya "main") seçin
5. Save'e tıklayın

Site birkaç dakika içinde `https://alperdigital.github.io/md` adresinde yayınlanacaktır.

## Tema

Bu site [Minimal](https://github.com/pages-themes/minimal) temasını kullanmaktadır. GitHub Pages tarafından desteklenen diğer temalar:

- Architect
- Cayman
- Dinky
- Hacker
- Leap day
- Merlot
- Midnight
- Minima
- Modernist
- Slate
- Tactile
- Time machine

Tema değiştirmek için `_config.yml` dosyasındaki `theme` ayarını değiştirin.

## İçerik Ekleme

### Yeni Blog Yazısı

`_posts/` klasörüne `YYYY-MM-DD-baslik.md` formatında bir dosya ekleyin:

```markdown
---
layout: post
title: "Yazı Başlığı"
date: 2025-01-27 10:00:00 +0300
categories: genel
---

Yazı içeriği buraya...
```

### Yeni Sayfa

Root dizine `sayfa-adi.md` dosyası ekleyin:

```markdown
---
layout: default
title: Sayfa Başlığı
permalink: /sayfa-adi/
---

Sayfa içeriği buraya...
```

## Özelleştirme

### Site Ayarları

`_config.yml` dosyasını düzenleyerek site ayarlarını değiştirebilirsiniz:

- `title`: Site başlığı
- `description`: Site açıklaması
- `url`: Site URL'i
- `theme`: Kullanılan tema

### CSS Özelleştirme

`assets/css/style.scss` dosyası oluşturarak CSS'i özelleştirebilirsiniz:

```scss
---
---
@import "{{ site.theme }}";

/* Özel CSS buraya */
```

## Katkıda Bulunma

1. Repository'yi fork edin
2. Yeni bir branch oluşturun (`git checkout -b feature/yeni-ozellik`)
3. Değişikliklerinizi commit edin (`git commit -am 'Yeni özellik eklendi'`)
4. Branch'inizi push edin (`git push origin feature/yeni-ozellik`)
5. Pull Request oluşturun

## Lisans

Bu proje açık kaynaklıdır ve özgürce kullanılabilir.

## İletişim

Sorularınız veya önerileriniz için GitHub Issues kullanabilirsiniz.

---

**Not:** Bu site sürekli geliştirilmektedir. Yeni özellikler ve içerikler yakında eklenecektir.

