# Sql-syntax


Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız

## Relationships

```sql
1-One to Many
2-One to One
3-Many to Many

One to Many

Products                  |    Category
                          |
id  Name    Price  catid  |    id  name
1  rolex     2000  1      |     1  saat
2  mi 6       500         |     2  telefon
3  samsung s6 5000 2      |
 
-- Not: rolex bir saat olduğu için catid sayesinde onu saat ketgorisine alabildim yani category verisindeki saat yapısına onu bağladım temel olarak rolex artık bir saat yani 1 ürünü çoklu kategoriye bağladık

Many to Many

Products                  |    ProductCategory       |   Category
                          |                          |
id  Name    Price         |   productid categoryid   |    id  name
1  rolex     2000         |   1         1            |     1  saat
2  casio       500        |   1         3            |     2  telefon
3  samsung s6 5000        |   2         1            |     3  elektronik

-- Not: artık saat ve telefon bi yandan elektronik parçalarda yani samsung hem telefon hemde elektronik olarak geçiyor

One to One

Products                |    Product_Details
                        |
id  Name    Price       |    id  color  kg
1  rolex     2000       |     1  red    150gr
2  mi 6       500       |     2  black  100gr
3  samsung s6 5000      |     3  black  350gr
 
-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

## Temel sql sorguları

### Select - kayıt seçme

```sql
select * --bütün kolonlar bize gelsin diyoruz

select * from shopapp.products --burda sadece shopp daki products kolonunu alır

select Name from shopapp.products --products daki sadece name kolonunu seçtik

select Name as ProductName, price as fiyat from ShopApp.Product
-- üst tarafda Name kolonun un adını ProductName olarak değşitirdik ve price adını
-- fiyat olarak değiştirdik as kodu burda bize isim değiştirmede yaradı
-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### Where - Kayıt filtreleme

```sql
select * from ShopApp.Prdocut where Id = 1 -- bu bir sorgulamadır yani burda 
-- sadece Id 1 i almak istediğimizi belirttik

select * from ShopApp.Product Where Price > 2000 And 4000 -- fiyat 2000 den büyük
-- 2000 ve 4000 arası sayıları göster

select * from ShopApp.Product Where Name = 'samsung s6' --istersek sadece tek bir
-- alanı isteyebiliriz

-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### Where - Operatörleri

```sql
select * from ShopApp.Product Where Price Between 2000 and 4000
-- 2000 4000 arası bütün kayıtları getirir

select * from ShopApp.Product Where Category IN ('telefon','bilgisayar')
--bütün telefon ve bilgisayarları sıralar

select * from ShopApp.Product Where Name LIKE '%Samsung%'
-- verideki sadece içinde samsung adı geçen tüm verileri gösterir sonunda
-- s6 veya s7. olması farketmez hepsini getirir

-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### Order - Kayıt Sıralama

```sql
select * from ShopApp.Product order by Price --fiyata göre en düşükden en büyüğe
-- sıralar

select * from ShopApp.Product order by name DESC --azalandan artana sıralar

select * from ShopApp.Product order by Price ASC -- artandan azalana sıralar 

-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### Sql Fonksiyonları

```sql
-- min(), max(), count(), avg(), sum()

select min(price) from ShopApp.Product --minumum fiyat bilgisini bize. getirir 

select max(price) from ShopApp.Product --maximum fiyat biligisni bize getirir

select count(*) from ShopApp.Product --bize toplam kaç ürün olduğunu gösterir

select avg(price) from ShopApp.Product --bütün ürünlerin ortalamasını verdi

select sum(price) from ShopApp.Product --bütün ürünlerin toplamını verdi

-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

