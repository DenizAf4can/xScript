# xScript Kütüphane Dökümantasyonu

**Sürüm**: 1.05

**Açıklama**: xScript, Roblox exploitleri için tasarlanmış güçlü bir kütüphanedir. Oyuncular, karakterler, parçalar, GUI elemanları ve daha fazlasıyla etkileşim kurmak ve manipüle etmek için geniş bir fonksiyon yelpazesi sunar. Bu dökümantasyon, her fonksiyonun parametreleri, dönüş değerleri ve kullanım notları dahil olmak üzere ayrıntılı bilgi sağlar.

**Not**: Bazı fonksiyonlar, exploitörün sağladığı belirli özelliklere veya fonksiyonlara (örn. `getclipboard`, `setclipboard`, `mouse_move`) dayanır. Tam işlevsellik için exploitörünüzün bu özellikleri desteklediğinden emin olun.

## İçindekiler
- Oyuncu Fonksiyonları
- Karakter Fonksiyonları
- Parça Fonksiyonları
- Örnek Fonksiyonları
- Fare ve Giriş Fonksiyonları
- Yardımcı Fonksiyonlar
- ESP ve Görsel Fonksiyonlar
- Webhook ve Ağ Fonksiyonları

---

## Oyuncu Fonksiyonları

### `xScript.GetLocalPlayer()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Oyuncu - Yerel oyuncu nesnesi.
- **Açıklama**: Players servisinden yerel oyuncu nesnesini döndürür.

### `xScript.GetPlayer(playerName)`
- **Parametreler**: 
  - `playerName`: String - Bulunacak oyuncunun adı.
- **Dönüş Değeri**: Oyuncu veya nil - Verilen isme sahip oyuncu nesnesi, bulunamazsa nil.
- **Açıklama**: Players servisinden isme göre oyuncu nesnesini bulur ve döndürür.

### `xScript.GetPlayerPosition(playerName)`
- **Parametreler**: 
  - `playerName`: String - Oyuncunun adı.
- **Dönüş Değeri**: Vector3 veya nil - Oyuncunun HumanoidRootPart pozisyonu, bulunamazsa nil.
- **Açıklama**: Belirtilen oyuncunun karakter pozisyonunu alır.
- **Notlar**: Oyuncu, karakter veya HumanoidRootPart bulunamazsa nil döner.

### `xScript.GetNearestPlayer(maxDistance)`
- **Parametreler**: 
  - `maxDistance`: Number (isteğe bağlı) - Dikkate alınacak maksimum mesafe. Varsayılan sonsuz.
- **Dönüş Değeri**: Oyuncu veya nil - Belirtilen mesafe içindeki en yakın oyuncu, yoksa nil.
- **Açıklama**: Yerel oyuncuya en yakın oyuncuyu belirtilen mesafe içinde bulur.
- **Notlar**: Yerel oyuncuyu hariç tutar. Yerel karakterin HumanoidRootPart'ını gerektirir.

### `xScript.GetPlayersInRadius(centerReference, radius)`
- **Parametreler**: 
  - `centerReference`: Herhangi - Merkez nokta (Vector3, CFrame, BasePart veya Model olabilir).
  - `radius`: Number - Arama yarıçapı.
- **Dönüş Değeri**: Tablo - Belirtilen yarıçap içindeki Oyuncu nesnelerinin listesi.
- **Açıklama**: Merkez noktadan verilen yarıçap içinde karakterleri bulunan tüm oyuncuları döndürür.
- **Notlar**: Mesafe hesaplaması için HumanoidRootPart pozisyonunu kullanır. Merkez referansı geçersizse boş tablo döner.

### `xScript.PlayerList()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Tablo - Oyundaki tüm oyuncu isimlerinin listesi.
- **Açıklama**: Şu anda oyunda olan tüm oyuncuların isimlerini içeren bir tablo döndürür.

---

## Karakter Fonksiyonları

### `xScript.GetLocalCharacter()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Model veya nil - Yerel oyuncunun karakter modeli, bulunamazsa nil.
- **Açıklama**: Yerel oyuncunun karakter modelini döndürür.

