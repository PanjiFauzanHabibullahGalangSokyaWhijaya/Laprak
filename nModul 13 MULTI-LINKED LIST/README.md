 # <h1 align="center">Laporan Praktikum Modul 13 <br> Multi-Linked List</h1>
<p align="center">PANJI FAUZAN HABIBULLAH GALANG SOKYA WHIJAYA - 103112430162</p>

## Dasar Teori

Multi-linked list adalah jenis daftar khusus yang memiliki dua atau lebih urutan kunci logis. Sebelum memahami multi-linked list lebih jauh, mari lihat kembali apa itu linked list. Linked list adalah struktur data yang tidak memiliki batasan ukuran selama memori heap masih tersedia. Kita telah mengenal berbagai jenis linked list seperti Singly Linked List dan Doubly Linked List. Di sini kita akan mempelajari tentang multi-linked list.

Dalam multi-linked list, setiap node dapat memiliki N buah pointer yang mengarah ke node-node lain. Multi-linked list umumnya digunakan untuk mengatur beberapa urutan dari satu kumpulan elemen.

Properti dari Multi-Linked List:

Berikut adalah properti dari multi-linked list:

- Merupakan daftar terintegrasi dari struktur-struktur yang saling berkaitan.
- Semua node saling terhubung menggunakan link berupa pointer.
- Node-node yang terhubung memiliki data yang saling terkait.
- Node mengandung pointer yang menghubungkan satu struktur ke struktur lainnya.

Struktur Multi-Linked List:

Struktur multi-linked list bergantung pada struktur node-nya. Secara umum, satu node biasanya berisi dua komponen utama:
- Daftar pointer
- Semua data yang relevan

## Guided

### soal 1
anak.cpp

```go
#include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }

    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else 
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
        cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;

    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");

    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");

    printAll(list);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{0C03C0FB-55BF-4BA1-B3F6-3F1DD037CBAF}.png)

Program ini membentuk multilist. Tiap parent node punya daftar child node sendiri.
- ParentNode dan ChildNode adalah struktur linked list.
- insertParent() menambah parent baru ke akhir list.
- insertChild() mencari parent berdasarkan nama lalu menambah child ke daftar anaknya.
- printAll() menampilkan seluruh parent beserta anak-anaknya.

## Unguided

### Soal 1

Perhatikan program 46 multilist.h, buat multilist.cpp untuk implementasi semua fungsi pada
multilist.h. Buat main.cpp untuk pemanggilan fungsi-fungsi tersebut.

```go
#include <iostream>
using namespace std;

int main()
{
    double a,b,j,kr,kl,bg;

    cout<<"Input 2 bilangan: ";
    cin>>a;
    cin>>b;
    j=a+b;
    kr=a-b;
    kl=a*b;
    bg=a/b;
    
    cout<<"Penjumlahan="<<j<<"\nPengurangan="<<kr<<"\nPerkalian="<<kl<<"\nPembagian="<<bg<<endl;
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)

Program ini adalah program aritmatika sederhana yang menghitung hasil penjumlahan, pengurangan, perkalian, dan pembagian. Saya menggunakan double karena double adalah float untuk win64

### Soal 2

Buatlah ADT Multi Linked list sebagai berikut di dalam file “circularlist.h”:
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)
- Terdapat 11 fungsi/prosedur untuk ADT circularlist
  * procedure CreateList( input/output L : List )
  * function alokasi( x : infotype ) → address
  * procedure dealokasi( input/output t P : address )
  * procedure insertFirst( input/output L : List, input P : address )
  * procedure insertAfter( input/output L : List, input Prec : address, P : address)
  * procedure insertLast( input/output L : List, input P : address )
  * procedure deleteFirst( input/output L : List, input/output P : address )
  * procedure deleteAfter( input/output L : List, input Prec : address, input/output t P : address )
  * procedure deleteLast( input/output L : List, P : address )
  * function findElm( L : List, x : infotype ) → address
  * procedure printInfo( input L : List )
 
Keterangan :
- fungsi findElm mencari elemen di dalam list L berdasarkan nim
  * fungsi mengembalikan elemen dengan dengan info nim == x.nim jika ditemukan
  * fungsi mengembalikan NIL jika tidak ditemukan
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)
Buatlah implementasi ADT Doubly Linked list pada file “circularlist.cpp”. Tambahkan fungsi/prosedur
berikut pada file “main.cpp”.
- fungsi create ( in nama, nim : string, jenis_kelamin : char, ipk : float)
  * fungsi disediakan, ketik ulang code yang diberikan
  * fungsi mengalokasikan sebuah elemen list dengan info sesuai input
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)
Cobalah hasil implementasi ADT pada file “main.cpp”
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)

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

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)
2. https://www.geeksforgeeks.org/dsa/introduction-to-multi-linked-list/
