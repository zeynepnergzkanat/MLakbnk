# Fake News Detection — Logistic Regression Pipeline

**Proje Türü:** Gözetimli Öğrenme – İkili Sınıflandırma  
**Model:** Logistic Regression (GridSearch CV ile optimize edilmiş `C` hiperparametresi)

# Problemin Tanımı
Günümüzde çevrim-içi platformlarda paylaşılan sahte haberler (fake news) kamuoyunu yanlış yönlendirebilir, toplumsal kutuplaşmayı artırabilir ve kurumların itibarına zarar verebilir. 
Bu proje, haber metinlerini **gerçek (real)** veya **sahte (fake)** olarak otomatik etiketlemek için makine öğrenmesi temelli bir çözüm sunar.

##  EDA & Veri Ön İşleme Özetleri
| **Eksik Veri Kontrolü** | `text` ve `label` dışındaki alanlar çıkartıldı, eksik satırlar atıldı. |
| **Etiket Dağılımı** | Veri dengeli (≈ 50 % real / 50 % fake). |
| **Metin Temizleme** | Küçük harf, URL silme, noktalama & rakam temizliği. |
| **Özellik Çıkarma** | `max_features=3000` olacak şekilde **TF-IDF** vektörleştirme. |
| **Eğitim/Test Bölmesi** | %80 eğitim – %20 test, **stratify** ile sınıf oranı korundu. |

##  Model Seçimi & Neden Logistic Regression?
| **Baseline Performans** | Basit, yorumlanabilir ve metin verilerinde TF-IDF ile genellikle güçlü bir başlangıç performansı sunar. |
| **Ayrışabilirlik** | Sahte ve gerçek haber uzayının doğrusal olarak makul ayrılabildiği gözlemlendi (hızlı prototiplerle test edildi). |
| **Hız & Kaynak Tüketimi** | Eğitim ve tahmin süresi düşüktür; Kaggle/CI ortamlarında bellek dostudur. |
| **Şeffaflık** | Katsayılar özellik önemini verir; hangi kelimelerin sınıfa etkili olduğunu açıklamak kolaydır. |

> Diğer modeller (SVM, KNN, Decision Tree) denendi; ancak Logistic Regression hem **benzer doğruluk** sağladı hem de **daha düşük bellek/zaman** gereksinimi ile raporlanabilirliği yüksek tuttu.

##  Nihai Sonuçlar (Test Kümesi)
| **Accuracy** | **0.83** |
| **Precision** | 0.84 |
| **Recall** | 0.82 |
| **F1-Score** | 0.83 |
| **Cross-Val (5-Fold)** | 0.82 ± 0.01 |

> `C = 1` değeri, GridSearchCV ile en tutarlı sonucu verdi.

##  Gerçek Dünya Faydaları
* **Haber Ajansları:** Otomatik ön-filtreleme ile editör yükünü azaltır.  
* **Sosyal Medya Platformları:** Şüpheli içerikleri bayraklayarak yanlış bilgilendirmeyi azaltır.  
* **Kurumsal İtibar Yönetimi:** Marka hakkındaki sahte haberleri erken tespit eder.

##  Proje Nasıl Geliştirilebilir?
1. **Dil Modeli Tabanlı Özellikler**  
   - BERT, RoBERTa gibi transformer tabanlı gömüler eklenerek doğruluk arttırılabilir.  
2. **Ensemble Yaklaşımlar**  
   - Lojistik Regresyon + Gradient Boosting gibi yöntemlerle oy-birliği veya ağırlıklı ortalama yapılabilir.  
3. **Metadata Kullanımı**  
   - Kaynak, tarih, yazar bilgileri gibi ek sütunlar modele dâhil edilebilir.  
4. **Veri Artırma & Çapraz Kaynak Toplama**  
   - Farklı dillerde veya platformlardan veri seti birleştirilerek genelleme kabiliyeti genişletilebilir.  
5. **Model Explainability**  
   - LIME / SHAP ile kelime-bazlı etki görselleştirilebilir; editörlere içgörü sağlar.

Kaggle'daki Notebook Linki: https://www.kaggle.com/code/zeynepnergizkanat/ml-akbnk
