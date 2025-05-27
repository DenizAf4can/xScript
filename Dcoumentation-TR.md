# xScript Kütüphane Dökümantasyonu

**Sürüm**: 1.05

**Açıklama**: xScript, Roblox exploitleri için tasarlanmış güçlü bir kütüphanedir. Oyuncular, karakterler, parçalar, GUI elemanları ve daha fazlasıyla etkileşim kurmak ve manipüle etmek için geniş bir fonksiyon yelpazesi sunar. Bu dökümantasyon, her fonksiyonun parametreleri, dönüş değerleri ve ayrıntılı açıklamalarını içerir.

**Not**: Bazı fonksiyonlar, exploitörün sağladığı belirli özelliklere (örn. `getclipboard`, `setclipboard`, `mouse_move`) dayanır. Tam işlevsellik için exploitörünüzün bu özellikleri desteklediğinden emin olun.

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
  - `centerReference`: Herhangi - Merkez nokta (Vector3, CFrame, BasePart veya Model).
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

### `xScript.FindAllInstances(name, parent, recursive, classHint)`
- **Parametreler**: 
  - `name`: String - Aranacak isim (büyük/küçük harf duyarsız).
  - `parent`: Instance - Aranacak ebeveyn örneği.
  - `recursive`: Boolean (isteğe bağlı) - Özyinelemeli arama. Varsayılan false.
  - `classHint`: String veya Tablo (isteğe bağlı) - Filtreleme için sınıf adı(ları).
- **Dönüş Değeri**: Tablo - Tüm eşleşen örneklerin listesi.
- **Açıklama**: Ebeveyn içinde isme göre tüm örnekleri arar, isteğe bağlı özyineleme ve sınıf filtreleme ile.
- **Notlar**: Ebeveyn veya isim geçersizse boş tablo döner.

### `xScript.RepeatUntilFind(instanceName, parent, recursive, timeoutSeconds, pollingRate)`
- **Parametreler**: 
  - `instanceName`: String - Bulunacak örneğin adı.
  - `parent`: Instance - Aranacak ebeveyn.
  - `recursive`: Boolean (isteğe bağlı) - Özyinelemeli arama. Varsayılan false.
  - `timeoutSeconds`: Number (isteğe bağlı) - Maksimum bekleme süresi (saniye). Varsayılan 10.
  - `pollingRate`: Number (isteğe bağlı) - Kontroller arasındaki aralık (saniye). Varsayılan 0.05.
- **Dönüş Değeri**: Instance veya nil - Bulunan örnek, zaman aşımına uğrarsa nil.
- **Açıklama**: Örnek bulunana veya zaman aşımına kadar isme göre örnek arar.
- **Notlar**: Asenkron yüklenen örnekleri beklemek için kullanışlıdır.

### `xScript.WaitForProperty(instance, propertyName, targetValue, timeoutSeconds)`
- **Parametreler**: 
  - `instance`: Instance - İzleme yapılacak örnek.
  - `propertyName`: String - Kontrol edilecek özellik adı.
  - `targetValue`: Herhangi - Beklenen değer.
  - `timeoutSeconds`: Number (isteğe bağlı) - Maksimum bekleme süresi (saniye). Varsayılan 5.
- **Dönüş Değeri**: Boolean - Özellik hedef değere ulaşırsa true, yoksa false.
- **Açıklama**: Belirtilen özellik hedef değere ulaşana veya zaman aşımına kadar bekler.
- **Notlar**: Polling kullanır. Örnek veya propertyName geçersizse uyarır.

### `xScript.SetParent(instance, newParent)`
- **Parametreler**: 
  - `instance`: Instance - Yeniden ebeveynlenecek örnek.
  - `newParent`: Instance - Yeni ebeveyn örneği.
- **Dönüş Değeri**: Boolean - Başarılıysa true, değilse false.
- **Açıklama**: Belirtilen örneğin ebeveynini değiştirir.
- **Notlar**: Örnek nil ise false döner ve uyarır.