```sql
-- String fonksiyonlar

select length(name) from ShopApp.Product --name deki isimlerin karakterlerini gös
--terir

select right('escan',3) -- sağdan ücüncü karakteri alır

select lower(name) from ShopApp.Product --bütün karakterleri küçük yapar

select upper(name) from ShopApp.Product --bütün karakterleri büyütür

select name replace(name,' ','-') from ShopApp.Product --bütün boşlukları - yapar

select trim(name) from ShopApp.Product -- name deki boşlukları siler

-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### Group By

<img width="711" alt="Screen Shot 2021-08-19 at 10 29 36" src="https://user-images.githubusercontent.com/84273839/130026637-b8faafb1-5265-4af3-97c5-4b70d0e2670c.png">


```sql
select distinct Category from shopapp.product -- tekrarlayan alanlar bize tek
-- alanda gelir

select category from shopapp.product group by category
-- aslında distinct la. aynı görevi görüyor aralarında pek bir fark yok

-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### Insert - Kayıt ekleme

```sql
select * from shopapp.product
INSERT INTO shopapp.product (Name,Price,ImageUrl,Category,Description)
VALUES ("samsung s10",2000,"1.jpg","telefon","süper telefon s7 gibi patlamıyor");
-- burda ilk önce tüm kolonları yazdırdık sonra Insert ile yeni bir alan ekledik
-- Values bölümünde üstteki ile aynı hizada değerleri girdik
-- Not: NN yani not null seçili alanları boş bırakamazsınız
 -- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### Update - kayıt güncelleme

```sql
UPDATE shopapp.product
SET Name = 'samsung s7'
WHERE id = 1
-- Eğer where komutu ile id 1 i seçmez iseniz namedeki herşeyi samsung s7 yapar

SET SQL_SAFE_UPDATES = 0;
UPDATE shopapp.product
SET Price = Price + 1000
-- veritabanındaki tüm price lara 1000 ekler kodun.  başında çalıştırdığımız kod
-- aslında bir güvenlik önlemi normalde bu set kodunu yazmasaydık program bize
-- hata vericekdi çünkü böyle büyük bir değişikliği yanlışlıkla yapmak gerçekden
-- üzücü olurdu oyüzden en başta bu güvenlik önleyiciyi kapattık ve kodu yolladık

-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### Delete - kayıt silme

