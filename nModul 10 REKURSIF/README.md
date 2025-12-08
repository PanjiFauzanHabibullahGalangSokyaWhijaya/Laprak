 # <h1 align="center">Laporan Praktikum Modul 10 <br> Rekursif</h1>
<p align="center">PANJI FAUZAN HABIBULLAH GALANG SOKYA WHIJAYA - 103112430162</p>

## Dasar Teori

Rekursi
Rekursi adalah teknik membuat suatu fungsi memanggil dirinya sendiri.
Rekurensi berlanjut bekerja hingga beberapa kondisi terpenuhi.
Untuk mencegah rekursi tak terbatas, pernyataan if...else (atau pendekatan serupa) dapat digunakan di mana satu cabang membuat panggilan rekursif dan yang lainnya tidak.

Rekursif menyediakan cara untuk memecah masalah rumit menjadi masalah sederhana yang lebih mudah dipecahkan.

Rekursi mungkin agak sulit dipahami. Cara terbaik untuk memahami cara kerjanya adalah dengan bereksperimen.

Keuntungan Rekursi C++
- Itu membuat kode kita lebih pendek dan bersih.
- Rekursi diperlukan dalam permasalahan yang berkaitan dengan struktur data dan algoritma tingkat lanjut, seperti Penelusuran Grafik dan Pohon.

Kekurangan Rekursi C++
- Dibutuhkan banyak ruang tumpukan dibandingkan dengan program berulang.
- Menggunakan lebih banyak waktu prosesor.
- Mungkin lebih sulit untuk men-debugnya dibandingkan dengan program iteratif yang setara.

## Guided

### soal 1
rekursif(tree).cpp

```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *kiri, *kanan;
};

Node *buatNode(int nilai)
{
    Node *baru = new Node();
    baru->data = nilai;
    baru->kiri = baru->kanan = NULL;
    return baru;
}

Node *insert(Node *root, int nilai)
{
    if (root == NULL)
        return buatNode(nilai);
    
    if (nilai < root->data)
        root->kiri = insert(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = insert(root->kanan, nilai);

    return root;
}

Node *search(Node *root, int nilai)
{
    if (root == NULL || root->data == nilai)
        return root;

    if (nilai < root->data)
        return search(root->kiri, nilai);

    return search(root->kanan, nilai);
}

Node *nilaiTerkecil(Node *node)
{
    Node *current = node;
    while (current && current->kiri != NULL)
        current = current->kiri;

        return current;
}

Node *hapus(Node *root, int nilai)
{
    if (root == NULL)
        return root;

    if (nilai < root->data)
        root->kiri = hapus(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = hapus(root->kanan, nilai);
    else
    {
        if (root->kiri == NULL)
        {
            Node *temp = root->kanan;
            delete root;
            return temp;
        }
        else if (root->kanan == NULL){
            Node *temp = root->kiri;
            delete root;
            return temp;
        }
        Node *temp = nilaiTerkecil(root->kanan);
        root->data = temp->data;
        root->kanan = hapus(root->kanan, temp->data);
    }
    return root;
}

Node *update(Node *root, int Lama, int baru)
{
    if (search(root, Lama) != NULL)
    {
        root = hapus(root, Lama);
        root = insert(root, baru);
        cout << "Data " << Lama << " diupdate menjadi " << baru << endl;
    }
    else
    {
        cout << "Data " << Lama << " tidak ditemukan!" << endl;
    }
    return root;
}

void preOrder(Node *root)
{
    if (root != NULL)
    {
        cout << root->data << " ";
        preOrder(root->kiri);
        preOrder(root->kanan);
    }
}

void inOrder(Node *root)
{
    if (root != NULL)
    {
        inOrder(root->kiri);
        cout << root->data << " ";
        inOrder(root->kanan);
    }
}

void postOrder(Node *root)
{
    if (root != NULL)
    {
        postOrder(root->kiri);
        postOrder(root->kanan);
        cout << root->data << " ";
    }
}

int main()
{
    Node *root = NULL;

    cout << "=== 1. INSERT DATA ===" << endl;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 20);
    insert(root, 3);
    insert(root, 7);
    insert(root, 15);
    insert(root, 25);
    cout << "Data berhasil dimasukan.\n" << endl;

    cout << "=== 2. TAMPILKAN TREE (TRAVELSAL) ===" << endl;
    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "=== 3. TEST SEARCH ===" << endl;
    int cari1 = 7, cari2 = 99;
    cout << "Cari " << cari1 << ": " << (search(root,cari1) ? "Ketemu" : "Tidak Aada") << endl;
    cout << "Cari " << cari2 << ": " << (search(root,cari2) ? "Ketemu" : "Tidak Aada") << endl;
    cout << endl;

    cout << "=== 4. TEST UPDATE ===" << endl;
    root = update(root, 5, 8);
    cout << "Hasil Order setelah update: ";
    cout << endl;
    cout << endl;

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "== 5. TEST DELETE ===" << endl;
    cout << "Menghapus angka 20..." << endl;
    root = hapus(root, 20);

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{07EF7F73-691B-49EB-88BA-1B3D819961C6}.png)

Program ini membuat Binary Search Tree (BST) dengan fitur:
- Insert digunakan untuk menambah data sesuai aturan BST (kiri lebih kecil, kanan lebih besar).
- Search digunakan untuk mencari nilai di tree.
- Delete digunakan untuk menghapus node (tanpa anak, satu anak, atau dua anak).
- Update digunakan untuk menghapus nilai lama lalu memasukkan nilai baru.
- Traversal digunakan untuk menampilkan tree dengan PreOrder, InOrder, dan PostOrder.

Program melakukan semua operasi tersebut di fungsi main() untuk demonstrasi.

## Unguided

### Soal 1

Buatlah ADT Binary Search Tree menggunakan Linked list sebagai berikut di dalam file
“bstree.h”:
> ![Screenshot bagian x](output/{73FAE1E6-CB1A-4C32-ACA0-120CF31918BC}.png)

Buatlah implementasi ADT Binary Search Tree pada file “bstree.cpp” dan cobalah hasil
implementasi ADT pada file “main.cpp”
> ![Screenshot bagian x](output/{CD05BF11-4C5D-4050-A0E5-DB93F0D17E40}.png)

bstree.cpp, bstree.h, main.cpp
```go
#include <iostream>
#include "bstree.h"
using namespace std;