### `xScript.GetCharacter(playerName)`
- **Parametreler**: 
  - `playerName`: String - Oyuncunun adı.
- **Dönüş Değeri**: Model veya nil - Belirtilen oyuncunun karakter modeli, bulunamazsa nil.
- **Açıklama**: Belirtilen oyuncunun karakter modelini alır.

### `xScript.GetHealth(playerName)`
- **Parametreler**: 
  - `playerName`: String - Oyuncunun adı.
- **Dönüş Değeri**: Number veya nil - Oyuncunun humanoid sağlık değeri, bulunamazsa nil.
- **Açıklama**: Belirtilen oyuncunun humanoid sağlık değerini alır.
- **Notlar**: Oyuncu, karakter veya humanoid bulunamazsa nil döner.

### `xScript.GetWalkspeed(playerName)`
- **Parametreler**: 
  - `playerName`: String - Oyuncunun adı.
- **Dönüş Değeri**: Number veya nil - Oyuncunun humanoid yürüme hızı, bulunamazsa nil.
- **Açıklama**: Belirtilen oyuncunun karakterinin yürüme hızını alır.
- **Notlar**: Oyuncu, karakter veya humanoid bulunamazsa nil döner.

### `xScript.GetJumpPower(playerName)`
- **Parametreler**: 
  - `playerName`: String - Oyuncunun adı.
- **Dönüş Değeri**: Number veya nil - Oyuncunun humanoid zıplama gücü, bulunamazsa nil.
- **Açıklama**: Belirtilen oyuncunun karakterinin zıplama gücünü alır.
- **Notlar**: Oyuncu, karakter veya humanoid bulunamazsa nil döner.

### `xScript.GetCharacterHeadPosition(playerName)`
- **Parametreler**: 
  - `playerName`: String - Oyuncunun adı.
- **Dönüş Değeri**: Vector3 veya nil - Oyuncunun baş parçasının pozisyonu, bulunamazsa nil.
- **Açıklama**: Belirtilen oyuncunun baş pozisyonunu alır.
- **Notlar**: Oyuncu, karakter veya baş parçası bulunamazsa nil döner.

### `xScript.GetPartUnderPlayer(playerName)`
- **Parametreler**: 
  - `playerName`: String - Oyuncunun adı.
- **Dönüş Değeri**: BasePart veya nil - Oyuncunun HumanoidRootPart'ının altındaki parça, yoksa nil.
- **Açıklama**: Raycasting kullanarak belirtilen oyuncunun karakterinin altındaki parçayı bulur.
- **Notlar**: Oyuncunun kendi karakterini raycast'ten hariç tutar.

### `xScript.SetLocalPlayerPosition(vector3)`
- **Parametreler**: 
  - `vector3`: Vector3 - Yerel oyuncunun karakteri için yeni pozisyon.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel oyuncunun karakterini belirtilen pozisyona ışınlar.
- **Notlar**: HumanoidRootPart'ın CFrame'ini ayarlar. Karakter veya HumanoidRootPart bulunamazsa uyarır.

### `xScript.SetHealth(number)`
- **Parametreler**: 
  - `number`: Number - Yeni sağlık değeri.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel oyuncunun humanoid sağlık değerini ayarlar.
- **Notlar**: Yerel karakter veya humanoid bulunamazsa uyarır.

### `xScript.SetWalkspeed(number, bypass)`
- **Parametreler**: 
  - `number`: Number - Yeni yürüme hızı değeri.
  - `bypass`: Boolean (isteğe bağlı) - True ise, metamethod hook ile yürüme hızını 16'ya zorlar. Varsayılan false.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel oyuncunun humanoid yürüme hızını ayarlar.
- **Notlar**: `bypass` true ise, metamethod hook kullanarak yürüme hızını 16 olarak override eder. Humanoid bulunamazsa uyarır.

### `xScript.SetJumpPower(number, bypass)`
- **Parametreler**: 
  - `number`: Number - Yeni zıplama gücü değeri.
  - `bypass`: Boolean (isteğe bağlı) - True ise, metamethod hook ile zıplama gücünü 50'ye zorlar. Varsayılan false.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel oyuncunun humanoid zıplama gücünü ayarlar.
