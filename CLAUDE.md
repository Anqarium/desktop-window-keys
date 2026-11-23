# desktop-window-keys

Sanal masaüstleri arasında pencere taşıma ve sabitleme için Windhawk modu (C++, tek dosya
`desktop-window-keys.wh.cpp`). Davranış ve kararlar için `README.md`'ye bak; burada yalnız
çalışma kuralları var.

- Dil: açıklamalar, dokümantasyon ve commit mesajları Türkçe (Conventional Commits). Kod
  yorumları ve mod meta verisi (`==WindhawkMod==`, ayar adları) İngilizce, Windhawk geleneği.
- Kaynak mod: `ramensoftware/windhawk-mods` commit `dc9cd28`, `mods/virtual-desktop-helper.wh.cpp`.
  Yalnız gereken kısımları al (COM arayüzleri, sürüm IID tablosu, kısayol iş parçacığı,
  pin); numaralı masaüstü kısayolları gibi kullanılmayan özellikleri taşıma. Kaynağa atıfı
  mod readme'sinde koru.
- Belgelenmemiş COM arayüzlerinin IID'leri Windows sürümüne göre değişir; yeni bir sürüm
  eklerken kaynağı belirt (ör. VirtualDesktopAccessor).
- Doğrulama: Windhawk'ta derle, gerçek masaüstlerinde kısayolları dene, Windhawk log'unda
  `RegisterHotKey` sonuçlarına bak (Win tuşlu kombinasyonların kaydı ayrıca kontrol edilir).
  Commit öncesi derleme kontrolü Windhawk dışından da yapılabilir: `C:\Program Files\Windhawk\Compiler\bin\clang++.exe`
  ile `Compiler\compile_flags.txt` bayrakları + `-DWH_MOD_ID=L"desktop-window-keys" -DWH_MOD_VERSION=L"x" -Wall -c`
  (link adımı `InternalWh_*` sembolleri yüzünden Windhawk dışında başarısız olur, bu beklenir).
- Mod hiç tepki vermiyorsa önce süreç listesinde `windhawk.exe -tool-mod "local@desktop-window-keys"`
  var mı bak; yoksa sorun kod değil, sürecin başlamaması. Log için editörde "Enable logging" açık olmalı.
- Yönetici yetkili pencere öndeyken `SendInput` UIPI ile sessizce düşer (dönüş değeri başarılı);
  Windhawk 1.7.3'te çözümü yok, kod bunu `CanInjectInputTo` ile önceden tespit eder.
- Vault: istekler `C:/Users/demir/Obsidian/Obsidian Vault/Projects/desktop-window-keys/requests/`,
  proje kartı `knowledge/projects/desktop-window-keys.md`. İş seçmek için `/brifing`.
