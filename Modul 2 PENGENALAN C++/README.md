 # <h1 align="center">Laporan Praktikum Modul 2 <br> Pengenalan C++</h1>
<p align="center">PANJI FAUZAN HABIBULLAH GALANG SOKYA WHIJAYA - 103112430162</p>

## Dasar Teori

Struktur data digunakan untuk menyimpan dan mengatur data agar mudah diakses dan dikelola. Salah satu contohnya adalah **array**, yang memungkinkan penyimpanan beberapa nilai dalam satu variabel dengan tipe data yang sama. Array dideklarasikan dengan menentukan tipe data, nama array, serta jumlah elemen yang akan disimpan.

Selain array, C++ juga memiliki **pointer**, yaitu variabel khusus yang menyimpan alamat memori dari variabel lain, bukan nilainya langsung. Pointer memungkinkan program mengakses dan memanipulasi data di memori secara efisien, sehingga sangat penting untuk pemrograman tingkat sistem dan manajemen memori dinamis.

## Guided

### soal 1
07_call_by_pointer.cpp

```go
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(&a, &b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int *px, int *py)
{
    int temp = *px;
    *px = *py;
    *py = temp;
}
```

> Output
> ![Screenshot bagian x](output/{8BC353BF-E69D-46BE-9E9A-6554CE2A0E7F}.png)

Program ini digunakan untuk menukar nilai dua variabel (a dan b) menggunakan pointer. Program ini menunjukkan cara kerja pointer dalam fungsi untuk mengubah nilai variabel di luar fungsi. Tanpa pointer, nilai variabel a dan b di fungsi main tidak akan berubah karena C++ menggunakan pass-by-value secara default.

### soal 2
08_call_by_reference.cpp

```go
#include <iostream>
using namespace std;

void tukar(int &x, int &y); 

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(a, b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}
```

> Output
> ![Screenshot bagian x](output/{8BC353BF-E69D-46BE-9E9A-6554CE2A0E7F}.png)

Program ini digunakan untuk menukar nilai dua variabel (a dan b) menggunakan referensi (reference). Program ini menggunakan pass by reference agar fungsi dapat mengubah nilai variabel asli tanpa pointer.

## Unguided

### Soal 1

1. Buatlah sebuah program untuk melakukan transpose pada sebuah matriks persegi berukuran 3x3. Operasi transpose adalah mengubah baris menjadi kolom dan sebaliknya. Inisialisasi matriks awal di dalam kode, kemudian buat logika untuk melakukan transpose dan simpan hasilnya ke dalam matriks baru. Terakhir, tampilkan matriks awal dan matriks hasil transpose.

```go
#include <iostream>
using namespace std;

int main()
{

    int matriks[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int transpose[3][3]; 

    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            transpose[j][i] = matriks[i][j];
        }
    }

    cout << "Matriks Awal:\n";
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
    }

    cout << "\nMatriks Hasil Transpose:\n";
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            cout << transpose[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)

Program ini adalah program aritmatika sederhana yang menghitung hasil penjumlahan, pengurangan, perkalian, dan pembagian. Saya menggunakan double karena double adalah float untuk win64

### Soal 2

Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-input-kan user adalah bilangan bulat positif mulai dari 0 s.d 100
contoh:
79: tujuh puluh Sembilan

```go
#include <iostream>
using namespace std;

string angkaKeTulisan(int n)
{
    string satuan[] = {"", "Satu", "Dua", "Tiga", "Empat", "Lima",
                       "Enam", "Tujuh", "Delapan", "Sembilan"};

    if (n == 0)
        return "Nol";
    else if (n == 10)
        return "Sepuluh";
    else if (n == 11)
        return "Sebelas";
    else if (n == 100)
        return "Seratus";
    else if (n < 10)
        return satuan[n];
    else if (n < 20)
    {
        int belas = n%10;
        string hasil = satuan[belas] + " Belas";
        return hasil;
    }
    else
    {
        int puluh = n / 10;
        int sisa = n % 10;
        string hasil = satuan[puluh] + " Puluh";
        if (sisa > 0)
            hasil += " " + satuan[sisa];
        return hasil;
    }
}

int main()
{
    int angka;
    cout << "Masukkan angka (0-100): ";
    cin >> angka;

    if (angka < 0 || angka > 100)
    {
        cout << "Angka di luar jangkauan!" << endl;
    }
    else
    {
        cout << angka << ": " << angkaKeTulisan(angka) << endl;
    }

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/WhatsAppImage2025-10-07at11.36.09.jpeg)

Program ini mengkonversi angka menjadi latin. Di sini saya menggunakan fungsi dan array

### Soal 3

Buatlah program yang dapat memberikan input dan output sbb.
> ![Screenshot bagian x](output/{F626FCED-9EB9-4D1E-8A7F-21D9194D1611}.png)

```go
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Input: ";
    cin >> n;
    cout << "Output: "<<endl;

    for (int i = n; i >= 1; i--) {

        for (int s = 0; s < (n - i); s++) {
            cout << "  ";
        }
        for (int j = i; j >= 1; j--) {
            cout << j << " ";
        }
        cout << "* ";
        for (int j = 1; j <= i; j++) {
            cout << j << " ";
        }
        cout << endl;
    }

    for (int s = 0; s < n; s++) {
        cout << "  ";
    }
    cout << "*" << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{78A35B0E-8CB4-4DF5-A70B-D94521A279D9}.png)

Program ini menampilkan pola angka simetris dengan bintang di tengahnya, berdasarkan input angka n. Program ini menggeser pola ke kanan setiap baris dengan penambahan spasi. Saya di sini menggunakan nested loop

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)
2. https://learn.microsoft.com/id-id/cpp/cpp/void-cpp?view=msvc-170
3. https://www.duniailkom.com/tutorial-belajar-c-plus-plus-tipe-data-float-dan-double-bahasa-c-plus-plus/