### `xScript.DeleteLocalInstance(instance)`
- **Parametreler**: 
  - `instance`: Instance - Silinecek örnek.
- **Dönüş Değeri**: Boolean - Başarılıysa true, değilse false.
- **Açıklama**: Belirtilen örneği yok eder.
- **Notlar**: Örnek nil veya ebeveyni yoksa false döner ve uyarır.

### `xScript.ClearChildren(instance)`
- **Parametreler**: 
  - `instance`: Instance - Çocukları silinecek örnek.
- **Dönüş Değeri**: Yok
- **Açıklama**: Belirtilen örneğin tüm çocuklarını yok eder.
- **Notlar**: Örnek nil ise uyarır.

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

### `xScript.MouseUp(button)`
- **Parametreler**: 
  - `button`: Enum.UserInputType - Serbest bırakılacak fare düğmesi (MouseButton1, MouseButton2, MouseButton3).
- **Dönüş Değeri**: Yok
- **Açıklama**: Belirtilen fare düğmesinin serbest bırakılmasını simüle eder.
- **Notlar**: Exploitör fonksiyonları (`mouse1up` gibi) gerektirir. Mevcut değilse veya düğme geçersizse uyarır.

### `xScript.MouseClick(button)`
- **Parametreler**: 
  - `button`: Enum.UserInputType - Tıklanacak fare düğmesi (MouseButton1, MouseButton2, MouseButton3).
- **Dönüş Değeri**: Yok
- **Açıklama**: Belirtilen fare düğmesine kilomètres bir tıklama (bas ve bırak) simülasyonu yapar.
- **Notlar**: Exploitör fonksiyonları (`mouse1click` gibi) gerektirir. Mevcut değilse veya düğme geçersizse uyarır.

### `xScript.SimulateKey(keyCode, duration)`
- **Parametreler**: 
  - `keyCode`: Enum.KeyCode - Simüle edilecek tuş.
  - `duration`: Number (isteğe bağlı) - Tuşu basılı tutma süresi (saniye). Varsayılan 0.1.
- **Dönüş Değeri**: Boolean - Başarılıysa true, değilse false.
- **Açıklama**: Belirtilen süre boyunca bir tuşa basılmasını ve tutulmasını simüle eder.
- **Notlar**: Exploitöre özgü tuş basma fonksiyonları (`keypress` veya `key_press`) gerektirir. Mevcut değilse uyarır.

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

### `xScript.SetGravity(number)`
- **Parametreler**: 
  - `number`: Number - Yeni yerçekimi değeri.
- **Dönüş Değeri**: Yok
- **Açıklama**: Workspace'in yerçekimini ayarlar.
- **Notlar**: Giriş bir sayı değilse uyarır.

### `xScript.ToggleFog(enable)`
- **Parametreler**: 
  - `enable`: Boolean - Sisi etkinleştirmek veya devre dışı bırakmak için.
- **Dönüş Değeri**: Yok
- **Açıklama**: Lighting özelliklerini ayarlayarak oyundaki sisi açar/kapatır.
- **Notlar**: Etkinleştirildiğinde sis maksimuma ayarlanır; devre dışı bırakıldığında önceki ayarlar veya varsayılanlar geri yüklenir. Lighting mevcut değilse uyarır.

### `xScript.Create(class, name, parent)`
- **Parametreler**: 
  - `class`: String - Oluşturulacak örneğin sınıf adı.
  - `name`: String - Yeni örneğe atanacak isim.
  - `parent`: Instance (isteğe bağlı) - Yeni örneğin ebeveyni.
- **Dönüş Değeri**: Instance - Yeni oluşturulan örnek.
- **Açıklama**: Belirtilen sınıf, isim ve isteğe bağlı ebeveyn ile yeni bir örnek oluşturur.