address alokasi(infotype x) {
    address p = new Node;
    p->info = x;
    p->left = NULL;
    p->right = NULL;
    return p;
}

void insertNode(address &root, infotype x) {
    if (root == NULL) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
}

address findNode(infotype x, address root) {
    if (root == NULL) {
        return NULL;
    } else if (x == root->info) {
        return root;
    } else if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void printInOrder(address root) {
    if (root != NULL) {
        printInOrder(root->left);
        cout << root->info << " - ";
        printInOrder(root->right);
    }
}
```
```go
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

typedef int infotype;

typedef struct Node *address;

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void printInOrder(address root);

#endif
```
```go
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    cout << "Hello world!\n";

    address root = NULL;

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);

    printInOrder(root);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{1536EEC3-857E-480F-A92A-AC832555583C}.png)

- bstree.h berisi struktur Node (info, left, right) dan deklarasi fungsi BST, seperti alokasi, insertNode, findNode, printInOrder.
- bstree.cpp berisi implementasi fungsi BST:
  * alokasi: buat node baru.
  * insertNode: masukkan angka ke BST (kiri lebih kecil, kanan lebih besar, duplikat diabaikan).
  * findNode: mencari nilai.
  * printInOrder: menampilkan isi tree secara urut (Left–Root–Right).
 
Program melakukan semua operasi tersebut di fungsi main() untuk demonstrasi.

### Soal 2

Buatlah fungsi untuk menghitung jumlah node dengan fungsi berikut.
- fungsi hitungJumlahNode( root:address ) : integer

  /* fungsi mengembalikan integer banyak node yang ada di dalam BST*/
- fungsi hitungTotalInfo( root:address, start:integer ) : integer

  /* fungsi mengembalikan jumlah (total) info dari node-node yang ada di dalam BST*/
- fungsi hitungKedalaman( root:address, start:integer ) : integer

  /* fungsi rekursif mengembalikan integer kedalaman maksimal dari binary tree */
> ![Screenshot bagian x](output/{7C3AD20F-063B-45E8-B0D3-8747099E86D7}.png)

