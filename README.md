# desktop-window-keys

Windows 11 sanal masaüstleri için bir Windhawk modu. Etkin pencereyi klavye kısayoluyla
komşu masaüstüne taşır ve pencereyi tüm masaüstlerine sabitler.

## Davranış (kararlar, 2026-11-23)

| Kısayol | İşlem |
|---|---|
| `Ctrl+Win+Shift+Sol` / `Sağ` | Etkin pencereyi önceki / sonraki masaüstüne taşı |
| `Ctrl+Win+Shift+Üst` / `Alt` | Etkin pencereyi tüm masaüstlerine sabitle / sabitlemeyi kaldır |

- **Ayar: "Taşınan pencereyi takip et".** İşaretliyse pencereyle birlikte hedef masaüstüne
  geçilir. İşaretli değilse yalnız pencere gider, kullanıcı bulunduğu masaüstünde kalır.
- Kısayollar sabit: modun kaynak aldığı modeldeki Alt tabanlı varsayılanlar kullanılmaz. Bir
  kısayol başka bir uygulama tarafından kullanılıyorsa kayıt başarısızlığı loglanır.
- Windows'ta bu işlemlerin yerleşik karşılığı yalnızca Görev Görünümü'ndeki (Win+Tab) sağ tık
  menüsü ("Move to", "Show this window on all desktops"); kısayol yok.

## Kaynak

Sıfırdan yazılmadı: [u2x1/virtual-desktop-helper](https://github.com/ramensoftware/windhawk-mods/blob/dc9cd28419f63d2d86396bcb845cf8e307186d5e/mods/virtual-desktop-helper.wh.cpp)
(v2.5.0, VD.ahk tabanlı) modunun işe yarayan kısımları (belgelenmemiş sanal masaüstü COM
arayüzleri, Windows sürümüne göre IID tablosu, kısayol iş parçacığı, pin) alınıp sadeleştirilir.
`windhawk-mods` deposunda lisans dosyası yok; repo herkese açılmadan veya mod yayımlanmadan
önce lisans durumu netleştirilmeli.

## Kurulum

Windhawk → "Create a new mod" → `desktop-window-keys.wh.cpp` içeriğini yapıştır → derle ve
etkinleştir. Ayarlardan Windows sürümünü seç (`winver`).