- **Notlar**: `bypass` true ise, metamethod hook kullanarak zıplama gücünü 50 olarak override eder. Humanoid bulunamazsa uyarır.

### `xScript.FreezeLocalCharacter(enable)`
- **Parametreler**: 
  - `enable`: Boolean - Yerel karakteri dondurmak veya çözmek için.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel karakteri dondurur: yürüme hızını 0'a, zıplama gücünü 0'a ayarlar, PlatformStand'i etkinleştirir ve HumanoidRootPart'ı anchorlar.
- **Notlar**: Devre dışı bırakıldığında önceki ayarları geri yükler. Humanoid veya HumanoidRootPart bulunamazsa uyarır.

### `xScript.Fly(enable, speed)`
- **Parametreler**: 
  - `enable`: Boolean - Uçmayı etkinleştirmek veya devre dışı bırakmak için.
  - `speed`: Number (isteğe bağlı) - Uçma hızı. Varsayılan 100.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel karakter için uçmayı etkinleştirir, WASDQE tuşlarıyla tüm yönlerde hareket sağlar.
- **Notlar**: Kapatıldığında uçmayı devre dışı bırakır ve yürüme hızını geri yükler. Karakter, humanoid veya HumanoidRootPart bulunamazsa uyarır.

### `xScript.InfiniteJump(enable)`
- **Parametreler**: 
  - `enable`: Boolean - Sonsuz zıplamayı etkinleştirmek veya devre dışı bırakmak için.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel karakterin havadayken sonsuz zıplamasına izin verir, FreeFalling durumunu algılar.
- **Notlar**: Humanoid bulunamazsa uyarır.

### `xScript.ForceJump()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel karakterin humanoid durumunu değiştirerek zıplamasını sağlar.
- **Notlar**: Humanoid bulunamazsa uyarır.

### `xScript.RespawnLocalPlayer()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Boolean - Başarılıysa true, değilse false.
- **Açıklama**: Yerel oyuncunun karakterini yeniden yükleyerek respawn eder.
- **Notlar**: Yerel oyuncu bulunamazsa uyarır.

### `xScript.Kill()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel karakterin sağlığını 0'a ayarlayarak öldürür.
- **Notlar**: Humanoid bulunamazsa uyarır.

---

## Parça Fonksiyonları

### `xScript.GetPosition(object)`
- **Parametreler**: 
  - `object`: Herhangi - Pozisyonu alınacak nesne (BasePart, Model, CFrame veya Vector3).
- **Dönüş Değeri**: Vector3 veya nil - Nesnenin pozisyonu, geçersizse nil.
- **Açıklama**: Çeşitli nesne türlerinden pozisyonu alır.
- **Notlar**: Modeller için PrimaryPart'ın pozisyonunu kullanır. Geçersiz nesne türleri için nil döner.

### `xScript.GetNearestPart(options)`
- **Parametreler**: 
  - `options`: Tablo (isteğe bağlı) - Filtreleme seçenekleri: `maxDistance`, `excludePlayerCharacters`, `includeInvisible`, `includeUncollidable`, `classNames`, `nameFilter`, `filterFunction`.
- **Dönüş Değeri**: BasePart veya nil - Kriterlere uyan en yakın parça, yoksa nil.
- **Açıklama**: Yerel karakterin pozisyonundan workspace'teki en yakın parçayı bulur.
- **Notlar**: Yerel karakterin HumanoidRootPart'ını gerektirir. Seçenekler için koda bakın.

### `xScript.GetAllPartsInRadius(centerReference, radius, options)`
- **Parametreler**: 
  - `centerReference`: Herhangi - Merkez nokta (Vector3, CFrame, BasePart veya Model).
  - `radius`: Number - Arama yarıçapı.
  - `options`: Tablo (isteğe bağlı) - `GetNearestPart`'a benzer filtreleme seçenekleri.
- **Dönüş Değeri**: Tablo - Yarıçap içindeki kriterlere uyan BasePart'ların listesi.
- **Açıklama**: Merkez noktadan belirtilen yarıçap içindeki tüm parçaları döndürür.
- **Notlar**: Merkez referansı geçersizse boş tablo döner. Seçenekler için koda bakın.

