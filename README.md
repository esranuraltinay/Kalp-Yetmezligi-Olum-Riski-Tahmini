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
| Kaynak | UCI Heart Failure Clinical Records Dataset |
| Örnek sayısı | 299 hasta / kayıt |
| Öznitelik sayısı | 12 |
| Hedef | DEATH_EVENT (Takip süresi içinde ölüm durumu: 0 = Hayatta, 1 = Vefat) |
| Sınıf oranı | %32.1 Vefat (96 hasta), %67.8 Hayatta (203 hasta) |
| Lisans / erişim | Açık Erişim |

## Yöntem (kısaca)

Ön işleme → model → değerlendirme → açıklama zincirini üç–dört cümleyle yazın. Ayrıntı raporda.

## Sonuçlar (kısaca)

| Model | ROC-AUC | PR-AUC | Kalibrasyon (Brier) |
|---|---|---|---|
| Temel (lojistik) | | | |
| <Model 2> | | | |

Bir cümle: en önemli bulgu ne?

## Nasıl çalıştırılır

```bash
# Colab: notebooks/ altındaki defterleri sırayla açın; her defterin ilk hücresi veriyi indirir.
# Yerel:
conda create -n proje python=3.12 -y && conda activate proje
pip install -r requirements.txt
jupyter lab
```

## Depo yapısı

```
notebooks/   01_veri_kesif.ipynb · 02_model.ipynb · 03_aciklama.ipynb
src/         yeniden kullanılan fonksiyonlar (ön işleme, metrikler, çizimler)
rapor/       main.tex, kaynaklar.bib, sekiller/ ve derlenmiş rapor.pdf
data/        README.md (indirme talimatı) — veri dosyası YOK
```

## Tekrarlanabilirlik

- Rastgelelik tohumu: `SEED = 42` (tüm defterlerde)
- Bölme stratejisi: <StratifiedKFold / GroupKFold(hasta) / zaman-farkında>
- Ortam: `requirements.txt` (sürümler sabit)

## Kaynaklar

Raporun kaynakçasıyla aynı; en az üç hakemli makale.
