 # <h1 align="center">Laporan Praktikum Modul 6 <br> Doubly Linked List</h1>
<p align="center">PANJI FAUZAN HABIBULLAH GALANG SOKYA WHIJAYA - 103112430162</p>

## Dasar Teori

Doubly linked list adalah linked list bidirectional. Jadi, kita bisa melintasinya secara dua arah. Tidak seperti singly linked list, simpul doubly linked list berisi satu pointer tambahan yang disebut previous pointer. Pointer ini menunjuk ke simpul sebelumnya. Saat menambahkan atau menghapus node dalam doubly linked list, dibutuhkan lebih banyak perubahan pointer dibandingkan dengan operasi yang sama pada singly linked list. Namun, operasinya justru lebih sederhana dan berpotensi lebih efisien (terutama untuk node selain node pertama), karena tidak perlu melacak node sebelumnya selama penelusuran atau menelusuri daftar untuk menemukan node sebelumnya agar pointer dapat diubah.

In a data structure, a doubly linked list is represented using nodes that have three fields:
1. Data
2. A pointer to the next node (next)
3. A pointer to the previous node (prev)

## Guided

### soal 1
guided1.cpp

```go
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

void insertDepan(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->prev = nullptr;
    newNode->next = head;

    if (head != nullptr)
       head->prev = newNode;
    else
       tail = newNode;

    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan. \n";
}

void insertBelakang(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    newNode->prev = tail;

    if (tail != nullptr)
        tail->next = newNode;
    else
        head = newNode;

    tail = newNode;
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int data) {
    Node* current = head;
    while (current != nullptr && current ->data != target)
        current = current->next;

    if(current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = current->next;
    newNode->prev = current;

    if (current->next != nullptr)
        current->next->prev = newNode;
    else
        tail = newNode;

    current->next = newNode;
    cout << "Data " << data << " berhasil disisipkan setelah " << target << ".\n";
}

void hapusDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = head;
    head = head->next;

    if (head != nullptr)
        head->prev = nullptr;
    else
        tail = nullptr;

    cout << "Data " << temp->data << " dihapus dari depan.\n";
    delete temp;
}

void hapusBelakang() {
    if  (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = tail;
    tail = tail->prev;

    if (tail != nullptr)
        tail->next = nullptr;
    else
        head = nullptr;
    
    cout << "Data " << temp->data << " dihapus dari belakang.\n";
    delete temp;
}

void hapusData(int target) {
    Node* current = head;
    while (current != nullptr && current->data != target)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    if (current == head)
        hapusDepan();
    else if (current == tail)
        hapusBelakang();
    else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        cout << "Data " << target << " dihapus.\n";
        delete current;
    }
}

void updateData(int oldData, int newData) {
    Node* current = head;
    while (current != nullptr && current->data != oldData)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << oldData << " tidak ditemukan.\n";
        return;
    }

    current->data = newData;
    cout << "Data " << oldData << " diubah menjadi " << newData << ".\n";
}

void tampilDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari depan): ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
    }
    cout << "\n";
}

void tampilBelakang() {
    if (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari belakang): ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->prev;
    }
    cout << "\n";
}

int main(){
    int pilihan, data, target, oldData, newData;

    do {
        cout << "\n===== MENU DOUBLE LINKED LIST =====\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah Data\n";
        cout << "4. Hapus Depan\n";
        cout << "5. Hapus Belakang\n";
        cout << "6. Hapus Data Tertentu\n";
        cout << "7. Update Data\n";
        cout << "8. Tampil dari Depan\n";
        cout << "9. Tampil dari Belakang\n";
        cout << "0. Keluar\n";
        cout << "===================================\n";
        cout << "Pilih menu: ";

        cin >> pilihan;
        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> data;
                insertSetelah(target, data);
                break;
            case 4:
                hapusDepan();
                break;
            case 5:
                hapusBelakang();
                break;
            case 6:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> target;
                hapusData(target);
                break;
            case 7:
                cout << "Masukkan data lama: ";
                cin >> oldData;
                cout << "Masukkan data baru: ";
                cin >> newData;
                updateData(oldData, newData);
                break;
            case 8:
                tampilDepan();
                break;
            case 9:
                tampilBelakang();
                break;
            case 0:
                cout << "Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
                break;
        }

    } while (pilihan != 0);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/1.png)

Program ini membuat double linked list yang bisa menambah, menghapus, mengubah, dan menampilkan data dari depan atau belakang.
Setiap node menyimpan data, serta pointer ke node sebelum dan sesudahnya.
Menu utama digunakan untuk menjalankan semua operasi tersebut secara interaktif.
- Struct Node = Menyimpan data, pointer ke node sebelumnya (prev), dan berikutnya (next).
- head & tail = Menunjuk node pertama dan terakhir dari list.
- insertDepan / insertBelakang = Menambah node baru di depan atau belakang list.
- insertSetelah = Menyisipkan node baru setelah data tertentu.
- hapusDepan / hapusBelakang / hapusData = Menghapus node di depan, belakang, atau berdasarkan nilai tertentu.
- updateData = Mengubah nilai data lama menjadi baru.
- tampilDepan / tampilBelakang = Menampilkan isi list dari depan ke belakang atau sebaliknya.
- main() = Menyediakan menu interaktif untuk menjalankan semua operasi di atas.

## Unguided

### Soal 1

Buatlah ADT Doubly Linked list sebagai berikut di dalam file “Doublylist.h”:
> ![Screenshot bagian x](output/2.png)
Buatlah implementasi ADT Doubly Linked list pada file “Doublylist.cpp” dan coba hasil
implementasi ADT pada file “main.cpp”.
> ![Screenshot bagian x](output/3.png)

Doublylist.cpp, Doublylist.h, dan main.cpp
```go
#include "Doublylist.h"
#include <iostream>
using namespace std;

