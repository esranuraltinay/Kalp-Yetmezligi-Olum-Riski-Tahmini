# Veri 

Veri dosyaları GitHub deposuna eklenmez. Notebook'ların ilk hücresinde yer alan kod, veri setini UCI Machine Learning Repository üzerinden otomatik olarak indirir ve Colab ortamına yükler.

1. **Kaynak:** [UCI Machine Learning Repository – Heart Failure Clinical Records](https://archive.ics.uci.edu/dataset/519/heart+failure+clinical+records)
2. **İndirme yöntemi:** `urllib.request.urlretrieve()` kullanılarak veri seti belirtilen URL üzerinden otomatik indirilir.
3. **Dosya adı:** `heart_failure_clinical_records_dataset.csv`
4. **Kayıt ve sütun sayısı:** 299 hasta, 12 öznitelik ve 1 hedef değişken (`DEATH_EVENT`), toplam 13 sütun.
5. **Kullanım:** Veri seti açık erişimlidir. Kullanım ve atıf koşulları için UCI kaynak sayfasını inceleyin.
