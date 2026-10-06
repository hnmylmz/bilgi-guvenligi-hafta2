Hafta 2 · Parola Kırma ve Özet Güvenliği Laboratuvarı

Bu çalışma, Kali Linux ortamında hashcat aracı kullanılarak zayıf ve modern özet (hash) algoritmalarının kırma hızlarının, güvenlik seviyelerinin ve tuzlama (salting) mekanizmasının deneysel olarak analiz edilmesini içerir.



1. Deneysel Hız ve Kırma Verileri

Terminal çıktıları üzerinden ölçülen değerler:



MD5 Hızı: 230 H/s (Sözlük saldırısı tamamlanma süresi: anlık / <1 sn)

SHA-256 Hızı: 44,287 H/s (~44.2 kH/s)

bcrypt Hızı: 36 H/s (Donanım direnci nedeniyle belirgin yavaşlık)

Çözülen Parola Oranı: 8/8 (%100 başarı)

2. Soruların Cevapları

1) Hangi özet anında kırıldı, hangisi yavaştı, neden?

MD5 ve SHA-256 anında kırıldı: Bu algoritmalar genel veri bütünlüğünü (checksum) sağlamak amacıyla geliştirilmiş, olabildiğince hızlı çalışacak şekilde tasarlanmış özet fonksiyonlarıdır. Donanım hızlandırmalarıyla çok yüksek işlem kapasitesine ulaşabilirler; bu nedenle eldeki 28 kelimelik sözlükle eşleşmeler anında tamamlanmıştır.

bcrypt çok yavaştı (36 H/s): bcrypt, parola saklama amacıyla tasarlanmış bir anahtar türetme (Key Derivation) fonksiyonudur. İçerisinde maliyet faktörü (work factor / round sayısı) ve bellek kısıtı barındırır. CPU ve GPU donanımları üzerinde paralel işlem yapılmasını zorlaştırarak hesaplama hızını saniyede sadece onlar basamağına (36 H/s) düşürmüştür.

2) MD5 ile SHA-256 arasında kırma kolaylığı açısından fark var mıydı?

Saldırı kolaylığı açısından pratikte fark yoktu: Kriptografik açıdan SHA-256, matematiksel çakışma (collision) direnci bakımından MD5'ten çok daha modern ve güvenlidir. Ancak parola saklama ve sözlük/kaba kuvvet saldırıları söz konusu olduğunda SHA-256 da tek başına aşırı hızlı hesaplandığı için MD5 gibi neredeyse anında kırılmıştır. Dolayısıyla tuzsuz SHA-256 da parola saklama için tek başına yetersizdir.

3) bcrypt neden hem kullanıcı için sorun değil hem saldırgan için kâbus?

Kullanıcı için sorun değildir: Bir kullanıcı sisteme parola girerken bcrypt hash'inin hesaplanması ~100–300 ms sürer. Bir insanın tek bir oturum açma işleminde saniyenin üçte biri kadar beklemesi hissedilmez ve kullanıcı deneyimini etkilemez.

Saldırgan için kâbustur: Saldırgan ele geçirdiği hash'i çözmek için milyarlarca parolayı denemek zorundadır. Saniyede milyarlarca işlem yapmak yerine saniyede yalnızca 36 deneme yapabilmesi, saldırının aylar veya yüzyıllar sürmesine neden olur; saldırıyı ekonomik ve pratik açıdan imkânsız kılar.

4) 'Tuz' (salt) ne işe yarar?

Rainbow Table saldırılarını engeller: Parolaya eklenen rastgele bir karakter dizisi (tuz) sayesinde, önceden hazırlanmış devasa özet tabloları (Rainbow Tables) işe yaramaz hale gelir.

Aynı parolayı kullanan hesapların özetlerini farklılaştırır: İki farklı kullanıcı aynı parolayı (örneğin 123456) seçse dahi, her birine sistem tarafından farklı rastgele tuzlar atandığı için veritabanında üretilen özetler tamamen farklı görünür. Böylece tek bir özeti kırmak diğer aynı parolaya sahip kullanıcıları ifşa etmez
Hafta 2 · Parola Kırma ve Özet Güvenliği Laboratuvarı