### `xScript.SetPosition(targetObject, vector3)`
- **Parametreler**: 
  - `targetObject`: BasePart veya Model - Taşınacak nesne.
  - `vector3`: Vector3 - Yeni pozisyon.
- **Dönüş Değeri**: Yok
- **Açıklama**: Hedef nesneyi belirtilen pozisyona taşır.
- **Notlar**: Modeller için PrimaryPart'ın CFrame'ini ayarlar. Nesne taşınamazsa veya PrimaryPart eksikse uyarır.

### `xScript.HighlightPart(part, color, duration)`
- **Parametreler**: 
  - `part`: BasePart - Vurgulanacak parça.
  - `color`: Color3 (isteğe bağlı) - Vurgu rengi. Varsayılan sarı (RGB: 255, 255, 0).
  - `duration`: Number (isteğe bağlı) - Vurgunun kalacağı süre (saniye). Belirtilmezse kalıcı.
- **Dönüş Değeri**: SelectionBox veya nil - Oluşturulan SelectionBox örneği, geçersizse nil.
- **Açıklama**: Belirtilen parçaya SelectionBox kullanarak vurgu efekti ekler.
- **Notlar**: Parçadaki mevcut vurguları kaldırır. Parça geçersizse uyarır.

---

## Örnek Fonksiyonları

### `xScript.GetChildrenOfType(instance, className)`
- **Parametreler**: 
  - `instance`: Instance - Aranacak ebeveyn örneği.
  - `className`: String - Filtreleme için sınıf adı.
- **Dönüş Değeri**: Tablo - Belirtilen sınıfa sahip çocukların listesi.
- **Açıklama**: Örnekteki belirtilen sınıfa sahip tüm doğrudan çocukları döndürür.
- **Notlar**: Örnek veya className geçersizse boş tablo döner.

### `xScript.GetDescendantsOfType(instance, className)`
- **Parametreler**: 
  - `instance`: Instance - Aranacak ebeveyn örneği.
  - `className`: String - Filtreleme için sınıf adı.
- **Dönüş Değeri**: Tablo - Belirtilen sınıfa sahip torunların listesi.
- **Açıklama**: Örnekteki belirtilen sınıfa sahip tüm torunları döndürür.
- **Notlar**: Örnek veya className geçersizse boş tablo döner.

### `xScript.FindInstance(name, parent, recursive, classHint)`
- **Parametreler**: 
  - `name`: String - Aranacak isim (büyük/küçük harf duyarsız).
  - `parent`: Instance - Aranacak ebeveyn örneği.
  - `recursive`: Boolean (isteğe bağlı) - Özyinelemeli arama. Varsayılan false.
  - `classHint`: String veya Tablo (isteğe bağlı) - Filtreleme için sınıf adı(ları).
- **Dönüş Değeri**: Instance veya nil - İlk eşleşen örnek, bulunamazsa nil.
- **Açıklama**: Ebeveyn içinde isme göre örnek arar, isteğe bağlı özyineleme ve sınıf filtreleme ile.
- **Notlar**: Ebeveyn veya isim geçersizse nil döner.

---

## Fare ve Giriş Fonksiyonları

### `xScript.GetMousePosition()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Vector2 - Ekrandaki mevcut fare pozisyonu.
- **Açıklama**: UserInputService kullanarak fare imlecinin mevcut pozisyonunu döndürür.
- **Notlar**: UserInputService mevcut değilse (0,0) döner ve uyarır.

### `xScript.MouseMove(x, y)`
- **Parametreler**: 
  - `x`: Number - Fareyi taşınacak x koordinatı.
  - `y`: Number - Fareyi taşınacak y koordinatı.
- **Dönüş Değeri**: Yok
- **Açıklama**: Fare imlecini belirtilen koordinatlara taşır.
- **Notlar**: Exploitörde `mouse_move` fonksiyonunu gerektirir. Mevcut değilse uyarır.

### `xScript.MouseDown(button)`
- **Parametreler**: 
  - `button`: Enum.UserInputType - Basılacak fare düğmesi (MouseButton1, MouseButton2, MouseButton3).
