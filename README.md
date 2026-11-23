# desktop-window-keys

Windows 11 sanal masaüstleri için bir Windhawk modu. Etkin pencereyi klavye kısayoluyla
komşu masaüstüne taşır ve pencereyi tüm masaüstlerine sabitler.

## Davranış (kararlar, 2026-11-23)

| Kısayol | İşlem |
|---|---|
| `Ctrl+Win+Shift+Sol` / `Sağ` | Etkin pencereyi önceki / sonraki masaüstüne taşı |
| `Ctrl+Win+Shift+Üst` / `Alt` | Etkin pencereyi tüm masaüstlerine sabitle / sabitlemeyi kaldır |

- **Kenarda döngü:** son masaüstünde Sağ ilk masaüstüne, ilk masaüstünde Sol son masaüstüne
  taşır. Kullanıcının kullandığı [Virtual Desktop Hotkey Cycle](https://github.com/ramensoftware/windhawk-mods/blob/910d825f1c812f1f50da53a5d28c226581e0bf2e/mods/virtual-desktop-hotkey-cycle.wh.cpp)
  modu Win+Ctrl+Sol/Sağ geçişini de böyle döndürür; ikisi tutarlı kalır.
- **Ayar: "Taşınan pencereyi takip et".** İşaretliyse pencereyle birlikte hedef masaüstüne
  geçilir. İşaretli değilse yalnız pencere gider, kullanıcı bulunduğu masaüstünde kalır.
- **Kenarda animasyon yönü:** Takip açıkken kenardan dönüşte geçiş Explorer'ın Win+Ctrl+Ok
  kısayolu enjekte edilerek yapılır; animasyon basılan yöne kayar, döngüyü Virtual Desktop
  Hotkey Cycle yapar. Öndeki pencere yönetici yetkiliyse Windows (UIPI) enjeksiyonu engeller;
  bu durumda COM geçişi kullanılır ve animasyon ters yöne kayar. Windhawk 1.7.3'te çözümü
  yok; 2.0'ın UIAccess süreci (`@include windhawk-mod-uiaccess.exe`, alpha'da) bunu kaldırır.
- **Sabitleme durum atar, değiştirmez (toggle değil):** Üst her zaman sabitler, Alt her zaman
  kaldırır; zaten o durumdaki pencerede bir şey yapmaz. Sabitleme `IVirtualDesktopPinnedApps`
  (`PinView`/`UnpinView`) ile yapılır; IID'si Windows sürümüne göre değişmez, servis alınamazsa
  yalnız sabitleme kısayolları devre dışı kalır, taşıma çalışır.
- **Sabitleme rozeti:** Kısayolla sabitlenen pencerenin sağ üst köşesinde Windows vurgu
  renginde küçük, yarı saydam, tıklamayı geçiren bir nokta durur. Nokta modun kendi penceresidir
  (katmanlı, `WS_EX_TRANSPARENT`) ve Z sırasında hedefin hemen üstünde tutulur. Böylece büyütülmüş
  ve tam ekran pencerede de görünür, üstüne gelen pencerelerin altında kalır.
  `SetWinEventHook` ile konum, ön plan, küçültme ve yok olma izlenir. Hook'lar yalnız rozet
  varken açıktır. Saniyelik bir denetim Görev Görünümü'nden kaldırılan sabitlemeyi ve kapanan
  pencereyi yakalar.
  - Kenarlık rengi (`DWMWA_BORDER_COLOR`) denendi, bırakıldı: büyütülmüş ve tam ekran pencerede
    kenarlık görünmüyor, yönetici pencerelerinde de UIPI çağrıyı reddediyor.
  - Yalnız Görev Görünümü'nden sabitlenen pencereler rozet almaz.
  - Yönetici yetkili pencerenin (ör. Windhawk editörü) yanına Z sırasında yerleştirme UIPI
    yüzünden `ERROR_ACCESS_DENIED` verir. O pencerede rozet yalnız pencere öndeyken
    `HWND_TOPMOST` olarak görünür, öbür zamanlar gizlenir.
- Kısayollar sabit: modun kaynak aldığı modeldeki Alt tabanlı varsayılanlar kullanılmaz. Bir
  kısayol başka bir uygulama tarafından kullanılıyorsa kayıt başarısızlığı loglanır.
- Windows'ta bu işlemlerin yerleşik karşılığı yalnızca Görev Görünümü'ndeki (Win+Tab) sağ tık
  menüsü ("Move to", "Show this window on all desktops"); kısayol yok.

## Kaynak

Sıfırdan yazılmadı: [u2x1/virtual-desktop-helper](https://github.com/ramensoftware/windhawk-mods/blob/dc9cd28419f63d2d86396bcb845cf8e307186d5e/mods/virtual-desktop-helper.wh.cpp)
(v2.5.0, VD.ahk tabanlı) modunun işe yarayan kısımları (belgelenmemiş sanal masaüstü COM
arayüzleri, Windows sürümüne göre IID tablosu, kısayol iş parçacığı, pin) alınıp sadeleştirilir.
## Lisans

[MIT](LICENSE). Kaynak modun lisansı belirtilmemiş (`windhawk-mods` deposunda lisans dosyası
yok); ondan alınan kısımların hakkı yazarına (u2x1) aittir ve atıf mod readme'sinde korunur.

## Kurulum

Windhawk → "Create a new mod" → `desktop-window-keys.wh.cpp` içeriğini yapıştır → derle ve
etkinleştir. Ayarlardan Windows sürümünü seç (`winver`).
