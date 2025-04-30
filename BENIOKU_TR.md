### Temel Linux Eğitimi

#### GNU/Linux Temelleri

GNU/Linux, özgür ve açık kaynak kodlu bir işletim sistemi çekirdeği olan Linux üzerine kurulu, GNU Projesi'nin araçları ve felsefesiyle birleşmiş bir işletim sistemi ailesidir. Katmanlı bir yapıya sahiptir:

*   **Kullanıcı Katmanı (User Space):** Uygulamaların, masaüstü ortamlarının ve kullanıcıların doğrudan etkileşimde bulunduğu katmandır.
*   **Çekirdek (Kernel):** Donanım ve yazılım arasındaki iletişimi yöneten, sistem kaynaklarını (CPU, bellek, G/Ç aygıtları) kontrol eden merkezi bileşendir.
*   **Donanım (Hardware):** Bilgisayarın fiziksel bileşenleridir (CPU, RAM, disk, ağ kartı vb.).

#### Linux Dağıtımları (Distro)

Linux çekirdeğini temel alan, üzerine çeşitli yazılımlar (masaüstü ortamı, paket yöneticisi, uygulamalar) eklenerek oluşturulan tam teşekküllü işletim sistemleridir. Yüzlerce farklı dağıtım bulunur, her biri farklı amaçlara ve kullanıcı kitlelerine hitap edebilir. Dağıtımlar arasındaki temel farklardan biri kullandıkları paket yönetim sistemleridir:

*   **apt (Advanced Package Tool):** Debian ve Ubuntu gibi Debian tabanlı dağıtımlarda kullanılan paket yöneticisidir. `.deb` uzantılı paketleri yönetir.
*   **yum (Yellowdog Updater, Modified) / dnf (Dandified YUM):** Red Hat, CentOS, Fedora gibi Red Hat tabanlı dağıtımlarda kullanılan paket yöneticileridir. `.rpm` uzantılı paketleri yönetir. (DNF, YUM'un modern halefidir.)
*   **WSL (Windows Subsystem for Linux):** Bir Linux dağıtımı değil, Windows işlet sistemi üzerinde doğrudan Linux komut satırı araçlarını, yardımcı programlarını ve uygulamalarını çalıştırmayı sağlayan bir uyumluluk katmanıdır.

#### Kullanıcı Arayüzleri ve Erişim

Linux sistemleriyle etkileşim kurmanın temel yolları:

*   **GUI (Graphical User Interface - Grafik Kullanıcı Arayüzü):** Pencereler, ikonlar ve menüler aracılığıyla görsel bir etkileşim sunar (örn: GNOME, KDE, XFCE).
*   **CLI (Command Line Interface - Komut Satırı Arayüzü):** Metin tabanlı komutlar aracılığıyla sistemle etkileşim kurulur.
*   **Terminal Emülatörü:** GUI ortamında CLI'a erişim sağlayan uygulamalardır (örn: GNOME Terminal, Konsole, xterm).
*   **Shell (Kabuk):** Kullanıcıdan aldığı komutları yorumlayıp çekirdeğe ileten arayüz programıdır (örn: Bash, Zsh, Fish).
*   **TTY (Teletypewriter):** Eskiden fiziksel klavye ve yazıcının bağlı olduğu "teletypewriter" cihazlarına referanstır. GUI olmadan da sisteme doğrudan metin tabanlı giriş/çıkış yapmayı sağlayan sanal konsollardır. Genellikle `Ctrl + Alt + F1` ile `F6` (veya `F7`/`F8`) tuş kombinasyonlarıyla erişilir.
*   **PTY (Pseudo-TTY):** Terminal emülatörleri gibi programların kullandığı sahte (pseudo) TTY'lerdir.

#### Shell (Kabuk) İşleyişi ve Yönetimi

Komutların işlenme akışı genellikle şu şekildedir:
`Shell (CLI)` > `Kernel` > `CPU` > `Donanım`

Varsayılan kabuğu değiştirmek için aşağıdaki komutlar kullanılabilir:

*   `chsh -s /yol/kabuk_adi`: Kullanıcının varsayılan kabuğunu değiştirir (örn: `chsh -s /bin/zsh`).
*   `/etc/passwd` dosyasını düzenlemek: Kullanıcı bilgilerinin tutulduğu bu dosyada ilgili kullanıcının kabuk yolu manuel olarak değiştirilebilir (örn: `sudo vim /etc/passwd`), ancak `chsh` kullanmak daha güvenlidir.

Bir aracın (kabuk veya başka bir komut) sistemdeki yerini bulmak için:

*   `which komut_adi`: Komutun çalıştırılabilir dosyasının tam yolunu gösterir (örn: `which bash`, `which zsh`).

#### Dahili (Built-in) Komutlar ve Alias'lar

Kabuğun kendi içinde tanımlı olan, ayrı bir çalıştırılabilir dosyası olmayan komutlardır.

*   `compgen -b`: Tüm dahili komutları listeler.
*   `compgen -a`: Tanımlı tüm alias'ları (komut takma adları) listeler.

#### $PATH Ortam Değişkeni

Kabuğun, çalıştırılmak istenen bir komutun dosyasını hangi dizinlerde arayacağını belirten, iki nokta üst üste (:) ile ayrılmış dizin yollarının listesidir.

*   **Sistem Geneli $PATH Tanımları:** `/etc/profile`, `/etc/bash.bashrc`, `/etc/environment` gibi dosyalarda tanımlanabilir.
*   **Kullanıcı Bazlı $PATH Tanımları:** `~/.bashrc`, `~/.bash_profile`, `~/.profile`, `~/.zshrc` (Zsh kullanılıyorsa) gibi kullanıcının ev dizinindeki dosyalarda tanımlanır.

#### Bash Shell Kısayolları (Örnekler)

*   `Ctrl + L`: Ekranı temizler (`clear` komutu gibi).
*   `Ctrl + C`: Çalışan komutu sonlandırır.
*   `Ctrl + D`: Kabuktan çıkar (EOF - End of File sinyali gönderir).
*   `Ctrl + Z`: Çalışan komutu arka plana atar (durdurur).
*   `Ctrl + R`: Komut geçmişinde geriye doğru arama yapar.
*   `Ctrl + A`: İmleci satır başına taşır.
*   `Ctrl + E`: İmleci satır sonuna taşır.
*   `Alt + .` (veya `Esc` + `.`): Önceki komutun son argümanını getirir.
*   `Ctrl + _`: Son yapılan değişikliği geri alır (Undo).

#### Yardım Alma Yöntemleri

*   `help <dahili_komut>`: Belirtilen dahili komut hakkında yardım gösterir.
*   `komut --help` veya `komut -h`: Çoğu komutun temel kullanım bilgilerini ve seçeneklerini gösterir.
*   `man <komut>`: Komutun detaylı kılavuz sayfasını (manual page) gösterir.
    *   `man -k <ifade>` (veya `apropos <ifade>`): İfadeyle ilgili kılavuz sayfalarını arar.
*   `info <komut>`: Bazı komutlar için daha detaylı, hiperlinkli bilgi sunan `info` sayfalarını gösterir.

#### Linux Dizin Sistemi Hiyerarşisi (FHS - Filesystem Hierarchy Standard)

Linux'ta dosya ve dizinler belirli bir standart yapıya göre organize edilir. Temel dizinler ve amaçları:

*   **/ (Kök Dizin):** Tüm dosya sisteminin en üst seviyesindeki dizindir. Diğer tüm dizinler bu dizinin altında yer alır. Sistem açılışında çekirdek tarafından ilk bağlanan (mount edilen) dosya sistemidir.
*   **/bin (Essential User Binaries):** Temel kullanıcı komutlarını (binary/executable) içerir (`ls`, `cp`, `mv`, `cat` gibi). Tek kullanıcı modunda bile sistemin çalışması için gereklidir.
*   **/sbin (Essential System Binaries):** `/bin`'e benzer, ancak genellikle sadece sistem yöneticisi (root) tarafından kullanılan sistem yönetimi komutlarını içerir (`fdisk`, `ifconfig`, `reboot`, `mkfs` gibi).
*   **/dev (Device Files):** Sisteme bağlı fiziksel (hard disk, klavye) ve sanal aygıtları temsil eden özel dosyalardır. Linux'ta "her şey bir dosyadır" felsefesinin bir yansımasıdır (`/dev/sda`, `/dev/tty1` gibi).
*   **/etc (Etcetera - Yapılandırma Dosyaları):** Sistem genelindeki programların ve servislerin yapılandırma dosyalarını içerir (`/etc/passwd`, `/etc/fstab`, `/etc/network/interfaces` gibi).
*   **/opt (Optional Add-on Software):** Üçüncü parti yazılımların veya standart dışı paketlerin kurulduğu dizindir. Genellikle her yazılım kendi alt dizinine kurulur (örn: `/opt/google/chrome`).
*   **/proc (Process Information):** Disk üzerinde yer kaplamayan, sistem belleğindeki bilgileri (çekirdek, süreçler, donanım durumu vb.) dosya sistemi arayüzü üzerinden sunan sanal bir dosya sistemidir (`/proc/cpuinfo`, `/proc/meminfo`).
*   **/root (Root User Home Directory):** Sistem yöneticisi olan "root" kullanıcısının özel ev dizinidir.
*   **/run (Runtime Variable Data):** Sistem çalışırken oluşturulan geçici verileri (PID dosyaları, soketler) içerir. Sistem yeniden başlatıldığında içeriği genellikle silinir. `/var/run` dizininin modern karşılığıdır.
*   **/var (Variable Files):** Sistem çalışırken boyutları sürekli değişen dosyaları içerir (log dosyaları `/var/log`, e-posta kuyrukları `/var/spool/mail`, web sunucusu verileri `/var/www` gibi).
*   **/tmp (Temporary Files):** Uygulamaların ve kullanıcıların geçici dosyalar oluşturduğu dizindir. İçeriği genellikle sistem yeniden başlatıldığında silinir.
*   **/usr (Unix System Resources):** Kullanıcılar tarafından kullanılan uygulamaların, kütüphanelerin ve paylaşılan verilerin büyük çoğunluğunu içerir. İkincil bir hiyerarşi gibidir (`/usr/bin`, `/usr/sbin`, `/usr/lib`, `/usr/local`, `/usr/share`). Temel sistemin çalışması için zorunlu olmayan yazılımlar genellikle buradadır.
    *   `/usr/bin`: Kullanıcı komutları (çoğu normal kullanıcı tarafından çalıştırılabilir).
    *   `/usr/sbin`: Sistem yönetim komutları (genellikle root tarafından çalıştırılabilir).
    *   `/usr/lib`: Uygulamalar tarafından kullanılan paylaşımlı kütüphaneler.
    *   `/usr/share`: Mimari bağımsız veriler (belgeler, ikonlar, yazı tipleri vb.).
    *   `/usr/local`: Yerel olarak (paket yöneticisi dışında) kurulan yazılımlar için ayrılmış hiyerarşi (`/usr/local/bin`, `/usr/local/lib` vb.).
*   **/home (Home Directories):** Normal kullanıcıların kişisel ev dizinlerini içerir (örn: `/home/ahmet`, `/home/ayse`). Kullanıcıların kişisel dosyaları, belgeleri, ayarları burada saklanır.
*   **/boot (Boot Loader Files):** İşletim sisteminin başlatılması (boot) için gerekli olan dosyaları içerir (Linux çekirdeği `vmlinuz`, `initramfs`, önyükleyici `GRUB` yapılandırması gibi).
*   **/lib (Essential Shared Libraries):** `/bin` ve `/sbin` dizinlerindeki temel komutların çalışması için gerekli olan paylaşılan kütüphane dosyalarını (`.so`) ve çekirdek modüllerini içerir.
*   **/mnt (Mount Point):** Sistem yöneticisinin geçici olarak dosya sistemlerini (başka disk bölümü, ağ paylaşımı) bağlamak (mount etmek) için kullandığı genellikle boş olan bir dizindir.
*   **/media (Removable Media Devices):** USB bellekler, CD/DVD sürücüler gibi çıkarılabilir medya aygıtlarının genellikle otomatik olarak bağlandığı dizindir.
*   **/srv (Service Data):** Sistemin sunduğu servislerle ilgili verilerin saklandığı dizindir (örn: web sunucusu dosyaları `/srv/www`, FTP verileri `/srv/ftp`).

#### Temel Dosya Sistemi Komutları

##### pwd (Print Working Directory)

*   Bulunulan mevcut çalışma dizininin tam yolunu ekrana yazdırır.

##### cd (Change Directory)

*   Dizinler arasında geçiş yapmayı sağlar.
*   **Göreceli Yol (Relative Path):** Mevcut dizine göre hedef dizini tarif eder (örn: `cd Belgeler`, `cd ../Muzik`).
*   **Mutlak Yol (Absolute Path):** Kök dizinden (`/`) başlayarak hedef dizini tarif eder (örn: `cd /home/gokhan/Belgeler`, `cd /etc/nginx`).
*   `cd -`: Bir önceki bulunulan dizine geri döner.
*   `cd` (argümansız): Kullanıcının ev dizinine gider (`/home/kullanici_adi`).
*   `cd ..`: Bir üst dizine çıkar.
*   **Tırnak İşaretleri ve Kaçış Karakteri:**
    *   `''` (Tek Tırnak): İçindeki tüm karakterleri (dolar işareti `$`, yıldız `*` dahil) olduğu gibi kabul eder, özel anlamlarını yok sayar. Toplu kaçış sağlar.
    *   `""` (Çift Tırnak): İçindeki çoğu karakteri olduğu gibi kabul eder ancak `$`, `\`, ``` ` ``` (ters tırnak) gibi bazı karakterlerin özel anlamlarını korur (değişken genişletmesi, komut ikamesi, kaçış karakteri).
    *   `\` (Ters Eğik Çizgi - Kaçış Karakteri): Kendisinden sonra gelen özel karakterin (boşluk, `*`, `$`, `(` vb.) özel anlamını yok sayarak normal bir karakter gibi davranmasını sağlar. Örnek: `cd yeni\ klasor` komutu, "yeni klasor" adındaki (boşluk içeren) dizine geçiş yapar.

##### ls (List Directory Contents)

*   Dizin içeriklerini listeler.
*   `ls -l`: Uzun liste formatında detaylı bilgi verir (izinler, sahip, grup, boyut, tarih, dosya adı).
    *   `-rw-r--r-- 1 gokhan staff 1590684 Mar 25 21:19 Test.png`
        *   `(-)`: Dosya tipi (`-`: dosya, `d`: dizin, `l`: sembolik link vb.).
        *   `rw-r--r--`: İzinler (sahip `rwx`, grup `rwx`, diğerleri `rwx`). `r`: okuma (4), `w`: yazma (2), `x`: çalıştırma (1), `-`: izin yok (0). `chmod 755 dosya` -> `rwxr-xr-x` izinlerini verir.
        *   `1`: Hard link sayısı.
        *   `gokhan`: Dosya sahibi.
        *   `staff`: Dosyanın ait olduğu grup.
        *   `1590684`: Dosya boyutu (byte).
        *   `Mar 25 21:19`: Son değiştirilme tarihi/saati.
        *   `Test.png`: Dosya/dizin adı.
        *   `@` (macOS'ta): Genişletilmiş özniteliklerin (Extended Attributes) olduğunu gösterir.
*   `ls -a`: Gizli dosyalar dahil tüm içeriği gösterir (`.` ile başlayanlar).
*   `ls -h`: `-l` ile birlikte kullanıldığında dosya boyutlarını okunabilir formatta (KB, MB, GB) gösterir.
*   `ls -s`: Dosyaları boyutlarına göre (genellikle büyükten küçüğe) sıralayarak listeler (blok boyutunu da gösterebilir).
*   `ls -t`: Dosyaları değiştirilme zamanına göre (en yeniden en eskiye) sıralar.
*   `ls -r`: Sıralama düzenini tersine çevirir (örn: `ls -trl` -> en eski dosyadan en yeniye doğru listeler).
*   `ls -ld <dizin_adi>`: Dizinin kendisinin özelliklerini gösterir (içeriğini değil).
*   `ls -l <dosya_adi>`: Belirtilen dosyanın özelliklerini gösterir.
*   `ls -R`: Özyinelemeli (recursive) olarak tüm alt dizinleri ve dosyaları listeler.

##### mkdir (Make Directory)

*   Yeni dizinler oluşturur.
*   `mkdir dizin1 dizin2`: Birden fazla dizin oluşturur.
*   `mkdir -p ust_dizin/alt_dizin/torun_dizin`: Gerekli üst dizinleri de otomatik olarak oluşturur (parent).

##### rmdir (Remove Directory)

*   Sadece **içi boş** olan dizinleri siler.

##### rm (Remove)

*   Dosyaları veya dizinleri siler.
*   `rm dosya1 dosya2`: Belirtilen dosyaları siler.
*   `rm -r dizin_adi`: Dizini ve içindeki tüm alt dizin/dosyaları özyinelemeli olarak siler. **Dikkatli kullanılmalıdır!**
*   `rm -i`: Silmeden önce onay ister (interactive).
*   `rm -f`: Onay istemeden zorla siler (force). **Çok dikkatli kullanılmalıdır!**

#### Bash Kabuk Genişletmeleri (Shell Expansion)

Kabuk, bir komutu çalıştırmadan önce komut satırındaki belirli karakterleri veya ifadeleri değerlendirip dönüştürür. Bu işleme kabuk genişletmesi denir. Sıra önemlidir: Önce genişletme yapılır, komutun son hali netleşir, sonra komut çalıştırılır.

*   **`{}` (Brace Expansion - Küme Parantezi Genişletmesi):** Virgülle ayrılmış veya aralık belirtilmiş ifadeleri genişleterek birden çok dize oluşturur. Dosya/dizin oluşturma gibi işlerde kullanışlıdır.
    *   `echo {a,b,c}d` -> `ad bd cd`
    *   `mkdir proje{1..5}` -> `proje1`, `proje2`, `proje3`, `proje4`, `proje5` adında dizinler oluşturur.
    *   `echo {1..10..2}` -> `1 3 5 7 9` (Başlangıç..Bitiş..Adım)
    *   `echo {a..c}{1..2}` -> `a1 a2 b1 b2 c1 c2`
*   **`~` (Tilde Expansion - Tilde Genişletmesi):**
    *   `~`: Geçerli kullanıcının ev dizinine genişler (`/home/kullanici`).
    *   `~kullanici`: Belirtilen kullanıcının ev dizinine genişler (`/home/kullanici`).
*   **Değişken Genişletmesi (Variable Expansion):** `$` ile başlayan değişken adları, değişkenin değeriyle değiştirilir.
    *   `echo $HOME` -> Kullanıcının ev dizinini yazdırır.
    *   `echo "Kullanıcı: $USER"` -> `Kullanıcı: gokhan` gibi bir çıktı verir.
*   **Komut İkamesi (Command Substitution):** Bir komutun çıktısını başka bir komutun içinde kullanmayı sağlar.
    *   `$(komut)` veya ``` `komut` ``` (ters tırnak - eski yöntem): İçerideki komut çalıştırılır ve çıktısı o noktaya yerleştirilir. `$(...)` kullanımı tercih edilir.
    *   `echo "Bugünün tarihi: $(date)"` -> `Bugünün tarihi: Wed Apr 30 15:30:00 TRT 2025` gibi bir çıktı verir.
    *   `files=$(ls *.txt)` -> Mevcut dizindeki `.txt` dosyalarının listesini `files` değişkenine atar.
*   **Aritmetik Genişletme (Arithmetic Expansion):** Matematiksel işlemler yapmak için kullanılır.
    *   `$((ifade))` : İçerideki matematiksel ifade hesaplanır ve sonucuyla değiştirilir.
    *   `echo $((5 * 3))` -> `15` çıktısını verir.
    *   `x=10; echo $(($x + 5))` -> `15` çıktısını verir.
*   **Süreç İkamesi (Process Substitution):** Bir komutun çıktısını geçici bir dosya gibi ele alıp başka bir komuta girdi olarak vermeyi sağlar.
    *   `< (komut)` veya `> (komut)`: Komutun çıktısı/girdisi geçici bir dosya yolu (örn: `/dev/fd/63`) ile temsil edilir.
    *   `diff <(ls dizin1) <(ls dizin2)` -> `dizin1` ve `dizin2` içeriklerinin farkını gösterir.
*   **Kelime Bölme (Word Splitting):** Genişletmelerden sonra, tırnak içinde olmayan sonuçlar `$IFS` (Internal Field Separator - genellikle boşluk, tab, newline) karakterlerine göre kelimelere ayrılır.
*   **Dosya Adı Genişletmesi (Filename Expansion - Globbing):** Joker karakterler (`*`, `?`, `[]`) kullanılarak mevcut dosya ve dizin adlarıyla eşleşenleri bulur ve komuta argüman olarak ekler. **Sadece var olan dosya/dizin adlarıyla eşleşir, yeni isimler üretmez.**
    *   `*`: Sıfır veya daha fazla sayıda herhangi bir karakterle eşleşir (gizli dosyaları `.` ile başlamadıkça kapsamaz). `ls *.txt` -> sonu `.txt` ile biten tüm dosyaları listeler.
    *   `?`: Herhangi tek bir karakterle eşleşir. `ls rapor?.doc` -> `rapor1.doc`, `raporA.doc` gibi dosyalarla eşleşir.
    *   `[]`: Köşeli parantez içindeki karakterlerden herhangi biriyle eşleşir. Aralık (`[a-z]`, `[0-9]`) veya liste (`[abc]`) belirtilebilir. `ls [abc]*.txt` -> adı `a`, `b` veya `c` ile başlayan `.txt` dosyalarını listeler.
    *   `[!...]` veya `[^...]`: Köşeli parantez içindeki karakterler *dışındaki* herhangi bir karakterle eşleşir. `ls [!0-9]*.log` -> adı rakamla başlamayan `.log` dosyalarını listeler.

#### Regex (Regular Expressions - Düzenli İfadeler)

Metin içinde belirli kalıpları (desenleri) aramak, eşleştirmek ve işlemek için kullanılan özel bir karakter dizisidir. Kabuk genişletmesindeki joker karakterlerden (`*`, `?`, `[]`) daha güçlü ve esnektir. `grep`, `sed`, `awk` gibi araçlar tarafından yaygın olarak kullanılır.

*   **Temel Fark:** Globbing (kabuk genişletmesi) dosya adlarıyla eşleşirken, Regex metin içeriğiyle eşleşir. Kullanılan bazı karakterler benzer olsa da anlamları ve kapsamları farklıdır.

#### Metinsel Verilerle Çalışma

Linux/Unix felsefesinin temellerinden biri "Her şey bir dosyadır" ilkesidir. Komutların çıktıları, klavye girdileri, hatta donanım aygıtları bile dosya benzeri akışlar (byte stream) olarak ele alınır.

#### Yönlendirmeler (Redirection) ve Dosya Tanımlayıcıları (File Descriptors - fd)

Çalışan her sürecin (process) varsayılan olarak üç standart veri akışı vardır:

*   **`0` - stdin (Standard Input - Standart Girdi):** Sürecin veri aldığı varsayılan yer (genellikle klavye).
*   **`1` - stdout (Standard Output - Standart Çıktı):** Sürecin normal çıktılarını gönderdiği varsayılan yer (genellikle ekran/terminal).
*   **`2` - stderr (Standard Error - Standart Hata):** Sürecin hata mesajlarını gönderdiği varsayılan yer (genellikle ekran/terminal).

Bu akışlar, dosya tanımlayıcıları (file descriptors) adı verilen numaralarla temsil edilir. Yönlendirme operatörleri, bu akışların hedefini değiştirmemizi sağlar:

*   `< dosya`: Standart girdiyi klavye yerine `dosya`dan alır. `komut < girdi.txt`
*   `> dosya`: Standart çıktıyı ekran yerine `dosya`ya yönlendirir. Dosya varsa üzerine yazar. `ls -l > liste.txt`
*   `>> dosya`: Standart çıktıyı ekran yerine `dosya`nın sonuna ekler. Dosya yoksa oluşturur. `echo "Yeni log" >> log.txt`
*   `2> dosya`: Standart hatayı ekran yerine `dosya`ya yönlendirir. Dosya varsa üzerine yazar. `komut_hata_verebilir 2> hatalar.txt`
*   `2>> dosya`: Standart hatayı ekran yerine `dosya`nın sonuna ekler. `komut_hata_verebilir 2>> hatalar.txt`
*   `&> dosya` veya `> dosya 2>&1`: Hem standart çıktıyı hem de standart hatayı `dosya`ya yönlendirir. `2>&1` ifadesi, "stderr'i (2) stdout'un (1) şu anki hedefine (&) yönlendir" anlamına gelir. Sıralama önemlidir (`> dosya 2>&1`).
*   `|` (Pipe - Boru Hattı): Bir komutun standart çıktısını (`stdout`) başka bir komutun standart girdisine (`stdin`) bağlar. `ls -l | grep ".txt"`

##### Özel Dosyalar

*   `/dev/stdin`, `/dev/stdout`, `/dev/stderr`: Sırasıyla fd 0, 1 ve 2'ye işaret eden sembolik linklerdir. Çalışan sürece göre `/proc/self/fd/0`, `/proc/self/fd/1`, `/proc/self/fd/2`'ye bağlanırlar.
*   `/dev/tty`: Sürecin kontrol eden terminaline işaret eder.
*   `/dev/null`: "Kara delik" olarak da bilinir. Buraya yönlendirilen her türlü veri kaybolur. İstenmeyen çıktıları bastırmak için kullanılır. `komut > /dev/null 2>&1` (hem stdout hem stderr'i yok sayar).

#### Metin İşleme Araçları

##### cat (Concatenate)

*   Dosyaların içeriğini standart çıktıya (genellikle ekrana) yazar veya dosyaları birleştirir.
*   `cat dosya.txt`: Dosyanın içeriğini gösterir.
*   `cat dosya1.txt dosya2.txt`: İki dosyanın içeriğini art arda gösterir.
*   `cat dosya1.txt dosya2.txt > birlesik_dosya.txt`: İki dosyanın içeriğini birleştirip yeni bir dosyaya yazar.
*   `cat -n dosya.txt`: Satır numaralarıyla birlikte gösterir.

##### tac (cat tersten)

*   Dosyanın satırlarını ters sırada (son satırdan ilk satıra doğru) yazdırır.

##### rev (Reverse)

*   Dosyanın her satırındaki karakterleri ters sırada yazdırır (satır sırası değişmez).

##### touch

*   Var olmayan dosyaları oluşturur veya var olan dosyaların erişim/değiştirilme zaman damgalarını günceller.
*   `touch yeni_dosya.txt`: `yeni_dosya.txt` adında boş bir dosya oluşturur (varsa zaman damgasını günceller).
*   `touch -a dosya.txt`: Sadece erişim zamanını günceller.
*   `touch -m dosya.txt`: Sadece değiştirilme zamanını günceller.

##### stat

*   Dosya veya dosya sistemi hakkındaki durum bilgilerini (inode, boyut, izinler, zaman damgaları vb.) gösterir.
*   `stat dosya.txt`: Dosyanın detaylı bilgilerini listeler.
    *   `Size`: Dosyanın boyutu (byte).
    *   `Blocks`: Diskte kapladığı blok sayısı.
    *   `IO Block`: G/Ç işlemleri için blok boyutu.
    *   `regular file`/`directory`/`symbolic link`: Dosya tipi.
    *   `Device`: Dosyanın bulunduğu aygıt numarası.
    *   `Inode`: Dosyanın benzersiz inode numarası.
    *   `Links`: Dosyaya işaret eden hard link sayısı.
    *   `Access (Uid/Gid)`: Sahip kullanıcı ID ve grup ID'si.
    *   `Access`, `Modify`, `Change` zaman damgaları.

##### echo

*   Argüman olarak verilen metni veya değişken değerlerini standart çıktıya yazdırır. Genellikle kabuk betiklerinde mesaj yazdırmak için kullanılır. Standart girdiden okuma yapmaz.
*   `echo "Merhaba Dünya"`
*   `echo "Ev dizinim: $HOME"`
*   `echo -e "Birinci satır\nİkinci satır"`: `-e` seçeneği ile `\n` (yeni satır), `\t` (tab) gibi kaçış karakterlerinin yorumlanmasını sağlar.

##### paste

*   Birden fazla dosyanın satırlarını yan yana birleştirir (varsayılan ayırıcı tab karakteridir).
*   `paste dosya1.txt dosya2.txt`: `dosya1`'in ilk satırı, bir tab, `dosya2`'nin ilk satırı; sonra ikinci satırlar şeklinde devam eder.
*   `paste -d ',' dosya1.txt dosya2.txt`: Ayırıcı olarak virgül kullanır.

##### sort

*   Girdi satırlarını (dosyadan veya standart girdiden) alfabetik veya numerik olarak sıralar.
*   `sort dosya.txt`: Satırları alfabetik olarak sıralar.
*   `sort -n dosya.txt`: Satırları numerik olarak sıralar.
*   `sort -r dosya.txt`: Ters sırada sıralar.
*   `sort -k 2 dosya.txt`: İkinci alana (sütuna) göre sıralar.
*   `ls -l | sort -k 5 -n`: Dosyaları boyutlarına göre (5. sütun) numerik olarak sıralar.

##### shuf (Shuffle)

*   Girdi satırlarını rastgele karıştırır.
*   `shuf dosya.txt`: Dosyanın satırlarını karıştırır.
*   `ls | shuf -n 3`: Listelenen dosyalardan rastgele 3 tanesini seçer.

##### nl (Number Lines)

*   Girdi satırlarını numaralandırarak yazdırır.
*   `nl dosya.txt`: Boş olmayan satırları numaralandırır.
*   `nl -ba dosya.txt`: Tüm satırları (boş olanlar dahil) numaralandırır.

##### wc (Word Count)

*   Dosyadaki veya standart girdideki satır, kelime ve byte/karakter sayılarını sayar.
*   `wc dosya.txt`: `satır_sayısı kelime_sayısı byte_sayısı dosya.txt` formatında çıktı verir.
*   `wc -l dosya.txt`: Sadece satır sayısını verir.
*   `wc -w dosya.txt`: Sadece kelime sayısını verir.
*   `wc -c dosya.txt`: Sadece byte sayısını verir.
*   `wc -m dosya.txt`: Sadece karakter sayısını verir (çok baytlı karakterleri doğru sayar).
*   `ls -1 | wc -l`: Mevcut dizindeki dosya/dizin sayısını verir (`ls -1` her girdiyi ayrı satıra yazar).

##### pipe (|) ile Filtreleme

Komutların çıktılarını birbirine bağlayarak karmaşık işlemler yapmak mümkündür. Her komut bir önceki komutun çıktısını işler.

*   `find /etc/ -name "*.conf" -type f 2> /dev/null | sort | nl | head -n 20`: `/etc` altında `.conf` uzantılı dosyaları bulur (hataları gizler), sonuçları sıralar, numaralandırır ve ilk 20 satırı gösterir.
*   Bu işlem geçici dosyalarla da yapılabilir:
    `find /etc/ -name "*.conf" -type f 2> /dev/null > bulunan.txt`
    `sort < bulunan.txt > sirali.txt`
    `nl < sirali.txt > numarali.txt`
    `head -n 20 numarali.txt`
    (Pipe kullanmak daha verimli ve pratiktir.)

##### xargs (Extended Arguments)

*   Standart girdiden okuduğu verileri (genellikle satır satır) bir komuta argüman olarak ekler. Standart girdiyi doğrudan kabul etmeyen komutlarla (örn: `echo`, `rm`, `cp`) pipe kullanmak gerektiğinde çok işe yarar.
*   `cat silinecek_dosyalar.txt | xargs rm`: `silinecek_dosyalar.txt` içindeki her satırı `rm` komutuna argüman olarak verir.
*   `find . -name "*.tmp" | xargs rm`: Bulunan `.tmp` uzantılı dosyaları siler.
*   `find . -name "*.log" -print0 | xargs -0 rm`: Dosya adlarında boşluk veya özel karakterler olabilecek durumlar için `-print0` (null karakterle ayır) ve `xargs -0` (null karakterle oku) kullanılır, bu daha güvenli bir yöntemdir.

##### tee (T Borusu)

*   Standart girdiden okuduğu veriyi hem standart çıktıya (genellikle ekrana veya bir sonraki pipe'a) hem de belirtilen bir veya daha fazla dosyaya yazar. Boru hattındaki veriyi bir yandan izlerken bir yandan kaydetmek için kullanılır.
*   `ls -l | tee dosya_listesi.txt | less`: `ls -l` çıktısını hem `dosya_listesi.txt` dosyasına yazar hem de `less` komutuna gönderir.
*   `echo "Yeni ayar" | sudo tee -a /etc/yapilandirma.conf`: Standart çıktıdan gelen "Yeni ayar" metnini `sudo` yetkisiyle `/etc/yapilandirma.conf` dosyasının sonuna ekler. `sudo echo "..." >> /etc/...` komutu genellikle izin hatası verir çünkü yönlendirme (`>>`) işlemi `sudo` yetkisi alınmadan önce kabuk tarafından yapılır, `tee` bu sorunu çözer. `-a` (append) seçeneği dosyanın üzerine yazmak yerine sonuna ekler.

##### grep (Global Regular Expression Print)

*   Dosyalarda veya standart girdide belirtilen bir deseni (metin veya regex) arar ve eşleşen satırları standart çıktıya yazar.
*   `grep "aranan_metin" dosya.txt`: `dosya.txt` içinde "aranan_metin" geçen satırları bulur.
*   `cat log.txt | grep "ERROR"`: `log.txt` içeriğini `grep`'e yönlendirerek "ERROR" içeren satırları filtreler.
*   `grep -i "metin" dosya.txt`: Büyük/küçük harf duyarsız arama yapar (ignore case).
*   `grep -v "metin" dosya.txt`: "metin" içermeyen satırları gösterir (invert match).
*   `grep -r "metin" /dizin/yolu`: Belirtilen dizin ve alt dizinlerindeki dosyalarda "metin" arar (recursive).
*   `grep -l "metin" *.txt`: İçinde "metin" geçen `.txt` dosyalarının sadece adlarını listeler (list filenames).
*   `grep -n "metin" dosya.txt`: Eşleşen satırların numaralarını da gösterir.
*   `grep -E "desen1|desen2" dosya.txt`: Genişletilmiş Regex kullanarak "desen1" veya "desen2" içeren satırları bulur (Extended Regex). `egrep` komutu ile aynı işlevi görür.
*   `grep "^baslangic" dosya.txt`: Satır başında "baslangic" ile başlayanları bulur.
*   `grep "son$" dosya.txt`: Satır sonunda "son" ile bitenleri bulur.

###### Basit Regex Kuralları (grep, sed, awk için)

*   `.`: Herhangi tek bir karakterle eşleşir (yeni satır `\n` hariç).
*   `*`: Kendinden önceki karakterin sıfır veya daha fazla kez tekrarıyla eşleşir (`a*` -> "", "a", "aa", "aaa"...).
*   `+`: Kendinden önceki karakterin bir veya daha fazla kez tekrarıyla eşleşir (`a+` -> "a", "aa", "aaa"...). (Genellikle `-E` gerektirir).
*   `?`: Kendinden önceki karakterin sıfır veya bir kez tekrarıyla eşleşir (`a?` -> "" veya "a"). (Genellikle `-E` gerektirir).
*   `^`: Satırın başlangıcıyla eşleşir.
*   `$`: Satırın sonuyla eşleşir.
*   `[]`: Karakter kümesi. İçindeki karakterlerden herhangi biriyle eşleşir (`[abc]`). Aralık belirtilebilir (`[a-z]`, `[0-9]`).
*   `[^...]`: Ters karakter kümesi. İçindeki karakterler *dışındaki* herhangi bir karakterle eşleşir (`[^0-9]` -> rakam olmayan).
*   `{n}`: Kendinden önceki karakterin tam olarak `n` kez tekrarıyla eşleşir (`a{3}` -> "aaa"). (Genellikle `-E` gerektirir).
*   `{n,}`: Kendinden önceki karakterin en az `n` kez tekrarıyla eşleşir (`a{2,}` -> "aa", "aaa"...). (Genellikle `-E` gerektirir).
*   `{n,m}`: Kendinden önceki karakterin en az `n`, en fazla `m` kez tekrarıyla eşleşir (`a{2,4}` -> "aa", "aaa", "aaaa"). (Genellikle `-E` gerektirir).
*   `|`: Veya (Alternation). İki desenden biriyle eşleşir (`kedi|köpek`). (Genellikle `-E` gerektirir).
*   `()`: Gruplama. Desenleri gruplamak veya yakalamak için kullanılır (`(ab)+` -> "ab", "abab"...). (Genellikle `-E` gerektirir).
*   `\`: Özel karakterlerin (örn: `.`, `*`, `[`, `\`) özel anlamını kaldırıp normal karakter olarak eşleşmesini sağlar (kaçış karakteri). `grep "\." dosya.txt` -> nokta karakterini arar.

##### find

*   Belirtilen bir dizin ağacında (alt dizinler dahil) dosyaları ve dizinleri çeşitli kriterlere göre arar.
*   `find /yol/dizin -name "aranan_ad"`: Belirtilen yolda tam adı "aranan_ad" olan dosyaları/dizinleri bulur. Joker karakterler (`*`, `?`, `[]`) kullanılabilir (tırnak içinde yazmak genellikle iyidir). `find . -name "*.log"`
*   `find . -iname "aranan_ad"`: `-name` gibi ama büyük/küçük harf duyarsız arama yapar.
*   `find /yol -type f`: Sadece dosyaları bulur.
*   `find /yol -type d`: Sadece dizinleri bulur.
*   `find /yol -type l`: Sadece sembolik linkleri bulur.
*   `find /yol -size +10M`: Boyutu 10 Megabyte'tan büyük dosyaları bulur (`+`: büyük, `-`: küçük. `k`: Kilobyte, `M`: Megabyte, `G`: Gigabyte).
*   `find /yol -mtime +7`: Son 7 günden daha önce değiştirilmiş dosyaları bulur (`+`: daha eski, `-`: daha yeni. `mmin` dakika cinsinden).
*   `find /yol -user kullanici_adi`: Belirtilen kullanıcıya ait dosyaları bulur.
*   `find /yol -group grup_adi`: Belirtilen gruba ait dosyaları bulur.
*   `find /yol -perm 644`: İzinleri tam olarak 644 olan dosyaları bulur. `-perm /644` en az bu izinlere sahip olanları bulur.
*   `find /yol -empty`: Boş dosyaları veya dizinleri bulur.
*   `find /yol -name "*.tmp" -delete`: Bulunan `.tmp` uzantılı dosyaları siler.
*   `find /yol -name "*.log" -exec rm {} \;`: Bulunan her `.log` dosyası için `rm` komutunu çalıştırır. `{}` bulunan dosyayı temsil eder, `\;` komutun sonunu belirtir. Daha verimli alternatif: `find /yol -name "*.log" -exec rm {} +` (birden çok dosyayı tek `rm` komutuna argüman olarak verir).
*   `find . \( -name "*.txt" -or -name "*.log" \) -type f`: Adı `.txt` veya `.log` ile biten dosyaları bulur (`-or`, `-and` (varsayılan), `-not` kullanılabilir, parantezler `\(` ve `\)` ile kaçış gerektirir).
*   `find . -regex ".*\.py$"`: Adı `.py` ile biten dosyaları bulmak için Regex kullanır. `-regex` tüm yolu (sadece dosya adını değil) desene göre kontrol eder.

##### locate

*   Sistemdeki dosyaları hızlı bir şekilde bulmak için önceden oluşturulmuş bir veritabanını kullanır. `find` komutuna göre çok daha hızlıdır ancak veritabanı güncel değilse yeni oluşturulan/silinen dosyaları bulamayabilir/gösterebilir.
*   `locate dosya_adi`: Veritabanında dosya adını arar.
*   `sudo updatedb`: `locate` komutunun kullandığı veritabanını günceller. Yeni dosya ekledikten/sildikten sonra çalıştırmak gerekebilir.

##### cut

*   Dosya veya standart girdideki satırların belirli bölümlerini (sütunları veya karakter aralıklarını) kesip alır.
*   `cut -d ':' -f 1 /etc/passwd`: `/etc/passwd` dosyasında `:` karakterini ayırıcı olarak kullanarak her satırın 1. alanını (kullanıcı adı) alır.
*   `cut -c 1-10 dosya.txt`: Her satırın ilk 10 karakterini alır.
*   `ls -l | cut -c 50-`: `ls -l` çıktısının her satırında 50. karakterden sonrasını alır (dosya adlarını almaya yakın).

##### tr (Translate)

*   Standart girdiden okuduğu verideki karakterleri değiştirir veya siler.
*   `echo "Merhaba Dunya" | tr 'a-z' 'A-Z'`: Küçük harfleri büyük harfe çevirir -> `MERHABA DUNYA`.
*   `echo "Bu:bir:test" | tr ':' ' '`: `:` karakterlerini boşlukla değiştirir -> `Bu bir test`.
*   `cat dosya.txt | tr -d '\r' > yeni_dosya.txt`: Windows satır sonu karakterlerini (`\r`) siler (DOS'tan Unix'e dönüştürme). `-d` (delete) silme işlemi yapar.
*   `echo "Tekrarlarrrr varrr" | tr -s 'r'`: Tekrar eden `r` karakterlerini teke indirir -> `Tekrarlar var`. `-s` (squeeze-repeats).
*   `cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1`: Rastgele alfanümerik 32 karakterlik bir parola üretir.
    *   `tr -dc 'a-zA-Z0-9'`: Girdideki alfanümerik olmayan tüm karakterleri siler (`-d` delete, `-c` complement).
    *   `fold -w 32`: Akışı 32 karakterlik satırlara böler.
    *   `head -n 1`: İlk satırı alır.

##### sed (Stream Editor)

*   Metin akışları (dosya veya standart girdi) üzerinde düzenleme (bulma, değiştirme, ekleme, silme) yapan güçlü bir araçtır. Genellikle betiklerde otomatik metin işleme için kullanılır.
*   Temel Kullanım: `sed 'komut' dosya.txt` veya `komut_ciktisi | sed 'komut'`
*   **`s` (Substitute - Değiştirme):** `sed 's/eski/yeni/g' dosya.txt`
    *   `s`: Değiştirme komutu.
    *   `/`: Ayırıcı karakter (başka karakterler de kullanılabilir: `sed 's#eski#yeni#g'`).
    *   `eski`: Aranacak desen (metin veya regex).
    *   `yeni`: Yerine konulacak metin.
    *   `g` (global): Satırdaki tüm eşleşmeleri değiştirir. Olmazsa sadece ilk eşleşme değişir.
    *   Örnek: `sed 's/elma/armut/g' meyveler.txt`
*   **Adresleme:** Komutların hangi satırlarda uygulanacağını belirtir.
    *   `sed '3s/a/A/g' dosya.txt`: Sadece 3. satırda değiştirme yapar.
    *   `sed '1,5s/a/A/g' dosya.txt`: 1. satırdan 5. satıra kadar (dahil) değiştirme yapar.
    *   `sed '/^#/d' dosya.txt`: `#` ile başlayan satırları siler (`d` komutu). `/.../` adresleme için regex kullanır.
*   **`d` (Delete - Silme):** Belirtilen adreslerdeki satırları siler.
    *   `sed '5d' dosya.txt`: 5. satırı siler.
    *   `sed '/^\s*$/d' dosya.txt`: Boş veya sadece boşluk içeren satırları siler.
*   **`p` (Print - Yazdırma):** Belirtilen adreslerdeki satırları yazdırır. Genellikle `-n` seçeneği ile kullanılır (`-n` varsayılan yazdırmayı engeller).
    *   `sed -n '10p' dosya.txt`: Sadece 10. satırı yazdırır.
    *   `sed -n '/hata/p' log.txt`: "hata" içeren satırları yazdırır (`grep "hata" log.txt` ile benzer).
*   **`a` (Append - Sonrasına Ekle):** Belirtilen adresteki satırdan *sonra* yeni bir satır ekler.
    *   `sed '3a Yeni eklenen satır' dosya.txt`: 3. satırdan sonra metni ekler.
*   **`i` (Insert - Öncesine Ekle):** Belirtilen adresteki satırdan *önce* yeni bir satır ekler.
    *   `sed '1i ## Başlık ##' dosya.txt`: 1. satırdan önce metni ekler.
*   **`-e`:** Birden fazla `sed` komutunu aynı anda çalıştırmak için kullanılır.
    *   `sed -e 's/eski1/yeni1/' -e 's/eski2/yeni2/' dosya.txt`
*   **`-i`:** Dosyayı yerinde düzenler (çıktıyı ekrana vermek yerine doğrudan dosyayı değiştirir). **Dikkatli kullanılmalıdır!** Yedek almak için `-i.bak` şeklinde kullanılabilir.
    *   `sed -i 's/HATA/UYARI/g' log.txt`

##### awk

*   Güçlü bir metin işleme ve raporlama dilidir. Satırları kayıtlara (records), satır içindeki boşlukla ayrılmış bölümleri alanlara (fields) ayırarak çalışır. `sed`'den daha karmaşık işlemler ve programlama mantığı için uygundur. `gawk` (GNU awk) en yaygın sürümüdür.
*   **Temel Yapı:** `awk 'desen { aksiyon }' dosya.txt`
    *   `desen`: Hangi satırlarda işlem yapılacağını belirler (regex veya koşul). Desen belirtilmezse tüm satırlarda işlem yapılır.
    *   `aksiyon`: Desenle eşleşen satırlar için yapılacak işlemler (genellikle `print` kullanılır). Aksiyon belirtilmezse varsayılan aksiyon `{ print $0 }` (tüm satırı yazdır) çalışır.
*   **Alanlar (Fields):**
    *   `$0`: Tüm satır (kayıt).
    *   `$1`: Birinci alan.
    *   `$2`: İkinci alan.
    *   `$NF`: Son alan (Number of Fields).
*   **Örnekler:**
    *   `awk '{ print $1 }' dosya.txt`: Her satırın ilk alanını yazdırır.
    *   `awk '{ print $NF }' dosya.txt`: Her satırın son alanını yazdırır.
    *   `ls -l | awk '{ print $9 " -> " $1 }'`: `ls -l` çıktısının 9. (dosya adı) ve 1. (izinler) alanlarını yazdırır.
    *   `awk '/hata/ { print $0 }' log.txt`: "hata" içeren satırları yazdırır (`grep "hata" log.txt` gibi).
    *   `awk '$3 > 100 { print $1, $3 }' veri.txt`: 3. alanı 100'den büyük olan satırların 1. ve 3. alanlarını yazdırır.
    *   `awk -F ':' '{ print $1 }' /etc/passwd`: Ayırıcı olarak `:` kullanarak (`-F ':'`) `/etc/passwd` dosyasının ilk alanını (kullanıcı adları) yazdırır.
    *   `awk 'BEGIN { print "Başlık" } { print $1 } END { print "Toplam:", NR }' dosya.txt`: İşlem başlamadan önce "Başlık" yazar (`BEGIN`), her satırın ilk alanını yazar, işlem bittikten sonra toplam satır sayısını (`NR` - Number of Records) yazar (`END`).

#### Sayfalama Araçları (Pagers)

Uzun çıktıları ekranda sayfa sayfa görüntülemek için kullanılır.

##### more

*   Temel sayfalama aracıdır.
*   `ls -l /etc | more`: Çıktıyı sayfa sayfa gösterir.
*   `Space`: Sonraki sayfa.
*   `Enter`: Sonraki satır.
*   `q`: Çıkış.
*   Geriye doğru gitme özelliği yoktur.

##### less

*   `more` komutundan daha gelişmiş ve esnek bir sayfalama aracıdır.
*   `ls -l /etc | less`: Çıktıyı `less` ile açar.
*   `Space` veya `f`: Sonraki sayfa.
*   `b`: Önceki sayfa.
*   `Yukarı/Aşağı Ok Tuşları`: Satır satır gezinme.
*   `/desen`: İleriye doğru arama.
*   `?desen`: Geriye doğru arama.
*   `n`: Sonraki eşleşme.
*   `N`: Önceki eşleşme.
*   `q`: Çıkış.

##### head

*   Dosyanın veya standart girdinin başlangıç kısmını (varsayılan olarak ilk 10 satırı) gösterir.
*   `head dosya.txt`: İlk 10 satırı gösterir.
*   `head -n 5 dosya.txt`: İlk 5 satırı gösterir.
*   `head -c 20 dosya.txt`: İlk 20 byte'ı gösterir.

##### tail

*   Dosyanın veya standart girdinin son kısmını (varsayılan olarak son 10 satırı) gösterir. Log dosyalarını takip etmek için çok kullanışlıdır.
*   `tail dosya.txt`: Son 10 satırı gösterir.
*   `tail -n 20 dosya.txt`: Son 20 satırı gösterir.
*   `tail -c 50 dosya.txt`: Son 50 byte'ı gösterir.
*   `tail -f log.txt`: Dosyanın sonuna eklenen yeni satırları gerçek zamanlı olarak takip eder (follow). `Ctrl+C` ile çıkılır.

#### Dosya ve Dizin Yönetimi

##### cp (Copy)

*   Dosyaları veya dizinleri kopyalar.
*   `cp kaynak_dosya hedef_dosya`: Dosyayı kopyalar ve yeni bir isim verir.
*   `cp kaynak_dosya hedef_dizin/`: Dosyayı belirtilen dizine kopyalar.
*   `cp dosya1 dosya2 dosya3 hedef_dizin/`: Birden çok dosyayı bir dizine kopyalar.
*   `cp -r kaynak_dizin hedef_dizin/`: Dizini ve içeriğini özyinelemeli olarak kopyalar.
*   `cp -i`: Kopyalama sırasında üzerine yazma durumunda onay ister (interactive).
*   `cp -v`: Kopyalanan dosyaları gösterir (verbose).
*   `cp -p`: İzinler, sahip bilgisi ve zaman damgalarını koruyarak kopyalar (preserve).

##### mv (Move)

*   Dosyaları veya dizinleri taşır veya yeniden adlandırır.
*   `mv eski_ad yeni_ad`: Dosyayı/dizini yeniden adlandırır.
*   `mv kaynak_dosya hedef_dizin/`: Dosyayı belirtilen dizine taşır.
*   `mv dosya1 dosya2 dizin1 hedef_dizin/`: Birden çok dosyayı/dizini bir dizine taşır.
*   `mv -i`: Taşıma sırasında üzerine yazma durumunda onay ister.
*   `mv -n`: Üzerine yazma durumunda işlemi yapmaz (no-clobber).
*   `mv -v`: Taşınan dosyaları gösterir.

##### rm (Remove)

*   Dosyaları veya dizinleri siler (Yukarıda detayları verilmişti). **Dikkatli kullanılmalıdır!**

##### shred (Secure Delete)

*   Dosyaların içeriğini diskten kurtarılmasını zorlaştırmak için üzerine rastgele veriler yazarak kalıcı olarak siler. Normal `rm` sadece dosyanın işaretçisini (inode bağlantısını) kaldırır, verinin kendisi üzerine yazılana kadar diskte kalabilir.
*   `shred dosya.txt`: Varsayılan olarak 3 kez dosyanın üzerine rastgele veri yazar.
*   `shred -n 5 dosya.txt`: 5 kez üzerine yazar.
*   `shred -u dosya.txt`: Üzerine yazdıktan sonra dosyayı siler (`rm` gibi).
*   `shred -v dosya.txt`: İşlem adımlarını gösterir.
*   `shred -z dosya.txt`: Son olarak üzerine sıfırlarla yazar (rastgele veri yazdığını gizlemek için).
*   `shred -uvz -n 10 gizli_dosya.txt`: 10 kez rastgele veri yazar, son olarak sıfırlarla yazar, adımları gösterir ve dosyayı siler.

#### Linkler (Links)

Dosyalara veya dizinlere farklı isimlerle erişim sağlayan işaretçilerdir.

*   **Hard Link (Sert Bağlantı):**
    *   Aynı dosya verisine (aynı inode'a) işaret eden birden fazla dosya adı oluşturur.
    *   Orijinal dosya silinse bile, hard link var olduğu sürece dosya verisi diskte kalır ve erişilebilir olur.
    *   Sadece aynı dosya sistemi (partition) içinde oluşturulabilir.
    *   Dizinler için genellikle hard link oluşturulamaz (döngüsel referans riskinden dolayı).
    *   Oluşturma: `ln kaynak_dosya hard_link_adi`
    *   `ls -li` komutu ile inode numaraları ve link sayıları görülebilir. Hard linklerin inode numaraları aynıdır ve link sayıları artar.
*   **Soft Link (Symbolic Link - Sembolik Bağlantı):**
    *   Bir dosya veya dizinin yolunu (path) içeren özel bir dosyadır (Windows'taki kısayol gibi).
    *   Orijinal dosya veya dizine bir işaretçi görevi görür.
    *   Orijinal dosya silinirse veya yeri değişirse soft link çalışmaz hale gelir ("kırık link").
    *   Farklı dosya sistemleri arasında oluşturulabilir.
    *   Dizinler için de oluşturulabilir.
    *   Oluşturma: `ln -s /tam/yol/kaynak_dosya_veya_dizin soft_link_adi`
    *   `ls -l` komutu ile `l` harfiyle başlar ve `->` ile işaret ettiği hedefi gösterir.

#### Arşivleme ve Sıkıştırma

##### tar (Tape Archive)

*   Birden fazla dosyayı ve dizini tek bir arşiv dosyasında (`.tar`) birleştirir. Varsayılan olarak sıkıştırma yapmaz, sadece dosyaları paketler.
*   **Arşiv Oluşturma:** `tar -cf arsiv_adi.tar dosya1 dizin1 ...`
    *   `-c`: Create (Yeni arşiv oluştur).
    *   `-f`: File (Arşiv dosyasının adını belirtir. Bu seçenekten hemen sonra arşiv adı gelmelidir).
    *   `-v`: Verbose (İşlem yapılan dosyaları listeler). `tar -cvf arsiv.tar dosyalar/`
*   **Arşiv İçeriğini Listeleme:** `tar -tf arsiv_adi.tar`
    *   `-t`: List (Arşivin içeriğini göster).
*   **Arşivden Dosya Çıkarma (Ayıklama):** `tar -xf arsiv_adi.tar`
    *   `-x`: Extract (Arşivden dosyaları çıkar).
    *   `tar -xf arsiv.tar -C /hedef/dizin`: Arşivi belirtilen hedef dizine çıkarır.
    *   `tar -xvf arsiv.tar`: Çıkarılan dosyaları listeler.
*   **Arşive Dosya Ekleme:** `tar -rf arsiv_adi.tar eklenecek_dosya`
    *   `-r` veya `--append`: Var olan arşive dosya ekler (çok verimli olmayabilir).
*   **Arşivden Dosya Silme:** `tar --delete -f arsiv_adi.tar silinecek_dosya`
    *   `--delete`: Arşivden dosya siler (çok verimli olmayabilir).

##### Sıkıştırma Araçları (gzip, bzip2, xz)

*   Dosyaların boyutunu küçültmek için kullanılırlar. Genellikle `tar` ile birlikte kullanılırlar.
*   **gzip:** Yaygın kullanılan, hızlı bir sıkıştırma aracıdır. `.gz` uzantısını kullanır.
    *   `gzip dosya.txt`: `dosya.txt`'yi sıkıştırır ve `dosya.txt.gz` oluşturur, orijinal dosyayı siler.
    *   `gzip -k dosya.txt`: Orijinal dosyayı silmeden sıkıştırır (keep).
    *   `gzip -d dosya.txt.gz`: Sıkıştırılmış dosyayı açar (`gunzip dosya.txt.gz` ile aynı).
    *   `gzip -r dizin/`: Dizindeki tüm dosyaları özyinelemeli olarak sıkıştırır.
*   **bzip2:** `gzip`'e göre genellikle daha iyi sıkıştırma oranı sunar ancak daha yavaştır. `.bz2` uzantısını kullanır.
    *   `bzip2 dosya.txt`
    *   `bzip2 -k dosya.txt`
    *   `bzip2 -d dosya.txt.bz2` (`bunzip2 dosya.txt.bz2` ile aynı).
*   **xz:** Genellikle en iyi sıkıştırma oranını sunar ancak en yavaş olanıdır. `.xz` uzantısını kullanır.
    *   `xz dosya.txt`
    *   `xz -k dosya.txt`
    *   `xz -d dosya.txt.xz` (`unxz dosya.txt.xz` ile aynı).

##### Tek Seferde Arşivleme ve Sıkıştırma (`tar` ile)

`tar` komutu sıkıştırma araçlarını doğrudan çağırabilir.

*   **gzip ile:** `tar -czf arsiv_adi.tar.gz dizin_veya_dosyalar`
    *   `-z`: gzip kullanarak sıkıştır/aç.
*   **bzip2 ile:** `tar -cjf arsiv_adi.tar.bz2 dizin_veya_dosyalar`
    *   `-j`: bzip2 kullanarak sıkıştır/aç.
*   **xz ile:** `tar -cJf arsiv_adi.tar.xz dizin_veya_dosyalar`
    *   `-J`: xz kullanarak sıkıştır/aç.

*   **Sıkıştırılmış Arşivi Açma:**
    *   `tar -xzf arsiv_adi.tar.gz`
    *   `tar -xjf arsiv_adi.tar.bz2`
    *   `tar -xJf arsiv_adi.tar.xz`
    (Genellikle `tar -xf arsiv_adi` komutu dosya uzantısına bakarak doğru sıkıştırma yöntemini otomatik algılar.)

##### Sıkıştırılmış Dosyaları Okuma Araçları

*   `zcat dosya.gz`: `.gz` uzantılı dosyayı açmadan içeriğini ekrana basar (`gzcat` ile aynı).
*   `zless dosya.gz`: `.gz` uzantılı dosyayı açmadan `less` ile görüntüler.
*   `zgrep desen dosya.gz`: `.gz` uzantılı dosyayı açmadan içinde desen arar.
*   `bzcat`, `bzless`, `bzgrep` (`.bz2` için)
*   `xzcat`, `xzless`, `xzgrep` (`.xz` için)

#### Sistem Bilgisi Komutları

##### date

*   Sistemin tarih ve saatini gösterir veya ayarlar.
*   `date`: Mevcut tarih ve saati gösterir.
*   `date +"%Y-%m-%d %H:%M:%S"`: Belirtilen formatta tarih ve saati gösterir.

##### cal (Calendar)

*   Takvimi gösterir.
*   `cal`: İçinde bulunulan ayın takvimini gösterir.
*   `cal 2025`: 2025 yılının tamamını gösterir.
*   `cal 5 2025`: Mayıs 2025 takvimini gösterir.

##### which

*   Bir komutun çalıştırılabilir dosyasının tam yolunu `$PATH` değişkeninde arayarak bulur.
*   `which ls` -> `/bin/ls` (veya benzeri)
*   `which python`

##### type

*   Bir komutun türünü belirtir (alias, keyword, function, builtin, file).
*   `type cd` -> `cd is a shell builtin`
*   `type ls` -> `ls is aliased to 'ls --color=auto'` (eğer alias tanımlıysa) veya `ls is /bin/ls`
*   `type -a komut`: Komut adıyla eşleşen tüm türleri gösterir (örn: hem alias hem dosya varsa).

##### file

*   Bir dosyanın türünü içeriğine bakarak tahmin etmeye çalışır.
*   `file belge.txt` -> `belge.txt: ASCII text`
*   `file resim.jpg` -> `resim.jpg: JPEG image data, ...`
*   `file /bin/bash` -> `/bin/bash: ELF 64-bit LSB executable, ...`

##### lsb_release

*   Linux Standard Base (LSB) ve dağıtım hakkındaki bilgileri gösterir.
*   `lsb_release -a`: Tüm bilgileri gösterir (Distributor ID, Description, Release, Codename).

##### uname (Unix Name)

*   Sistem çekirdeği ve işletim sistemi hakkındaki temel bilgileri gösterir.
*   `uname`: Çekirdek adını gösterir (`Linux`).
*   `uname -a`: Tüm bilgileri gösterir (çekirdek adı, hostname, çekirdek sürümü, makine mimarisi vb.).
*   `uname -r`: Çekirdek sürümünü gösterir.
*   `uname -m`: Makine donanım adını (mimariyi) gösterir (`x86_64` gibi).

##### uptime

*   Sistemin ne kadar süredir çalıştığını, mevcut kullanıcı sayısını ve sistem yük ortalamalarını gösterir.

##### free

*   Sistemdeki toplam, kullanılan ve boş bellek (RAM) miktarını ve takas (swap) alanı kullanımını gösterir.
*   `free`: Varsayılan olarak kilobyte cinsinden gösterir.
*   `free -h`: Okunabilir formatta (MB, GB) gösterir (human-readable).
*   `free -m`: Megabyte cinsinden gösterir.

##### du (Disk Usage)

*   Dosya veya dizinlerin diskte kapladığı alanı hesaplar.
*   `du dosya.txt`: Dosyanın kapladığı alanı (genellikle kilobyte cinsinden blok sayısı) gösterir.
*   `du dizin/`: Dizinin ve içindeki alt dizinlerin ayrı ayrı kapladığı alanları gösterir.
*   `du -sh dizin/`: Dizinin toplam boyutunu okunabilir formatta gösterir (`-s`: summary, `-h`: human-readable).
*   `du -h --max-depth=1 /home/user`: Belirtilen dizinin altındaki birinci seviye dosya ve dizinlerin boyutlarını okunabilir formatta gösterir.

##### df (Disk Free)

*   Bağlı olan dosya sistemlerinin toplam boyutunu, kullanılan alanı, boş alanı ve bağlanma noktasını gösterir.
*   `df`: Tüm bağlı dosya sistemlerini gösterir (genellikle 1K bloklar halinde).
*   `df -h`: Okunabilir formatta gösterir.
*   `df -T`: Dosya sistemi türünü de gösterir.
*   `df .`: Mevcut dizinin bulunduğu dosya sisteminin bilgilerini gösterir.

#### Paket Yönetimi

Linux dağıtımlarında yazılımların (paketlerin) kurulması, güncellenmesi, kaldırılması ve yönetilmesi işlemlerini kolaylaştıran sistemlerdir.

*   **Kaynak Koddan Kurulum:** Paket yöneticileri öncesinde, yazılımlar genellikle kaynak kodları indirilip, derlenip (`./configure`, `make`, `sudo make install`) sisteme manuel olarak kurulurdu. Bağımlılıkların (yazılımın çalışması için gereken diğer kütüphane ve programlar) da manuel olarak bulunup kurulması gerekirdi. Bu yöntem hala kullanılsa da zahmetli ve yönetimi zordur.
*   **Paket Yöneticileri:** Bu süreci otomatikleştirirler. Yazılımları önceden derlenmiş, kuruluma hazır paketler halinde sunuculardan (repository - depo) indirir, bağımlılıkları otomatik olarak çözer ve kurar, güncellemeleri ve kaldırma işlemlerini kolayca yapmayı sağlarlar.

##### Debian Tabanlı Sistemler (Debian, Ubuntu, Mint vb.)

*   **Paket Formatı:** `.deb`
*   **Düşük Seviye Araç:** `dpkg` (Paketleri doğrudan kurar, kaldırır, sorgular ama bağımlılıkları otomatik çözmez).
    *   `sudo dpkg -i paket_adi.deb`: Paketi kurar.
    *   `sudo dpkg -r paket_adi`: Paketi kaldırır (yapılandırma dosyalarını bırakır).
    *   `sudo dpkg -P paket_adi`: Paketi tamamen kaldırır (purge).
    *   `dpkg -l | grep paket_adi`: Paketin kurulu olup olmadığını kontrol eder.
*   **Yüksek Seviye Araç:** `apt` (Advanced Package Tool - `apt-get`, `apt-cache` gibi araçların modern birleşimi). Bağımlılıkları yönetir, depolardan paketleri bulur, indirir ve kurar.
    *   `sudo apt update`: Paket listelerini depolardan günceller. Kurulum/güncelleme yapmadan önce çalıştırılması önerilir.
    *   `sudo apt upgrade`: Kurulu paketleri mevcut en güncel sürümlerine yükseltir.
    *   `sudo apt full-upgrade` (veya `dist-upgrade`): `upgrade` gibi çalışır ancak sistemin temel bileşenlerini değiştirmesi veya yeni paketler kurması/kaldırması gerekirse bunu da yapar.
    *   `sudo apt install paket_adi`: Yeni bir paket kurar veya kurulu paketi günceller.
    *   `sudo apt remove paket_adi`: Paketi kaldırır (yapılandırma dosyalarını bırakır).
    *   `sudo apt purge paket_adi`: Paketi tamamen kaldırır.
    *   `sudo apt autoremove`: Artık ihtiyaç duyulmayan (bağımlılık olarak kurulmuş ama ana paket kaldırılmış) paketleri temizler.
    *   `apt search anahtar_kelime`: Depolarda anahtar kelimeye göre paket arar.
    *   `apt show paket_adi`: Paket hakkındaki detaylı bilgileri gösterir.
    *   `sudo apt install -f`: Bozuk bağımlılıkları düzeltmeye çalışır (fix-broken).
    *   `sudo apt clean`: İndirilen `.deb` paketlerinin önbelleğini (`/var/cache/apt/archives/`) temizler.
*   **Depo Listesi:** `/etc/apt/sources.list` dosyası ve `/etc/apt/sources.list.d/` dizinindeki dosyalar, `apt`'nin paketleri indireceği sunucu adreslerini (repositories) içerir. Bu dosyalarda değişiklik yapıldıktan sonra `sudo apt update` çalıştırılmalıdır.

##### Red Hat Tabanlı Sistemler (RHEL, CentOS, Fedora, Oracle Linux vb.)

*   **Paket Formatı:** `.rpm`
*   **Düşük Seviye Araç:** `rpm` (Paketleri doğrudan yönetir, bağımlılıkları otomatik çözmez).
    *   `sudo rpm -i paket_adi.rpm`: Paketi kurar (install).
    *   `sudo rpm -U paket_adi.rpm`: Paketi günceller (upgrade), kurulu değilse kurar.
    *   `sudo rpm -e paket_adi`: Paketi kaldırır (erase).
    *   `rpm -q paket_adi`: Paketin kurulu olup olmadığını sorgular (query).
    *   `rpm -qa`: Kurulu tüm paketleri listeler.
*   **Yüksek Seviye Araç:** `yum` (Yellowdog Updater, Modified) veya `dnf` (Dandified YUM - `yum`'un modern ve genellikle daha hızlı halefi). Bağımlılıkları yönetir, depolardan paketleri bulur, indirir ve kurar. (Komutlar genellikle `yum` ve `dnf` için benzerdir, modern sistemlerde `dnf` tercih edilir).
    *   `sudo dnf check-update` (veya `yum check-update`): Güncellenebilecek paketleri listeler.
    *   `sudo dnf update` (veya `yum update`): Kurulu tüm paketleri günceller.
    *   `sudo dnf install paket_adi` (veya `yum install paket_adi`): Yeni bir paket kurar.
    *   `sudo dnf remove paket_adi` (veya `yum remove paket_adi`): Paketi kaldırır.
    *   `sudo dnf autoremove` (veya `yum autoremove`): Artık ihtiyaç duyulmayan bağımlılıkları kaldırır.
    *   `dnf search anahtar_kelime` (veya `yum search anahtar_kelime`): Depolarda paket arar.
    *   `dnf info paket_adi` (veya `yum info paket_adi`): Paket hakkındaki bilgileri gösterir.
    *   `sudo dnf clean all` (veya `yum clean all`): Paket önbelleğini temizler.
*   **Depo Listesi:** `/etc/yum.repos.d/` dizinindeki `.repo` uzantılı dosyalar depo bilgilerini içerir.

#### Kullanıcı ve Grup Yönetimi

Linux çok kullanıcılı bir sistemdir. Kullanıcılar ve gruplar, dosya erişim izinlerini ve sistem kaynaklarına erişimi yönetmek için kullanılır.

##### Kullanıcı Türleri

*   **Root (Super User):** Kullanıcı ID'si (UID) 0 olan, sistem üzerinde tam yetkiye sahip özel kullanıcıdır. Sistem yönetimi için kullanılır.
*   **System Users (Sistem Kullanıcıları):** Belirli servisleri veya uygulamaları çalıştırmak için oluşturulan, genellikle oturum açma yetkisi olmayan kullanıcılardır (örn: `www-data`, `nobody`). UID'leri genellikle belirli bir aralıkta (örn: 1-999) olur.
*   **Normal Users (Normal Kullanıcılar):** Sistemi günlük işler için kullanan standart kullanıcılardır. UID'leri genellikle 1000 ve üzeridir. Sınırlı yetkilere sahiptirler, kendi dosyaları dışında sistem dosyalarını değiştiremezler.

##### `sudo` Komutu

Normal kullanıcıların, kendi şifrelerini girerek geçici olarak `root` yetkileriyle veya başka bir kullanıcı olarak komut çalıştırmasını sağlar. Hangi kullanıcıların hangi komutları `sudo` ile çalıştırabileceği `/etc/sudoers` dosyasında veya `/etc/sudoers.d/` dizinindeki dosyalarda tanımlanır. Bu dosyaları düzenlemek için `sudo visudo` komutu kullanılmalıdır (sentaks kontrolü yapar).

##### Kullanıcı Oluşturma ve Yönetme

*   `sudo adduser yeni_kullanici`: İnteraktif olarak yeni bir kullanıcı oluşturur (ev dizini, grup oluşturma, şifre sorma vb. adımları içerir). Genellikle tercih edilen yöntemdir.
*   `sudo useradd yeni_kullanici`: Daha düşük seviyeli bir komuttur, sadece kullanıcıyı oluşturur. Ev dizini oluşturmak için `-m`, grup belirtmek için `-g`, ek gruplar için `-G`, kabuk belirtmek için `-s` gibi seçenekler manuel olarak eklenebilir.
*   `sudo passwd kullanici_adi`: Kullanıcının şifresini ayarlar veya değiştirir. Yeni oluşturulan kullanıcıya şifre atamak için gereklidir.
*   `sudo userdel kullanici_adi`: Kullanıcıyı siler.
*   `sudo userdel -r kullanici_adi`: Kullanıcıyı ve ev dizinini (`/home/kullanici_adi`) siler.
*   `sudo usermod [seçenekler] kullanici_adi`: Kullanıcının özelliklerini değiştirir (örn: `sudo usermod -aG grup_adi kullanici_adi` -> kullanıcıyı ek gruba ekler, `sudo usermod -s /bin/zsh kullanici_adi` -> kabuğunu değiştirir).
*   `su - kullanici_adi`: Belirtilen kullanıcıya geçiş yapar (`-` ile kullanıcının ortam değişkenlerini ve ev dizinini yükler). Root'a geçmek için `su -` veya `sudo su -` kullanılabilir.

##### Kullanıcı Bilgi Dosyaları

*   `/etc/passwd`: Kullanıcı hesap bilgilerini içerir (kullanıcı adı, UID, GID, ev dizini, kabuk). Şifreler burada saklanmaz. Herkes tarafından okunabilir.
*   `/etc/shadow`: Kullanıcıların şifrelenmiş şifrelerini ve şifre geçerlilik bilgilerini içerir. Sadece `root` tarafından okunabilir.
*   `/etc/group`: Grup bilgilerini içerir (grup adı, GID, üyeler).

##### Grup Yönetimi

*   Her kullanıcı oluşturulduğunda genellikle aynı isimde bir *birincil grup* (primary group) da oluşturulur ve kullanıcı bu gruba üye yapılır. Kullanıcının oluşturduğu dosyalar varsayılan olarak bu gruba ait olur.
*   Kullanıcılar ayrıca bir veya daha fazla *ikincil gruba* (secondary group) üye olabilirler.
*   `sudo groupadd yeni_grup`: Yeni bir grup oluşturur.
*   `sudo groupdel grup_adi`: Grubu siler.
*   `sudo groupmod -n yeni_ad eski_ad`: Grubun adını değiştirir.
*   `sudo gpasswd -a kullanici_adi grup_adi`: Kullanıcıyı belirtilen gruba ekler (ikincil grup olarak).
*   `sudo gpasswd -d kullanici_adi grup_adi`: Kullanıcıyı gruptan çıkarır.
*   `groups`: Mevcut kullanıcının üye olduğu grupları listeler.
*   `groups kullanici_adi`: Belirtilen kullanıcının üye olduğu grupları listeler.

#### Erişim İzinleri (Permissions)

Linux'ta her dosya ve dizinin kimlerin ne yapabileceğini belirleyen izinleri vardır.

*   **İzin Türleri:**
    *   `r` (Read - Okuma): Dosya içeriğini okuma, dizin içeriğini listeleme (`ls`).
    *   `w` (Write - Yazma): Dosya içeriğini değiştirme, dizin içinde dosya/dizin oluşturma/silme/yeniden adlandırma.
    *   `x` (Execute - Çalıştırma): Dosyayı program gibi çalıştırma, dizine `cd` ile girme.
*   **İzin Sahipleri:**
    *   **User (u):** Dosyanın sahibi olan kullanıcı.
    *   **Group (g):** Dosyanın ait olduğu grup. Bu gruptaki kullanıcılar için geçerli izinler.
    *   **Others (o):** Sahip veya grup üyesi olmayan diğer tüm kullanıcılar.
*   **Gösterim (`ls -l` çıktısında):**
    *   İlk karakter dosya tipini gösterir (`-`: dosya, `d`: dizin, `l`: link).
    *   Sonraki 9 karakter 3'lü gruplar halinde user, group ve others izinlerini gösterir: `rwx r-x r--`
        *   `rwx`: Okuma, yazma, çalıştırma izni var.
        *   `r-x`: Okuma ve çalıştırma izni var, yazma izni yok.
        *   `r--`: Sadece okuma izni var.
        *   `---`: Hiçbir izin yok.
*   **Sayısal (Octal) Gösterim:** İzinleri 3 haneli bir sayı ile ifade etme yöntemidir. Her hane user, group, others sırasıyla temsil eder. Her iznin sayısal değeri vardır: `r=4`, `w=2`, `x=1`, `-=0`. Bir hanedeki izinlerin değerleri toplanır.
    *   `rwx` = 4 + 2 + 1 = `7`
    *   `r-x` = 4 + 0 + 1 = `5`
    *   `rw-` = 4 + 2 + 0 = `6`
    *   `r--` = 4 + 0 + 0 = `4`
    *   `---` = 0 + 0 + 0 = `0`
    *   Örnek: `rwxr-xr--` -> `754`

##### `chmod` (Change Mode)

Dosya veya dizinlerin izinlerini değiştirmek için kullanılır. Sadece dosya sahibi veya `root` kullanabilir.

*   **Sembolik Yöntem:** `chmod [ugoa][+-=][rwx] dosya/dizin`
    *   `u`, `g`, `o`, `a` (all - hepsi) : Kimin izninin değişeceğini belirtir.
    *   `+`, `-`, `=` : İzin ekleme, çıkarma veya tam olarak ayarlama.
    *   `r`, `w`, `x` : Hangi iznin etkileneceği.
    *   Örnekler:
        *   `chmod u+x betik.sh`: Sahibe çalıştırma izni ekler.
        *   `chmod g-w rapor.txt`: Grup için yazma iznini kaldırır.
        *   `chmod o=r belge.doc`: Diğerleri için sadece okuma izni ayarlar.
        *   `chmod a+r gizli_dizin`: Herkese okuma izni ekler (dizin için listeleme).
        *   `chmod ug+rw,o-w dosya.txt`: Sahip ve gruba okuma/yazma ekler, diğerlerinden yazmayı kaldırır.
*   **Sayısal (Octal) Yöntem:** `chmod NNN dosya/dizin` (NNN yerine 3 haneli sayısal kod gelir).
    *   Örnekler:
        *   `chmod 755 dizin`: `rwxr-xr-x` (Sahip tam yetki, grup ve diğerleri okuma/çalıştırma). Dizinler için yaygın kullanılır.
        *   `chmod 644 dosya.txt`: `rw-r--r--` (Sahip okuma/yazma, grup ve diğerleri sadece okuma). Normal dosyalar için yaygın kullanılır.
        *   `chmod 700 gizli_betik.sh`: `rwx------` (Sadece sahip tam yetki).
*   **`-R` Seçeneği:** Değişikliği dizin ve içindeki tüm alt dosya/dizinlere özyinelemeli olarak uygular.
    *   `chmod -R 755 public_html/`

##### `chown` (Change Owner)

Dosya veya dizinlerin sahibini ve/veya grubunu değiştirmek için kullanılır. Genellikle sadece `root` kullanabilir.

*   `sudo chown yeni_sahip dosya.txt`: Dosyanın sahibini değiştirir.
*   `sudo chown :yeni_grup dosya.txt`: Dosyanın grubunu değiştirir.
*   `sudo chown yeni_sahip:yeni_grup dosya.txt`: Hem sahibi hem de grubu değiştirir.
*   `sudo chown -R kullanici:grup /dizin/yolu`: Dizinin ve içeriğinin sahipliğini özyinelemeli olarak değiştirir.

##### `chgrp` (Change Group)

Sadece dosya veya dizinin grubunu değiştirmek için kullanılır (`chown :yeni_grup` ile aynı işlevi görür).

*   `sudo chgrp yeni_grup dosya.txt`
*   `sudo chgrp -R yeni_grup /dizin/yolu`

#### Disk Yönetimi

##### Depolama Temelleri

*   **Bit ve Byte:** `1 Byte = 8 Bit`.
*   **Sektör (Sector):** Diskteki verinin okunup yazılabileceği en küçük fiziksel birim (genellikle 512 byte veya 4096 byte).
*   **Blok (Block):** Dosya sisteminin veriyi adresleyebileceği en küçük mantıksal birimdir. Genellikle birden fazla sektörün birleşimidir (örn: Linux'ta yaygın olarak 4096 byte = 4KB). Bir dosya, ne kadar küçük olursa olsun, diskte en az bir blok yer kaplar.
*   **Inode (Index Node):** Dosya sistemindeki her dosya veya dizin için meta verileri (izinler, sahip, boyut, zaman damgaları, disktaki veri bloklarının adresleri vb.) tutan veri yapısıdır. Dosya adı, inode numarasına bir referanstır.
*   **Decimal vs. Binary:** Disk üreticileri genellikle kapasiteyi decimal (1 KB = 1000 Byte, 1 MB = 1000 KB) olarak belirtirken, işletim sistemleri genellikle binary (1 KiB = 1024 Byte, 1 MiB = 1024 KiB) olarak hesaplar. Bu nedenle 1 TB'lık bir disk işletim sisteminde yaklaşık 931 GiB olarak görünebilir.

##### Bölümlendirme Tabloları (Partition Tables)

Diski mantıksal bölümlere ayırma yapısını tanımlar.

*   **MBR (Master Boot Record):** Eski standarttır. En fazla 4 birincil bölüm veya 3 birincil + 1 genişletilmiş bölüm destekler. Maksimum disk boyutu limiti yaklaşık 2 TB'dir.
*   **GPT (GUID Partition Table):** Modern standarttır. Çok daha fazla bölüm (varsayılan 128) ve çok daha büyük disk boyutları (teorik olarak Zettabyte seviyeleri) destekler. UEFI sistemlerle birlikte kullanılır.

##### BIOS ve UEFI

Bilgisayarın açılış sürecini başlatan ve yöneten firmware (donanım yazılımı) sistemleridir.

*   **BIOS (Basic Input/Output System):** Eski sistemdir. Donanımı başlatır, MBR'ı okur ve önyükleyiciyi (bootloader) çalıştırır.
*   **UEFI (Unified Extensible Firmware Interface):** Modern sistemdir. Daha hızlı açılış, daha büyük disk desteği (GPT ile), daha gelişmiş arayüz ve güvenlik özellikleri sunar.

##### Önyükleyici (Bootloader)

İşletim sisteminin çekirdeğini belleğe yükleyip başlatmaktan sorumlu programdır (örn: GRUB, LILO). MBR veya GPT'den sonra çalışır. Birden fazla işletim sistemi kuruluysa, hangisinin başlatılacağını seçme menüsü sunabilir.

##### Dosya Sistemi (Filesystem)

Disk üzerindeki verilerin nasıl organize edileceğini, depolanacağını, erişileceğini ve yönetileceğini belirleyen yapı ve kurallar bütünüdür. Diski bölümlendirdikten sonra, her bölüme bir dosya sistemi formatı uygulanmalıdır (`mkfs` komutu ile).

*   **Yaygın Linux Dosya Sistemleri:**
    *   `ext4`: En yaygın kullanılan, kararlı ve olgun Linux dosya sistemidir. Günlükleme (journaling) özelliği sayesinde veri bütünlüğünü korur.
    *   `XFS`: Yüksek performanslı, büyük dosyalar ve dosya sistemleri için optimize edilmiş, günlüklemeli bir dosya sistemidir.
    *   `Btrfs`: Modern, kopya-üzerine-yazma (copy-on-write), anlık görüntü (snapshot), dahili RAID gibi gelişmiş özellikler sunan bir dosya sistemidir.
*   **Diğer Dosya Sistemleri:** `FAT32`, `exFAT` (USB bellekler için uyumluluk), `NTFS` (Windows ile uyumluluk).

##### Disk Yönetimi Komutları

*   `lsblk` (List Block Devices): Sistemdeki blok aygıtlarını (diskler ve bölümleri) ağaç yapısında listeler.
    *   `lsblk -f`: Dosya sistemi türü, UUID ve bağlanma noktası gibi ek bilgileri gösterir.
*   `fdisk`: MBR bölümlendirme tablosuna sahip diskleri yönetmek (bölüm oluşturma, silme, türünü değiştirme) için kullanılır. İnteraktif bir komuttur.
    *   `sudo fdisk -l`: Tüm diskleri ve bölümlerini listeler.
    *   `sudo fdisk /dev/sda`: `/dev/sda` diski üzerinde işlem yapmak için interaktif moda geçer.
*   `gdisk`: GPT bölümlendirme tablosuna sahip diskleri yönetmek için kullanılır (`fdisk`'in GPT versiyonu).
*   `parted`: Hem MBR hem de GPT diskleri yönetebilen daha gelişmiş bir araçtır. Hem interaktif hem de komut satırı modunda kullanılabilir.
*   `mkfs` (Make Filesystem): Bir disk bölümü üzerine dosya sistemi oluşturur (formatlar).
    *   `sudo mkfs.ext4 /dev/sdb1`: `/dev/sdb1` bölümünü `ext4` olarak formatlar.
    *   `sudo mkfs.xfs /dev/sdb2`: `/dev/sdb2` bölümünü `XFS` olarak formatlar.
    *   `sudo mkfs -t ntfs /dev/sdc1`: `/dev/sdc1` bölümünü `NTFS` olarak formatlar (`-t` ile tip belirtme).
*   `mount`: Bir dosya sistemini (disk bölümü, USB bellek, ağ paylaşımı) belirtilen bir dizine (bağlanma noktası - mount point) bağlayarak erişilebilir hale getirir.
    *   `sudo mount /dev/sdb1 /mnt/veri`: `/dev/sdb1` bölümünü `/mnt/veri` dizinine bağlar (`/mnt/veri` dizini önceden var olmalıdır).
    *   `mount`: Bağlı olan tüm dosya sistemlerini listeler.
    *   `sudo mount -o remount,rw /dev/sda1`: `/dev/sda1`'i yeniden okuma/yazma modunda bağlar.
*   `umount`: Bağlı olan bir dosya sisteminin bağlantısını kaldırır.
    *   `sudo umount /mnt/veri`: `/mnt/veri`'ye bağlı olan aygıtın bağlantısını keser.
    *   `sudo umount /dev/sdb1`: Aygıt adıyla da bağlantı kesilebilir.
    *   **Not:** Bağlantıyı kesmeden önce o dizin içinde çalışan bir süreç olmamalıdır (`cd` ile içinde olmamak gibi).
*   `/etc/fstab` (File System Table): Sistemin açılışında otomatik olarak bağlanacak dosya sistemlerinin tanımlandığı dosyadır. Her satır bir dosya sistemini tanımlar (Aygıt/UUID, Bağlanma Noktası, Dosya Sistemi Türü, Bağlama Seçenekleri, Dump, Pass). Bu dosyayı düzenledikten sonra `sudo mount -a` komutu ile yeni tanımlar test edilebilir/uygulanabilir. UUID kullanmak (`lsblk -f` ile bulunur), aygıt adlarının (`/dev/sda1`) değişme ihtimaline karşı daha güvenilirdir.
*   **LVM (Logical Volume Management):** Fiziksel diskleri veya bölümleri bir havuzda toplayıp (Volume Group - VG), bu havuzdan esnek boyutlu mantıksal birimler (Logical Volume - LV) oluşturmayı sağlayan gelişmiş bir disk yönetim sistemidir. Bölümleri yeniden boyutlandırmayı, disk ekleyip çıkarmayı kolaylaştırır. (Detaylı konu, ayrı incelenmelidir).

#### Süreç (Process) Yönetimi

*   **Süreç (Process) Nedir?** Çalışmakta olan bir programın örneğidir. Bir program disk üzerinde pasif bir dosya iken, çalıştırıldığında belleğe yüklenir ve bir süreç haline gelir. Her sürecin kendine ait bir kimlik numarası (PID - Process ID), bellek alanı, dosya tanımlayıcıları ve durumu (çalışıyor, uyuyor, zombi vb.) vardır.
*   **Süreç Türleri:**
    *   **Foreground Processes (Ön Plan Süreçleri):** Terminalde başlatılan ve terminalin kontrolünü elinde tutan süreçlerdir. Komut bitene kadar veya kullanıcı müdahale edene kadar terminal başka komut almaz.
    *   **Background Processes (Arka Plan Süreçleri):** Terminalden başlatılıp terminalin kontrolünü geri veren süreçlerdir. Komutun sonuna `&` eklenerek başlatılır (`sleep 60 &`).
    *   **Daemons (Servisler):** Sistemin açılışıyla başlayan ve genellikle kullanıcı etkileşimi olmadan arka planda sürekli çalışan özel süreçlerdir (örn: web sunucusu, veritabanı sunucusu).
*   **Job Control (İş Kontrolü):** Kabuğun (özellikle Bash, Zsh), mevcut terminal oturumundaki ön plan ve arka plan süreçlerini (job - iş) yönetme yeteneğidir.
    *   `jobs`: Mevcut oturumdaki işleri listeler (arka plandakiler ve durdurulmuş olanlar).
    *   `fg %is_numarasi`: Belirtilen işi ön plana getirir (foreground).
    *   `bg %is_numarasi`: Durdurulmuş bir işi arka planda çalıştırmaya devam ettirir (background).
    *   `Ctrl+Z`: Ön plandaki işi durdurur (suspend) ve arka plana atar.
*   **Komut Zincirleme/Gruplama:**
    *   `komut1 ; komut2`: `komut1` bittikten sonra (başarılı veya başarısız) `komut2` çalışır.
    *   `komut1 && komut2`: `komut1` başarılı olursa (`exit code 0`) `komut2` çalışır.
    *   `komut1 || komut2`: `komut1` başarısız olursa (`exit code != 0`) `komut2` çalışır.
    *   `(komut1 ; komut2)`: Komutları bir alt kabukta (subshell) gruplayarak çalıştırır.

##### Süreçleri İzleme ve Yönetme

*   `ps` (Process Status): Sistemdeki süreçlerin anlık durumunu gösterir.
    *   `ps aux`: Tüm kullanıcıların tüm süreçlerini detaylı formatta gösterir (BSD stili).
    *   `ps -ef`: Tüm süreçleri tam formatta gösterir (System V stili).
    *   `ps -ejH`: Süreçleri ağaç yapısında gösterir.
    *   `ps -p PID`: Belirtilen PID'ye sahip sürecin bilgisini gösterir.
    *   `pgrep process_name`: Belirtilen isme sahip süreçlerin PID'lerini listeler.
*   `top`: Sistemdeki süreçleri gerçek zamanlı olarak izleyen, CPU ve bellek kullanımına göre sıralayan interaktif bir araçtır. `Shift+M` belleğe, `Shift+P` CPU'ya göre sıralar, `k` ile süreç sonlandırılabilir, `q` ile çıkılır.
*   `htop`: `top` komutuna benzer ancak daha kullanıcı dostu, renkli ve fare desteği olan interaktif bir süreç izleme aracıdır (genellikle ayrıca kurulması gerekir).
*   `kill`: Süreçlere sinyal göndererek onları yönetmeyi sağlar (genellikle sonlandırmak için).
    *   `kill PID`: Sürece varsayılan olarak TERM (terminate - 15) sinyalini gönderir (nazikçe kapanmasını ister).
    *   `kill -9 PID`: Sürece KILL (9) sinyalini gönderir (zorla kapatır, veri kaybı olabilir, son çare olarak kullanılmalıdır).
    *   `kill -l`: Gönderilebilecek tüm sinyalleri listeler (örn: HUP (1), INT (2), STOP (19), CONT (18)).
*   `pkill process_name`: Belirtilen isme sahip tüm süreçlere sinyal gönderir. `pkill -9 firefox`
*   `killall process_name`: `pkill` gibi çalışır ancak genellikle tam süreç adıyla eşleşir. `killall -9 sleep`
*   `tmux` (Terminal Multiplexer): Tek bir terminal penceresi içinde birden fazla bağımsız terminal oturumu (pencere, bölme) oluşturmayı ve yönetmeyi sağlayan bir araçtır. Özellikle SSH bağlantılarında, bağlantı kopsa bile oturumların ve çalışan süreçlerin arka planda devam etmesini sağlar. Oturumlara daha sonra tekrar bağlanılabilir (attach). (Detaylı konu, ayrı incelenmelidir).

#### Servis Yönetimi (systemd)

Modern Linux dağıtımlarının çoğunda sistemin açılış sürecini (init) ve servisleri (daemons) yöneten sistem `systemd`'dir.

*   **Unit (Birim):** `systemd` tarafından yönetilen kaynaklardır (servisler `.service`, bağlanma noktaları `.mount`, aygıtlar `.device`, hedefler `.target` vb.).
*   `systemctl`: `systemd`'yi kontrol etmek için kullanılan ana komuttur. `sudo` gerektirir.
    *   `systemctl status service_adi.service` (veya sadece `service_adi`): Servisin durumunu (aktif, pasif, hata durumu, son loglar) gösterir. `systemctl status sshd`
    *   `systemctl start service_adi`: Servisi başlatır.
    *   `systemctl stop service_adi`: Servisi durdurur.
    *   `systemctl restart service_adi`: Servisi yeniden başlatır.
    *   `systemctl reload service_adi`: Servisin yapılandırma dosyalarını yeniden yükler (servisi durdurmadan, destekliyorsa).
    *   `systemctl enable service_adi`: Servisin sistem açılışında otomatik olarak başlamasını sağlar.
    *   `systemctl disable service_adi`: Servisin sistem açılışında otomatik olarak başlamasını engeller.
    *   `systemctl is-enabled service_adi`: Servisin açılışta otomatik başlayıp başlamadığını kontrol eder.
    *   `systemctl list-units --type=service --all`: Tüm servis birimlerini (aktif ve pasif) listeler.
    *   `systemctl list-unit-files --type=service`: Mevcut tüm servis dosyalarını ve durumlarını (enabled, disabled, static) listeler.

#### Log Yönetimi

Sistemde meydana gelen olayların (hatalar, uyarılar, bilgi mesajları, kullanıcı girişleri, servis aktiviteleri) kaydedildiği dosyalardır. Sorun giderme ve sistem analizi için kritiktir.

*   **Geleneksel Loglama (syslog):**
    *   Log dosyaları genellikle `/var/log` dizininde düz metin olarak tutulur.
    *   `rsyslogd` veya `syslog-ng` gibi servisler log mesajlarını toplar ve ilgili dosyalara yazar.
    *   **Önemli Log Dosyaları:**
        *   `/var/log/syslog` veya `/var/log/messages`: Genel sistem mesajları.
        *   `/var/log/auth.log` veya `/var/log/secure`: Kimlik doğrulama ve yetkilendirme logları (giriş denemeleri, `sudo` kullanımı).
        *   `/var/log/kern.log`: Çekirdek (kernel) logları.
        *   `/var/log/boot.log`: Sistem açılış logları.
        *   `/var/log/apt/` (Debian/Ubuntu): `apt` paket yöneticisi logları.
        *   `/var/log/yum.log` veya `/var/log/dnf.log` (Red Hat/Fedora): `yum`/`dnf` logları.
        *   Uygulamaya özel loglar (örn: `/var/log/nginx/`, `/var/log/apache2/`, `/var/log/mysql/`).
*   **systemd Journal:**
    *   `systemd` kullanan sistemlerde, loglar merkezi ve yapılandırılmış bir ikili (binary) formatta `journald` servisi tarafından toplanır.
    *   `journalctl`: Journal loglarını görüntülemek ve sorgulamak için kullanılır.
        *   `journalctl`: Tüm logları gösterir (en yeniden eskiye).
        *   `journalctl -n 20`: Son 20 log kaydını gösterir.
        *   `journalctl -f`: Yeni logları gerçek zamanlı olarak takip eder.
        *   `journalctl -u service_adi.service`: Belirtilen servise ait logları gösterir. `journalctl -u sshd`
        *   `journalctl --since "1 hour ago"`: Son 1 saate ait logları gösterir. (`"YYYY-MM-DD HH:MM:SS"` formatı da kullanılabilir).
        *   `journalctl -p err`: Sadece hata (error) seviyesindeki logları gösterir (`emerg`, `alert`, `crit`, `err`, `warning`, `notice`, `info`, `debug`).
        *   `journalctl _PID=1234`: Belirtilen PID'ye ait logları gösterir.
*   **Log Rotasyonu:** Log dosyalarının zamanla çok büyümesini engellemek için eski logları arşivleyen veya silen mekanizmadır. Genellikle `logrotate` aracı ile yönetilir (`/etc/logrotate.conf` ve `/etc/logrotate.d/`).

#### Temel Ağ (Network) Kavramları ve Komutları

##### Ağ Temelleri

*   **IP Adresi (Internet Protocol Address):** Bir ağdaki cihazı benzersiz olarak tanımlayan mantıksal adrestir (örn: `192.168.1.10`, `2001:0db8:85a3::8a2e:0370:7334`). IPv4 (32-bit) ve IPv6 (128-bit) sürümleri vardır.
*   **MAC Adresi (Media Access Control Address):** Ağ arayüz kartının (Ethernet, Wi-Fi) donanım üzerinde tanımlı, fiziksel olarak benzersiz adresidir (örn: `0A:1B:2C:3D:4E:5F`). Layer 2'de (Veri Bağlantı Katmanı) kullanılır.
*   **LAN (Local Area Network - Yerel Alan Ağı):** Aynı fiziksel ağ segmentindeki (genellikle aynı bina veya ev içindeki) cihazların oluşturduğu ağdır.
*   **WAN (Wide Area Network - Geniş Alan Ağı):** Farklı coğrafi konumlardaki LAN'ları birbirine bağlayan ağdır (İnternet en büyük WAN'dır).
*   **Router (Yönlendirici):** Farklı ağları birbirine bağlayan ve paketlerin ağlar arasında doğru hedefe yönlendirilmesini sağlayan cihazdır. IP adreslerine göre (Layer 3) çalışır. Yönlendirme tabloları (routing tables) kullanır.
*   **Switch (Anahtar):** Aynı LAN içindeki cihazları birbirine bağlayan cihazdır. MAC adreslerine göre (Layer 2) çalışır. Paketleri sadece ilgili porta göndererek ağ trafiğini optimize eder.
*   **Gateway (Ağ Geçidi):** Bir ağdan başka bir ağa (genellikle LAN'dan İnternet'e) çıkış kapısı görevi gören router'ın IP adresidir.
*   **DNS (Domain Name System - Alan Adı Sistemi):** İnsanların okuyabildiği alan adlarını (`www.google.com`) bilgisayarların anlayabildiği IP adreslerine (`172.217.160.142`) çeviren dağıtık sistemdir.
*   **DHCP (Dynamic Host Configuration Protocol - Dinamik Ana Bilgisayar Yapılandırma Protokolü):** Bir ağdaki cihazlara otomatik olarak IP adresi, alt ağ maskesi (subnet mask), ağ geçidi ve DNS sunucusu gibi bilgileri atayan protokoldür.

##### Hostlar Nasıl Haberleşir?

*   **Aynı LAN İçinde:**
    1.  Kaynak cihaz, hedef cihazın IP adresini bilir ancak MAC adresini bilmez.
    2.  Kaynak cihaz, LAN'a bir ARP (Address Resolution Protocol) isteği gönderir: "Bu IP adresine sahip cihazın MAC adresi nedir?"
    3.  Hedef IP adresine sahip cihaz, ARP yanıtı ile kendi MAC adresini kaynağa bildirir.
    4.  Kaynak cihaz, hedef MAC adresini ARP tablosuna (önbelleğine) kaydeder.
    5.  İletişim artık doğrudan kaynak MAC'ten hedef MAC'e yapılır (Switch üzerinden).
*   **Farklı LAN'lar Arasında (Router Üzerinden):**
    1.  Kaynak cihaz, hedef IP adresinin kendi LAN'ında olmadığını anlar.
    2.  Paketi, kendi ağ geçidi (gateway) olarak tanımlanmış router'ın MAC adresine gönderir (Router'ın MAC adresini ARP ile öğrenir). Paketin içindeki hedef IP adresi değişmez.
    3.  Router paketi alır, hedef IP adresine bakar ve kendi yönlendirme tablosuna göre paketi bir sonraki router'a veya doğrudan hedef LAN'a iletir. Bu sırada paketin kaynak MAC adresi router'ın MAC adresi, hedef MAC adresi ise bir sonraki hop'un (router veya hedef cihaz) MAC adresi olacak şekilde güncellenir.
    4.  Bu işlem, paket hedef ağa ulaşana kadar tekrarlanır. Son router paketi hedef cihazın MAC adresine gönderir.
*   **İnternet Üzerinden (Örn: www.google.com):**
    1.  Cihazınız, DNS sunucusuna `www.google.com`'un IP adresini sorar.
    2.  DNS, Google'ın sunucularına ait (genellikle bir Load Balancer/Edge Router'a ait) bir IP adresi döndürür.
    3.  Cihazınız, bu hedef IP adresine doğru paketi ağ geçidine (router) gönderir.
    4.  Paket, İnternet üzerindeki birçok router'dan geçerek Google'ın ağına ulaşır.
    5.  Google'ın Load Balancer'ı isteği alır ve uygun bir backend sunucusuna yönlendirir. Bu iç mekanizma dışarıdan görünmez.

##### Ağ Protokolleri (Özet)

*   **ARP:** IP -> MAC çevirimi (LAN içi).
*   **IP:** Mantıksal adresleme ve yönlendirme (Ağ Katmanı).
*   **TCP (Transmission Control Protocol):** Güvenilir, bağlantı odaklı veri iletimi (Taşıma Katmanı - HTTP, FTP, SMTP).
*   **UDP (User Datagram Protocol):** Hızlı, bağlantısız veri iletimi (Taşıma Katmanı - DNS, DHCP, VoIP).
*   **ICMP (Internet Control Message Protocol):** Ağ durumu ve hata mesajları için kullanılır (`ping`, `traceroute`).
*   **HTTP/HTTPS:** Web sayfaları aktarımı (Uygulama Katmanı).
*   **FTP:** Dosya aktarımı (Uygulama Katmanı).
*   **SMTP:** E-posta gönderimi (Uygulama Katmanı).
*   **POP3/IMAP:** E-posta alımı (Uygulama Katmanı).
*   **SSH:** Güvenli uzaktan komut çalıştırma ve dosya aktarımı (Uygulama Katmanı).
*   **DNS:** Alan adı -> IP çevirimi (Uygulama Katmanı).
*   **DHCP:** Otomatik IP yapılandırması (Uygulama Katmanı).

##### Temel Ağ Komutları

*   `ping hedef_ip_veya_domain`: Hedef cihaza ICMP echo istekleri göndererek erişilebilirliğini ve yanıt süresini test eder. `ping google.com` veya `ping 8.8.8.8`. `Ctrl+C` ile durdurulur.
*   `ip`: Ağ arayüzlerini, IP adreslerini, yönlendirme tablolarını ve ARP önbelleğini yönetmek için modern ve güçlü bir araçtır (`ifconfig`, `route`, `arp` komutlarının yerini almıştır).
    *   `ip addr show` (veya `ip a`): Tüm ağ arayüzlerini ve atanmış IP adreslerini listeler.
    *   `ip link show`: Ağ arayüzlerinin bağlantı katmanı bilgilerini (MAC adresi, durum: UP/DOWN) gösterir.
    *   `sudo ip link set eth0 up/down`: Belirtilen arayüzü etkinleştirir/devre dışı bırakır.
    *   `ip route show` (veya `ip r`): IP yönlendirme tablosunu gösterir (hangi ağlara hangi arayüz ve gateway üzerinden gidileceği).
    *   `ip neigh show`: Komşu tablosunu (ARP önbelleğini - IP/MAC eşleşmeleri) gösterir.
*   `ifconfig`: (Eski) Ağ arayüzlerini ve IP adreslerini listeler/yapılandırır. Modern sistemlerde `ip` komutu tercih edilir.
*   `route`: (Eski) IP yönlendirme tablosunu gösterir/yönetir. `ip route` tercih edilir.
*   `arp`: (Eski) ARP önbelleğini gösterir/yönetir. `ip neigh` tercih edilir. `arp -a`
*   `hostname`: Sistemin ana bilgisayar adını (hostname) gösterir veya ayarlar.
    *   `hostname`: Mevcut adı gösterir.
    *   `hostname -I`: Sistemin tüm IP adreslerini gösterir.
*   `nslookup domain_adi [dns_sunucusu]`: Alan adının IP adresini sorgular. `nslookup google.com`
*   `dig domain_adi [tip] [@dns_sunucusu]`: DNS sorguları yapmak için daha detaylı ve esnek bir araçtır.
    *   `dig google.com`: A kaydını (IPv4 adresi) sorgular.
    *   `dig google.com MX`: MX kaydını (posta sunucusu) sorgular.
    *   `dig google.com AAAA`: AAAA kaydını (IPv6 adresi) sorgular.
    *   `dig @8.8.8.8 google.com`: Belirtilen DNS sunucusuna sorgu yapar.
*   `traceroute domain_veya_ip` (veya `tracepath`): Bir paketin hedefe ulaşana kadar geçtiği router'ları (hop'ları) ve gecikme sürelerini göstermeye çalışır. Ağdaki yavaşlama noktalarını bulmak için kullanılır.
*   `ss` (Socket Statistics): Sistemdeki aktif ağ bağlantılarını, dinlenen portları ve soket istatistiklerini gösterir (`netstat`'ın modern alternatifidir).
    *   `ss -tulnp`: Dinlenen tüm TCP (`t`) ve UDP (`u`) portlarını, port numaralarıyla (`n`) ve ilgili süreci (`p`) gösterir (genellikle `sudo` gerektirir).
    *   `ss -tan`: Tüm TCP bağlantılarını gösterir.
*   `netstat`: (Eski) Ağ bağlantılarını, yönlendirme tablolarını, arayüz istatistiklerini vb. gösterir. `ss` ve `ip` komutları tercih edilir.
*   `wget url`: Belirtilen URL'den dosya indirir. `wget https://example.com/dosya.zip`
*   `curl url`: URL'den veri transferi yapmak için çok yönlü bir araçtır. Web sayfalarını indirme, API'lerle etkileşim, dosya yükleme/indirme gibi birçok işlevi vardır. `curl https://example.com` (sayfanın HTML içeriğini ekrana basar). `curl -O url` dosyayı indirir (`wget` gibi).
*   `ssh kullanici@hedef_ip_veya_domain`: Uzak bir Linux/Unix sunucusuna güvenli kabuk (Secure Shell) bağlantısı kurar.
*   `scp kaynak_dosya kullanici@hedef_ip:hedef_yol`: SSH üzerinden güvenli dosya kopyalama (Secure Copy) yapar. Uzak sunucudan dosya almak için: `scp kullanici@hedef_ip:kaynak_dosya yerel_hedef`
*   `nmtui`: (NetworkManager kuruluysa) Metin tabanlı bir arayüzle ağ bağlantılarını (IP ayarları, Wi-Fi, Ethernet) yapılandırmayı sağlar. Değişiklikler kalıcı olur.
*   `tcpdump`: Güçlü bir komut satırı paket analiz aracıdır. Ağ arayüzünden geçen paketleri yakalayıp detaylı olarak incelemeyi sağlar. Genellikle ağ sorunlarını derinlemesine analiz etmek için kullanılır (`sudo` gerektirir). `sudo tcpdump -i eth0`
*   `nmap`: Ağ keşfi ve güvenlik taraması için popüler bir araçtır. Ağdaki aktif cihazları, açık portları ve çalışan servisleri tespit etmek için kullanılır (genellikle ayrıca kurulması gerekir).
    *   `nmap hedef_ip`: Hedef IP'deki yaygın portları tarar.
    *   `nmap -sn 192.168.1.0/24`: Yerel ağdaki aktif cihazları bulmaya çalışır (ping scan).
    *   `nmap -p 1-1000 hedef_ip`: Hedefteki ilk 1000 portu tarar.
*   `/etc/hosts`: Yerel bir DNS çözümleme dosyasıdır. Bu dosyaya eklenen IP-Hostname eşleşmeleri, DNS sunucusuna sorulmadan önce kullanılır. Belirli siteleri engellemek veya yerel geliştirme ortamları için alan adları tanımlamak amacıyla kullanılabilir.
*   `/etc/resolv.conf`: Sistemin kullanacağı DNS sunucularının adreslerini içerir. Genellikle NetworkManager veya DHCP tarafından otomatik olarak yönetilir.