### `xScript.Backpack()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Backpack veya nil - Yerel oyuncunun backpack'i, bulunamazsa nil.
- **Açıklama**: Yerel oyuncunun backpack nesnesini döndürür.
- **Notlar**: Yerel oyuncu bulunamazsa uyarır.

### `xScript.EquipTool(tool)`
- **Parametreler**: 
  - `tool`: String veya Tool - Ekipman yapılacak tool, isim veya örnek olarak.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel oyuncunun backpack'inden belirtilen tool'u ekipman yapar.
- **Notlar**: String verilirse, backpack'te isme göre arar. Tool veya humanoid bulunamazsa uyarır.

### `xScript.UnequipTools()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel oyuncunun karakterinden tüm tool'ları çıkarır.
- **Notlar**: Humanoid bulunamazsa uyarır.

### `xScript.CharacterTools(enable)`
- **Parametreler**: 
  - `enable`: Boolean - Tüm tool'ları ekipman yapmak veya çıkarmak için.
- **Dönüş Değeri**: Yok
- **Açıklama**: True ise backpack'teki tüm tool'ları ekipman yapar, false ise tüm tool'ları çıkarır.
- **Notlar**: Yerel oyuncu veya humanoid bulunamazsa uyarır.

### `xScript.Teleport(placeId)`
- **Parametreler**: 
  - `placeId`: Number - Işınlanılacak yerin ID'si.
- **Dönüş Değeri**: Yok
- **Açıklama**: TeleportService kullanarak yerel oyuncuyu belirtilen yere ışınlar.

### `xScript.Rejoin(sameserver)`
- **Parametreler**: 
  - `sameserver`: Boolean (isteğe bağlı) - Aynı sunucuya yeniden katılmak için. Varsayılan false.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel oyuncunun oyuna yeniden katılmasını sağlar, isteğe bağlı olarak aynı sunucuya.
- **Notlar**: TeleportService kullanır.

### `xScript.Time()`
- **Parametreler**: Yok
- **Dönüş Değeri**: Tablo - Mevcut UTC tarih ve saati temsil eden tablo.
- **Açıklama**: `os.date("!*t")` kullanarak mevcut tarih ve saati döndürür.
- **Notlar**: Tablo formatı için Roblox os.date dökümantasyonuna bakın.

### `xScript.Kick(message)`
- **Parametreler**: 
  - `message`: String - Gösterilecek kick mesajı.
- **Dönüş Değeri**: Yok
- **Açıklama**: Yerel oyuncuyu belirtilen mesajla oyundan atar.

### `xScript.ExecutorName()`
- **Parametreler**: Yok
- **Dönüş Değeri**: String - Exploitörün adı, mevcut değilse "Unknown".
- **Açıklama**: Kullanılan exploitörün adını döndürür.
- **Notlar**: `getexecutorname` fonksiyonunu gerektirir. Mevcut değilse uyarır ve "Unknown" döner.

### `xScript.FireButton(button)`
- **Parametreler**: 
  - `button`: GuiButton - Tıklama simüle edilecek GUI düğmesi.
- **Dönüş Değeri**: Yok
- **Açıklama**: Belirtilen GUI düğmesine tıklama simülasyonu yapar, tıklama bağlantılarını tetikler.
- **Notlar**: `getconnections` gerektirir. Mevcut değilse veya düğme geçersizse uyarır.

### `xScript.FireRemote(remoteEvent, ...)`
- **Parametreler**: 
  - `remoteEvent`: RemoteEvent - Tetiklenecek remote event.
  - `...`: Herhangi - Remote event'e geçirilecek değişken argümanlar.
- **Dönüş Değeri**: Yok
- **Açıklama**: Belirtilen remote event'i sunucuya belirtilen argümanlarla tetikler.
- **Notlar**: remoteEvent geçersizse uyarır.