void CreateList(List &L) {
    L.first = nullptr;
    L.last = nullptr;
}

address alokasi(kendaraan x) {
    address P = new ElmList;
    P->info = x;
    P->next = nullptr;
    P->prev = nullptr;
    return P;
}

void dealokasi(address P) {
    delete P;
}

bool cekNopol(const List &L, const string &nopol) {
    address P = L.first;
    while (P != nullptr) {
        if (P->info.nopol == nopol)
            return true;
        P = P->next;
    }
    return false;
}

void insertLast(List &L, address P) {
    if (L.first == nullptr) {
        L.first = L.last = P;
    } else {
        P->next = L.first;
        L.first->prev = P;
        L.first = P;
    }
}

void printInfo(const List &L) {
    if (L.first == nullptr) {
        cout << "\nList kosong.\n";
        return;
    }

    cout << "\nDATA LIST 1\n" << endl;
    address P = L.first;
    while (P != nullptr) {
        cout << "No polisi : " << P->info.nopol << endl;
        cout << "Warna     : " << P->info.warna << endl;
        cout << "Tahun     : " << P->info.thnBuat << endl;
        P = P->next;
    }
}
```
```go
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <string>
using namespace std;

struct kendaraan {
    string nopol;
    string warna;
    int thnBuat;
};

struct ElmList;
typedef ElmList* address;

struct ElmList {
    kendaraan info;
    address next;
    address prev;
};

struct List {
    address first;
    address last;
};

void CreateList(List &L);
address alokasi(kendaraan x);
void dealokasi(address P);
void insertLast(List &L, address P);
void printInfo(const List &L);
bool cekNopol(const List &L, const string &nopol);

#endif
```
```go
#include <iostream>
#include "Doublylist.h"
using namespace std;

