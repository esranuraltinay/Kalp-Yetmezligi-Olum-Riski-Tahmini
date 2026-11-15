# Kalp Yetmezliğinde Ölüm Riski Tahmini

> SVY 5430 Biyomedikal Verilerin Analizi ve Yapay Zeka · Fırat Üniversitesi YBAE · 2026–2027 Güz
> Proje kodu: **BVYZ-01** · Öğrenci: Esranur Altınay

Bu depo, dönem projesinin tüm kodunu, çalıştırılabilir defterlerini ve LaTeX raporunu içerir.
**Veri dosyaları depoya konmaz**; `data/README.md` verinin nereden ve nasıl indirileceğini anlatır.

## Klinik soru

Serum kreatinin ve ejeksiyon fraksiyonu gibi klinik değişkenler kullanılarak kalp yetmezliği hastalarının ölüm riskinin tahmin edilip edilemeyeceği incelenmiştir. Bu çalışma, yüksek riskli hastaların erken tanınması ve klinik müdahale süreçlerinin optimize edilmesi açısından kritik önem taşır.

## Veri

| | |
|---|---|
| Kaynak | [UCI Heart Failure Clinical Records Dataset](https://archive.ics.uci.edu/dataset/519/heart+failure+clinical+records) |
| Örnek sayısı | 299 hasta / kayıt |
| Öznitelik sayısı | 12 |
| Hedef | DEATH_EVENT (Takip süresi içinde ölüm durumu: 0 = Hayatta, 1 = Vefat) |
| Sınıf oranı | %32.1 Vefat (96 hasta), %67.8 Hayatta (203 hasta) |
| Lisans / erişim | Açık Erişim |

## Yöntem (kısaca)

Veri setinde eksik ve yinelenen kayıtlar kontrol edilmiş, aykırı değerler incelenmiş ve tahmin anında bilinmeyen takip süresini temsil eden time değişkeni model girdilerinden çıkarılmıştır. Sürekli değişkenler StandardScaler ile ölçeklendirilmiş, ikili değişkenler mevcut 0/1 değerleriyle bırakılmıştır. Temel model olarak Lojistik Regresyon kullanılmıştır. Hiperparametre seçimi için 3 katlı iç, model değerlendirmesi için 5 katlı dış StratifiedKFold çapraz doğrulama uygulanmıştır. Ön işleme ve model adımları Pipeline içerisinde birleştirilerek veri sızıntısı önlenmeye çalışılmıştır.

## Sonuçlar (kısaca)

| Model | ROC-AUC | PR-AUC | Kalibrasyon (Brier) |
|---|---|---|---|
| Temel (Lojistik Regresyon) |0.7832 |0.6578 |0.1910 |
| <Model 2> | | | |

Lojistik Regresyon modeli genel ayırt etme performansı göstermiş olsa da varsayılan 0.50 karar eşiğinde ölüm olaylarının yalnızca %7,29'unu yakalamıştır. Bu nedenle pozitif sınıfı yakalama başarısının geliştirilmesi gerekmektedir.

## Nasıl çalıştırılır

```bash
# Colab: notebooks/ altındaki defterleri sırayla açın; her defterin ilk hücresi veriyi indirir. Sırasıyla hücreleri çalıştırın. Veri setinin indirilmesi ve dosya yolları için defterlerdeki açıklamaları takip edin.
# Yerel:
conda create -n proje python=3.12 -y
conda activate proje
pip install -r requirements.txt
jupyter lab
```

## Depo yapısı

```
notebooks/   01_baslangic.ipynb · 02_model.ipynb · 03_aciklama.ipynb
src/         yeniden kullanılan fonksiyonlar
rapor/       main.tex, kaynaklar.bib, sekiller/ ve derlenmiş rapor.pdf
data/        README.md (indirme talimatı) — veri dosyası YOK
```

## Tekrarlanabilirlik


- Rastgelelik tohumu: `SEED = 42`
- Bölme stratejisi: 5 katlı dış ve 3 katlı iç `StratifiedKFold`
- Katmanlama değişkeni: `DEATH_EVENT`
- Ön işleme: `Pipeline` içerisinde gerçekleştirilir ve ölçeklendirme yalnızca ilgili eğitim katında öğrenilir.
- Ortam: `requirements.txt` (kütüphane sürümleri belirtilmiştir).

## Kaynaklar

Raporun kaynakçasıyla aynı; en az üç hakemli makale.
