# Install matplotlib kalau belum terinstall
# !pip install matplotlib

import numpy as np
import matplotlib.pyplot as plt

# Fungsi Membership Segitiga
def triangular(x, a, b, c):
    return np.maximum(np.minimum((x - a) / (b - a), (c - x) / (c - b)), 0)

# Fungsi Membership Trapesium
def trapezoidal(x, a, b, c, d):
    return np.maximum(np.minimum(np.minimum((x - a) / (b - a), 1), (d - x) / (d - c)), 0)

# Range data untuk plotting
x_berat = np.linspace(2, 9, 100)
x_tinggi = np.linspace(45, 75, 100)
x_kesehatan = np.linspace(0, 7, 100)

# Berat Badan
berat_rendah = triangular(x_berat, 2, 3, 4)
berat_normal = triangular(x_berat, 3.5, 5, 6.5)
berat_tinggi = triangular(x_berat, 6, 7.5, 9)

# Tinggi Badan
tinggi_pendek = triangular(x_tinggi, 45, 50, 55)
tinggi_normal = triangular(x_tinggi, 52, 60, 68)
tinggi_tinggi = triangular(x_tinggi, 65, 70, 75)

# Kesehatan
kesehatan_tidak_sehat = trapezoidal(x_kesehatan, 0, 0, 2, 4)
kesehatan_sehat = trapezoidal(x_kesehatan, 3, 5, 7, 7)

# Plotting Fungsi Keanggotaan Berat Badan
plt.figure(figsize=(10, 6))
plt.plot(x_berat, berat_rendah, label='Rendah')
plt.plot(x_berat, berat_normal, label='Normal')
plt.plot(x_berat, berat_tinggi, label='Tinggi')
plt.title('Fungsi Keanggotaan Berat Badan')
plt.xlabel('Berat Badan (kg)')
plt.ylabel('Derajat Keanggotaan')
plt.legend()
plt.grid(True)
plt.show()

# Plotting Fungsi Keanggotaan Tinggi Badan
plt.figure(figsize=(10, 6))
plt.plot(x_tinggi, tinggi_pendek, label='Pendek')
plt.plot(x_tinggi, tinggi_normal, label='Normal')
plt.plot(x_tinggi, tinggi_tinggi, label='Tinggi')
plt.title('Fungsi Keanggotaan Tinggi Badan')
plt.xlabel('Tinggi Badan (cm)')
plt.ylabel('Derajat Keanggotaan')
plt.legend()
plt.grid(True)
plt.show()

# Plotting Fungsi Keanggotaan Kesehatan
plt.figure(figsize=(10, 6))
plt.plot(x_kesehatan, kesehatan_tidak_sehat, label='Tidak Sehat')
plt.plot(x_kesehatan, kesehatan_sehat, label='Sehat')
plt.title('Fungsi Keanggotaan Kesehatan')
plt.xlabel('Skor Kesehatan')
plt.ylabel('Derajat Keanggotaan')
plt.legend()
plt.grid(True)
plt.show()

# -----------------------------------------------
# Menghitung Keanggotaan untuk Berat = 4.2, Tinggi = 56, Kesehatan = 3.5

berat_input = 4.2
tinggi_input = 56
kesehatan_input = 3.5

# Berat Badan
mu_berat_rendah = triangular(berat_input, 2, 3, 4)
mu_berat_normal = triangular(berat_input, 3.5, 5, 6.5)
mu_berat_tinggi = triangular(berat_input, 6, 7.5, 9)

# Tinggi Badan
mu_tinggi_pendek = triangular(tinggi_input, 45, 50, 55)
mu_tinggi_normal = triangular(tinggi_input, 52, 60, 68)
mu_tinggi_tinggi = triangular(tinggi_input, 65, 70, 75)

# Kesehatan
mu_kesehatan_tidak_sehat = trapezoidal(kesehatan_input, 0, 0, 2, 4)
mu_kesehatan_sehat = trapezoidal(kesehatan_input, 3, 5, 7, 7)

# Print hasil keanggotaan
print("=== Nilai Keanggotaan ===")
print(f"Berat Badan (4.2 kg): Rendah={mu_berat_rendah:.3f}, Normal={mu_berat_normal:.3f}, Tinggi={mu_berat_tinggi:.3f}")
print(f"Tinggi Badan (56 cm): Pendek={mu_tinggi_pendek:.3f}, Normal={mu_tinggi_normal:.3f}, Tinggi={mu_tinggi_tinggi:.3f}")
print(f"Kesehatan (3.5): Tidak Sehat={mu_kesehatan_tidak_sehat:.3f}, Sehat={mu_kesehatan_sehat:.3f}")

# -----------------------------------------------
# Aturan Fuzzy

print("\n=== Evaluasi Aturan Fuzzy ===")

# R1: Jika Berat Badan Rendah dan Tinggi Pendek dan Kesehatan Tidak Sehat, maka Kurang Gizi
r1 = min(mu_berat_rendah, mu_tinggi_pendek, mu_kesehatan_tidak_sehat)
print(f"Rule 1 (Kurang Gizi): {r1:.3f}")

# R2: Jika Berat Badan Normal dan Tinggi Normal dan Kesehatan Sehat, maka Normal
r2 = min(mu_berat_normal, mu_tinggi_normal, mu_kesehatan_sehat)
print(f"Rule 2 (Normal): {r2:.3f}")

# R3: Jika Berat Badan Tinggi dan Tinggi Tinggi dan Kesehatan Sehat, maka Gizi Lebih
r3 = min(mu_berat_tinggi, mu_tinggi_tinggi, mu_kesehatan_sehat)
print(f"Rule 3 (Gizi Lebih): {r3:.3f}")