int main() {
    List L;
    CreateList(L);
    int pilihan;
    kendaraan k;

    do {
        cout << "\n=== MENU DATA KENDARAAN ===\n";
        cout << "1. Masukkan Data Kendaraan\n";
        cout << "2. Tampilkan Semua Data\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "\nMasukkan Nomor Polisi: ";
                cin >> k.nopol;
                cout << "Masukkan Warna Kendaraan: ";
                cin >> k.warna;
                cout << "Masukkan Tahun Kendaraan: ";
                cin >> k.thnBuat;
                if (cekNopol(L, k.nopol)) {
                    cout << "Nomor polisi sudah terdaftar\n";
                    break;
                }
                insertLast(L, alokasi(k));
                break;
            case 2:
                printInfo(L);
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
                break;
        }

    } while (pilihan != 0);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/4.png)

Program ini:
- Menggunakan doubly linked list untuk menyimpan data kendaraan.
- Dapat menambah dan menampilkan data kendaraan.
- Mencegah duplikasi nomor polisi dengan cekNopol.
- Struktur kodenya rapi dan modular karena dipisah dalam tiga file:
  * Doublylist.h => deklarasi
  * Doublylist.cpp => implementasi
  * main.cpp => menu interaktif
- Menu interaktif memberi tiga opsi:
  * Masukkan Data = Memasukkan data kendaraan baru dengan validasi agar nopol tidak boleh duplikat.
  * Tampilkan Data = Menampilkan seluruh isi list.
  * Keluar = Mengakhiri program.

### Soal 2

Carilah elemen dengan nomor polisi D001 dengan membuat fungsi baru.
fungsi findElm( L : List, x : infotype ) : address
> ![Screenshot bagian x](output/5.png)

Doublylist.cpp, Doublylist.h, dan main.cpp
```go
#include "Doublylist.h"
#include <iostream>
using namespace std;

void CreateList(List &L) {
    L.first = nullptr;
    L.last = nullptr;
}

address alokasi(kendaraan x) {
    address P = new ElmList;
    P->info = x;
    P->next = nullptr;
    P->prev = nullptr;
    return P;
}

void dealokasi(address P) {
    delete P;
}

bool cekNopol(const List &L, const string &nopol) {
    address P = L.first;
    while (P != nullptr) {
        if (P->info.nopol == nopol)
            return true;
        P = P->next;
    }
    return false;
}

address findElm(List L, string nopol) {
    address P = L.first;
    while (P != nullptr) {
        if (P->info.nopol == nopol) {
            return P;  // Ketemu
        }
        P = P->next;
    }
    return nullptr;  // Tidak ditemukan
}

void insertLast(List &L, address P) {
    if (L.first == nullptr) {
        L.first = L.last = P;
    } else {
        P->next = L.first;
        L.first->prev = P;
        L.first = P;
    }
}

void printInfo(const List &L) {
    if (L.first == nullptr) {
        cout << "\nList kosong.\n";
        return;
    }

    cout << "\nDATA LIST 1\n" << endl;
    address P = L.first;
    while (P != nullptr) {
        cout << "No polisi : " << P->info.nopol << endl;
        cout << "Warna     : " << P->info.warna << endl;
        cout << "Tahun     : " << P->info.thnBuat << endl;
        P = P->next;
    }
}
```
```go
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <string>
using namespace std;

struct kendaraan {
    string nopol;
    string warna;
    int thnBuat;
};

struct ElmList;
typedef ElmList* address;

struct ElmList {
    kendaraan info;
    address next;
    address prev;
};

struct List {
    address first;
    address last;
};

void CreateList(List &L);
address alokasi(kendaraan x);
void dealokasi(address P);
void insertLast(List &L, address P);
void printInfo(const List &L);
bool cekNopol(const List &L, const string &nopol);
address findElm(List L, string nopol);

#endif
```
```go
#include <iostream>
#include "Doublylist.h"
using namespace std;

int main() {
    List L;
    CreateList(L);
    int pilihan;
    kendaraan k;

    do {
        cout << "\n=== MENU DATA KENDARAAN ===\n";
        cout << "1. Masukkan Data Kendaraan\n";
        cout << "2. Tampilkan Semua Data\n";
        cout << "3. Cari Data Kendaraan\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "\nMasukkan Nomor Polisi: ";
                cin >> k.nopol;
                cout << "Masukkan Warna Kendaraan: ";
                cin >> k.warna;
                cout << "Masukkan Tahun Kendaraan: ";
                cin >> k.thnBuat;
                if (cekNopol(L, k.nopol)) {
                    cout << "Nomor polisi sudah terdaftar\n";
                    break;
                }
                insertLast(L, alokasi(k));
                break;
            case 2:
                printInfo(L);
                break;
            case 3:
                cout << "\nMasukkan Nomor Polisi yang dicari: ";
                cin >> k.nopol;
                {
                    address hasil = findElm(L, k.nopol);
                    if (hasil != nullptr) {
                        cout << "\nNomor Polisi : " << hasil->info.nopol << endl;
                        cout << "Warna        : " << hasil->info.warna << endl;
                        cout << "Tahun        : " << hasil->info.thnBuat << endl;
                    } else {
                        cout << "Data tidak ditemukan.\n";
                    }
                }
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
                break;
        }

    } while (pilihan != 0);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/6.png)

findElm menelusuri doubly linked list dari awal, membandingkan nopol tiap elemen. Jika ditemukan, mengembalikan alamat elemen tersebut; jika tidak, mengembalikan nullptr. Jika pengguna memasukkan nomor polisi D001, maka program akan menampilkan detail kendaraan seperti di gambar (nopol, warna, dan tahun).

### Soal 3

Hapus elemen dengan nomor polisi D003 dengan procedure delete.
- procedure deleteFirst( input/output L : List,
  P : address )
- procedure deleteLast( input/output L : List,
  P : address )
- procedure deleteAfter( input Prec : address,
  input/output P : address )
> ![Screenshot bagian x](output/7.png)

Doublylist.cpp, Doublylist.h, dan main.cpp
```go
#include "Doublylist.h"
#include <iostream>
using namespace std;

