
## E-TicaretDataBase
SQL Projesi 


## 1. Categories Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/63f0eae7-0007-4171-8ae1-5e385c0233a4)

```MSSQL
Id
Name
IsActive
MainCategoryId
CreatedDate
UpdatedDate
Path
VatRate
```

AÇIKLAMA:
Bu veritabanı tablosu ürün kategorilerini hiyerarşik bir yapıda düzenlememizi sağlayan bir yapı sunar. Bu hiyerarşi ana kategorilerin ve bu ana kategorilere bağlı alt kategorilerin tanımlanmasına olanak tanır. "MainCategoryId" alanı bu bağlantıları kurmamıza yardımcı olur, yani her alt kategori hangi ana kategoriye ait olduğunu belirtir. "Path" alanı ise bir kategorinin tam konumunu gösterir; örneğin, "Mobilya" kategorisi "Ofis Mobilyaları" alt kategorisinin içindeyse bu ilişkiyi yansıtır. "VatRate" alanı ise her bir kategori için geçerli olan vergi oranını içerir.

Bu tablo ürün kategorilerini düzenlemek, sorgulamak ve yönetmek için etkili bir araç sağlar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 2. CategoryEquivalents Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/640a6d40-9241-41b5-a9d5-de3ebf1e0512)

```MSSQL
Id
CategoryId
EquivalentId
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu tablo farklı kategoriler arasındaki ilişkileri yönetmeyi amaçlar. Örneğin "Bilgisayar" ile "Elektronik Cihazlar" kategorileri arasında eşdeğerlik kurularak, "Bilgisayar" ürünleri "Elektronik Cihazlar" altında da görüntülenebilir. Bu yapı kategoriler arasındaki bağlantıları yönetmek ve benzer kategorileri gruplamak için kullanışlıdır. "CategoryId" ve "EquivalentId" alanları sayesinde eşdeğer kategorileri tanımlayabilir, bu bilgiyi sorgularla kullanabilirsiniz. Bu tablo kategorilerin ilişkilerini net bir şekilde göstererek veriyi daha anlamlı hale getirir.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 3. CategoryFields Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/85312bf1-8f59-4a82-afe9-071e8d3663d0)

```MSSQL
Id
Name
CategoryId
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu veritabanı tablosu kişiselleştirilmiş ürün kategori özellikleri eklemek amacıyla tasarlanmıştır. Örneğin bir "Mutfak Eşyaları" kategorisi için "Malzeme", "Kapasite", "Renk Seçeneği" gibi özel alanlar oluşturmak mümkündür. Bu tür özel alanlar ürünlerin daha detaylı ve spesifik bir şekilde kategorize edilmesine yardımcı olur. "CategoryId" alanı sayesinde her özel özellik hangi kategoriye ait olduğunu belirler, böylece her kategori için farklı özelleştirilmiş alanlar tanımlayabilirsiniz. Bu tablo ürünlerin daha ayrıntılı ve esnek bir şekilde sınıflandırılmasına olanak sağlayarak kategori yönetimini geliştirir.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 4. CommentImageUrls Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/97a21b6f-ed84-4f15-bda0-4b1a4b76dce2)

```MSSQL
Id
CommentId
ImageUrl
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu tablo kullanıcı yorumlarına resim eklemeyi desteklemek için oluşturulmuştur. Örneğin ürün incelemelerine görseller eklemek istendiğinde bu tablo kullanılır. "ImageUrl" alanı, her yorum için ilişkilendirilmiş resimlerin URL'lerini içerir, böylece kullanıcılar yorumlarına görsel içerik ekleyebilirler. "CommentId" alanı, her resmin hangi yorumla ilişkili olduğunu gösterir, böylece resimler ve yorumlar arasındaki ilişki belirlenebilir. Bu yapı kullanıcıların yorumlarına görsel zenginlik katmak için kullanışlı bir araç sağlar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 5. CommentLikes Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/60d15a1e-c57b-48b7-8474-b2fbc211d912)

```MSSQL
Id
UserId
CommentId
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu veritabanı tablosu kullanıcıların yorumlara beğeni eklemesini sağlamak için tasarlanmıştır. Örneğin bir forum veya blog platformunda kullanıcıların yorumlara destek ifadesi veya beğeni eklemelerini istediğinizde bu tablo kullanılır. "UserId" alanı her beğeninin hangi kullanıcı tarafından yapıldığını belirtir, böylece her kullanıcının hangi yorumları beğendiğini takip edebilirsiniz. "CommentId" alanı, beğeninin hangi yorumla ilişkilendirildiğini gösterir; bu sayede popüler yorumları veya en çok beğeni alan yorumları belirlemek mümkün olur. Bu tablo yorumlara beğeni eklemek ve kullanıcı etkileşimini artırmak için kullanışlı bir yapı sağlar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 6. Comments Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/b3e72caa-c5f1-4b59-ae4f-95fe95037753)

