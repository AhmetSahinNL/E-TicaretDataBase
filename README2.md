
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 1. CategoryListByNameAndCategoryPath Prosedürü

```MSSQL
CREATE PROCEDURE CategoryListByNameAndCategoryPath 
AS
BEGIN
    WITH CategoryHierarchy AS
    (
        -- Ana kategorileri bul
        SELECT 
            Id,
            Name,
            CAST(Name AS NVARCHAR(MAX)) AS CategoryPath
        FROM 
            Categories
        WHERE 
            MainCategoryId IS NULL
        UNION ALL
        -- Alt kategorileri bul
        SELECT 
            c.Id,
            c.Name,
            CAST(ch.CategoryPath + ' > ' + c.Name AS NVARCHAR(MAX)) AS CategoryPath
        FROM 
            Categories c
        JOIN 
            CategoryHierarchy ch ON ch.Id = c.MainCategoryId
    )
    SELECT * FROM CategoryHierarchy
    ORDER BY CategoryPath;
END
```

AÇIKLAMA:

Bu SQL saklama prosedürü bir e-ticaret sitesindeki kategori yapısını hiyerarşik bir şekilde listeleyen ve her kategorinin adını ve kategorinin hiyerarşik yolu (path) bilgisini içeren sonuçları döndüren bir sorgu oluşturur. Kısacası veritabanındaki kategorileri ağaç yapısına göre düzenler ve her kategorinin tam yolunu temsil eden bir "CategoryPath" alanı oluşturur.

Prosedürün işleyişi adım adım şu şekildedir:
• Ana kategorileri bulma:
İlk adımda 'Categories' tablosundan ana kategorileri seçer. Ana kategoriler 'MainCategoryId' alanı NULL olan kategorilerdir. Bu kategoriler hiyerarşinin en üst düzeyinde yer alır.
• Alt kategorileri bulma:
Daha sonra, CategoryHierarchy adı verilen bir ortak tablo ifadesi (Common Table Expression - CTE) kullanılarak alt kategoriler bulunur. Alt kategoriler Categories tablosunda ana kategorilere bağlı olan ve MainCategoryId alanı dolu olan kategorilerdir. Bu adım bir döngü (recursive) mantığı kullanır. Her adımda mevcut kategorinin altındaki alt kategorileri bulmak için aynı CTE tekrar çağrılır.
• Hiyerarşik yolu oluşturma:
Her kategori için, CategoryPath adında bir sütun oluşturulur. Bu sütun, o kategorinin hiyerarşik yolunu temsil eder. Her alt kategori üst kategorisinin CategoryPath değeri ile birleştirilerek oluşturulan bir yol alır. Bu sayede bir kategorinin tüm hiyerarşik yolu görsel olarak anlaşılabilir bir şekilde temsil edilir.
• Sonuçları sıralama:
Son olarak, oluşturulan hiyerarşik kategori listesi CategoryPath değerine göre sıralanır. Bu sayede sonuçlar hiyerarşik yapıya göre düzgün bir şekilde sıralanmış olur.

Bu prosedürü çağırdığınızda tüm kategorilerin adlarını ve onların hiyerarşik yollarını içeren bir sonuç kümesi alırsınız. Bu sonuçları örneğin bir e-ticaret sitesinde kategori gezinmesi veya raporlama amaçlarıyla kullanabilirsiniz.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 2. CategoryListWithSubCategories Prosedürü

```MSSQL
CREATE PROCEDURE CategoryListWithSubCategories
AS
BEGIN
    WITH CategoryHierarchy AS (
        SELECT 
            Id,
            Name,
            IsActive,
            MainCategoryId,
            CAST(Name AS VARCHAR(MAX)) AS Hierarchy
        FROM
            Categories
        WHERE 
            MainCategoryId IS NULL

        UNION ALL

        SELECT
            c.Id,
            c.Name,
            c.IsActive,
            c.MainCategoryId,
            CAST((ch.Hierarchy + ' > ' + c.Name) AS VARCHAR(MAX)) AS Hierarchy
        FROM 
            Categories c
        INNER JOIN CategoryHierarchy ch
        ON ch.Id = c.MainCategoryId
    )
    SELECT Hierarchy FROM CategoryHierarchy WHERE IsActive = 1;
END
```

AÇIKLAMA:

Bu SQL saklama prosedürü bir e-ticaret sitesindeki kategori yapısını ve alt kategorileri bir araya getiren ve etkin (aktif) kategorilerin hiyerarşik yollarını içeren sonuçları döndüren bir sorgu oluşturur. Özellikle kategori ağaç yapısını ve alt kategorileri içeren hiyerarşik bir liste oluştururken yalnızca etkin kategorileri listelemeyi sağlar.

