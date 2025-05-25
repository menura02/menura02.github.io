### html5 / Javascript kullanarak (kutuphane kullanmadan) bir oyun yaziyorum. Oyunda R tusuna basarak leveli resetlemek istiyorum. bana bir fonksiyon oner

HTML5 ve JavaScript kullanarak yazdığınız oyunda, 'R' tuşuna basıldığında seviyeyi sıfırlamak için bir fonksiyon oluşturabilirsiniz. Aşağıda, klavye olaylarını dinleyen ve 'R' tuşuna basıldığında seviyeyi sıfırlayan bir örnek fonksiyon sunulmaktadır. Bu fonksiyon, kütüphane kullanılmadan saf JavaScript ile yazılmıştır ve oyununuzun mevcut yapısına uyarlanabilir.
javascript
// Seviyeyi sıfırlamak için fonksiyon
function resetLevel() {
    // Burada oyununuzun seviyesini sıfırlamak için gerekli kodları yazabilirsiniz.
    // Örnek sıfırlama işlemleri:
    // 1. Oyuncunun pozisyonunu başlangıç noktasına getir
    // 2. Skoru sıfırla
    // 3. Oyun nesnelerini başlangıç durumuna getir
    // 4. Zamanlayıcıları sıfırla
    // 5. Canvas'ı temizle (eğer kullanıyorsanız)
    
    console.log("Seviye sıfırlandı!");
    // Örnek: Oyuncunun pozisyonunu sıfırlama
    // player.x = 0;
    // player.y = 0;
    // score = 0;
    // enemies = [];
    // ctx.clearRect(0, 0, canvas.width, canvas.height);
}