void CreateList(List &L) {
    L.first = nullptr;
    L.last = nullptr;
}

address alokasi(kendaraan x) {
    address P = new ElmList;
    P->info = x;
    P->next = nullptr;
    P->prev = nullptr;
    return P;
}

void dealokasi(address P) {
    delete P;
}

bool cekNopol(const List &L, const string &nopol) {
    address P = L.first;
    while (P != nullptr) {
        if (P->info.nopol == nopol)
            return true;
        P = P->next;
    }
    return false;
}

address findElm(List L, string nopol) {
    address P = L.first;
    while (P != nullptr) {
        if (P->info.nopol == nopol) {
            return P;  // Ketemu
        }
        P = P->next;
    }
    return nullptr;  // Tidak ditemukan
}

void insertLast(List &L, address P) {
    if (L.first == nullptr) {
        L.first = L.last = P;
    } else {
        P->next = L.first;
        L.first->prev = P;
        L.first = P;
    }
}

void printInfo(const List &L) {
    if (L.first == nullptr) {
        cout << "\nList kosong.\n";
        return;
    }

    cout << "\nDATA LIST 1\n" << endl;
    address P = L.first;
    while (P != nullptr) {
        cout << "No polisi : " << P->info.nopol << endl;
        cout << "Warna     : " << P->info.warna << endl;
        cout << "Tahun     : " << P->info.thnBuat << endl;
        P = P->next;
    }
}

void deleteFirst(List &L, address &P) {
    if (L.first == nullptr) {
        P = nullptr;
    } else if (L.first == L.last) {
        P = L.first;
        L.first = L.last = nullptr;
    } else {
        P = L.first;
        L.first = L.first->next;
        L.first->prev = nullptr;
        P->next = nullptr;
    }
}

