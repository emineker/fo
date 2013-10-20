#  Mysql İpuçları

.fx: first

Emin Eker `<emineker@gmail.com>`

http://emineker.net/

Nisan 2013

---

##  Çalışcan Süreçleri İzleme

*   Açık olan tüm süreçleri göster

        !sql
        mysql> show processlist;

*   Süreçleri öldür

        !sql
        mysql> kill id_number;

---

##  Tablo Sütunları ve Özellikleri

        !sql
        mysql> describe table_name;

        veya

        mysql> explain table_name;

---

##  Tablo Temizleme

bir tablonun içeriğini silmek ve tablonun tüm ayarlarını sıfırla

        !sql
        mysql> truncate table_name;


örneğin herhangi bir sütununun `auto_increment` özelliği varsa bu değeri sıfırlar

---

##  auto_increment Değerini Değiştirme

integer, primary key ve auto_increment özelliğine sahip bir sütunu bulunan tablodan
herhangi bir sebeple sildiğiniz kayıtların artırmış olduğu primary key'lerinin kaldığı noktayı değiştirmek

        !sql
        mysql> select auto_increment from information_schema.tables \
                where table_name='foo';

        mysql> alter table table_name auto_increment = 444;


not
:   Tabloda bulunan en büyük primary key'den küçük bir değerle değiştiremezsiniz.
Tablo bağlantılarının korunması adına bu değişikliğin yapılması önerilmez.

---

##  Tablo Oluşturma Açıklamaları

        !sql
        mysql> show create table table_name;

---

##  Kayıtları Karıştır

*   Kayıtları karıştırarak seç

        !sql
        mysql> select * from table_name order by rand();

*   Rastgele bir kayıt seç

        !sql
        mysql> select * from table_name order by rand() limit 1;

---

##  Parola Değiştir

Yönetme yetkiniz bulunduğu kullanıcı için

        !sql
        mysql> set password for 'root'@'localhost' = password('new_password');

