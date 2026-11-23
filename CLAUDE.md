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
- Vault: istekler `C:/Users/demir/Obsidian/Obsidian Vault/Projects/desktop-window-keys/requests/`,
  proje kartı `knowledge/projects/desktop-window-keys.md`. İş seçmek için `/brifing`.