bstree.cpp, bstree.h, main.cpp
```go
#include <iostream>
#include "bstree.h"
using namespace std;

address alokasi(infotype x) {
    address p = new Node;
    p->info = x;
    p->left = NULL;
    p->right = NULL;
    return p;
}

void insertNode(address &root, infotype x) {
    if (root == NULL) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
}

address findNode(infotype x, address root) {
    if (root == NULL) {
        return NULL;
    } else if (x == root->info) {
        return root;
    } else if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void printInOrder(address root) {
    if (root != NULL) {
        printInOrder(root->left);
        cout << root->info << " - ";
        printInOrder(root->right);
    }
}

int hitungJumlahNode(address root) {
    if (root == nullptr)
        return 0;
    return 1 + hitungJumlahNode(root->left) + hitungJumlahNode(root->right);
}

int hitungTotalInfo(address root) {
    if (root == nullptr)
        return 0;
    return root->info + hitungTotalInfo(root->left) + hitungTotalInfo(root->right);
}

int hitungKedalaman(address root, int start) {
    if (root == nullptr)
        return start;
    int leftDepth  = hitungKedalaman(root->left,  start + 1);
    int rightDepth = hitungKedalaman(root->right, start + 1);
    return max(leftDepth, rightDepth);
}
```
```go
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

typedef int infotype;

typedef struct Node *address;

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void printInOrder(address root);
int hitungJumlahNode(address root);
int hitungTotalInfo(address root);
int hitungKedalaman(address root, int start);

#endif
```
```go
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    address root = NULL;

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);

    printInOrder(root);
    cout << endl;
    cout << "kedalaman : " << hitungKedalaman(root, 0) << endl;
    cout << "jumlah Node : " << hitungJumlahNode(root) << endl;
    cout << "total : " << hitungTotalInfo(root) << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{F7D1B7AA-F09B-473A-8C63-8C869EEFF063}.png)

Program ini berisi:
- bstree.h berisi deklarasi: 
  * Node menyimpan nilai (info) serta pointer left dan right.
  * alokasi() untuk membuat node baru.
  * insertNode() untuk memasukkan data ke BST.
  * findNode() untuk mencari data.
  * printInOrder() mencetak tree secara in-order.
  * hitungJumlahNode() untuk menghitung total node.
  * hitungTotalInfo() untuk menjumlahkan seluruh nilai info.
  * hitungKedalaman() untuk mencari kedalaman maksimum tree.
 
- bstree.cpp mengisi implementasi fungsi BST:
  * alokasi(x) akan membuat node baru.
  * insertNode(root, x) memasukkan data ke BST (kiri jika lebih kecil, kanan jika lebih besar).
  * findNode(x, root) untuk mencari node.
  * printInOrder(root) mencetak tree secara terurut (kiri–root–kanan).
  * hitungJumlahNode(root) untuk menghitung total node.
  * hitungTotalInfo(root) untuk menjumlahkan seluruh nilai / info node.
  * hitungKedalaman(root, start) untuk menghitung kedalaman maksimum tree.
 
- main.cpp
  * Membuat BST
  * Memasukkan data (1,2,6,4,5,3,6,7) (Catatan: nilai 6 dimasukkan dua kali tetapi BST tidak menerima duplikat.)
  * Menampilkan hasil in-order
  * Menampilkan:
    - Kedalaman tree
    - Total node
    - Total penjumlahan nilai

### Soal 3

Print tree secara pre-order dan post-order.
> ![Screenshot bagian x](output/{F626FCED-9EB9-4D1E-8A7F-21D9194D1611}.png)

```go
#include <iostream>
using namespace std;

typedef int infotype;
typedef struct Node *address;

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x) {
    address p = new Node;
    p->info = x;
    p->left = NULL;
    p->right = NULL;
    return p;
}

void insertNode(address &root, infotype x) {
    if (root == NULL) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
}

void InOrder(address root) {
    if (root != NULL) {
        InOrder(root->left);
        cout << root->info << " - ";
        InOrder(root->right);
    }
}

void PreOrder(Node *root) {
    if (root != NULL) {
        cout << root->info << " - ";
        PreOrder(root->left);
        PreOrder(root->right);
    }
}

void PostOrder(Node *root) {
    if (root != NULL) {
        PostOrder(root->left);
        PostOrder(root->right);
        cout << root->info << " - ";
    }
}

int main() {
    address root = NULL;

    insertNode(root, 6);
    insertNode(root, 4); 
    insertNode(root, 7); 
    insertNode(root, 2); 
    insertNode(root, 5); 
    insertNode(root, 1); 
    insertNode(root, 3); 

    cout << "PreOrder  : ";
    PreOrder(root);
    cout << endl;
    cout << "InOrder   : ";
    InOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    PostOrder(root);
    cout << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{78A35B0E-8CB4-4DF5-A70B-D94521A279D9}.png)

Program ini membuat Binary Search Tree (BST) dengan operasi dasar:
- Node menyimpan info, left, dan right.
- insertNode() memasukkan data secara rekursif sesuai aturan BST.
- InOrder, PreOrder, PostOrder menampilkan tree dalam tiga jenis traversal.
Pada main(), program menampilkan traversal PreOrder, InOrder, dan PostOrder.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)
2. https://www.programiz.com/cpp-programming/recursion
3. https://www.w3schools.com/cpp/cpp_functions_recursion.asp