```MSSQL
Id
OrderId
Rating
Comment
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu veritabanı tablosu müşterilerin siparişlerle ilgili yorumlar yapmalarını ve ürün veya hizmetlerin kalitesini puanlayabilmelerini sağlamak için kullanılır. Örneğin bir otel rezervasyon sitesinde müşteriler, konaklama deneyimlerini değerlendirmek ve yorumlamak amacıyla bu tabloyu kullanabilirler.

"OrderId" alanı, her yorumun hangi sipariş veya rezervasyonla ilişkilendirildiğini gösterir, böylece hangi yorumun hangi rezervasyonla bağlantılı olduğunu takip etmek mümkün olur. Bu tablo müşteri görüşlerini kaydetmek, işletme performansını değerlendirmek ve iyileştirmeler yapmak için veri toplamak üzere kullanışlı bir yapı sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 7. Invoices Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/2027abc1-e7d2-4acc-8235-e18a108b5756)

```MSSQL
Id
OrderId
InvoiceNumber
Date
DeliveryDate
CreatedDate
UpdatedDate
Discount
```

AÇIKLAMA:
Bu veritabanı tablosu siparişlerin faturalarını saklama amacıyla oluşturulmuştur. Her bir fatura belirli bir siparişe ait bilgileri içerir ve siparişin detaylarını, ödeme bilgilerini ve varsa indirim detaylarını içerebilir. "OrderId" alanı her faturanın hangi siparişe ait olduğunu belirler, böylece hangi faturanın hangi siparişle ilişkili olduğunu takip edebilirsiniz. Bu yapı finansal işlemleri yönetmek, fatura bilgilerini saklamak ve siparişlerin ödeme durumunu takip etmek için kullanışlı bir çözümdür.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 8. Orders Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/a518d23b-dff2-499f-be78-150840962430)

```MSSQL
Id
UserId
ProductFieldId
SellingPrice
Stock
UserAddressId
CreatedDate
UpdatedDate
OrderStatusId
CargoTracingNumber
```

AÇIKLAMA:
Bu veritabanı tablosu siparişlerin organizasyonu ve izlenmesi için tasarlanmıştır. Her siparişin özgün kimliğini, ürünün satış fiyatını, mevcut stok miktarını, teslimat adresini ve diğer ayrıntıları içerir. "UserId" alanı, hangi kullanıcının hangi siparişi oluşturduğunu belirleyerek siparişleri izlemeye yardımcı olur. "OrderStatusId" alanı siparişin anlık durumunu belirtir ve siparişin ilerlemesini gösterir, böylece siparişin hangi aşamada olduğunu takip edebilirsiniz. Bu tablo e-ticaret veya sipariş tabanlı platformlarda sipariş yönetimini desteklemek için etkili bir yapı sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 9. OrderStatuses Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/fd2fdedf-fdb7-4efa-8ceb-9ffb67abe19c)

```MSSQL
Id
Name
CreatedDate
UpdatedDate
IsActive
```

AÇIKLAMA:
Bu veritabanı tablosu, siparişlerin çeşitli aşamalarını izlemek ve düzenlemek amacıyla kullanılır. Siparişlerin farklı durumlarını adlandırarak her bir aşamayı temsil eder. "IsActive" alanı ise bir sipariş durumunun etkin olup olmadığını belirtir. Örneğin bir sipariş durumu artık kullanılmayacaksa bu alanı pasif konumuna getirerek yeni siparişlerde bu durumu seçilemez hale getirebilirsiniz.

Bu tablo siparişlerin yönetimi ve izlenmesi için pratik bir yapı sunar ve farklı sipariş durumlarını tanımlamanıza yardımcı olur.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 10. PaymentDetails Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/aa15d9f3-adec-4c16-ab77-6318d2c43221)

```MSSQL
Id
OrderId
PaymentPrice
PaymentType
CreatedDate
UpdatedDate
KKPaymentConfirmId
BankName
IsCompleted
CompletedDate
Description
```
AÇIKLAMA:
Bu veritabanı tablosu siparişlerin ödeme detaylarını izlemek amacıyla oluşturulmuştur. "OrderId" alanı, hangi siparişin hangi ödeme bilgilerine sahip olduğunu belirlerken "PaymentType" alanı ödeme yöntemini ifade eder, böylece kullanılan ödeme türleri takip edilir. "IsCompleted" alanı ödeme işleminin tamamlanıp tamamlanmadığını gösterirken "CompletedDate" alanı ise tamamlanma tarihini içerir. Bu tablo ödeme işlemlerini düzenlemek, ödeme türlerini izlemek ve sipariş ödeme detaylarını tutmak için etkili bir yapı sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 11. ProductFieldCategoryFields Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/fee99d93-e1df-4642-a702-3901ca56c864)

```MSSQL
Id
ProductFieldId
CategoryFieldId
Value
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu tablo ürün özellikleri ile kategori alanlarının ilişkisini yönetmek amacıyla tasarlanmıştır. Örneğin bir e-ticaret platformunda ürünlerin "Renk", "Beden", "Malzeme" gibi özelliklerini, "Kumaş Türü", "Boyut Seçenekleri" gibi kategori alanlarıyla ilişkilendirmek için kullanılır. "ProductFieldId" ve "CategoryFieldId" alanları, ürün özelliği ile kategori alanı arasındaki bağlantıyı sağlarken "Value" alanı bu ilişkinin değerini içerir. Bu yapı ürün ve kategori bilgilerinin daha esnek ve detaylı bir şekilde yönetilmesine yardımcı olur.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 12. ProductFieldImageUrls Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/c82fc53e-430f-4d12-9995-f68c7aa06b29)

