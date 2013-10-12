#  Mysqldump

.fx: first

Emin Eker `<emineker@gmail.com>`

http://emineker.net/

Kasım 2012

---

##  Mysqldump Nedir?

Mysql veritabanı yöneticisinde

*   Bir veya birden fazla veritabanın
*   Bir veya birden fazla tablonun

yedeklenmesini (dışarı aktarılmasını) sağlayan mysql aracı

*   Daha ayrıntılı bilgilere erişebilmek için (kaynak)

        !sh
        $ man mysqldump

---

##  Veritabanı Yedeğinin Alınması

*   Yalnızca bir veritabanı yedeğinin alınması

        !sh
        $ mysqldump -u root -p db_name > db-name.sql

*   Yalnızca seçilen veritabanlarının yedeğinin alınması

        !sh
        $ mysqldump -u root -p --databases \
                db_name_1 db_name_2 > databases.sql

*   Tüm veritabanının yedeğinin alınması

        !sh
        $ mysqldump -u root -p --all-databases > all-databases.sql

---

##  Tabloların Yedeğinin Alınması

*   Bir veritabanı içerisindeki bir tek tablonun yedeğinin alınması

        !sh
        $ mysqldump -u root -p db_name table_name > table-name.sql

*   Bir veritabanı içerisindeki birden fazla tablonun yedeğinin alınması

        !sh
        $ mysqldump -u root -p db_name t_name_1 t_name_2 > tables.sql

---

##  Verisiz Yedek Alınması

*   Tüm veritabanları için

        !sh
        $ mysqldump -u root -p --all-databases --no-data > all-databases.sql

*   Bir veritabanı içerisinde bir tablo için

        !sh
        $ mysqldump -u root -p db_name table_name --no-data > table-infos.sql

Bu şekilde sadece veritabanı ve tablo bilgileri veya sadece tablo bilgileri yedeği alınabilir

---

##  Sadece Veri Yedeğinin Alınması

Tablo bilgisi olmadan sadece var olan kayıtlarının yedeğinin alınması

*   Tüm veritabanları için

        !sh
        $ mysqldump -u root -p --all-databases --no-create-info > \
                all-databases.sql

*   Bir veritabanı içerisinde bir tablo için

        !sh
        $ mysqldump -u root -p db_name table_name --no-create-info > \
                table-infos.sql

Bu şekilde veritabanı ve tablo bilgileri veya tablo bilgileri
olmadan verilerin yedekleri alınabilir

---

##  Geçerli Bilgilerin Silinmesi

Yedekleri Mysql'e aktarma sırasında veritabanında bulunan
eski veritabanı veya tabloların silinmesinin sağlanması

*   Veritabanının silinmesi

        !sh
        $ mysql -u root -p db_name –-add-drop-database < db-name.sql

*   Tablonun silinmesi

        !sh
        $ mysql -u root -p db_name -–add-drop-table < db-name.sql

Bu parametreler alınan yedeğe `drop database` ve `create database` özeliklerini ekler.
Bu özellikler yedeğin geri yüklenmesi sırasında Mysql'de bulunan
veritabanı veya tablonun silinmesi ve yedekle gelen bilgiler doğrultusunda
yeniden yüklenmesini sağlar.

---

##  Yedeğin Zaman Damgası İle Alınması

*   Tüm veritabanının yedeğinin alınması

        !sh
        $ mysqldump -u root -p --all-databases > \
                $(date +%Y-%m-%d-%H-%M-%S).sql

---

##  Yedeğin Paketlenmesi

Yedeğin saklanması için sıkıştırma araçları kullanılabilir

*   Yedeğin alınması

        !sh
        $ mysqldump -u root -p --all-databases > all-databases.sql

*   tar.gz paketi halinde saklanması

        !sh
        $ tar czvf all-databases.tar.gz all-databases.sql

*   Geçici dosyayı sil

        !sh
        $ rm all-databases.sql

---

##  Yedeğin İçe Aktarılması

*   Eğer yedek sadece tablo bilgilerinden ve verilerden oluşuyor ise öncelikle
Mysql'de bir veritabanı oluşturulmalı ve yedek bu işlemden sonra içe
aktarılmalıdır

        !sh
        $ mysql -u root -p new_db_name < db-name.sql


:   Yedek, oluşacak veritabanı bilgisine de sahipse restore işlemi sırasında
veritabanı isminin verilmesine gerek yoktur

---

##  Yedeklerin Karakter Kodlaması

*   Yedek oluşturulurken, içe aktarma işlemlerinde karakter problemleri ile
karşılaşmamak adına yedeğin istenilen kodlama şekline getirilmesi

        !sh
        $ mysqldump -u root -p db_name \
                –-default-character-set=utf8 > db_name.sql

*   Yedeklerin geri yükleme işlemleri sırasında karakter problemleri ile
karşılaşıldığı taktirde

        !sh
        $ mysql -u root -p db_name \
                –-default-character-set=utf8 < db-name.sql

burada istenilen kodlama seçeneği kullanılabilir

---

##  Tabloları Kilitleme

Yedeği alınan tabloların içe aktarma işlemleri sırasında bu tabloya
yeni bir kayıt eklenmesini engellemek gerekebilir

*   Yedeğin alınması

        !sh
        $ mysqldump -u root -p db_name --add-locks > db_name.sql

*   İçe aktarılması

        !sh
        $ mysql -u root -p db_name --add-locks < db-name.sql