- **Dönüş Değeri**: Yok
- **Açıklama**: Belirtilen fare düğmesine basılmasını simüle eder.
- **Notlar**: Exploitör fonksiyonları (`mouse1down` gibi) gerektirir. Mevcut değilse veya düğme geçersizse uyarır.

---

## Yardımcı Fonksiyonlar

### `xScript.GetClipboard()`
- **Parametreler**: Yok
- **Dönüş Değeri**: String - Mevcut pano içeriği, mevcut değilse boş string.
- **Açıklama**: Panodaki mevcut içeriği alır.
- **Notlar**: `getclipboard` fonksiyonunu gerektirir. Mevcut değilse uyarır ve "" döner.

### `xScript.SetClipboard(text)`
- **Parametreler**: 
  - `text`: String - Panoya ayarlanacak metin.
- **Dönüş Değeri**: Yok
- **Açıklama**: Pano içeriğini belirtilen metne ayarlar.
- **Notlar**: `setclipboard` fonksiyonunu gerektirir. Mevcut değilse uyarır.

### `xScript.GetHwid()`
- **Parametreler**: Yok
- **Dönüş Değeri**: String - İstemcinin donanım kimliği.
- **Açıklama**: RbxAnalyticsService kullanarak istemcinin donanım kimliğini döndürür.

---

## ESP ve Görsel Fonksiyonlar

### `xScript.ToggleXRay(enable, targetTransparency, excludeCharacters)`
- **Parametreler**: 
  - `enable`: Boolean - XRay efektini etkinleştirmek veya devre dışı bırakmak için.
  - `targetTransparency`: Number (isteğe bağlı) - Etkinleştirildiğinde parçalar için şeffaflık değeri (0-1). Varsayılan 0.6.
  - `excludeCharacters`: Boolean (isteğe bağlı) - Oyuncu karakterlerini hariç tutmak için. Varsayılan true.
- **Dönüş Değeri**: Yok
- **Açıklama**: Workspace'teki tüm parçaları şeffaf yapar (XRay efekti), isteğe bağlı olarak oyuncu karakterlerini hariç tutar.
- **Notlar**: Devre dışı bırakıldığında orijinal şeffaflığı geri yükler. targetTransparency geçersizse uyarır.

### `xScript.AttachESP(targetPart, type, options)`
- **Parametreler**: 
  - `targetPart`: BasePart veya Humanoid - ESP eklenecek hedef.
  - `type`: String - ESP türü ("Billboard" veya "Highlight").
  - `options`: Tablo (isteğe bağlı) - `Color`, `Text`, `Duration` gibi seçenekler.
- **Dönüş Değeri**: Instance veya nil - Oluşturulan ESP örneği (BillboardGui veya SelectionBox), geçersizse nil.
- **Açıklama**: Hedefe ESP efekti (Billboard veya Highlight) ekler.
- **Notlar**: Billboard, Humanoid'ler için Head kullanır. Seçenekler için koda bakın. Geçersizse uyarır.

---

## Webhook ve Ağ Fonksiyonları

### `xScript.CreateWebSocket(url)`
- **Parametreler**: 
  - `url`: String - Bağlanılacak WebSocket URL'si.
- **Dönüş Değeri**: Tablo veya nil - WebSocket istemci nesnesi, başarısız olursa nil.
- **Açıklama**: `Send`, `Close` metodları ve `OnMessage`, `OnClose`, `OnError` olayları ile WebSocket bağlantısı oluşturur.
- **Notlar**: Exploitör WebSocket desteğini gerektirir. Mevcut değilse veya bağlantı başarısız olursa uyarır.

### `xScript.SendWebhook(webhook, message)`
- **Parametreler**: 
  - `webhook`: String - Discord webhook URL'si.
  - `message`: String - Gönderilecek mesaj.
- **Dönüş Değeri**: Yok
- **Açıklama**: Belirtilen Discord webhook'una düz metin mesajı gönderir.
- **Notlar**: HTTP istek fonksiyonu (`http_request`, `request` vb.) gerektirir. Mevcut değilse veya başarısız olursa uyarır.