```sql
DELETE FROM shopapp.product --bütün veri tabanını siler

DELETE FROM shopapp.product WHERE Id = 1

DELETE FROM shopapp.product WHERE Price > 2000

DELETE FROM shopapp.product WHERE description is NUll --içi boş olan descripton
-- silinir

--gördüğünüz gibi kullanımı aşırı basit

-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

## Sql veritabanı yönetimi

### Diagram

<img width="170" alt="Screen Shot 2021-08-19 at 10 29 59" src="https://user-images.githubusercontent.com/84273839/130026685-a5f9413a-b91b-4d3a-962b-e6ab6126d934.png">

### Öncelikle modelleri  öğrenelim  mysql tarafında ev butonuna tıklayın ardından ikinci sıradaki model iconuna tıklayın

<img width="706" alt="Screen Shot 2021-08-19 at 10 30 33" src="https://user-images.githubusercontent.com/84273839/130026774-304d096d-e278-410c-9e2b-dbdd43ee3da2.png">

### Model yazısındaki + işaretine tıklayıp bir model oluşturun

<img width="706" alt="Screen Shot 2021-08-19 at 10 31 16" src="https://user-images.githubusercontent.com/84273839/130026871-cf103937-aa4a-4040-b3fd-cde58c1070da.png">

### Ardından Add Diagram yazan yere tıklayın.

<img width="73" alt="Screen Shot 2021-08-19 at 10 31 48" src="https://user-images.githubusercontent.com/84273839/130026942-19f2e0ab-b377-41cb-b163-d973d79e6ccf.png">

### tablo işaretine bastık dan sonra boş bir yere tıklayın tebrikler ilk table oluşturdunuz.

## Fiziksel bağlantıların yapılması

<img width="73" alt="Screen Shot 2021-08-19 at 10 32 25" src="https://user-images.githubusercontent.com/84273839/130027033-dc63ca91-f096-4f26-92df-c80fea8f18c8.png">

### Burdaki 1:1 = One to One bunu dersin başında anlatmıştık bu çizgiler bunları temsil ediyor iki. tane table olsun biri film diğeri director bir director birden çok filmde bulunabilir buyüzden one to many çizgisini kullanacağız

### Farkettiyseniz aynı One to one dan iki adet var bunlardan biri çizgili biri çizgisiz bunun anlamı ise bir film için yönetmen olması gerekiyorsa burdaki ilişki tipi düz çizgi olmalı bunu isterseniz internetten daha detaylı öğrenebilirsiniz

<img width="706" alt="Screen Shot 2021-08-19 at 10 32 47" src="https://user-images.githubusercontent.com/84273839/130027078-7f7ada2f-f64a-469c-a7f8-c1c5cb586b35.png">

### Veri tabanı şeması - Forward Engineer

En üst de bulunan "Database" tuşuna bastığımıza önümüze iki adet seçenek çıkıyor "reverse engineer" ve "Forward engineer" elimizde bir model yoksa reverse seçmelisiniz fakat biz önceki notumuzda bir model oluşturmuştuk o yüzden forward diyoruz connection bilgilerini tamamlıyoruz ileri diyoruz ileri diyoruz tekrar ileri diyoruz ve diagram ile yaptığımız tüm işlemlerin kodlarını bize gösteriyor sonra birdaha ileri diyoruz ve kendi localhostumuza geldiğimizde yaptığımız şema ve diagram gelmiş bulunuyor -- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız

### Var olan Veri tabanı ile  - Reverse Engineer

Model alanına geliyoruz  ve en sondaki yani 3. ok iconuna tıklıyoruz ve en baştakine tıklıyoruz ileri diyoruz ileri diyoruz ve bize databaselerimi gösteriyor burda hangisini seçmek isterseniz önceki derslerimizde kullandığımız shopapp i seçiyorum ben tekrar ileri diyoruz ileri diyoruz ve modelimiz oluşturuluyor ve artık shopapp adında bir modelimiz var -- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız

### Veri tabanındaki bilgilerin saklanması - generate scripts

üst tarafdan server ardından data export ve ordan istediğiniz database i seçiyorsunuz ve alt tarafdan Dump data only i seçiyoruz ki sadece dataları exportlayalım  sağ üstten advanced options gelip en aşağıdaki complete -insert onaylıyoruz ve start export dediğimizde tüm scriptler indirilmiş oldu -- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız

### Hazır veri tabanı kullanma - northwind

[https://github.com/dalers/mywind](https://github.com/dalers/mywind) Öncelikle database e buradan ulaşabilirsiniz

northwind.sql ve northwind-data.sql  i sağ üstten Raw diyip çıkan sayfadan control+s diyerek kaydedin

ardından workbench e girip file open sql scripts e tıklayın bunu çalıştırdığınızda bütün tablolar geliyor -- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız

## Birden fazla tabloda kayıt seçme

<img width="706" alt="Screen Shot 2021-08-19 at 10 33 26" src="https://user-images.githubusercontent.com/84273839/130027167-0126a039-8ebc-4456-a6ee-6ecc17bcb16f.png">

### Inner join

```sql
select * from orders inner join customers --burda oreders ile customers ı 
-- inner joinledik
on order.customer_id = customers.id --burdada bir sorgu yaptık order daki 
-- customer_id ile customers daki id nin inner joinlerini aldık
-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### left join

```sql
select * from customers
left join orders --customers.id deki sadece kesişen bilgiler gelirken
on order.customer_id = customers.id --customer_id deki tüm bilgiler gelir
-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### right join

```sql
select * from orders right join employees
on employees.id = employee_id
-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```

### ikiden fazla tablo birleşimi

```sql
select * from orders inner join customers 

on order.customer_id = customers.id 

inner join order_details on order_details.order_id = order.id --order_details ın
-- order_id si ile order ın id sini birleştirdik önceden de customer_id ile 
-- customer ın id sini birleştirmiştik yani 2 adet birleştirme yapmış olduk
-- Notlar tamamen Escan Dönmez e aittir izinsiz kullanmayınız
```