void deleteLast(List &L, address &P) {
    if (L.first == nullptr) {
        P = nullptr;
    } else if (L.first == L.last) {
        P = L.last;
        L.first = L.last = nullptr;
    } else {
        P = L.last;
        L.last = L.last->prev;
        L.last->next = nullptr;
        P->prev = nullptr;
    }
}

void deleteAfter(address Prec, address &P) {
    if (Prec != nullptr && Prec->next != nullptr) {
        P = Prec->next;
        Prec->next = P->next;
        if (P->next != nullptr)
            P->next->prev = Prec;
        P->next = P->prev = nullptr;
    }
}
```
```go
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <string>
using namespace std;

struct kendaraan {
    string nopol;
    string warna;
    int thnBuat;
};

struct ElmList;
typedef ElmList* address;

struct ElmList {
    kendaraan info;
    address next;
    address prev;
};

struct List {
    address first;
    address last;
};

void CreateList(List &L);
address alokasi(kendaraan x);
void dealokasi(address P);
void insertLast(List &L, address P);
void printInfo(const List &L);
bool cekNopol(const List &L, const string &nopol);
address findElm(List L, string nopol);
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(address Prec, address &P);

#endif
```
```go
#include <iostream>
#include "Doublylist.h"
using namespace std;

int main() {
    List L;
    CreateList(L);
    int pilihan;
    kendaraan k;

    do {
        cout << "\n=== MENU DATA KENDARAAN ===\n";
        cout << "1. Masukkan Data Kendaraan\n";
        cout << "2. Tampilkan Semua Data\n";
        cout << "3. Cari Data Kendaraan\n";
        cout << "4. Hapus Data Kendaraan\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "\nMasukkan Nomor Polisi: ";
                cin >> k.nopol;
                cout << "Masukkan Warna Kendaraan: ";
                cin >> k.warna;
                cout << "Masukkan Tahun Kendaraan: ";
                cin >> k.thnBuat;
                if (cekNopol(L, k.nopol)) {
                    cout << "Nomor polisi sudah terdaftar\n";
                    break;
                }
                insertLast(L, alokasi(k));
                break;
            case 2:
                printInfo(L);
                break;
            case 3:
                cout << "\nMasukkan Nomor Polisi yang dicari: ";
                cin >> k.nopol;
                {
                    address hasil = findElm(L, k.nopol);
                    if (hasil != nullptr) {
                        cout << "\nNomor Polisi : " << hasil->info.nopol << endl;
                        cout << "Warna        : " << hasil->info.warna << endl;
                        cout << "Tahun        : " << hasil->info.thnBuat << endl;
                    } else {
                        cout << "Data tidak ditemukan.\n";
                    }
                }
                break;
            case 4: {
                string hapusNopol;
                cout << "\nMasukkan Nomor Polisi yang akan dihapus: ";
                cin >> hapusNopol;

                address P = findElm(L, hapusNopol);
                if (P == nullptr) {
                    cout << "Data dengan nomor polisi " << hapusNopol << " tidak ditemukan.\n";
                } else {
                    if (P == L.first) {
                        deleteFirst(L, P);
                    } else if (P == L.last) {
                        deleteLast(L, P);
                    } else {
                        deleteAfter(P->prev, P);
                    }
                    dealokasi(P);
                    cout << "Data dengan nomor polisi " << hapusNopol << " berhasil dihapus.\n";
                }
                break;
            }
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
                break;
        }

    } while (pilihan != 0);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/8.png)

- deleteFirst menghapus elemen paling awal.
- deleteLast menghapus elemen paling akhir.
- deleteAfter menghapus elemen di tengah (setelah node tertentu).
  Program mencari node berdasarkan nomor polisi, lalu memanggil prosedur penghapusan yang sesuai dengan posisi node tersebut.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)
2. https://learn.microsoft.com/id-id/cpp/cpp/void-cpp?view=msvc-170
3. https://www.duniailkom.com/tutorial-belajar-c-plus-plus-tipe-data-float-dan-double-bahasa-c-plus-plus/