```MSSQL
Id
ImageUrl
CreatedDate
UpdatedDate
ProductFieldId
```

AÇIKLAMA:
Bu veritabanı tablosu ürün özelliklerine ait görselleri yönetmek ve depolamak amacıyla tasarlanmıştır. Örneğin bir e-ticaret platformunda "Siyah renk" veya "XL beden" gibi ürün özellikleri için ilişkilendirilmiş resimleri bu tabloda saklamak mümkündür. Her bir resim bir ürün özelliği ile ilişkilidir ve bu tablo sayesinde bu ilişkiyi düzenleyebilirsiniz.

"ProductFieldId" alanı her resmin hangi ürün özelliği ile ilişkilendirildiğini göstererek, her bir özellik için ait olan resimleri kolayca tanımlamanıza yardımcı olur. Bu tablo ürünlerin daha çekici ve ayrıntılı bir şekilde sunulması için kullanışlı bir araç sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 13. ProductFields Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/5a36cb81-95e8-4a44-8586-c66b8607bea4)

```MSSQL
Id
Name
CreatedDate
UpdatedDate
ProductSelectionId
MainImageUrl
MainProductFieldId
IsActive
Price
SellingPrice
Stock
IsVatInclude
```

AÇIKLAMA:
Bu veritabanı tablosu ürün özelliklerini yönetmek ve bu özelliklere ait ayrıntıları depolamak için özel olarak tasarlanmıştır. Ürünlerin çeşitli özelliklerini, stok durumlarını, fiyatlarını, ana resimlerini ve diğer önemli detaylarını bu tablo üzerinden kolaylıkla takip edebilir ve yönetebilirsiniz. Bu yapı ürünlerin daha kapsamlı ve organize bir şekilde sunulması ve yönetilmesi için etkili bir araç sağlar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 14. Products Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/72543e2a-dcc5-4c9f-acae-1802840f521e)

```MSSQL
Id
Name
OverrangeRating
CreatedDate
UpdatedDate
SellerId
```

AÇIKLAMA:
Bu veritabanı tablosu e-ticaret platformları veya ürün yönetimi gerektiren sistemlerde ürünlerin depolanmasını sağlamak amacıyla oluşturulmuştur. "Name" alanı ürünlerin isimlerini içerir ve ürünleri isimleriyle kolayca tanımlamanızı sağlar. "SellerId" alanı ise ürünü satan satıcının kimliğini belirtir, böylece hangi ürünün hangi satıcıya ait olduğunu izleyebilirsiniz. Bu tablo ürünlerin yönetimi, satıcıların tanımlanması ve ürünlerin temel bilgilerinin saklanması için etkili bir yapı sağlar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 15. ProductSelections Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/feca4d28-bf19-405e-b22b-cb8c3dc4b34f)

