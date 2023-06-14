# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

## Proje Kurulumu
Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

### Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#### Tablolar 
`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]


##### Görevler
Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın. 


MIN-MAX, COUNT-AVG-SUM, GROUP BY, JOINS (INNER, OUTER, LEFT, RIGHT
	#ilk 3 soruyu join kullanmadan yazın.
	1) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
	
         SELECT ogrenci.ograd, ogrenci.ogrsoyad, islem.atarih FROM ogrenci , islem 
		 WHERE ogrenci.ogrno= islem.ogrno
		 ORDER BY ogrenci.ograd

	2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

	    SELECT kitap.kitapadi, tur.turadi FROM kitap, tur
		WHERE kitap.turno=tur.turno
		AND tur.turadi IN ('Fıkra', 'Hikaye');
	
	3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.
    
<!-- sorgu çalışmadı -->
	    SELECT ogrenci.ogrno, ogrenci.ograd, ogrenci.ogrsoyad ,kitap.kitapadi 
		FROM ogrenci,islem,kitap
		WHERE ogrenci.ogrno=islem.ogrno
		AND islem.kitapno=kitap.kitapno
		AND ogrenci.sinif='10A' OR ogrenci.sinif='10C'
		ORDER BY ogrenci.ogrno;
	#join ile yazın
	4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

	    SELECT ogrenci.ograd, ogrenci.ogrsoyad, islem.atarih FROM ogrenci
		INNER JOIN islem ON ogrenci.ogrno=islem.ogrno
	
	
	
	5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

	   SELECT kitap.kitapadi, tur.turadi FROM kitap
	   INNER JOIN tur ON kitap.turno= tur.turno
	   AND tur.turadi IN ('Fıkra', 'Hikaye');
	   
	
	
	6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.

	  SELECT ogrenci.ograd, ogrenci.ogrsoyad, ogrenci.ogrno, kitap.kitapadi 
	  FROM ogrenci
	  INNER JOIN islem ON ogrenci.ogrno = islem.ogrno
	  INNER JOIN kitap ON islem.kitapno= kitap.kitapno
	  WHERE sinif='10A' OR sinif='10C'
	  ORDER BY ogrenci.ograd
	
	
	7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.
	
	   SELECT ogrenci.ograd, ogrenci.ogrsoyad, islem.atarih
	   FROM ogrenci
	   LEFT JOIN islem ON ogrenci.ogrno = islem.ogrno
	   
	 
	8) Kitap almayan öğrencileri listeleyin.

	   SELECT ogrenci.ograd, ogrenci.ogrsoyad
	   FROM ogrenci
	   LEFT JOIN islem ON ogrenci.ogrno = islem.ogrno
	   WHERE islem.atarih IS NULL
	
	9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.

	    SELECT kitap.kitapno, kitap.kitapadi , COUNT(islem.islemno)
		FROM KİTAP
		LEFT JOIN islem ON kitap.kitapno = islem.kitapno
		GROUP BY kitap.kitapno, kitap.kitapadi
		ORDER BY kitap.kitapno ASC

	
	   
	
	10) Alınan kitapların kitap nu8marasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.


	11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.
	
	
	12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.
	
	
	13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.
	
	
	14) Tüm kitapların ortalama sayfa sayısını bulunuz.
	#AVG  
	     SELECT avg(sayfasayisi) FROM kitap
	
	15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.
	
	    SELECT kitap.kitapadi, kitap.sayfasayisi FROM kitap 
		WHERE kitap.sayfasayisi> (SELECT avg(sayfasayisi) FROM kitap)
	
	16) Öğrenci tablosundaki öğrenci sayısını gösterin

	    SELECT COUNT(ogrenci.ogrno) FROM ogrenci
	
	
	17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.

	    SELECT COUNT(*) AS toplamsayi FROM ogrenci
	
	
	18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.

	    
	
	
	19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

	    SELECT * FROM kitap WHERE kitap.sayfasayisi ORDER BY kitap.sayfasayisi desc LIMIT 1
	
	
	20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

	    SELECT kitap.kitapadi , kitap.sayfasayisi FROM kitap
		WHERE sayfasayisi= (SELECT MAX(sayfasayisi) FROM kitap)
	
	
	21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.
	
	    SELECT MIN(sayfasayisi) FROM kitap
	
	22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.
	 
	    SELECT kitap.kitapadi , kitap.sayfasayisi FROM kitap
		WHERE sayfasayisi= (SELECT MIN(sayfasayisi) FROM kitap)
	
	23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.
	    
		SELECT  MAX(sayfasayisi)
	    FROM kitap
		INNER JOIN tur ON kitap.turno= tur.turno
		WHERE turadi='Dram'
		
	
	24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.
	
        SELECT SUM(kitap.sayfasayisi) 
        FROM ogrenci
		INNER JOIN islem ON ogrenci.ogrno=islem.ogrno
		INNER JOIN kitap ON kitap.kitapno=islem.kitapno
        WHERE ogrenci.ogrno= 15 

	25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )

       SELECT ogrenci.ograd ,COUNT(*) AS adet
	   FROM ogrenci
	   GROUP BY ogrenci.ograd;
	
	26) Her sınıftaki öğrenci sayısını bulunuz.
	
	    SELECT sinif, COUNT(*) AS adet
        FROM ogrenci
        GROUP BY sinif
        ORDER BY adet;
	
	27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.
	
	    SELECT cinsiyet, COUNT(*) AS adet
        FROM ogrenci
        GROUP BY cinsiyet
        ORDER BY adet;
	
	28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.
	   
	   SELECT ogrenci.ograd, ogrenci.ogrsoyad, 
       SUM(kitap.sayfasayisi) AS toplamsayfasayisi
       FROM ogrenci
       INNER JOIN islem ON ogrenci.ogrno = islem.ogrno
       INNER JOIN kitap ON islem.kitapno = kitap.kitapno
       GROUP BY ogrenci.ograd, ogrenci.ogrsoyad 
       ORDER BY toplamsayfasayisi DESC;

	29) Her öğrencinin okuduğu kitap sayısını getiriniz.

	    SELECT 