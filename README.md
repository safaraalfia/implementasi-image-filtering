# Implementasi-Image-Filtering
Alfia Rohmah Safara (23422039)

```python
import numpy as np 
from PIL import Image 
 
# Membaca gambar input 
image_path = "/content/sample_data/1234.jpeg"  # Ganti dengan path gambar Anda 
input_image = Image.open(image_path).convert("L")  # Konversi ke skala abu-abu 
X = np.array(input_image) 
 
# Mengatur ukuran filter 
lebar_filter = 3  # Contoh lebar filter 
tinggi_filter = 3  # Contoh tinggi filter 
 
# Inisialisasi filter (H) sebagai matriks 2D (contoh filter sederhana) 
H = np.array([[1, 0, -1], 
              [1, 0, -1], 
              [1, 0, -1]])  # Contoh filter deteksi tepi (Sobel horizontal) 
 
# Menentukan ukuran gambar 
lebar_gambar, tinggi_gambar = X.shape 
 
# Inisialisasi gambar output (Y) dengan ukuran yang sama seperti X 
Y = np.zeros((lebar_gambar, tinggi_gambar)) 
 
# Menerapkan filter pada gambar 
for x in range(lebar_gambar - lebar_filter + 1): 
    for y in range(tinggi_gambar - tinggi_filter + 1): 
        intensity = 0  # Menginisialisasi intensitas baru untuk piksel 
        for k1 in range(lebar_filter): 
            for k2 in range(tinggi_filter): 
                intensity += H[k1, k2] * X[x + k1, y + k2] 
        Y[x, y] = intensity 
 
# Normalisasi nilai output agar berada di rentang 0-255 
Y = np.clip(Y, 0, 255) 
 
# Mengubah matriks output menjadi gambar dan menyimpannya 
output_image = Image.fromarray(Y.astype(np.uint8)) 
output_image.save("output_image.jpeg")  # Menyimpan gambar output 
output_image.show()  # Menampilkan gambar output
