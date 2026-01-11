# Project UAS Pengantar Pemrograman

Proyek ini dibuat untuk memenuhi tugas Ujian Akhir Semester pada mata kuliah Bahasa Pemrograman. Program ini merupakan aplikasi manajemen data sederhana yang dibangun dengan konsep **Object-Oriented Programming (OOP)** dan struktur **Modular**[cite: 4].

## Struktur File
Program dibagi menjadi beberapa modul untuk memenuhi syarat arsitektur modular:
1. `data.py`: Berisi Class Data untuk menyimpan struktur list/database[cite: 4].
2. `process.py`: Berisi Class Process untuk logika validasi dan pengolahan data.
3. `view.py`: Berisi Class View untuk menangani input user dan tampilan tabel.
4. `main.py`: File utama untuk menjalankan program.

## pemerograman Python

```py
# data.py

class Mahasiswa:
    def __init__(self, nama, nim, kelas):
        self.nama = nama
        self.nim = nim
        self.kelas = kelas

class DaftarMahasiswa:
    def __init__(self):
        self.daftar = []

    def tambah(self, mahasiswa):
        self.daftar.append(mahasiswa)
```
```py
# process.py

from data import Mahasiswa, DaftarMahasiswa

class ProsesMahasiswa:
    def __init__(self):
        self.repo = DaftarMahasiswa()

    def validasi_dan_simpan(self, nama, nim, kelas):
        try:
            # Validasi sederhana: memastikan semua field diisi
            if not nama or not nim or not kelas:
                raise ValueError("Semua data (Nama, NIM, Kelas) wajib diisi!")
            
            # Validasi panjang NIM (contoh minimal 8 karakter)
            if len(nim) < 5:
                raise ValueError("NIM terlalu pendek, periksa kembali.")

            # Jika lolos validasi, buat objek Mahasiswa dan simpan
            baru = Mahasiswa(nama, nim, kelas)
            self.repo.tambah(baru)
            return True, "Data berhasil disimpan."
        
        except ValueError as e:
            return False, str(e)
```
```py
# view.py
class TampilanMahasiswa:
    def form_input(self):
        print("\n--- Form Input Mahasiswa ---")
        nama = input("Nama Lengkap : ")
        nim = input("NIM          : ")
        kelas = input("Kelas (Contoh TI.25.C4): ")
        return nama, nim, kelas

    def tampilkan_tabel(self, data_mahasiswa):
        print("\n" + "="*55)
        print(f"{'No':<4} | {'NIM':<12} | {'Nama':<20} | {'Kelas':<10}")
        print("-" * 55)
        
        if not data_mahasiswa:
            print(f"{'TIDAK ADA DATA':^55}")
        else:
            for i, mhs in enumerate(data_mahasiswa, 1):
                print(f"{i:<4} | {mhs.nim:<12} | {mhs.nama:<20} | {mhs.kelas:<10}")
        
        print("="*55 + "\n")
```
```py
# main.py

from process import ProsesMahasiswa
from view import TampilanMahasiswa

def main():
    proses = ProsesMahasiswa()
    tampilan = TampilanMahasiswa()

    while True:
        print("PILIHAN MENU")
        print("1. Tambah Data")
        print("2. Lihat Data")
        print("3. Keluar")
        
        pilihan = input("Pilih menu (1/2/3): ")

        if pilihan == '1':
            nama, nim, kelas = tampilan.form_input()
            sukses, pesan = proses.validasi_dan_simpan(nama, nim, kelas)
            print(f"Status: {pesan}")
            
        elif pilihan == '2':
            tampilan.tampilkan_tabel(proses.repo.daftar)
            
        elif pilihan == '3':
            print("Program selesai. Terima kasih!")
            break
        else:
            print("Pilihan tidak valid!")

if __name__ == "__main__":
    main()

```
## penjelasan pemerograman 
1. Class Data (data.py)

Bagian ini bertanggung jawab penuh atas struktur data program.

Tujuan: Menentukan bagaimana data mahasiswa (Nama, NIM, Kelas) disimpan dalam sebuah objek.

Fungsi: Memisahkan penyimpanan data dari logika lainnya agar struktur data bersifat mandiri dan mudah dikelola.

3. Class Process (process.py)

Bagian ini berisi logika bisnis dan aturan jalannya program.

Tujuan: Mengolah data yang masuk dan melakukan validasi.

Validasi (Exception Handling): Menggunakan blok try-except untuk memastikan input pengguna tidak kosong dan sesuai format sebelum disimpan ke dalam sistem.

4. Class View (view.py)

Bagian ini berinteraksi langsung dengan pengguna.

Input: Meminta input dari pengguna secara interaktif (Nama, NIM, Kelas).

Output: Menampilkan data yang telah tersimpan dalam bentuk tabel yang rapi agar mudah dibaca oleh pengguna.

5. Main Program (main.py)

Ini adalah pengontrol utama atau entry point dari aplikasi.

Tujuan: Menghubungkan ketiga komponen (Data, View, dan Process) menjadi satu alur kerja.

Fungsi: Menjalankan perulangan menu (looping) sehingga pengguna dapat terus menambah atau melihat data sampai memilih untuk keluar.

## Output pemerograman python
