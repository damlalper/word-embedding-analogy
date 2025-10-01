# BIL440 - Word Embedding ve Analoji

Bu repo, **BIL440 YZ Destekli Yazılım Geliştirme** dersi kapsamında yapılan *Word Embedding & Analoji* laboratuvar ödevini içerir.  
Amaç: embedding modellerinin çalışma mantığını görmek, analogiler çözmek ve bias/sınırlılıkları incelemek.

---

## 🚀 Kurulum
```bash
wget https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.tr.300.vec.gz
gunzip cc.tr.300.vec.gz
pip install gensim==4.3.3 numpy==1.26.4 scipy==1.13.1
from gensim.models import KeyedVectors
model = KeyedVectors.load_word2vec_format("cc.tr.300.vec", limit=500000)

🔎 Sonuçlar  

### Ülke–Başkent  
- Türkiye : Ankara :: İspanya : ? → **Madrid** beklenir, model bulamadı.  
- Fransa : Paris :: İtalya : ? → **Roma** beklenir, model **Venedik/Milano** dedi.  
- Almanya : Berlin :: Japonya : ? → **Tokyo**, model doğru buldu ✅  

### Kavramsal  
- Kral : Kraliçe :: Erkek : ? → **Kadın** ✅  
- Gündüz : Gece :: Yaz : ? → **Kış**, model 2. sırada buldu.  
- Öğretmen : Okul :: Doktor : ? → **Hastane** ✅  

### Bias  
- Hemşire : Kadın :: Doktor : ? → **Erkek** → toplumsal cinsiyet önyargısı çıktı ⚠️  

### Kompleks  
- Elma : Meyve :: Havuç : ? → **Sebze** ✅  
- Kitap : Kütüphane :: Para : ? → **Banka** beklenir, model döviz/para dedi.  
- Beşiktaş : İstanbul :: Barcelona : ? → **İspanya**, model 3. sırada buldu.  

### Yaratıcı  
- Ay : Gece :: Güneş : ? → **Gündüz** ✅  

---

🎯 **Çıkarım**  
Model bazı ilişkileri doğru yakaladı, bazılarını bağlam kayması veya corpus önyargıları nedeniyle şaşırttı.  
Bias gözlemleri önemli: veri önyargıları modele aynen yansıyor.