### `xScript.InvokeRemote(remoteFunction, ...)`
- **Parametreler**: 
  - `remoteFunction`: RemoteFunction - Çağrılacak remote function.
  - `...`: Herhangi - Remote function'a geçirilecek değişken argümanlar.
- **Dönüş Değeri**: Herhangi - Remote function tarafından döndürülen sonuç, geçersizse nil.
- **Açıklama**: Belirtilen remote function'ı belirtilen argümanlarla çağırır ve sonucu döndürür.
- **Notlar**: remoteFunction geçersizse uyarır.

### `xScript.TeleportToNearestPlayer(maxDistance)`
- **Parametreler**: 
  - `maxDistance`: Number (isteğe bağlı) - En yakın oyuncu için dikkate alınacak maksimum mesafe.
- **Dönüş Değeri**: Boolean - Başarılıysa true, değilse false.
- **Açıklama**: Yerel oyuncuyu en yakın oyuncunun pozisyonuna, 5 birim yukarı offset ile ışınlar.
- **Notlar**: `GetNearestPlayer` ve `SetLocalPlayerPosition` kullanır.

### `xScript.ClickDetector(part)`
- **Parametreler**: 
  - `part`: BasePart - ClickDetector içeren parça.
- **Dönüş Değeri**: Boolean - ClickDetector bulunup tıklanmışsa true, değilse false.
- **Açıklama**: Belirtilen parçadaki ClickDetector'e tıklama simülasyonu yapar.
- **Notlar**: Parça veya ClickDetector geçersizse uyarır.

### `xScript.FireProximityPrompt(proximityPrompt)`
- **Parametreler**: 
  - `proximityPrompt`: ProximityPrompt - Tetiklenecek proximity prompt.
- **Dönüş Değeri**: Boolean - Başarılıysa true, değilse false.
- **Açıklama**: Belirtilen proximity prompt'u tetikler.
- **Notlar**: proximityPrompt geçersizse uyarır.

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

### `xScript.DetachESP(targetPart)`
- **Parametreler**: 
  - `targetPart`: BasePart veya Humanoid - ESP'si kaldırılacak hedef.
- **Dönüş Değeri**: Boolean - ESP kaldırıldıysa true, değilse false.
- **Açıklama**: Hedefteki eklenmiş ESP'yi (Billboard veya Highlight) kaldırır.

### `xScript.AttachClickEvent(guiObject, callbackFunction)`
- **Parametreler**: 
  - `guiObject`: GuiObject - Tıklama olayı eklenecek GUI nesnesi.
  - `callbackFunction`: Function - Tıklandığında çağrılacak fonksiyon.
- **Dönüş Değeri**: RBXScriptConnection veya nil - Bağlantı nesnesi, ekleme başarısızsa nil.
- **Açıklama**: Belirtilen GUI nesnesine tıklama olayı ekler.
- **Notlar**: TextButton, ImageButton ve sınırlı Frame/Label desteği (InputBegan ile). Geçersizse uyarır.

### `xScript.DetachClickEvent(guiObjectOrConnection)`
- **Parametreler**: 
  - `guiObjectOrConnection`: GuiObject veya RBXScriptConnection - Tıklama olayı kaldırılacak nesne veya bağlantı.
- **Dönüş Değeri**: Boolean - Başarılıysa true, değilse false.
- **Açıklama**: Belirtilen GUI nesnesinden veya bağlantıdan tıklama olayını kaldırır.
- **Notlar**: Argüman geçersizse veya bağlantı yoksa uyarır.

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

### `xScript.SendEmbed(webhook, data)`
- **Parametreler**: 
  - `webhook`: String - Discord webhook URL'si.
  - `data`: Tablo - Gönderilecek embed verisi (JSON kodlanabilir).
- **Dönüş Değeri**: Yok
- **Açıklama**: Belirtilen Discord webhook'una embed gönderir.
- **Notlar**: HTTP istek fonksiyonu gerektirir. Mevcut değilse veya başarısız olursa uyarır.