Prosedürün işleyişi adım adım şu şekildedir:
• Ana kategorileri bulma:
İlk adımda 'Categories' tablosundan ana kategorileri seçer. Ana kategoriler 'MainCategoryId' alanı NULL olan kategorilerdir. Bu kategoriler hiyerarşinin en üst düzeyinde yer alır.
• Alt kategorileri bulma:
Daha sonra 'CategoryHierarchy' adı verilen bir ortak tablo ifadesi (Common Table Expression - CTE) kullanılarak alt kategoriler bulunur. Bu adım önceki prosedürde olduğu gibi bir döngü (recursive) mantığı kullanır. Her adımda mevcut kategorinin altındaki alt kategorileri bulmak için aynı CTE tekrar çağrılır.
• Hiyerarşik yolu oluşturma:
Her kategori için 'Hierarchy' adında bir sütun oluşturulur. Bu sütun kategorinin hiyerarşik yolunu temsil eder. Ana kategorilerin Name değeri ile başlayan bu yol alt kategorilerde ch.Hierarchy ile birleştirilerek oluşturulur. Bu sayede her kategori ve alt kategorisinin hiyerarşik yolu elde edilir.
• Etkin kategorileri seçme:
Oluşturulan hiyerarşik kategori listesi içerisinde sadece etkin (aktif) kategorilere ait hiyerarşik yolları seçer. Bu 'IsActive' alanı 1 olan kategorileri listeleyerek etkin olmayan kategorileri dışarıda bırakır.

Bu prosedürü çağırdığınızda yalnızca etkin kategorilerin hiyerarşik yollarını içeren bir sonuç kümesi alırsınız. Bu sonuçları örneğin e-ticaret sitesindeki etkin kategorilerin hiyerarşik yapısını göstermek veya gezinmek için kullanabilirsiniz.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 3. MainCategoryListByCategoryId Prosedürü

```MSSQL
CREATE PROCEDURE MainCategoryListByCategoryId
@categoryId INT
AS
BEGIN
    WITH CategoryHierarchy AS (
        SELECT
            Id,
            Name,
            IsActive,
            MainCategoryId,
            CAST(Name AS VARCHAR(MAX)) AS Hierarchy
        FROM
            Categories
        WHERE 
            Id = @categoryId

        UNION ALL

        SELECT
            c.Id,
            c.Name,
            c.IsActive,
            c.MainCategoryId,
            CAST((c.name  + ' > ' + ch.Hierarchy) AS VARCHAR(MAX)) AS Hierarchy 
        FROM
            Categories c
        INNER JOIN CategoryHierarchy ch
        ON ch.MainCategoryId = c.Id
    )
    SELECT Hierarchy 
    FROM CategoryHierarchy
    WHERE IsActive = 1 AND MainCategoryId IS NULL;
END
```

AÇIKLAMA:

Bu SQL saklama prosedürü belirli bir kategori ID'sine (categoryId) dayanarak verilen kategorinin ana kategorisinin (ana kategori) hiyerarşik yolunu oluşturan ve etkin (aktif) ana kategorinin yolunu döndüren bir sorgu oluşturur. Yani verilen kategoriye ait ana kategorinin hiyerarşik yolunu oluşturarak döndürür.

Prosedürün işleyişi adım adım şu şekildedir:
• Belirli kategori ID'sine sahip kategoriyi bulma:
İlk adımda verilen '@categoryId' parametresi kullanılarak 'Categories' tablosundan belirli bir kategori bulunur. Bu kategori daha sonra ana kategorisine olan bağlantısı üzerinden hiyerarşi oluşturmak için temel oluşturacak kategoridir.
• Ana kategori hiyerarşisini oluşturma:
Daha sonra 'CategoryHierarchy' adı verilen bir ortak tablo ifadesi (Common Table Expression - CTE) kullanılarak ana kategori hiyerarşisi oluşturulur. Bu adım seçilen kategori üzerinden ana kategorisine doğru bir döngü (recursive) mantığı kullanarak hiyerarşiyi oluşturur.
• Hiyerarşik yolu oluşturma:
Her adımda mevcut kategori ve onun ana kategorisi için bir hiyerarşik yol oluşturulur. Bu yol 'c.Name' (mevcut kategori) ile 'ch.Hierarchy' (önceki adımda oluşturulan ana kategori hiyerarşisi) değerlerini birleştirerek elde edilir.
• Etkin ana kategoriyi seçme:
Oluşturulan hiyerarşik kategori listesi içerisinde sadece etkin (aktif) ana kategorinin yolunu seçer. Bu 'IsActive' alanı 1 olan ana kategoriyi listeleyerek etkin olmayan ana kategorileri dışarıda bırakır.

Bu prosedürü çağırdığınızda belirli bir kategoriye ait ana kategorinin etkin (aktif) olması durumunda bu ana kategorinin hiyerarşik yolunu elde edersiniz. Bu sonucu kullanarak örneğin bir ürünün veya kategorinin hangi ana kategoride olduğunu gösteren bir görsel veya rapor oluşturabilirsiniz.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