Bu çalışma, Kali Linux ortamında hashcat aracı kullanılarak zayıf ve modern özet (hash) algoritmalarının kırma hızlarının, güvenlik seviyelerinin ve tuzlama (salting) mekanizmasının deneysel olarak analiz edilmesini içerir.



1. Deneysel Hız ve Kırma Verileri

Terminal çıktıları üzerinden ölçülen değerler:



MD5 Hızı: 230 H/s (Sözlük saldırısı tamamlanma süresi: anlık / <1 sn)

SHA-256 Hızı: 44,287 H/s (~44.2 kH/s)

bcrypt Hızı: 36 H/s (Donanım direnci nedeniyle belirgin yavaşlık)

Çözülen Parola Oranı: 8/8 (%100 başarı)

2. Soruların Cevapları

1) Hangi özet anında kırıldı, hangisi yavaştı, neden?

MD5 ve SHA-256 anında kırıldı: Bu algoritmalar genel veri bütünlüğünü (checksum) sağlamak amacıyla geliştirilmiş, olabildiğince hızlı çalışacak şekilde tasarlanmış özet fonksiyonlarıdır. Donanım hızlandırmalarıyla çok yüksek işlem kapasitesine ulaşabilirler; bu nedenle eldeki 28 kelimelik sözlükle eşleşmeler anında tamamlanmıştır.

bcrypt çok yavaştı (36 H/s): bcrypt, parola saklama amacıyla tasarlanmış bir anahtar türetme (Key Derivation) fonksiyonudur. İçerisinde maliyet faktörü (work factor / round sayısı) ve bellek kısıtı barındırır. CPU ve GPU donanımları üzerinde paralel işlem yapılmasını zorlaştırarak hesaplama hızını saniyede sadece onlar basamağına (36 H/s) düşürmüştür.

2) MD5 ile SHA-256 arasında kırma kolaylığı açısından fark var mıydı?

Saldırı kolaylığı açısından pratikte fark yoktu: Kriptografik açıdan SHA-256, matematiksel çakışma (collision) direnci bakımından MD5'ten çok daha modern ve güvenlidir. Ancak parola saklama ve sözlük/kaba kuvvet saldırıları söz konusu olduğunda SHA-256 da tek başına aşırı hızlı hesaplandığı için MD5 gibi neredeyse anında kırılmıştır. Dolayısıyla tuzsuz SHA-256 da parola saklama için tek başına yetersizdir.

3) bcrypt neden hem kullanıcı için sorun değil hem saldırgan için kâbus?

Kullanıcı için sorun değildir: Bir kullanıcı sisteme parola girerken bcrypt hash'inin hesaplanması ~100–300 ms sürer. Bir insanın tek bir oturum açma işleminde saniyenin üçte biri kadar beklemesi hissedilmez ve kullanıcı deneyimini etkilemez.

Saldırgan için kâbustur: Saldırgan ele geçirdiği hash'i çözmek için milyarlarca parolayı denemek zorundadır. Saniyede milyarlarca işlem yapmak yerine saniyede yalnızca 36 deneme yapabilmesi, saldırının aylar veya yüzyıllar sürmesine neden olur; saldırıyı ekonomik ve pratik açıdan imkânsız kılar.

4) 'Tuz' (salt) ne işe yarar?

Rainbow Table saldırılarını engeller: Parolaya eklenen rastgele bir karakter dizisi (tuz) sayesinde, önceden hazırlanmış devasa özet tabloları (Rainbow Tables) işe yaramaz hale gelir.

Aynı parolayı kullanan hesapların özetlerini farklılaştırır: İki farklı kullanıcı aynı parolayı (örneğin 123456) seçse dahi, her birine sistem tarafından farklı rastgele tuzlar atandığı için veritabanında üretilen özetler tamamen farklı görünür. Böylece tek bir özeti kırmak diğer aynı parolaya sahip kullanıcıları ifşa etmez