```MSSQL
Id
Name
CreatedDate
UpdatedDate
ProductId
MainProductSelectionId
```

AÇIKLAMA:
Bu veritabanı tablosu ürün seçeneklerini düzenlemek ve bu seçeneklerin hiyerarşik yapısını tanımlamak amacıyla kullanılır. Örneğin, bir e-ticaret platformunda "Renk Seçenekleri" veya "Beden Seçenekleri" gibi ürün seçenekleri bu tablo üzerinde saklanabilir. Her bir ürün seçeneği belirli bir ürüne bağlıdır ve bu tablo sayesinde bu ilişki kurulur.

"ProductId" alanı hangi ürünün hangi seçeneklere sahip olduğunu belirterek, ürünlerin farklı seçeneklerini hızlıca tanımlamanıza olanak tanır. "MainProductSelectionId" alanı ise bir ürün seçeneğinin bir ana ürün seçeneğiyle bağlantısını ifade eder, böylece seçenekler arasında bir hiyerarşi oluşturabilirsiniz. Bu tablo ürün seçeneklerini yönetmek ve ürünlerin çeşitliliğini daha iyi organize etmek için kullanışlı bir yapı sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 16. Sellers Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/3242cd72-ac96-48a4-8954-1d44de898921)

```MSSQL
Id
Name
Address
TaxIdentityNumber
IdentityNumber
TaxDepartmentId
WebSite
PhoneNumber
Email
UserName
PasswordHash
PasswordSalt
IsConfirm
ConfirmCode
ConfirmCodeSendDate
ChangePasswordCode
ChangePasswordCodeSendDate
ChangePasswordIsCompleted
CreatedDate
UpdatedDate
AverageRating
IsActive
```

AÇIKLAMA:
Bu veritabanı tablosu satıcıların kimlik bilgilerini, hesap durumlarını, şifre doğrulamalarını, ortalama değerlendirmelerini ve temel hesap bilgilerini depolamak amacıyla kullanılır. "TaxDepartmentId" alanı ile satıcıların vergi dairesine ilişkilendirilme bilgisi tutulabilir ve "IsActive" alanı ile satıcı hesaplarının etkinlik durumu yönetilebilir. Bu tür bir tablo e-ticaret platformlarında veya pazaryerlerinde satıcı hesaplarının yönetimi ve genel bilgilerin saklanması için kullanışlı bir yapı sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 17. SellerTitles Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/f9c9d7e1-a593-473d-8bef-1a4b5dac9f23)

```MSSQL
Id
Title
CreatedDate
UpdatedDate
SellerId
```

AÇIKLAMA:
Bu veritabanı tablosu satıcı unvanlarını düzenlemek ve bu unvanların hangi satıcıya ait olduğunu izlemek amacıyla oluşturulmuştur. Örneğin bir e-ticaret platformunda farklı satıcıların çeşitli unvanları olabilir ve bu unvanları bu tablo üzerinde depolayabilirsiniz. "SellerId" alanı her unvanın hangi satıcıya ait olduğunu belirleyerek, satıcıların çeşitli unvanlarını takip etmenize yardımcı olur. Bu tablo satıcıların organizasyon içindeki rollerini ve pozisyonlarını belirlemek ve yönetmek için etkili bir araç sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 18. ShoppingCarts Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/47c968a9-35bc-466d-96b0-d2fb80f4295f)

