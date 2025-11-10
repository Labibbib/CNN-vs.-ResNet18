# **CNN vs. ResNet-18 for Image Classification Using CIFAR-10 Dataset**

## 📝 **Deskripsi Singkat**
Proyek ini bertujuan untuk membangun, melatih, dan mengevaluasi dua model Convolutional Neural Network (CNN) untuk tugas klasifikasi gambar menggunakan dataset CIFAR-10. Model pertama adalah CNN yang dirancang khusus (kustom), dan model kedua adalah arsitektur ResNet18 yang telah disesuaikan untuk dataset ini. Kedua model dibandingkan kinerjanya berdasarkan akurasi, presisi, recall, dan F1-score.

## 🔍 **Latar Belakang**
Klasifikasi gambar adalah salah satu tugas fundamental dalam Computer Vision dan Deep Learning. Dataset CIFAR-10 digunakan sebagai benchmark standar untuk tugas ini. Dataset ini terdiri dari 60.000 gambar berwarna ukuran 32x32 yang terbagi dalam 10 kelas (seperti 'airplane', 'automobile', 'bird', 'cat', dll.), dengan 50.000 gambar untuk pelatihan dan 10.000 gambar untuk pengujian.
Tugas ini ditujukan untuk memenuhi persyaratan dalam menyelesaikan UTS mata kuliah Deep Learning.

## 🎯 **Tujuan Proyek**
1. Klasifikasi CIFAR-10: Mengklasifikasikan dataset CIFAR-10 menggunakan model CNN kustom dan model ResNet18 pretrained yang disesuaikan dari modul PyTorch.
2. Hyperparameter Tuning: Melakukan tuning hyperparameter pada model CNN kustom untuk menemukan parameter terbaik guna meningkatkan akurasi, presisi, dan recall.
3. Perbandingan Model: Membandingkan kinerja model CNN kustom dengan model ResNet18 yang telah disesuaikan untuk menentukan model mana yang lebih baik dalam mengklasifikasikan dataset CIFAR-10.

## ⚙️ **Konfigurasi Model**
1. **Persiapan Data**
   - Dataset: CIFAR-10 (50000 data training, 10000 data test).
   - Partisi data: Dataset train dibagi menjadi 90% data training (45000) dan 10% data validasi (5000)
   - Augmentasi & Transformasi:
     - Data train: `RandomCrop(32, padding=4`, `RandomHorizontalFlip()`, dan `Normalize(mean=[0.5,0.5,0.5], std=[0.5,0.5,0.5]`.
     - Data validasi dan test: `Normalize(mean=[0.5,0.5,0.5], std=[0.5,0.5,0.5]`
2. **Model**
   - Model 1: CNN Kustom
     - Arsitektur: Model ini terdiri dari tiga blok konvolusi. Setiap blok berisi `Conv2d`, `BatchNorm2d`, `ReLu`, diikuti dengan lapisan `Pooling` (Max atau Avg). Fitur yang diekstraksi kemudian diratakan (flattened) kemudian di layer terakhir ada dua lapisan Fully Connected (`Linear` dengan `Dropout` untuk klasifikasi akhir.
     - Hyperparameter Tuning: Konfigurasi paramter terbaik setelah pencarian hyperparameter adalah
       - Filter konvolusi: (128, 256, 512)
       - Neuron FC (Fully Conected): 512
       - Dropout: 0.5
       - Batch Size: 64
       - Optimizer: SGD(momentum=0.9)
       - Learning Rate: 0.01
       - Weight Decay: 5e-4
   - Model 2: ResNet-18
     - Arsitektur: Menggunakan arsitektur ResNet18 dari `torchvision.models` yang idmodifikasi untuk gambar CIFAR-10. `conv1` diubah menjadi kernel $3\times 3$ dengan stride 1, `maxpool` awal diganti dengan `nn.Identity()`, dan lapisan `fc` terakhir diganti agar memiliki 10 output sesuai jumlah kelas CIFAR-10.
     - Setting training:
       - Epochs: 60
       - Optimizer: SGD
       - Learning Rate: 0.1
       - Momentum: 0.9
       - Weight Devay: 5e-4
       - Scheduler: `CosineAnnealingLR`
       - Earling Stopping: patience=15

## 🧮 **Hasil**
| Metrik | CNN Kustom (Best) | ResNet18 (Disesuaikan) |
| ----------- | :---------: | :----------: |
| Akurasi Training | 93.10% | 99.92% |
| Akurasi Validasi | 89.46% | 94.52% |
| **Akurasi Test** | **89.26%** | **94.25%** |
| F1-Score (Test) | 89.28% | 94.25% |

- **Performa CNN Kustom**: Model ini menunjukkan performa baik pada hampir semua kelas, tetapi pada kelas cat performanya lemah dengan Precision: 0.79, Recall: 0.79.
- **Performa ResNet18**: Model ini memiliki performa yang sangat tinggi di semua kelas, berbeda dengan model CNN kustom.

## 📰 **Kesimpulan**
1. Model ResNet18 yang telah disesuaikan secara signifikan menungguli model CNN kustom, dengan mencapai akurasi tes 94.25% dibandingkan 89.26% dari CNN Kustom. Tetapi model ResNet18 menunjukkan adanya indikasi overfitting.
2. Arsitektur ResNet18 yang lebih dalam dan penggunaan residual blocks terbukti lebih efektif dalam mengekstraksi fitur-fitur kompleks dari dataset CIFAR-10.

## 🙍‍♂️ **Kontributor**
- Alif Alamsyah (11220940000028)
- Ibnullabib (11220940000037)
