# 🧠 BIL440 - Word Embedding & Analoji  

Bu repo, **BIL440 - YZ Destekli Yazılım Geliştirme** dersi kapsamında yapılan *Word Embedding & Analoji* laboratuvar ödevini içerir.  

**Amaç:**  
- Embedding modellerinin mantığını gözlemlemek  
- Analojilerle (A : B :: C : ?) kelime ilişkilerini test etmek  
- Modelin sınırlılıklarını ve önyargılarını (bias) tartışmak  

---

## 🚀 Kurulum  

```bash
wget https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.tr.300.vec.gz
gunzip cc.tr.300.vec.gz
pip install gensim==4.3.3 numpy==1.26.4 scipy==1.13.1
from gensim.models import KeyedVectors
model = KeyedVectors.load_word2vec_format("cc.tr.300.vec", limit=500000)´´´´


```
🔎 Sonuçlar
-----------

### 🌍 Ülke–Başkent

* Türkiye : Ankara :: İspanya : ?  
  * **Beklenen:** Madrid  
  * **Model:** Bulamadı  

* Fransa : Paris :: İtalya : ?  
  * **Beklenen:** Roma  
  * **Model:** Venedik / Milano (yanlış)  

* Almanya : Berlin :: Japonya : ?  
  * **Beklenen:** Tokyo  
  * **Model:** Tokyo (✅ doğru, 1. sırada)  


### 👑 Kavramsal

* Kral : Kraliçe :: Erkek : ?  
  * **Beklenen:** Kadın  
  * **Model:** Kadın (✅ doğru)  

* Gündüz : Gece :: Yaz : ?  
  * **Beklenen:** Kış  
  * **Model:** Kış (2. sırada)  

* Öğretmen : Okul :: Doktor : ?  
  * **Beklenen:** Hastane  
  * **Model:** Hastane (✅ doğru)  


### ⚠️ Bias (Önyargı)

* Hemşire : Kadın :: Doktor : ?  
  * **Beklenen:** Tarafsız ilişki (meslek → meslek)  
  * **Model:** Erkek (⚠️ toplumsal cinsiyet önyargısı)  


### 🔀 Kompleks

* Elma : Meyve :: Havuç : ?  
  * **Beklenen:** Sebze  
  * **Model:** Sebze (✅ doğru)  

* Kitap : Kütüphane :: Para : ?  
  * **Beklenen:** Banka  
  * **Model:** Döviz / Para (yanlış, bağlam kayması)  

* Beşiktaş : İstanbul :: Barcelona : ?  
  * **Beklenen:** İspanya  
  * **Model:** İspanya (3. sırada)  


### 🌙 Yaratıcı

* Ay : Gece :: Güneş : ?  
  * **Beklenen:** Gündüz  
  * **Model:** Gündüz (✅ doğru)  


---

🎯 Çıkarımlar
-------------

* ✅ **Doğru bulunanlar:** Sebze, Hastane, Tokyo gibi doğrudan bağlamı güçlü örnekler.  
* ⚠️ **Yanlış çıkanlar:** Para–Banka ve Barcelona–İspanya gibi bağlamı farklı kullanılan kelimeler.  
* 📉 **Kısmi başarı:** Yaz–Kış ilişkisi, doğru ama 2. sırada çıktı.  
* 🔥 **Bias:** Hemşire–Doktor örneği, verideki toplumsal önyargının modele yansıdığını gösterdi.  


---

🛠️ Gelecek Çalışmalar
----------------------

* Türkçe için özel **analogik test seti** oluşturmak  
* Word2Vec, FastText ve BERT gibi farklı embedding’leri karşılaştırmak  
* Bias analizi için sistematik testler geliştirmek  


---

📚 Kaynaklar
------------

* [fastText Pretrained Vectors](https://fasttext.cc/docs/en/crawl-vectors.html)  
* Mikolov et al. (2013) - *Efficient Estimation of Word Representations in Vector Space*  
* [gensim](https://radimrehurek.com/gensim/) kütüphanesi  
