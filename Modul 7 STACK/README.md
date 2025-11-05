 # <h1 align="center">Laporan Praktikum Modul 7 <br> Stack</h1>
<p align="center">PANJI FAUZAN HABIBULLAH GALANG SOKYA WHIJAYA - 103112430162</p>

## Dasar Teori

Sebuah stack menyimpan banyak elemen dalam urutan tertentu yang disebut LIFO.

LIFO merupakan singkatan dari Last In, First Out (masuk terakhir, keluar pertama). Untuk memvisualisasikan konsep LIFO, bayangkan setumpuk pancake, di mana pancake ditambahkan dan diambil dari bagian atas tumpukan. Jadi, saat mengambil pancake, yang akan diambil selalu yang terakhir kali ditambahkan. Cara pengorganisasian elemen seperti ini disebut LIFO dalam computer science and programming.

Berbeda dengan vector, elemen dalam stack tidak dapat diakses menggunakan nomor indeks. Karena elemen selalu ditambahkan dan dihapus dari bagian atas, maka hanya elemen paling atas dari stack yang dapat diakses.

Untuk menggunakan stack, Anda harus menyertakan header file stack.

## Guided

### soal 1
guided1.cpp

```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpty(Node *top)
{
    return top == nullptr;
}

void push(Node *&top, int data)
{
    Node *newNode = new Node();
    newNode->data = data;
    newNode->next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpty(top))
    {
        cout << "Stack kosong, tidak bisa di pop!" << endl;
        return 0;
    }

    int poppedData = top->data;
    Node *temp = top;
    top = top->next;

    delete temp;
    return poppedData;
}

void show(Node *top)
{
    if (isEmpty(top))
    {
        cout << "Stack kosong." <<endl;
        return;
    }

    cout << "TOP -> ";
    Node *temp = top;

    while (temp != nullptr)
    {
        cout << temp->data << " -> ";
        temp = temp->next;
    }

    cout << "NULL" << endl;
}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan isi stack:" << endl;
    show(stack);

    cout << "Pop: " << pop(stack) << endl;

    cout << "Menampilkan sisa stack:" << endl;
    show(stack);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{4DA43ED0-6A8D-46FE-81D3-DE2FEA7D5A3C}.png)

Struktur:
- Node berisi data dan pointer next.
- top menunjuk ke elemen paling atas stack.

Fungsi utama:
- isEmpty() = cek apakah stack kosong.
- push() = menambah data ke atas stack.
- pop() = menghapus dan mengembalikan data paling atas.
- show() = menampilkan isi stack dari atas ke bawah.

## Unguided

### Soal 1

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file “stack.h”:
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)
Buatlah implementasi ADT Stack menggunakan Array pada file “stack.cpp” dan “main.cpp”
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)

stack.cpp, stack.h, dan main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!\n";
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) { 
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!\n";
        return -1;
    }
}

void printInfo(Stack S) {
    if (S.top == -1) {
        cout << "Stack kosong.\n";
        return;
    }

    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (S.top != -1) {
        push(temp, pop(S));
    }

    S = temp;
}
```
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif
```
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 8);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);

    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/{E48EADCA-AAAF-42F9-824D-3AAD108DFF77}.png)

Program ini membuat ADT Stack (tumpukan) menggunakan array.
Stack menyimpan data secara LIFO (Last In, First Out), data terakhir yang dimasukkan akan keluar lebih dulu.
- createStack() = menginisialisasi stack agar kosong.
- push() = menambah data ke puncak stack.
- pop() = menghapus data dari puncak stack.
- printInfo() = menampilkan isi stack dari atas ke bawah.
- balikStack() = membalik urutan isi stack.

Pada program utama (main.cpp), beberapa data dimasukkan dan dihapus, lalu isi stack ditampilkan sebelum dan sesudah dibalik.
Hasilnya menunjukkan bahwa urutan data dalam stack berhasil dibalik.

### Soal 2

Tambahkan prosedur pushAscending( in/out S : Stack, in x : integer)

int main()
{

Gambar 7-11 Output stack

STRUKTUR DATA 65

cout << "Hello world!" << endl;
Stack S;
createStack(S);
pushAscending(S,3);
pushAscending(S,4);
pushAscending(S,8);
pushAscending(S,2);
pushAscending(S,3);
pushAscending(S,9);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}
> ![Screenshot bagian x](output/WhatsAppImage2025-10-07at11.36.09.jpeg)

stack.cpp, stack.h, dan main.cpp
```go
#include "Stack.h"
#include <iostream>
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

bool isEmpty(Stack S) {
    return S.top == -1;
}

bool isFull(Stack S) {
    return S.top == MAX - 1;
}

void push(Stack &S, int x) {
    if (!isFull(S)) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!\n";
    }
}

int pop(Stack &S) {
    if (!isEmpty(S)) {
        int x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!\n";
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (!isEmpty(S)) {
        push(temp, pop(S));
    }
    S = temp;
}

void pushAscending(Stack &S, int x) {
    Stack temp;
    createStack(temp);

    // Pindahkan semua elemen yang lebih kecil dari x ke stack sementara
    while (!isEmpty(S) && S.info[S.top] < x) {
        push(temp, pop(S));
    }

    // Masukkan elemen baru
    push(S, x);

    // Kembalikan elemen dari stack sementara
    while (!isEmpty(temp)) {
        push(S, pop(temp));
    }
}
```
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;

struct Stack {
    int info[MAX];
    int top;
};

void createStack(Stack &S);
bool isEmpty(Stack S);
bool isFull(Stack S);
void push(Stack &S, int x);
int pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, int x);

#endif
```
```go
#include <iostream>
#include "Stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);

    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/WhatsAppImage2025-10-07at11.36.09.jpeg)

Penjelasan:
- pushAscending() menjaga agar elemen selalu dalam urutan menaik (ascending).
- Jika elemen baru lebih besar dari elemen atas, elemen tersebut disisipkan di posisi yang tepat dengan bantuan stack sementara.
- Setelah semua elemen dimasukkan, hasil akhir akan menampilkan urutan yang terjaga.

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
