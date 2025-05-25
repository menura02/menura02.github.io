
# Project 33

**Hoş geldiniz!**  
**Labirent Oyunu**, HTML5 ve JavaScript ile geliştirilmiş, zekanızı ve stratejik düşünme becerilerinizi test eden bir bulmaca oyunudur.  
Hareket yönlerinizi değiştiren yükseltmeleri toplayın ve her seviyeyi tamamlamak için şaha ulaşın.

---

## 🖼️ Oyun Ekran Görüntüsü

![Seviye1](https://github.com/user-attachments/assets/f891a854-9bc9-453f-b3e2-d8d0d33e8114)


---

## 📚 İçindekiler

- [Tanıtım](#tanıtım)
- [Özellikler](#özellikler)
- [Kurulum](#kurulum)
- [Kontroller](#kontroller)
- [Seviye Tasarımı](#seviye-tasarımı)
- [Teşekkürler](#teşekkürler)
- [Kullanılan Kaynaklar](#kullanılan-kaynaklar)

---

## Tanıtım

**Labirent Oyunu**, oyuncuların her biri giderek zorlaşan labirentlerde ilerlediği bir bulmaca oyunudur.  
Her seviyede hareket yönleriniz sınırlı başlar ve yol boyunca topladığınız yükseltmelerle, yükseltmeye girdiğiniz yönü kaybedip yeni yönü kazanırsınız.  
HTML5 Canvas ve JavaScript kullanılarak geliştirilen bu oyun, modern web tarayıcılarında kolayca çalışır ve hafif bir yapıya sahiptir.

---

## Özellikler

- **Çoklu Seviyeler**: 5 benzersiz seviye, her biri farklı labirent düzenleri ve zorluklarla dolu.  
- **Yön Kısıtlamaları**: Her seviyeye sınırlı hareket yönleriyle başlayın ve yükseltmelerle yeni yollar açın.  
- **Ses Efektleri**: Arka plan müziği, seviye tamamlama sesleri ve yükseltme efektleriyle zengin bir deneyim.  
- **Öğretici**: Yeni oyuncular için oyunun nasıl oynandığını açıklayan bir rehber.  
- **Sıfırlama Seçeneği**: `R` tuşuyla seviyeyi sıfırlayıp baştan deneyin.  
- **Görsel Göstergeler**: Kullanılabilir hareket yönlerini gösteren net bir arayüz.

---

## Kurulum

Oyunu aşağıdaki adresten oynayabilirsiniz:  
🔗 **[https://menura02.github.io/](https://menura02.github.io/)**

---

## Kontroller

- 🎮 **Yön Tuşları (↑, ↓, ←, →)**: Oyuncuyu mevcut yönlerde hareket ettirin.  
- 🔄 **R Tuşu**: Seviyeyi sıfırlayın.

---

## Seviye Tasarımı

Her seviye, oyuncuları stratejik düşünmeye zorlamak için özenle tasarlanmıştır.  
Labirentler, JavaScript kodundaki `levels` dizisinde tanımlanır ve şu şekilde yapılandırılır:

- **Harita (8x8 Izgara)**:  
  - `0`: Boş alan  
  - `1`: Duvar (siyah piyon)    
  - `3`: Hedef (şah)

- **Oyuncu**: Başlangıç koordinatları (`x`, `y`) ve ilk hareket yönleri.  
- **Yükseltmeler**: Hareket yönlerini değiştiren okların konumu.

###  Örnek Seviye

```javascript
{
  map: [
    [0, 0, 1, 0, 0, 0, 0, 0],
    [0, 0, 1, 0, 1, 1, 1, 0],
    [0, 0, 0, 0, 1, 3, 1, 0],
    [1, 1, 1, 0, 1, 0, 0, 0],
    [0, 0, 0, 0, 1, 1, 1, 0],
    [0, 1, 1, 1, 1, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 1, 0],
    [0, 0, 0, 0, 0, 0, 1, 0]
  ],
  player: { x: 1, y: 1, directions: ["↑", "←"] },
  upgrades: [
    { x: 5, y: 3, dir: "→" },
    { x: 4, y: 4, dir: "↓" }
  ]
}
```

---

## 🙏 Teşekkürler

**Geliştirici:** Eren Ertürk

---

## 🖼️ Ekran Görüntüsü


![Seviye4](https://github.com/user-attachments/assets/00fea961-c5e8-4fb4-8f88-50e2a178d4d5)


## 📦 Kullanılan Kaynaklar

- [Keyboard Direction Buttons](https://opengameart.org/content/keyboard-direction-buttons)  
- [Plingy Coin](https://opengameart.org/content/plingy-coin)  
- [Jara](https://opengameart.org/content/jara)  
- [Chess Grille](https://opengameart.org/content/chess-grille)
- [Pixel Chess Pieces](https://opengameart.org/content/pixel-chess-pieces)  
- [Lofi Hip Hop](https://opengameart.org/content/lofi-hip-hop)  
- [Bubbles 'Pop'](https://opengameart.org/content/bubbles-pop)  
- [Level Complete Splash](https://opengameart.org/content/level-complete-splash)


## Lisans
Bu proje MIT Lisansı altında lisanslanmıştır. Detaylar için [LICENSE](LICENSE) dosyasına bakın.
