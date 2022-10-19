# SQL Notes

- SQL QUERIES : NORTHWIND DATABASE
    
    ### BİR TABLODAKİ TÜM SATIRLARI GETİRME
    
    ```sql
    SELECT * FROM CUSTOMERS
    ```
    
    ### BİR TABLONUN BELİRLİ SÜTUNLARINI GETİRME
    
    ```sql
    SELECT ContactName,CompanyName,City FROM Customers
    ```
    
    ### VERİLERİ BİR KOŞULA GÖRE GETİRME
    
    ```sql
    SELECT * FROM Customers where City = 'London' 
    -- Ansi de metinler tek tirnaktir
    SELECT * FROM products where categoryId=1 or UnitPrice>=10 
    -- farkli iki kosul "or" ile yapilir
    ```
    
    ### VERİLERİ SIRALAMA
    
    ```sql
    SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME
    -- Ürünleri Alfabetik olarak sıralama
    SELECT * FROM PRODUCTS ORDER BY CATEGORYID,PRODUCTNAME
    -- Ürünleri Kategori ID sine göre sırala, kategorileri de kendi içinde sıralar.
    SELECT * FROM PRODUCTS WHERE CATEGORYID=1 ORDER BY UNITPRICE DESC
    -- artan siralama icin "asc" keywordu, azalan siralama icin "desc" keywordu kullanilir
    ```
    
    ### SATIR SAYISI SORGULAMA
    
    ```sql
    SELECT COUNT(*) FROM PRODUCTS
    -- Products tablosunda kac satir yada kac adet product oldugunu gosterir.
    SELECT COUNT(*) FROM PRODUCTS WHERE CATEGORYID=1
    -- Products tablosunda CategoryId si 1 olan urunlerin sayisini getirir.
    
    ```
    
    ### TABLOYU BELİRLİ ÖZELLİĞE GÖRE GRUPLANDIRMA
    
    ```sql
    SELECT CATEGORYID FROM PRODUCTS GROUP BY CATEGORYID
    -- Products Tablosunu CategoryId'ye gruplandırır, ve CategoryID kolonunu döndürür.
    SELECT CATEGORYID, COUNT(*) FROM PRODUCTS GROUP BY CATEGORYID
    --Products tablosunu CategoryId ye göre gruplandırıp her bir kategoride kaç ürün olduğunu döndürür.
    --Bu Group By sorgusunda her bir kategory için COUNT(*) o kategoriye ait ürünleri sayar.
    SELECT CATEGORYID,COUNT(*) FROM PRODUCTS WHERE UNITSINSTOCK<10 AND UNITPRICE>10 GROUP BY CATEGORYID
    -- Gruplandırma işlemi nihai bir tablo üzerine yapılır ve sonrasında gruplandırılan parametreyi referans alan yeni bir tablo oluşturulur. Bu tabloda ayni kategoriye ait ürün sayısı gösterilir.
    SELECT CATEGORYID, COUNT(*) FROM PRODUCTS GROUP BY CATEGORYID HAVING COUNT(*)<10
    -- Gruplandırılmış bir tabloda sorgu yapmak için "where" yerie "having" keywordu kullanılır.
    
    ```
    
    ### TABLOLARI BİRLEŞTİRME (JOIN İŞLEMİ)
    
    ```sql
    -- INNER JOIN ILE BİRLEŞTİRME İŞLEMİ
    -- İKİ TABLOYU ORTAK OLAN ÖZELLİĞE GÖRE EŞLEŞTİRİR. SADECE EŞLEŞE VERİLER GETİRİLİR.
    SELECT * FROM PRODUCTS INNER JOIN CATEGORIES ON PRODUCTS.CATEGORYID = CATEGORIES.CATEGORYID
    -- KATEGORİ ID'LERİ EŞLEŞEN VERİLER İÇİN HER İKİ TABLONN TÜM SÜTUNLARI BİRLEŞTİRİLİR.
    SELECT PRODUCTS.PRODUCTID,PRODUCTS.PRODUCTNAME,PRODUCTS.UNITPRICE,PRODUCTS.UNITSINSTOCK,CATEGORIES.CATEGORYNAME FROM PRODUCTS INNER JOIN CATEGORIES ON PRODUCTS.CATEGORYID = CATEGORIES.CATEGORYID
    -- Tablolar join edildikten sonra oluşan tablodan sadece belirli sütunları gösterme
    
    -- LEFT JOIN ILE BİRLEŞTİRME İŞLEMİ
    -- LEFT JOIN ISLEMINDE BIRLESTIRME ISLEMININ SOLUNDA KALAN TOBLONUN TÜM SATIRLARI BİRLEŞMEYE SAHİL OLACAK ŞEKİLDE DİĞER TABLO İLE EŞLEŞTİRME YAPILIR.
    -- SOLDAKİ TABLODA YER ALIP SAĞDAKİ TABLODA YER ALMAYAN SATIRLAR İÇİN SAĞDAKİ TABLODAKİ DEĞERLERİ "NULL" VERİRLİR.
    SELECT * FROM CUSTOMERS C LEFT JOIN ORDERS O ON C.CustomerID = O.CustomerID
    -- Bu sorguda orders tablosunda yer almayan Customer öğeleri de yer almaktadır. Bu öğeleri listelemek için Orders tablosunda CustomerID değeri NULL dönen öğeleri listelemek yeterlidir.
    SELECT * FROM CUSTOMERS C LEFT JOIN ORDERS O ON C.CustomerID = O.CustomerID WHERE O.CUSTOMERID IS NULL
    
    -- RIGHT JOIN ILE BİRLEŞTİRME İŞLEMİ
    -- RIGHT JOIN İŞLEMİ LEFT JOİN İŞLEMİNİN TABLOLARIN  YÖNLERİ DEĞİŞMİŞ HALİDİR.
    SELECT * FROM ORDERS O RIGHT JOIN CUSTOMERS C ON C.CustomerID = O.CustomerID
    ```