```MSSQL
Id
UserId
ProductFieldId
Stock
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu veritabanı tablosu kullanıcıların alışveriş sepetlerini düzenlemek ve yönetmek amacıyla tasarlanmıştır. "UserId" alanı her kullanıcının kendi sepetini oluşturabileceği şekilde tasarlanmıştır ve bu sepetlere farklı ürün alanları (ProductFieldId) ekleyebilirler. "Stock" alanı, sepete eklenen ürünün miktarını göstererek, kullanıcıların sepet içeriğini takip etmelerini sağlar. Bu tür bir tablo e-ticaret platformlarında kullanıcıların alışveriş sepetlerini düzenlemek ve içerdikleri ürünleri izlemek için kullanılır.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 19. TaxDepartments Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/73dae5c4-72f8-4db6-b814-b678eb32e2c3)

```MSSQL
Id
City
Town
Code
Name
```

AÇIKLAMA:
Bu veritabanı tablosu vergi dairesi bilgilerini düzenlemek ve bu bilgileri şehir ve ilçe bazında kategorize etmek amacıyla kullanılır. Vergi daireleri farklı şehirlerde ve ilçelerde yer alabilir, bu nedenle "City" ve "Town" alanları bu bağlantıyı ifade eder. Vergi dairesi kodu ("Code"), her bir vergi dairesini benzersiz bir şekilde tanımlamak için kullanılır ve "Name" alanı vergi dairesinin adını daha anlaşılır bir şekilde temsil eder. Bu tablo vergi dairesi bilgilerini düzenlemek ve bu bilgileri şehir ve ilçe düzeyinde sınıflandırmak için etkili bir yapı sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 20. TicketDetails Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/2c940aba-338d-4174-8f5f-95aa7e976f11)

```MSSQL
Id
TicketId
SellerId
UserId
Content
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu veritabanı tablosu kullanıcıların veya satıcıların destek taleplerinin detaylarını yönetmek ve bu talepleri ilgili taraflara bağlamak amacıyla kullanılır. "TicketId" alanı her bir destek talebinin kimliğini tanımlar ve bu sayede her talebin ayrıntıları aynı kayda bağlı olarak saklanır. "SellerId" ve "UserId" alanları, talebin ilgili olduğu satıcı veya kullanıcıyı gösterir ve her ikisi de isteğe bağlı olarak boş bırakılabilir. "Content" alanı talebin detaylarına dair metin içeriğini içerir. Bu tablo müşteri destek sistemleri veya yardım masası uygulamalarında destek taleplerini düzenlemek ve ilgili kişilere yönlendirmek için etkili bir yapı sağlar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 21. Tickets Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/10fff6a5-2e2d-4839-9806-ffd69bc83049)

```MSSQL
Id
SellerId
UserId
Subject
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu veritabanı tablosu kullanıcıların ve satıcıların destek taleplerini yönetmek ve bu talepleri ilgili taraflara bağlamak amacıyla kullanılır. "SellerId" ve "UserId" alanları, talebin hangi satıcı veya kullanıcıya ait olduğunu belirtir. "Subject" alanı talebin başlığını içerir ve kullanıcıların veya satıcıların hangi konuda destek talebi ilettiğini açıklar. "CreatedDate" alanı, talebin ne zaman oluşturulduğunu gösterir. Bu tablo müşteri destek sistemleri veya yardım masası uygulamalarında destek taleplerini kaydetmek, ilgili taraflara iletmek ve taleplerin durumunu izlemek için kullanışlı bir yapı sağlar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 22. UserAddresses Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/a6ea56bd-a106-471c-b61e-8127a5d14b47)

```MSSQL
Id
UserId
City
Town
Street
ZipCode
Address
PhoneNumber
Name
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu veritabanı tablosu kullanıcıların çeşitli teslimat adreslerini yönetmek için kullanılır. Her kullanıcı, birden fazla adrese sahip olabilir ve bu adresler farklı amaçlar için (ev, iş, kargo adresi vb.) belirlenebilir. Adresler, kullanıcının bulunduğu şehri, ilçeyi, sokak bilgisini, posta kodunu, iletişim numaralarını ve diğer ayrıntıları içerir. Bu tablo e-ticaret platformları, kargo hizmetleri ve benzeri uygulamalarda kullanıcıların farklı teslimat adreslerini ve iletişim bilgilerini düzenlemek ve saklamak için kullanışlı bir yapı sunar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 23. Users Tablosu

![resim](https://github.com/AhmetSahinNL/E-TicaretDataBase/assets/139613517/157877fb-0579-45ab-b5aa-ae558bc9908a)

```MSSQL
Id
Name
Email
PhoneNumber
PasswordHash
PasswordSalt
IsActive
CreatedDate
UpdatedDate
```

AÇIKLAMA:
Bu veritabanı tablosu kullanıcıların öz temel bilgilerini (ad, e-posta, telefon numarası), şifrelerinin güvenli bir şekilde saklanması (şifre karması ve tuzlama), hesap durumunu (etkin veya pasif), ve hesap oluşturma/güncelleme tarihlerini muhafaza etmek için kullanılır. Bu yapı kullanıcı hesaplarının yönetimi ve yetkilendirme işlemlerinin gerçekleştirilmesinde kullanılır. Özellikle web siteleri, uygulamalar, üyelik sistemleri ve güvenli kimlik doğrulama gerektiren platformlarda bu tablo kullanışlı ve güvenli bir temel oluşturur.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