// Klavye olaylarını dinlemek için olay dinleyici
document.addEventListener('keydown', function(event) {
    if (event.key === 'r' || event.key === 'R') {
        resetLevel();
    }
});
Açıklamalar:

    resetLevel Fonksiyonu:
        Bu fonksiyon, oyununuzun seviyesini sıfırlamak için gereken tüm işlemleri içermelidir. Örneğin, oyuncunun pozisyonunu, skoru, düşmanları veya diğer oyun nesnelerini başlangıç durumuna getirebilirsiniz.
        Yukarıdaki örnekte, yalnızca bir konsol mesajı yazdırılıyor; ancak siz bu fonksiyonu oyununuzun ihtiyaçlarına göre özelleştirebilirsiniz (örneğin, canvas'ı temizlemek, oyun değişkenlerini sıfırlamak).
    Klavyeden 'R' Tuşunu Algılama:
        document.addEventListener('keydown', ...) kullanılarak klavye olayları dinlenir.
        event.key özelliği, basılan tuşun değerini kontrol eder. Hem küçük harf 'r' hem de büyük harf 'R' için çalışır.
        'R' tuşuna basıldığında resetLevel fonksiyonu çağrılır.
    Uyarlamalar:
        Oyununuzun mevcut durumuna bağlı olarak, resetLevel fonksiyonu içinde sıfırlanması gereken değişkenleri ve nesneleri belirlemeniz gerekir.
        Örneğin, eğer bir canvas kullanıyorsanız, ctx.clearRect(0, 0, canvas.width, canvas.height); ile ekranı temizleyebilirsiniz.
        Oyuncunun başlangıç pozisyonu, skor, düşman listesi gibi değişkenleri sıfırlamak için oyununuzun veri yapısına uygun kodlar ekleyin.
    Ek İpuçları:
        Eğer oyun döngünüz (requestAnimationFrame veya setInterval) içindeyse, sıfırlama işlemi sırasında döngüyü durdurmanız veya yeniden başlatmanız gerekebilir.
        Oyun durumunu yönetmek için bir durum nesnesi (gameState) kullanıyorsanız, bu nesneyi başlangıç değerlerine döndürebilirsiniz.

Örnek Kullanım:

Eğer oyununuzda bir canvas ve basit bir oyuncu nesnesi varsa, aşağıdaki gibi bir yapı kullanılabilir:
javascript
// Örnek oyun değişkenleri
let player = { x: 0, y: 0 };
let score = 0;
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

function resetLevel() {
    player.x = 0; // Oyuncunun X pozisyonunu sıfırla
    player.y = 0; // Oyuncunun Y pozisyonunu sıfırla
    score = 0;    // Skoru sıfırla
    ctx.clearRect(0, 0, canvas.width, canvas.height); // Canvas'ı temizle
    console.log("Seviye sıfırlandı!");
}

// Klavye olayı
document.addEventListener('keydown', function(event) {
    if (event.key === 'r' || event.key === 'R') {
        resetLevel();
    }
});
HTML Örneği:
html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <title>Oyun</title>
</head>
<body>
    <canvas id="gameCanvas" width="800" height="600"></canvas>
    <script src="game.js"></script>
</body>
</html>

Bu kod, 'R' tuşuna basıldığında resetLevel fonksiyonunu çağırır ve oyununuzu sıfırlamak için temel bir yapı sağlar. Oyununuzun detaylarına göre resetLevel fonksiyonunu özelleştirmeniz gerekebilir. Eğer daha fazla detaya veya oyununuzun belirli bir yönüne odaklanmamı isterseniz, lütfen belirtin!
966ms
### karakteri hareket ettirebilecegim bir move fonksiyonu yaz (oyun 2boyutlu)

HTML5 ve JavaScript kullanarak 2 boyutlu bir oyunda karakteri hareket ettirmek için bir move fonksiyonu öneriyorum. Bu fonksiyon, klavye girişlerini (örneğin, W, A, S, D veya yön tuşları) algılayarak karakterin konumunu güncelleyecek ve saf JavaScript ile yazılacak, böylece herhangi bir kütüphaneye ihtiyaç duyulmayacak. Fonksiyon, oyununuzun mevcut yapısına entegre edilebilir ve özelleştirilebilir.
Önerilen move Fonksiyonu

Aşağıdaki kod, karakterin 2D düzlemde hareketini sağlayan bir move fonksiyonu içerir. Karakterin pozisyonu player nesnesinde saklanır ve klavye girişlerine göre güncellenir.
javascript
// Oyuncu nesnesi (örnek)
let player = {
    x: 0, // X pozisyonu
    y: 0, // Y pozisyonu
    speed: 5 // Hareket hızı (piksel cinsinden)
};

// Tuş durumlarını takip etmek için
const keys = {
    ArrowUp: false,
    ArrowDown: false,
    ArrowLeft: false,
    ArrowRight: false,
    KeyW: false,
    KeyA: false,
    KeyS: false,
    KeyD: false
};

// Hareket fonksiyonu
function move() {
    // Klavye girişlerine göre hareket
    if (keys.ArrowUp || keys.KeyW) {
        player.y -= player.speed; // Yukarı hareket
    }
    if (keys.ArrowDown || keys.KeyS) {
        player.y += player.speed; // Aşağı hareket
    }
    if (keys.ArrowLeft || keys.KeyA) {
        player.x -= player.speed; // Sola hareket
    }
    if (keys.ArrowRight || keys.KeyD) {
        player.x += player.speed; // Sağa hareket
    }

    // Sınır kontrolü (örneğin, canvas sınırları içinde tutma)
    const canvas = document.getElementById('gameCanvas');
    player.x = Math.max(0, Math.min(player.x, canvas.width - 20)); // 20: oyuncu genişliği
    player.y = Math.max(0, Math.min(player.y, canvas.height - 20)); // 20: oyuncu yüksekliği
}

// Klavye olaylarını dinleme
document.addEventListener('keydown', function(event) {
    if (event.key in keys) {
        keys[event.key] = true;
    }
});

document.addEventListener('keyup', function(event) {
    if (event.key in keys) {
        keys[event.key] = false;
    }
});

// Oyun döngüsü (örnek)
function gameLoop() {
    move(); // Hareket fonksiyonunu çağır
    render(); // Render fonksiyonu (örnek, aşağıda tanımlı)
    requestAnimationFrame(gameLoop);
}

// Örnek render fonksiyonu
function render() {
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    ctx.clearRect(0, 0, canvas.width, canvas.height); // Canvas'ı temizle
    ctx.fillStyle = 'blue'; // Oyuncu rengi
    ctx.fillRect(player.x, player.y, 20, 20); // Oyuncuyu çiz (20x20 kare)
}

// Oyun döngüsünü başlat
gameLoop();
Açıklamalar:

    Oyuncu Nesnesi (player):
        x ve y koordinatları, karakterin 2D düzlemdeki konumunu temsil eder.
        speed, karakterin her hareket adımında kaç piksel ilerleyeceğini belirler (örneğin, 5 piksel).
    Tuş Durumları (keys):
        keys nesnesi, hangi tuşların basılı olduğunu takip eder. Bu, aynı anda birden fazla tuşa basıldığında (örneğin, çapraz hareket) düzgün çalışmasını sağlar.
        Hem yön tuşları (ArrowUp, ArrowDown, vb.) hem de W, A, S, D tuşları desteklenir.
    move Fonksiyonu:
        Basılı tuşlara göre player.x ve player.y koordinatlarını günceller.
        Örneğin, ArrowUp veya W basılıysa, player.y azalır (yukarı hareket).
        Sınır kontrolü, karakterin canvas alanının dışına çıkmasını engeller. Burada, oyuncu boyutunun 20x20 piksel olduğu varsayılmıştır; bunu oyununuzun karakter boyutuna göre ayarlayabilirsiniz.
    Klavye Olayları:
        keydown ve keyup olay dinleyicileri, tuşların basılıp bırakıldığını algılar ve keys nesnesini günceller.
        Bu yaklaşım, sürekli hareket için uygundur (tuş basılı tutulduğunda karakter hareket eder).
    Oyun Döngüsü:
        gameLoop fonksiyonu, requestAnimationFrame ile sürekli çalışır ve her karede move ile render fonksiyonlarını çağırır.
        render fonksiyonu, canvas üzerinde oyuncuyu çizer (örnek olarak mavi bir kare).
    Özelleştirme:
        Hız: player.speed değerini değiştirerek hareket hızını ayarlayabilirsiniz.
        Boyut ve Görünüm: render fonksiyonunda fillRect yerine kendi karakter grafiğinizi (örneğin, bir sprite) kullanabilirsiniz.
        Sınırlar: Canvas boyutlarına veya oyununuzun harita sınırlarına göre sınır kontrolünü özelleştirebilirsiniz.
        Ek Kontroller: İsterseniz, çapraz hareketin hızını normalleştirmek için bir hız sınırlayıcı ekleyebilirsiniz (örneğin, Math.sqrt(2) ile bölme).

HTML Örneği:

Bu kodu çalıştırmak için aşağıdaki HTML dosyasını kullanabilirsiniz:
html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <title>2D Oyun</title>
</head>
<body>
    <canvas id="gameCanvas" width="800" height="600" style="border:1px solid black;"></canvas>
    <script src="game.js"></script>
</body>
</html>
Ek İpuçları:

    Çarpışma Kontrolü: Eğer oyununuzda engeller varsa, move fonksiyonuna çarpışma kontrolü ekleyebilirsiniz. Örneğin, yeni pozisyonun geçerli olup olmadığını kontrol edin.
    Animasyon: Karakterin hareketine animasyon eklemek için, render fonksiyonunda bir sprite sheet kullanabilirsiniz.
    Performans: requestAnimationFrame yerine setInterval kullanıyorsanız, kare hızını (örneğin, 60 FPS) sabitlemek için dikkatli olun.
    Seviye Sıfırlama Entegrasyonu: Daha önce önerdiğim resetLevel fonksiyonuyla entegre etmek için, resetLevel içinde player.x ve player.y değerlerini sıfırlayabilirsiniz.

Örnek Çarpışma Kontrolü Ekleme:

Eğer haritanızda engeller varsa, move fonksiyonunu şu şekilde güncelleyebilirsiniz:
javascript
function move() {
    let newX = player.x;
    let newY = player.y;

    if (keys.ArrowUp || keys.KeyW) {
        newY -= player.speed;
    }
    if (keys.ArrowDown || keys.KeyS) {
        newY += player.speed;
    }
    if (keys.ArrowLeft || keys.KeyA) {
        newX -= player.speed;
    }
    if (keys.ArrowRight || keys.KeyD) {
        newX += player.speed;
    }

    // Çarpışma kontrolü (örnek: engel bir dizi kareyse)
    if (!isColliding(newX, newY)) {
        player.x = Math.max(0, Math.min(newX, canvas.width - 20));
        player.y = Math.max(0, Math.min(newY, canvas.height - 20));
    }
}

function isColliding(x, y) {
    // Örnek: Engellerin olduğu bir dizi
    const obstacles = [
        { x: 100, y: 100, width: 50, height: 50 }
    ];
    for (let obstacle of obstacles) {
        if (x < obstacle.x + obstacle.width &&
            x + 20 > obstacle.x &&
            y < obstacle.y + obstacle.height &&
            y + 20 > obstacle.y) {
            return true; // Çarpışma var
        }
    }
    return false; // Çarpışma yok
}

Bu kod, karakterin hareketini engellerle çarpışmayı dikkate alarak sınırlandırır. Oyununuzun ihtiyaçlarına göre bu fonksiyonları daha da özelleştirebilirsiniz. Eğer belirli bir özellik (örneğin, belirli bir hareket mekaniği veya ek kontrol) eklemek isterseniz, lütfen detayları belirtin!










### Html5 / Javascript ile kodladigim projeme bir Tutorial menusu ekle. kodum: 
```
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8" />
  <title>Project 33</title>
  <style>
    /* Genel sayfa stili: Koyu arka plan ve beyaz metin */
    body {
      background-color: #111;
      color: white;
      font-family: sans-serif;
      text-align: center;
      margin: 0;
      padding: 20px;
    }

    /* Canvas (oyun tahtası) stili: Ortada, siyah arka plan */
    canvas {
      display: block;
      margin: 0 auto;
      background-color: black;
    }

    /* Yön UI konteyneri: Yön tuşlarını ve metni hizalı şekilde gösterir */
    #directionUI {
      width: 512px;
      margin: 10px auto 0 auto;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 5px;
      margin-top: 30px;
    }

    /* Yön UI’nin üst (yukarı oku) ve orta (sol/aşağı/sağ) satırları */
    #ui-up,
    #ui-middle {
      display: flex;
      justify-content: center;
      gap: 10px;
    }

    /* Yön UI’deki ok görsellerinin boyutu */
    #directionUI img {
      width: 48px;
      height: 48px;
    }

    /* Yeniden başlatma metni stili: Yön UI altında, sabit talimat */
    #restartText {
      width: 512px;
      margin: 10px auto 0 auto;
      font-size: 18px;
      color: #ffffff;
      text-align: center;
      display: none; /* Oyun başlamadan gizli */
      margin-top: 30px;
    }

    /* Ana menü stili: Dikey hizalı butonlar ve başlık */
    #mainMenu {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    /* Ana menü butonları: Yeşil, fareyle üzerine gelince renk değişir */
    #mainMenu button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
    }

    #mainMenu button:hover {
      background-color: #45a049;
    }

    /* Seviye tamamlama ve oyun sonu ekranları */
    #gameOverScreen, #gameCompleteScreen {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: rgba(0, 0, 0, 0.8);
      color: white;
      padding: 20px;
      border-radius: 10px;
      text-align: left;
      display: none;
      max-width: 600px;
      max-height: 80vh;
      overflow-y: auto;
    }

    /* Ekranlardaki butonlar */
    #gameOverScreen button, #gameCompleteScreen button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
    }

    #gameOverScreen button:hover, #gameCompleteScreen button:hover {
      background-color: #45a049;
    }

    /* Seviye sayacı: Oyun tahtası üstünde, seviye numarasını gösterir */
    #levelCounter {
      width: 512px;
      margin: 10px auto 0 auto;
      font-size: 24px;
      font-weight: bold;
      color: #ffffff;
      text-align: center;
      display: none;
      padding: 30px 20px;
    }
  </style>
</head>
<body>
  <!-- Ana oyun konteyneri -->
  <div id="gameContainer">
    <!-- Ana menü: Başlık ve butonlar -->
    <div id="mainMenu">
      <h1 style="margin-top: 200px; font-size: 80px;">PROJECT 33</h1>
      <button style="margin-top: 50px;" onclick="startLevel(0)">Oyuna Başla</button>
    </div>
    <!-- Seviye sayacı -->
    <div id="levelCounter">Seviye 1</div>
    <!-- 512x512 piksel canvas -->
    <canvas id="gameCanvas" width="512" height="512" style="display: none;"></canvas>
    <!-- Yön tuşları ve yeniden başlatma metni -->
    <div id="directionUI" style="display: none;">
      <div id="ui-up"></div>
      <div id="ui-middle"></div>
      <div id="restartText">Yeniden Başlamak İçin R’ye Basın</div>
    </div>
    <!-- Seviye tamamlama ekranı, Sonraki seviye ve menü butonları -->
    <div id="gameOverScreen">
      <h2>Seviye Tamamlandı!</h2>
      <button onclick="returnToMenu()">Ana Menüye Dön</button>
      <button onclick="nextLevel()">Sonraki Seviye</button>
    </div>
    <!-- Oyun sonu ekranı -->
    <div id="gameCompleteScreen" style="display: none;">
      <h2>Tebrikler, oyunu bitirdiniz!</h2>
      <button onclick="returnToMenu()">Ana Menüye Dön</button>
    </div>
  </div>

  <!-- Ses dosyaları -->
  <audio id="lobbyMusic" loop>
    <source src="assets/audio/lobby.mp3" type="audio/mpeg">
  </audio>
  <audio id="levelMusic" loop>
    <source src="assets/audio/level.ogg" type="audio/ogg">
  </audio>
  <audio id="levelCompleteSound">
    <source src="assets/audio/level_complete.wav" type="audio/wav">
  </audio>
  <audio id="upgradeSound">
    <source src="assets/audio/upgrade.ogg" type="audio/ogg">
  </audio>

  <script>
    // Canvas ve 2D bağlamını tanımla
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");
    const cellSize = 64; // Her hücre 64x64 piksel

    // HTML elementlerini tanımla
    const directionUI = document.getElementById("directionUI"); // Yön tuşları UI
    const mainMenu = document.getElementById("mainMenu"); // Ana menü
    const gameOverScreen = document.getElementById("gameOverScreen"); // Seviye tamamlama ekranı
    const gameCompleteScreen = document.getElementById("gameCompleteScreen"); // Oyun sonu ekranı
    const levelCounter = document.getElementById("levelCounter"); // Seviye sayacı
    const restartText = document.getElementById("restartText"); // Yeniden başlatma metni
    const lobbyMusic = document.getElementById("lobbyMusic"); // Menü müziği
    const levelMusic = document.getElementById("levelMusic"); // Seviye müziği
    const levelCompleteSound = document.getElementById("levelCompleteSound"); // Seviye tamamlama sesi
    const upgradeSound = document.getElementById("upgradeSound"); // Yükseltme sesi

    // Görsel varlıkları saklamak için nesne
    const assets = {};

    // Yüklenmesi gereken görsel dosyalar
    const imageFiles = {
      board: "assets/images/tahta.png", // Oyun tahtası
      player: "assets/images/kale.png", // Oyuncu (kale simgesi)
      wall: "assets/images/siyah_piyon.png", // Duvar (siyah piyon)
      goal: "assets/images/sah.png", // Hedef (şah simgesi)
      "↑": "assets/images/ok_yukari.png", // Yukarı ok
      "↓": "assets/images/ok_asagi.png", // Aşağı ok
      "←": "assets/images/ok_sol.png", // Sol ok
      "→": "assets/images/ok_sag.png", // Sağ ok
      dirUI: { // Yön UI görselleri
        base: "assets/images/KeyboardButtons_Base.png", // Pasif yön tuşu
        "↑": "assets/images/KeyboardButtonsDir_up.png", // Aktif yukarı tuşu
        "↓": "assets/images/KeyboardButtonsDir_down.png", // Aktif aşağı tuşu
        "←": "assets/images/KeyboardButtonsDir_left.png", // Aktif sol tuşu
        "→": "assets/images/KeyboardButtonsDir_right.png" // Aktif sağ tuşu
      }
    };

    // Oyun seviyeleri: Harita, oyuncu başlangıç noktası, yönler ve yükseltmeler
    const levels = [
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
        player: { x: 0, y: 0, directions: ["↓", "→"] },
        upgrades: [
          { x: 3, y: 3, dir: "↑" },
          { x: 7, y: 0, dir: "↓" },
          { x: 7, y: 3, dir: "←" }
        ]
      },
      {
        map: [
          [0, 0, 0, 0, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 1, 0, 0],
          [0, 0, 0, 0, 1, 0, 0, 0],
          [1, 1, 1, 0, 1, 3, 1, 0],
          [0, 0, 0, 0, 1, 0, 0, 0],
          [0, 1, 1, 1, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 0, 0]
        ],
        player: { x: 1, y: 1, directions: ["↓", "→"] },
        upgrades: [
          { x: 4, y: 1, dir: "←" },
          { x: 0, y: 6, dir: "→" },
          { x: 4, y: 6, dir: "↓" },
          { x: 3, y: 7, dir: "↑" },
          { x: 4, y: 7, dir: "→" }
        ]
      },
      {
        map: [
          [0, 0, 0, 1, 0, 0, 0, 0],
          [0, 0, 1, 1, 0, 1, 1, 0],
          [0, 0, 0, 0, 0, 1, 3, 0],
          [1, 1, 1, 0, 1, 1, 0, 0],
          [0, 0, 0, 0, 1, 0, 0, 0],
          [0, 1, 1, 1, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 1, 0]
        ],
        player: { x: 1, y: 1, directions: ["↓", "→"] },
        upgrades: [
          { x: 3, y: 4, dir: "↑" },
          { x: 7, y: 0, dir: "↓" },
          { x: 7, y: 6, dir: "←" }
        ]
      },
      {
        map: [
          [0, 0, 1, 0, 0, 0, 0, 0],
          [0, 0, 1, 0, 1, 1, 1, 0],
          [0, 0, 0, 0, 0, 0, 0, 0],
          [1, 0, 0, 0, 0, 0, 1, 0],
          [0, 0, 0, 0, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 1, 0],
          [0, 1, 1, 0, 0, 0, 1, 0],
          [0, 0, 3, 0, 0, 0, 1, 0]
        ],
        player: { x: 5, y: 5, directions: ["↑", "←"] },
        upgrades: [
          { x: 1, y: 5, dir: "→" },
          { x: 2, y: 3, dir: "↓" },
          { x: 7, y: 4, dir: "↑" },
          { x: 7, y: 0, dir: "←" }
        ]
      },
      {
        map: [
          [0, 0, 0, 0, 0, 0, 0, 0],
          [0, 0, 0, 1, 0, 0, 0, 0],
          [0, 0, 0, 1, 1, 1, 0, 0],
          [0, 0, 0, 0, 3, 1, 0, 1],
          [0, 0, 1, 1, 1, 1, 0, 0],
          [0, 0, 1, 0, 0, 0, 0, 0],
          [0, 0, 1, 0, 0, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 0, 0]
        ],
        player: { x: 7, y: 7, directions: ["↑", "←"] },
        upgrades: [
          { x: 5, y: 0, dir: "↓" },
          { x: 4, y: 1, dir: "→" },
          { x: 7, y: 4, dir: "←" },
          { x: 3, y: 7, dir: "↑" },
          { x: 0, y: 2, dir: "→" },
          { x: 2, y: 0, dir: "↓" }
        ]
      }
    ];

    // Oyun durumu değişkenleri
    let currentLevel = 0; // Mevcut seviye numarası
    let map, player, upgrades; // Aktif seviye haritası, oyuncu ve yükseltmeler
    let gameState = 'menu'; // Oyun durumu: menu, playing, gameOver

    // Görsel varlıkları yükler
    function loadAssets(callback) {
      const promises = [];
      // imageFiles nesnesindeki tüm görselleri yükle
      for (const key in imageFiles) {
        if (typeof imageFiles[key] === "string") {
          promises.push(loadImage(key, imageFiles[key]));
        } else {
          for (const dir in imageFiles[key]) {
            promises.push(loadImage(`${key}_${dir}`, imageFiles[key][dir]));
          }
        }
      }
      // Tüm görseller yüklendiğinde
      Promise.all(promises).then(() => {
        callback(); // Ana menüyü göster
        try {
          // Menü müziğini başlat
          lobbyMusic.play().catch((error) => {
            console.error("Lobby müziği oynatılamadı:", error);
            // Hata durumunda, kullanıcı etkileşimiyle müziği denemek için olay dinleyici ekle
            document.addEventListener('click', tryPlayLobbyMusic, { once: true });
          });
        } catch (error) {
          console.error("Lobby müziği başlatma hatası:", error);
        }
      });
    }

    // Kullanıcı tıklamasıyla menü müziğini başlatmayı dener
    function tryPlayLobbyMusic() {
      if (gameState === 'menu') {
        lobbyMusic.play().catch((error) => {
          console.error("Lobby müziği kullanıcı etkileşimiyle oynatılamadı:", error);
        });
      }
    }

    // Tek bir görseli yükler ve assets nesnesine ekler
    function loadImage(key, src) {
      return new Promise((resolve) => {
        const img = new Image();
        img.src = src;
        img.onload = () => {
          assets[key] = img; // Görseli assets nesnesine kaydet
          resolve();
        };
        img.onerror = () => {
          console.error(`Resim yüklenemedi: ${src}`);
          resolve(); // Hata olsa bile devam et
        };
      });
    }

    // Seviye sayacını günceller
    function updateLevelCounter() {
      levelCounter.textContent = `Seviye ${currentLevel + 1}`; // Mevcut seviye numarasını göster
    }

    // Yeni bir seviyeyi başlatır
    function startLevel(levelNum) {
      currentLevel = levelNum; // Seviye numarasını ayarla
      gameState = 'playing'; // Oyun durumunu oynama moduna geçir
      mainMenu.style.display = 'none'; // Ana menüyü gizle
      levelCounter.style.display = 'block'; // Seviye sayacını göster
      canvas.style.display = 'block'; // Oyun tahtasını göster
      directionUI.style.display = 'flex'; // Yön UI’yi göster
      restartText.style.display = 'block'; // Yeniden başlatma metnini göster
      lobbyMusic.pause(); // Menü müziğini durdur
      levelMusic.currentTime = 0; // Seviye müziğini başa al
      levelMusic.play().catch((error) => {
        console.error("Seviye müziği oynatılamadı:", error);
      });
      resetLevel(); // Seviyeyi başlat
      updateLevelCounter(); // Seviye sayacını güncelle
    }

    // Mevcut seviyeyi sıfırlar (oyuncu, yönler ve yükseltmeler)
    function resetLevel() {
      const level = levels[currentLevel]; // Mevcut seviye verilerini al
      map = JSON.parse(JSON.stringify(level.map)); // Haritayı kopyala
      player = {
        x: level.player.x,
        y: level.player.y,
        directions: [...level.player.directions] // Yönleri kopyala
      };
      upgrades = level.upgrades.map(u => ({ ...u })); // Yükseltmeleri kopyala
      gameOverScreen.style.display = 'none'; // Seviye tamamlama ekranını gizle
      gameCompleteScreen.style.display = 'none'; // Oyun sonu ekranını gizle
      canvas.style.display = 'block'; // Oyun tahtasını göster
      directionUI.style.display = 'flex'; // Yön UI’yi göster
      restartText.style.display = 'block'; // Yeniden başlatma metnini göster
      draw(); // Tahtayı çiz
      updateDirectionUI(); // Yön UI’yi güncelle
      updateLevelCounter(); // Seviye sayacını güncelle
    }

    // Oyun tahtasını çizer
    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height); // Canvas’ı temizle
      ctx.drawImage(assets.board, 0, 0, canvas.width, canvas.height); // Tahtayı çiz

      // Haritadaki her hücreyi tara
      for (let y = 0; y < 8; y++) {
        for (let x = 0; x < 8; x++) {
          if (map[y][x] === 1) {
            // Duvar çiz
            ctx.drawImage(assets.wall, x * cellSize, y * cellSize, cellSize, cellSize);
          } else if (map[y][x] === 3) {
            // Hedef çiz
            ctx.drawImage(assets.goal, x * cellSize, y * cellSize, cellSize, cellSize);
          }
        }
      }

      // Yükseltmeleri çiz
      for (const up of upgrades) {
        const img = assets[up.dir];
        ctx.drawImage(img, up.x * cellSize, up.y * cellSize, cellSize, cellSize);
      }

      // Oyuncuyu çiz
      ctx.drawImage(assets.player, player.x * cellSize, player.y * cellSize, cellSize, cellSize);
    }

    // Oyuncuyu belirtilen yönde hareket ettirir
    function move(dx, dy, dir) {
      const nx = player.x + dx; // Yeni X koordinatı
      const ny = player.y + dy; // Yeni Y koordinatı
      // Hareket sınırlar dışındaysa, geçersiz yönse veya duvara çarpıyorsa çık
      if (nx < 0 || nx >= 8 || ny < 0 || ny >= 8) return;
      if (!player.directions.includes(dir)) return;
      if (map[ny][nx] === 1) return;

      player.x = nx; // Oyuncunun X koordinatını güncelle
      player.y = ny; // Oyuncunun Y koordinatını güncelle

      // Yükseltme kontrolü
      const index = upgrades.findIndex(u => u.x === nx && u.y === ny);
      if (index !== -1) {
        upgradeSound.currentTime = 0; // Yükseltme sesini başa al
        upgradeSound.play().catch((error) => {
          console.error("Yükseltme sesi oynatılamadı:", error);
        });
        const newDir = upgrades[index].dir; // Yeni yön
        const dirIndex = player.directions.indexOf(dir); // Mevcut yönün indeksi
        if (dirIndex !== -1) {
          player.directions[dirIndex] = newDir; // Yönü değiştir
        }
        upgrades.splice(index, 1); // Yükseltmeyi kaldır
      }

      // Hedefe ulaşıldıysa
      if (map[ny][nx] === 3) {
        map[ny][nx] = 0; // Hedefi kaldır
        levelMusic.pause(); // Seviye müziğini durdur
        levelCompleteSound.currentTime = 0; // Tamamlama sesini başa al
        levelCompleteSound.play().catch((error) => {
          console.error("Seviye tamamlama sesi oynatılamadı:", error);
        });
        gameState = 'gameOver'; // Oyun durumunu güncelle
        canvas.style.display = 'none'; // Tahtayı gizle
        directionUI.style.display = 'none'; // Yön UI’yi gizle
        levelCounter.style.display = 'none'; // Seviye sayacını gizle
        restartText.style.display = 'none'; // Yeniden başlatma metnini gizle
        // Son seviye mi?
        if (currentLevel + 1 >= levels.length) {
          gameCompleteScreen.style.display = 'block'; // Oyun sonu ekranını göster
        } else {
          gameOverScreen.style.display = 'block'; // Seviye tamamlama ekranını göster
        }
        return;
      }

      draw(); // Tahtayı yeniden çiz
      updateDirectionUI(); // Yön UI’yi güncelle
    }

    // Bir sonraki seviyeye geçer
    function nextLevel() {
      currentLevel++; // Seviye numarasını artır
      if (currentLevel < levels.length) {
        gameState = 'playing'; // Oyun durumunu oynama moduna geçir
        gameOverScreen.style.display = 'none'; // Seviye tamamlama ekranını gizle
        canvas.style.display = 'block'; // Tahtayı göster
        directionUI.style.display = 'flex'; // Yön UI’yi göster
        levelCounter.style.display = 'block'; // Seviye sayacını göster
        restartText.style.display = 'block'; // Yeniden başlatma metnini göster
        levelMusic.currentTime = 0; // Seviye müziğini başa al
        levelMusic.play().catch((error) => {
          console.error("Seviye müziği oynatılamadı:", error);
        });
        resetLevel(); // Yeni seviyeyi başlat
        updateLevelCounter(); // Seviye sayacını güncelle
      } else {
        gameState = 'gameOver'; // Oyun durumunu güncelle
        gameOverScreen.style.display = 'none'; // Seviye tamamlama ekranını gizle
        gameCompleteScreen.style.display = 'block'; // Oyun sonu ekranını göster
        levelCounter.style.display = 'none'; // Seviye sayacını gizle
        restartText.style.display = 'none'; // Yeniden başlatma metnini gizle
        lobbyMusic.currentTime = 0; // Menü müziğini başa al
        lobbyMusic.play().catch((error) => {
          console.error("Lobby müziği oynatılamadı:", error);
        });
      }
    }

    // Ana menüye döner
    function returnToMenu() {
      gameState = 'menu'; // Oyun durumunu menü moduna geçir
      currentLevel = 0; // Seviye numarasını sıfırla
      gameOverScreen.style.display = 'none'; // Seviye tamamlama ekranını gizle
      gameCompleteScreen.style.display = 'none'; // Oyun sonu ekranını gizle
      mainMenu.style.display = 'flex'; // Ana menüyü göster
      levelCounter.style.display = 'none'; // Seviye sayacını gizle
      canvas.style.display = 'none'; // Tahtayı gizle
      directionUI.style.display = 'none'; // Yön UI’yi gizle
      restartText.style.display = 'none'; // Yeniden başlatma metnini gizle
      levelMusic.pause(); // Seviye müziğini durdur
      lobbyMusic.currentTime = 0; // Menü müziğini başa al
      lobbyMusic.play().catch((error) => {
        console.error("Lobby müziği oynatılamadı:", error);
      });
    }

    // Yön UI’yi günceller: Aktif yönleri gösterir
    function updateDirectionUI() {
      document.getElementById("ui-up").innerHTML = ""; // Üst satırı temizle
      document.getElementById("ui-middle").innerHTML = ""; // Orta satırı temizle

      // Yukarı yön tuşu
      const up = document.createElement("img");
      up.src = player.directions.includes("↑") ? assets["dirUI_↑"].src : assets["dirUI_base"].src;
      document.getElementById("ui-up").appendChild(up);

      // Sol yön tuşu
      const left = document.createElement("img");
      left.src = player.directions.includes("←") ? assets["dirUI_←"].src : assets["dirUI_base"].src;

      // Aşağı yön tuşu
      const down = document.createElement("img");
      down.src = player.directions.includes("↓") ? assets["dirUI_↓"].src : assets["dirUI_base"].src;

      // Sağ yön tuşu
      const right = document.createElement("img");
      right.src = player.directions.includes("→") ? assets["dirUI_→"].src : assets["dirUI_base"].src;

      // Orta satıra sol, aşağı, sağ tuşlarını ekle
      const middleRow = document.getElementById("ui-middle");
      middleRow.appendChild(left);
      middleRow.appendChild(down);
      middleRow.appendChild(right);
    }

    // Klavye girişlerini dinler
    document.addEventListener("keydown", (e) => {
      if (gameState !== 'playing') return; // Oyun oynanmıyorsa çık
      switch (e.key) {
        case "ArrowLeft": move(-1, 0, "←"); break; // Sol ok: Sola hareket
        case "ArrowRight": move(1, 0, "→"); break; // Sağ ok: Sağa hareket
        case "ArrowUp": move(0, -1, "↑"); break; // Yukarı ok: Yukarı hareket
        case "ArrowDown": move(0, 1, "↓"); break; // Aşağı ok: Aşağı hareket
        case "r":
        case "R":
          resetLevel(); // R tuşu: Seviyeyi sıfırla
          break;
      }
    });

    // Oyun başlangıcı: Görselleri yükle ve ana menüyü göster
    loadAssets(() => {
      mainMenu.style.display = 'flex';
    });
  </script>
</body>
</html>
```
Kod, orijinal yapıyı korurken tutorial ekranını ve işlevselliğini entegre eder.
```
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8" />
  <title>Project 33</title>
  <style>
    /* Genel sayfa stili: Koyu arka plan ve beyaz metin */
    body {
      background-color: #111;
      color: white;
      font-family: sans-serif;
      text-align: center;
      margin: 0;
      padding: 20px;
    }

    /* Canvas (oyun tahtası) stili: Ortada, siyah arka plan */
    canvas {
      display: block;
      margin: 0 auto;
      background-color: black;
    }

    /* Yön UI konteyneri: Yön tuşlarını ve metni hizalı şekilde gösterir */
    #directionUI {
      width: 512px;
      margin: 10px auto 0 auto;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 5px;
      margin-top: 30px;
    }

    /* Yön UI’nin üst (yukarı oku) ve orta (sol/aşağı/sağ) satırları */
    #ui-up,
    #ui-middle {
      display: flex;
      justify-content: center;
      gap: 10px;
    }

    /* Yön UI’deki ok görsellerinin boyutu */
    #directionUI img {
      width: 48px;
      height: 48px;
    }

    /* Yeniden başlatma metni stili: Yön UI altında, sabit talimat */
    #restartText {
      width: 512px;
      margin: 10px auto 0 auto;
      font-size: 18px;
      color: #ffffff;
      text-align: center;
      display: none; /* Oyun başlamadan gizli */
      margin-top: 30px;
    }

    /* Ana menü stili: Dikey hizalı butonlar ve başlık */
    #mainMenu {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    /* Ana menü butonları: Yeşil, fareyle üzerine gelince renk değişir */
    #mainMenu button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
    }

    #mainMenu button:hover {
      background-color: #45a049;
    }

    /* Seviye tamamlama, oyun sonu ve tutorial ekranları */
    #gameOverScreen, #gameCompleteScreen, #tutorialScreen {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: rgba(0, 0, 0, 0.8);
      color: white;
      padding: 20px;
      border-radius: 10px;
      text-align: left;
      display: none;
      max-width: 600px;
      max-height: 80vh;
      overflow-y: auto;
    }

    /* Ekranlardaki butonlar */
    #gameOverScreen button, #gameCompleteScreen button, #tutorialScreen button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
    }

    #gameOverScreen button:hover, #gameCompleteScreen button:hover, #tutorialScreen button:hover {
      background-color: #45a049;
    }

    /* Seviye sayacı: Oyun tahtası üstünde, seviye numarasını gösterir */
    #levelCounter {
      width: 512px;
      margin: 10px auto 0 auto;
      font-size: 24px;
      font-weight: bold;
      color: #ffffff;
      text-align: center;
      display: none;
      padding: 30px 20px;
    }

    /* Tutorial ekranı başlığı */
    #tutorialScreen h2 {
      text-align: center;
    }

    /* Tutorial ekranı listeleri */
    #tutorialScreen ul {
      margin: 10px 0;
      padding-left: 20px;
    }

    /* Tutorial ekranı paragrafları */
    #tutorialScreen p {
      margin: 10px 0;
    }
  </style>
</head>
<body>
  <!-- Ana oyun konteyneri -->
  <div id="gameContainer">
    <!-- Ana menü: Başlık ve butonlar -->
    <div id="mainMenu">
      <h1 style="margin-top: 200px; font-size: 80px;">PROJECT 33</h1>
      <button style="margin-top: 50px;" onclick="startLevel(0)">Oyuna Başla</button>
      <button onclick="showTutorial()">Tutorial</button>
    </div>
    <!-- Seviye sayacı -->
    <div id="levelCounter">Seviye 1</div>
    <!-- 512x512 piksel canvas -->
    <canvas id="gameCanvas" width="512" height="512" style="display: none;"></canvas>
    <!-- Yön tuşları ve yeniden başlatma metni -->
    <div id="directionUI" style="display: none;">
      <div id="ui-up"></div>
      <div id="ui-middle"></div>
      <div id="restartText">Yeniden Başlamak İçin R’ye Basın</div>
    </div>
    <!-- Seviye tamamlama ekranı, Sonraki seviye ve menü butonları -->
    <div id="gameOverScreen">
      <h2>Seviye Tamamlandı!</h2>
      <button onclick="returnToMenu()">Ana Menüye Dön</button>
      <button onclick="nextLevel()">Sonraki Seviye</button>
    </div>
    <!-- Oyun sonu ekranı -->
    <div id="gameCompleteScreen" style="display: none;">
      <h2>Tebrikler, oyunu bitirdiniz!</h2>
      <button onclick="returnToMenu()">Ana Menüye Dön</button>
    </div>
    <!-- Tutorial ekranı -->
    <div id="tutorialScreen" style="display: none;">
      <h2>Tutorial</h2>
      <p><strong>Proje 33’e Hoş Geldiniz!</strong></p>
      <p>Bu oyunda, bir labirenti geçerek hedefe ulaşmaya çalışacaksınız. Her seviyede farklı hareket kabiliyetleri ve engellerle karşılaşacaksınız. İşte başlamanız için kısa bir rehber:</p>
      <ol>
        <li>
          <strong>Amaç</strong>:
          <ul>
            <li>Her seviyede, şaha ulaşmalısınız.</li>
            <li>Tüm seviyeleri tamamlayarak oyunu bitirin!</li>
          </ul>
        </li>
        <li>
          <strong>Kontroller</strong>:
          <ul>
            <li><strong>Ok Tuşları (↑, ↓, ←, →)</strong>: Oyuncuyu hareket ettirmek için kullanın. Sadece aktif yönlerde hareket edebilirsiniz.</li>
            <li><strong>R Tuşu</strong>: Seviyeyi sıfırlamak için basın; oyuncu başlangıç noktasına döner ve yönler sıfırlanır.</li>
          </ul>
        </li>
        <li>
          <strong>Oyun Mekanikleri</strong>:
          <ul>
            <li><strong>Yönler</strong>: Her seviyede başlangıçta <strong style="color: red;">belirli yönlerde hareket edebilirsiniz</strong> (örneğin, sadece yukarı ve sola). Aktif yönler, ekranın altındaki yön göstergesinde görünür.</li>
            <li style="color: red;"><strong>Yükseltmeler</strong>: Tahtadaki ok simgeleri, hareket yönlerinizi değiştirir. Bir yükseltme aldığınızda, son kullandığınız yönü kaybedersiniz.</li>
            <li><strong>Engeller</strong>: Siyah piyonlar duvarları temsil eder; bu alanlara hareket edemezsiniz.</li>
          </ul>
        </li>
      </ol>
      <p><strong>Hazırsanız, “Oyuna Başla” butonuna tıklayın ve tahtayı fethedin!</strong></p>
      <button onclick="closeTutorial()">Kapat</button>
    </div>
  </div>

  <!-- Ses dosyaları -->
  <audio id="lobbyMusic" loop>
    <source src="assets/audio/lobby.mp3" type="audio/mpeg">
  </audio>
  <audio id="levelMusic" loop>
    <source src="assets/audio/level.ogg" type="audio/ogg">
  </audio>
  <audio id="levelCompleteSound">
    <source src="assets/audio/level_complete.wav" type="audio/wav">
  </audio>
  <audio id="upgradeSound">
    <source src="assets/audio/upgrade.ogg" type="audio/ogg">
  </audio>

  <script>
    // Canvas ve 2D bağlamını tanımla
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");
    const cellSize = 64; // Her hücre 64x64 piksel

    // HTML elementlerini tanımla
    const directionUI = document.getElementById("directionUI"); // Yön tuşları UI
    const mainMenu = document.getElementById("mainMenu"); // Ana menü
    const gameOverScreen = document.getElementById("gameOverScreen"); // Seviye tamamlama ekranı
    const gameCompleteScreen = document.getElementById("gameCompleteScreen"); // Oyun sonu ekranı
    const tutorialScreen = document.getElementById("tutorialScreen"); // Tutorial ekranı
    const levelCounter = document.getElementById("levelCounter"); // Seviye sayacı
    const restartText = document.getElementById("restartText"); // Yeniden başlatma metni
    const lobbyMusic = document.getElementById("lobbyMusic"); // Menü müziği
    const levelMusic = document.getElementById("levelMusic"); // Seviye müziği
    const levelCompleteSound = document.getElementById("levelCompleteSound"); // Seviye tamamlama sesi
    const upgradeSound = document.getElementById("upgradeSound"); // Yükseltme sesi

    // Görsel varlıkları saklamak için nesne
    const assets = {};

    // Yüklenmesi gereken görsel dosyalar
    const imageFiles = {
      board: "assets/images/tahta.png", // Oyun tahtası
      player: "assets/images/kale.png", // Oyuncu (kale simgesi)
      wall: "assets/images/siyah_piyon.png", // Duvar (siyah piyon)
      goal: "assets/images/sah.png", // Hedef (şah simgesi)
      "↑": "assets/images/ok_yukari.png", // Yukarı ok
      "↓": "assets/images/ok_asagi.png", // Aşağı ok
      "←": "assets/images/ok_sol.png", // Sol ok
      "→": "assets/images/ok_sag.png", // Sağ ok
      dirUI: { // Yön UI görselleri
        base: "assets/images/KeyboardButtons_Base.png", // Pasif yön tuşu
        "↑": "assets/images/KeyboardButtonsDir_up.png", // Aktif yukarı tuşu
        "↓": "assets/images/KeyboardButtonsDir_down.png", // Aktif aşağı tuşu
        "←": "assets/images/KeyboardButtonsDir_left.png", // Aktif sol tuşu
        "→": "assets/images/KeyboardButtonsDir_right.png" // Aktif sağ tuşu
      }
    };

    // Oyun seviyeleri: Harita, oyuncu başlangıç noktası, yönler ve yükseltmeler
    const levels = [
      {
        map: [ // Seviye 1 haritası (0: boş, 1: duvar, 3: hedef)
          [0, 0, 1, 0, 0, 0, 0, 0],
          [0, 0, 1, 0, 1, 1, 1, 0],
          [0, 0, 0, 0, 1, 3, 1, 0],
          [1, 1, 1, 0, 1, 0, 0, 0],
          [0, 0, 0, 0, 1, 1, 1, 0],
          [0, 1, 1, 1, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 1, 0],
          [0, 0, 0, 0, 0, 0, 1, 0]
        ],
        player: { x: 0, y: 0, directions: ["↓", "→"] }, // Oyuncu başlangıç: (0,0), yönler: aşağı, sağ
        upgrades: [ // Yükseltmeler: Konum ve yeni yön 
          { x: 3, y: 3, dir: "↑" },
          { x: 7, y: 0, dir: "↓" },
          { x: 7, y: 3, dir: "←" }
        ]
      },
      {
        map: [ // Seviye 2 haritası
          [0, 0, 0, 0, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 1, 0, 0],
          [0, 0, 0, 0, 1, 0, 0, 0],
          [1, 1, 1, 0, 1, 3, 1, 0],
          [0, 0, 0, 0, 1, 0, 0, 0],
          [0, 1, 1, 1, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 0, 0]
        ],
        player: { x: 1, y: 1, directions: ["↓", "→"] }, // Oyuncu başlangıç: (1,1), yönler: aşağı, sağ
        upgrades: [
          { x: 4, y: 1, dir: "←" },
          { x: 0, y: 6, dir: "→" },
          { x: 4, y: 6, dir: "↓" },
          { x: 3, y: 7, dir: "↑" },
          { x: 4, y: 7, dir: "→" }
        ]
      },
      {
        map: [ // Seviye 3 haritası   
          [0, 0, 0, 1, 0, 0, 0, 0],
          [0, 0, 1, 1, 0, 1, 1, 0],
          [0, 0, 0, 0, 0, 1, 3, 0],
          [1, 1, 1, 0, 1, 1, 0, 0],
          [0, 0, 0, 0, 1, 0, 0, 0],
          [0, 1, 1, 1, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 1, 0]
        ],
        player: { x: 1, y: 1, directions: ["↓", "→"] }, // Oyuncu başlangıç: (1,1), yönler: aşağı, sağ
        upgrades: [
          { x: 3, y: 4, dir: "↑" },
          { x: 7, y: 0, dir: "↓" },
          { x: 7, y: 6, dir: "←" }
        ]
      },
      {
        map: [ // Seviye 4 haritası   
          [0, 0, 1, 0, 0, 0, 0, 0],
          [0, 0, 1, 0, 1, 1, 1, 0],
          [0, 0, 0, 0, 0, 0, 0, 0],
          [1, 0, 0, 0, 0, 0, 1, 0],
          [0, 0, 0, 0, 1, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 1, 0],
          [0, 1, 1, 0, 0, 0, 1, 0],
          [0, 0, 3, 0, 0, 0, 1, 0]
        ],
        player: { x: 5, y: 5, directions: ["↑", "←"] }, // Oyuncu başlangıç: (5,5), yönler: yukarı, sol
        upgrades: [
          { x: 1, y: 5, dir: "→" },
          { x: 2, y: 3, dir: "↓" },
          { x: 7, y: 4, dir: "↑" },
          { x: 7, y: 0, dir: "←" }
        ]
      },
      {
        map: [ // Seviye 5 haritası  
          [0, 0, 0, 0, 0, 0, 0, 0],
          [0, 0, 0, 1, 0, 0, 0, 0],
          [0, 0, 0, 1, 1, 1, 0, 0],
          [0, 0, 0, 0, 3, 1, 0, 1],
          [0, 0, 1, 1, 1, 1, 0, 0],
          [0, 0, 1, 0, 0, 0, 0, 0],
          [0, 0, 1, 0, 0, 0, 0, 0],
          [0, 0, 0, 0, 0, 0, 0, 0]
        ],
        player: { x: 7, y: 7, directions: ["↑", "←"] }, // Oyuncu başlangıç: (7,7), yönler: yukarı, sol
        upgrades: [
          { x: 5, y: 0, dir: "↓" },
          { x: 4, y: 1, dir: "→" },
          { x: 7, y: 4, dir: "←" },
          { x: 3, y: 7, dir: "↑" },
          { x: 0, y: 2, dir: "→" },
          { x: 2, y: 0, dir: "↓" }
        ]
      }
    ];

    // Oyun durumu değişkenleri
    let currentLevel = 0; // Mevcut seviye numarası
    let map, player, upgrades; // Aktif seviye haritası, oyuncu ve yükseltmeler
    let gameState = 'menu'; // Oyun durumu: menu, playing, gameOver

    // Görsel varlıkları yükler
    function loadAssets(callback) {
      const promises = [];
      // imageFiles nesnesindeki tüm görselleri yükle
      for (const key in imageFiles) {
        if (typeof imageFiles[key] === "string") {
          promises.push(loadImage(key, imageFiles[key]));
        } else {
          for (const dir in imageFiles[key]) {
            promises.push(loadImage(`${key}_${dir}`, imageFiles[key][dir]));
          }
        }
      }
      // Tüm görseller yüklendiğinde
      Promise.all(promises).then(() => {
        callback(); // Ana menüyü göster
        try {
          // Menü müziğini başlat
          lobbyMusic.play().catch((error) => {
            console.error("Lobby müziği oynatılamadı:", error);
            // Hata durumunda, kullanıcı etkileşimiyle müziği denemek için olay dinleyici ekle
            document.addEventListener('click', tryPlayLobbyMusic, { once: true });
          });
        } catch (error) {
          console.error("Lobby müziği başlatma hatası:", error);
        }
      });
    }

    // Kullanıcı tıklamasıyla menü müziğini başlatmayı dener
    function tryPlayLobbyMusic() {
      if (gameState === 'menu') {
        lobbyMusic.play().catch((error) => {
          console.error("Lobby müziği kullanıcı etkileşimiyle oynatılamadı:", error);
        });
      }
    }

    // Tek bir görseli yükler ve assets nesnesine ekler
    function loadImage(key, src) {
      return new Promise((resolve) => {
        const img = new Image();
        img.src = src;
        img.onload = () => {
          assets[key] = img; // Görseli assets nesnesine kaydet
          resolve();
        };
        img.onerror = () => {
          console.error(`Resim yüklenemedi: ${src}`);
          resolve(); // Hata olsa bile devam et
        };
      });
    }

    // Tutorial ekranını gösterir
    function showTutorial() {
      mainMenu.style.display = 'none'; // Ana menüyü gizle
      tutorialScreen.style.display = 'block'; // Tutorial ekranını göster
    }

    // Tutorial ekranını kapatır ve ana menüye döner
    function closeTutorial() {
      tutorialScreen.style.display = 'none'; // Tutorial ekranını gizle
      mainMenu.style.display = 'flex'; // Ana menüyü göster
    }

    // Seviye sayacını günceller
    function updateLevelCounter() {
      levelCounter.textContent = `Seviye ${currentLevel + 1}`; // Mevcut seviye numarasını göster
    }

    // Yeni bir seviyeyi başlatır
    function startLevel(levelNum) {
      currentLevel = levelNum; // Seviye numarasını ayarla
      gameState = 'playing'; // Oyun durumunu oynama moduna geçir
      mainMenu.style.display = 'none'; // Ana menüyü gizle
      levelCounter.style.display = 'block'; // Seviye sayacını göster
      canvas.style.display = 'block'; // Oyun tahtasını göster
      directionUI.style.display = 'flex'; // Yön UI’yi göster
      restartText.style.display = 'block'; // Yeniden başlatma metnini göster
      lobbyMusic.pause(); // Menü müziğini durdur
      levelMusic.currentTime = 0; // Seviye müziğini başa al
      levelMusic.play().catch((error) => {
        console.error("Seviye müziği oynatılamadı:", error);
      });
      resetLevel(); // Seviyeyi başlat
      updateLevelCounter(); // Seviye sayacını güncelle
    }

    // Mevcut seviyeyi sıfırlar (oyuncu, yönler ve yükseltmeler)
    function resetLevel() {
      const level = levels[currentLevel]; // Mevcut seviye verilerini al
      map = JSON.parse(JSON.stringify(level.map)); // Haritayı kopyala
      player = {
        x: level.player.x,
        y: level.player.y,
        directions: [...level.player.directions] // Yönleri kopyala
      };
      upgrades = level.upgrades.map(u => ({ ...u })); // Yükseltmeleri kopyala
      gameOverScreen.style.display = 'none'; // Seviye tamamlama ekranını gizle
      gameCompleteScreen.style.display = 'none'; // Oyun sonu ekranını gizle
      canvas.style.display = 'block'; // Oyun tahtasını göster
      directionUI.style.display = 'flex'; // Yön UI’yi göster
      restartText.style.display = 'block'; // Yeniden başlatma metnini göster
      draw(); // Tahtayı çiz
      updateDirectionUI(); // Yön UI’yi güncelle
      updateLevelCounter(); // Seviye sayacını güncelle
    }

    // Oyun tahtasını çizer
    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height); // Canvas’ı temizle
      ctx.drawImage(assets.board, 0, 0, canvas.width, canvas.height); // Tahtayı çiz

      // Haritadaki her hücreyi tara
      for (let y = 0; y < 8; y++) {
        for (let x = 0; x < 8; x++) {
          if (map[y][x] === 1) {
            // Duvar çiz
            ctx.drawImage(assets.wall, x * cellSize, y * cellSize, cellSize, cellSize);
          } else if (map[y][x] === 3) {
            // Hedef çiz
            ctx.drawImage(assets.goal, x * cellSize, y * cellSize, cellSize, cellSize);
          }
        }
      }

      // Yükseltmeleri çiz
      for (const up of upgrades) {
        const img = assets[up.dir];
        ctx.drawImage(img, up.x * cellSize, up.y * cellSize, cellSize, cellSize);
      }

      // Oyuncuyu çiz
      ctx.drawImage(assets.player, player.x * cellSize, player.y * cellSize, cellSize, cellSize);
    }

    // Oyuncuyu belirtilen yönde hareket ettirir
    function move(dx, dy, dir) {
      const nx = player.x + dx; // Yeni X koordinatı
      const ny = player.y + dy; // Yeni Y koordinatı
      // Hareket sınırlar dışındaysa, geçersiz yönse veya duvara çarpıyorsa çık
      if (nx < 0 || nx >= 8 || ny < 0 || ny >= 8) return;
      if (!player.directions.includes(dir)) return;
      if (map[ny][nx] === 1) return;

      player.x = nx; // Oyuncunun X koordinatını güncelle
      player.y = ny; // Oyuncunun Y koordinatını güncelle

      // Yükseltme kontrolü
      const index = upgrades.findIndex(u => u.x === nx && u.y === ny);
      if (index !== -1) {
        upgradeSound.currentTime = 0; // Yükseltme sesini başa al
        upgradeSound.play().catch((error) => {
          console.error("Yükseltme sesi oynatılamadı:", error);
        });
        const newDir = upgrades[index].dir; // Yeni yön
        const dirIndex = player.directions.indexOf(dir); // Mevcut yönün indeksi
        if (dirIndex !== -1) {
          player.directions[dirIndex] = newDir; // Yönü değiştir
        }
        upgrades.splice(index, 1); // Yükseltmeyi kaldır
      }

      // Hedefe ulaşıldıysa
      if (map[ny][nx] === 3) {
        map[ny][nx] = 0; // Hedefi kaldır
        levelMusic.pause(); // Seviye müziğini durdur
        levelCompleteSound.currentTime = 0; // Tamamlama sesini başa al
        levelCompleteSound.play().catch((error) => {
          console.error("Seviye tamamlama sesi oynatılamadı:", error);
        });
        gameState = 'gameOver'; // Oyun durumunu güncelle
        canvas.style.display = 'none'; // Tahtayı gizle
        directionUI.style.display = 'none'; // Yön UI’yi gizle
        levelCounter.style.display = 'none'; // Seviye sayacını gizle
        restartText.style.display = 'none'; // Yeniden başlatma metnini gizle
        // Son seviye mi?
        if (currentLevel + 1 >= levels.length) {
          gameCompleteScreen.style.display = 'block'; // Oyun sonu ekranını göster
        } else {
          gameOverScreen.style.display = 'block'; // Seviye tamamlama ekranını göster
        }
        return;
      }

      draw(); // Tahtayı yeniden çiz
      updateDirectionUI(); // Yön UI’yi güncelle
    }

    // Bir sonraki seviyeye geçer
    function nextLevel() {
      currentLevel++; // Seviye numarasını artır
      if (currentLevel < levels.length) {
        gameState = 'playing'; // Oyun durumunu oynama moduna geçir
        gameOverScreen.style.display = 'none'; // Seviye tamamlama ekranını gizle
        canvas.style.display = 'block'; // Tahtayı göster
        directionUI.style.display = 'flex'; // Yön UI’yi göster
        levelCounter.style.display = 'block'; // Seviye sayacını göster
        restartText.style.display = 'block'; // Yeniden başlatma metnini göster
        levelMusic.currentTime = 0; // Seviye müziğini başa al
        levelMusic.play().catch((error) => {
          console.error("Seviye müziği oynatılamadı:", error);
        });
        resetLevel(); // Yeni seviyeyi başlat
        updateLevelCounter(); // Seviye sayacını güncelle
      } else {
        gameState = 'gameOver'; // Oyun durumunu güncelle
        gameOverScreen.style.display = 'none'; // Seviye tamamlama ekranını gizle
        gameCompleteScreen.style.display = 'block'; // Oyun sonu ekranını göster
        levelCounter.style.display = 'none'; // Seviye sayacını gizle
        restartText.style.display = 'none'; // Yeniden başlatma metnini gizle
        lobbyMusic.currentTime = 0; // Menü müziğini başa al
        lobbyMusic.play().catch((error) => {
          console.error("Lobby müziği oynatılamadı:", error);
        });
      }
    }

    // Ana menüye döner
    function returnToMenu() {
      gameState = 'menu'; // Oyun durumunu menü moduna geçir
      currentLevel = 0; // Seviye numarasını sıfırla
      gameOverScreen.style.display = 'none'; // Seviye tamamlama ekranını gizle
      gameCompleteScreen.style.display = 'none'; // Oyun sonu ekranını gizle
      mainMenu.style.display = 'flex'; // Ana menüyü göster
      levelCounter.style.display = 'none'; // Seviye sayacını gizle
      canvas.style.display = 'none'; // Tahtayı gizle
      directionUI.style.display = 'none'; // Yön UI’yi gizle
      restartText.style.display = 'none'; // Yeniden başlatma metnini gizle
      levelMusic.pause(); // Seviye müziğini durdur
      lobbyMusic.currentTime = 0; // Menü müziğini başa al
      lobbyMusic.play().catch((error) => {
        console.error("Lobby müziği oynatılamadı:", error);
      });
    }

    // Yön UI’yi günceller: Aktif yönleri gösterir
    function updateDirectionUI() {
      document.getElementById("ui-up").innerHTML = ""; // Üst satırı temizle
      document.getElementById("ui-middle").innerHTML = ""; // Orta satırı temizle

      // Yukarı yön tuşu
      const up = document.createElement("img");
      up.src = player.directions.includes("↑") ? assets["dirUI_↑"].src : assets["dirUI_base"].src;
      document.getElementById("ui-up").appendChild(up);

      // Sol yön tuşu
      const left = document.createElement("img");
      left.src = player.directions.includes("←") ? assets["dirUI_←"].src : assets["dirUI_base"].src;

      // Aşağı yön tuşu
      const down = document.createElement("img");
      down.src = player.directions.includes("↓") ? assets["dirUI_↓"].src : assets["dirUI_base"].src;

      // Sağ yön tuşu
      const right = document.createElement("img");
      right.src = player.directions.includes("→") ? assets["dirUI_→"].src : assets["dirUI_base"].src;

      // Orta satıra sol, aşağı, sağ tuşlarını ekle
      const middleRow = document.getElementById("ui-middle");
      middleRow.appendChild(left);
      middleRow.appendChild(down);
      middleRow.appendChild(right);
    }

    // Klavye girişlerini dinler
    document.addEventListener("keydown", (e) => {
      if (gameState !== 'playing') return; // Oyun oynanmıyorsa çık
      switch (e.key) {
        case "ArrowLeft": move(-1, 0, "←"); break; // Sol ok: Sola hareket
        case "ArrowRight": move(1, 0, "→"); break; // Sağ ok: Sağa hareket
        case "ArrowUp": move(0, -1, "↑"); break; // Yukarı ok: Yukarı hareket
        case "ArrowDown": move(0, 1, "↓"); break; // Aşağı ok: Aşağı hareket
        case "r":
        case "R":
          resetLevel(); // R tuşu: Seviyeyi sıfırla
          break;
      }
    });

    // Oyun başlangıcı: Görselleri yükle ve ana menüyü göster
    loadAssets(() => {
      mainMenu.style.display = 'flex';
    });
  </script>
</body>
</html>
```
