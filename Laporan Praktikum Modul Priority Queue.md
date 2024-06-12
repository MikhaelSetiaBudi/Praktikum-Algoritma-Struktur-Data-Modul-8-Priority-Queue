# <h1 align="center">Laporan Praktikum Modul Priority Queue</h1>
<p align="center">Mikhael Setia Budi</p>

## Dasar Teori
Priority queue adalah jenis queue yang mengatur elemen berdasarkan nilai
prioritasnya. Algoritma priority queue bekerja berdasarkan prinsip Higher Priority In First Out (HPIFO) dimana pekerjaan yang memiliki prioritas tertinggi akan diselesaikan lebih dulu [1]. Elemen dengan nilai prioritas lebih tinggi umumnya akan diambil
sebelum elemen dengan nilai prioritas lebih rendah. Dalam priority queue, setiap elemen memiliki nilai prioritas yang terkait dengannya.
Ketika menambahkan elemen ke antrian, elemen tersebut dimasukkan ke dalam posisi
berdasarkan nilai prioritasnya. Misalnya, jika menambahkan elemen dengan nilai
prioritas tinggi ke priority queue, elemen tersebut mungkin dimasukkan di dekat
bagian depan antrian, sementara elemen dengan nilai prioritas rendah mungkin
dimasukkan di dekat bagian belakang. Ada beberapa cara untuk mengimplementasikan priority queue, termasuk
menggunakan array, linked list, heap, atau binary search tree. Setiap metode memiliki
kelebihan dan kekurangannya sendiri, dan pilihan terbaik akan tergantung pada
kebutuhan spesifik aplikasi. Priority queue sering digunakan dalam sistem real-time, di mana urutan pemrosesan
elemen dapat memiliki konsekuensi yang signifikan. Heap dalam struktur data adalah struktur berbasis pohon biner (binary tree) dengan
aturan tertentu. Heap memiliki beberapa ciri khas yang membedakannya dari pohon
binary biasa, yaitu:

1. Complete Binary Tree

Heap harus berbentuk complete binary tree, di mana
setiap levelnya terisi penuh kecuali level paling bawah. Level paling bawah
pun harus terisi dari kiri ke kanan.

2. Order Property

Heap bisa dibagi menjadi dua jenis, yaitu max-heap dan
min-heap.

3. Max-heap

pada setiap node, nilai orang tua (parent) harus lebih besar atau
sama dengan nilai anaknya (children).

4. Min-heap

pada setiap node, nilai orang tua harus lebih kecil atau sama
dengan nilai anaknya.

Dengan aturan ini, nilai terbesar (max-heap) atau terkecil (min-heap) akan selalu
berada di node paling atas (root). Heap sering digunakan untuk algoritma sorting
seperti heap sort dan juga untuk priority queue.

## Guided 

```C++
#include <iostream>
#include <algorithm>

int H[50];
int heapSize = -1;

int parent(int i) {
    return (i - 1) / 2;
}

int leftChild(int i) {
    return ((2 * i) + 1);
}

int rightChild(int i) {
    return ((2 * i) + 2);
}

void shiftUp(int i) {
    while (i > 0 && H[parent(i)] < H[i]) {
        std::swap(H[parent(i)], H[i]);
        i = parent(i);
    }
}

void shiftDown(int i) {
    int maxIndex = i;
    int l = leftChild(i);
    if (l <= heapSize && H[l] > H[maxIndex]) {
        maxIndex = l;
    }
    int r = rightChild(i);
    if (r <= heapSize && H[r] > H[maxIndex]) {
        maxIndex = r;
    }
    if (i != maxIndex) {
        std::swap(H[i], H[maxIndex]);
        shiftDown(maxIndex);
    }
}

void insert(int p) {
    heapSize = heapSize + 1;
    H[heapSize] = p;
    shiftUp(heapSize);
}

int extractMax() {
    int result = H[0];
    H[0] = H[heapSize];
    heapSize = heapSize - 1;
    shiftDown(0);
    return result;
}

void changePriority(int i, int p) {
    int oldp = H[i];
    H[i] = p;
    if (p > oldp) {
        shiftUp(i);
    } else {
        shiftDown(i);
    }
}

int getMax() {
    return H[0];
}

void remove(int i) {
    H[i] = getMax() + 1;
    shiftUp(i);
    extractMax();
}

int main() {
    insert(45);
    insert(20);
    insert(14);
    insert(12);
    insert(31);
    insert(7);
    insert(11);
    insert(13);
    insert(7);
    
    std::cout << "Priority Queue : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    std::cout << "Node with maximum priority : " << extractMax() << "\n";
    std::cout << "Priority queue after extracting maximum : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    changePriority(2, 49);
    std::cout << "Priority queue after priority change : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    remove(3);
    std::cout << "Priority queue after removing the element : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    return 0;
}
```

**Code 1**
```C++
#include <iostream>
using namespace std;
```
kode diatas digunakan untuk mendefinisikan header file iostream yang berisi definisi objek input dan output standar seperti cin, dan cout. 
incluade <algorithm> mendefinisikan header untuk mendapatkan fungsi-fungsi algoritma seperti swap (algorithm)

**Code 2**
```C++
int H[50];
int heapSize = -1;
```
kode diatas digunakan untuk mendeklarasikan variabel global. variabel H adalah array integer yang digunakan untuk mengyimpan elemen-elemen dalam heap. heapSize adalah variabel yang menyimpan jumlah elemen saat ini dalam heap

**Code 3**
```C++
int parent(int i) {
    return (i - 1) / 2;
}

int leftChild(int i) {
    return ((2 * i) + 1);
}

int rightChild(int i) {
    return ((2 * i) + 2);
}
```
Fungsi parent(int i) digunakan untuk mengembalikan indek induk dari node ke-i dalam heap. 
leftChild(int i) digunakan untuk mengembalikan anak kiri dari node ke-i dalam heap.
rightChild(int i) digunakan untuk mengembalikan indeks anak kanan dari node ke-i dalam heap.

**Code 4**
```C++
void shiftUp(int i) {
    while (i > 0 && H[parent(i)] < H[i]) {
        std::swap(H[parent(i)], H[i]);
        i = parent(i);
    }
}
```
fungsi shifUp(int i) digunakan untuk memindahkan nde ke atas pada posisi yang sesuai dalam heap setelah penyisipan elemen baru.

**Code 5**
```C++
void shiftDown(int i) {
    int maxIndex = i;
    int l = leftChild(i);
    if (l <= heapSize && H[l] > H[maxIndex]) {
        maxIndex = l;
    }
    int r = rightChild(i);
    if (r <= heapSize && H[r] > H[maxIndex]) {
        maxIndex = r;
    }
    if (i != maxIndex) {
        std::swap(H[i], H[maxIndex]);
        shiftDown(maxIndex);
    }
}
```
fungsi shifDown(int i) digunakan untuk memindahkan node ke bawah pada posisi yang sesuai dalam heap setelah penghapusan elemen.

**Code 6**
```C++
void insert(int p) {
    heapSize = heapSize + 1;
    H[heapSize] = p;
    shiftUp(heapSize);
}
```
fungsi insert(int P) digunakan untuk menyisipkan elemen baru dengan prioritas p ke dalam heap.

**Code 7**
```C++
int extractMax() {
    int result = H[0];
    H[0] = H[heapSize];
    heapSize = heapSize - 1;
    shiftDown(0);
    return result;
}
```
fungsi extractMax() digunakan untuk menghapus dan mengembalikan elemen dengan prioritas tertinggi (maksimum) dari heap. 

**Code 8**
```C++
void changePriority(int i, int p) {
    int oldp = H[i];
    H[i] = p;
    if (p > oldp) {
        shiftUp(i);
    } else {
        shiftDown(i);
    }
}
```
fungsi changePriority(int i, int p) digunakan untuk mengubah prioritas elemen pada indeks i menjadi p.

**Code 9**
```C++
int getMax() {
    return H[0];
}
```
fungsi getMax() digunakan untuk mengembalikan nilai elemen dengan prioritas tertinggi (maksimum) dari heap.

**Code 10**
```C++
void remove(int i) {
    H[i] = getMax() + 1;
    shiftUp(i);
    extractMax();
```
fungsi  remove(int i) digunakan untuk menghapus elemen pada indeks i dari heap.

**Code 11**
```C++
int main() {
    insert(45);
    insert(20);
    insert(14);
    insert(12);
    insert(31);
    insert(7);
    insert(11);
    insert(13);
    insert(7);
    
    std::cout << "Priority Queue : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    std::cout << "Node with maximum priority : " << extractMax() << "\n";
    std::cout << "Priority queue after extracting maximum : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    changePriority(2, 49);
    std::cout << "Priority queue after priority change : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    remove(3);
    std::cout << "Priority queue after removing the element : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    return 0;
}
```
fungsi main merupakan fungsi utama dalam program yang akan dijalankan. dalam fungsi main terdapat fungsi insert() untuk menambahkan elemen-elemen ke dalam heap.
menampilkan isi dari heap. lalu elemen dengan prioritas tertinggi (maksimum) dihapus dengan menggunakan fungsi extractMax(), dan nilai elemen tersebut ditampilkan.
setelah ekstraksi elemen maksimum, isi dari heap ditampilkan kembali. prioritas dari elemen pada indeks ke-2 diubah menjadi 49. lalu menampilkan heap setelah perubahan prioritas.
elemen pada indeks ke-3 dihapus menggunakan fungsi remove(). lalu menampilkan heap setelah indeks ke-3 dihapus.
pada setiap cout menggunakan awalan std dikarenakan tidak menggunakan namespace std.

#### Output
```C++
Priority Queue : 45 31 14 13 20 7 11 12 7 
Node with maximum priority : 45
Priority queue after extracting maximum : 31 20 14 13 7 7 11 12
Priority queue after priority change : 49 20 31 13 7 7 11 12
Priority queue after removing the element : 49 20 31 12 7 7 11
```
menampilkan data heap, lalu menghapus nilai maksimum dalam heap, memunculkan heap kembali, mengubah indeks ke-2 menjadi 49, menampilkan setelah indeks ke-2 diubah,
mengampus indeks ke-3 dan menampilkannya.

#### Full Code Screenshoot
![alt text](https://github.com/MikhaelSetiaBudi/Praktikum-Algoritma-Struktur-Data-Modul-8-Priority-Queue/blob/master/Modul%208%20Alstrukdat/Code%20Guided%201%20Priority%20Queue.png?raw=true)

#### Output Screenshot
![alt text](https://github.com/MikhaelSetiaBudi/Praktikum-Algoritma-Struktur-Data-Modul-8-Priority-Queue/blob/master/Output%20Modul%208%20Alstrukdat/Output%20Guided%201%20Priority%20Queue.png?raw=true)

## Unguided 

### 1. Modifikasi guided diatas yang mana heap dikonstruksi secara manual berdasarkan user.

```C++
#include <iostream>
#include <algorithm>
#include <vector>

std::vector<int> H;
int heapSize = -1;

int parent(int i) {
    return (i - 1) / 2;
}

int leftChild(int i) {
    return ((2 * i) + 1);
}

int rightChild(int i) {
    return ((2 * i) + 2);
}

void shiftUp(int i) {
    while (i > 0 && H[parent(i)] < H[i]) {
        std::swap(H[parent(i)], H[i]);
        i = parent(i);
    }
}

void shiftDown(int i) {
    int maxIndex = i;
    int l = leftChild(i);
    if (l <= heapSize && H[l] > H[maxIndex]) {
        maxIndex = l;
    }
    int r = rightChild(i);
    if (r <= heapSize && H[r] > H[maxIndex]) {
        maxIndex = r;
    }
    if (i != maxIndex) {
        std::swap(H[i], H[maxIndex]);
        shiftDown(maxIndex);
    }
}

void insert(int p) {
    heapSize = heapSize + 1;
    if (heapSize < H.size()) {
        H[heapSize] = p;
    } else {
        H.push_back(p);
    }
    shiftUp(heapSize);
}

int extractMax() {
    int result = H[0];
    H[0] = H[heapSize];
    heapSize = heapSize - 1;
    shiftDown(0);
    return result;
}

void changePriority(int i, int p) {
    int oldp = H[i];
    H[i] = p;
    if (p > oldp) {
        shiftUp(i);
    } else {
        shiftDown(i);
    }
}

int getMax() {
    return H[0];
}

void remove(int i) {
    H[i] = getMax() + 1;
    shiftUp(i);
    extractMax();
}

int main() {
    int n, value;
    std::cout << "Masukkan jumlah elemen: ";
    std::cin >> n;
    std::cout << "Masukkan elemen-elemen: ";
    for (int i = 0; i < n; ++i) {
        std::cin >> value;
        insert(value);
    }
    
    std::cout << "Priority Queue : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    std::cout << "Node with maximum priority : " << extractMax() << "\n";
    std::cout << "Priority queue after extracting maximum : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    int index, newPriority;
    std::cout << "Masukkan indeks dan prioritas baru untuk diubah: ";
    std::cin >> index >> newPriority;
    changePriority(index, newPriority);
    std::cout << "Priority queue after priority change : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    std::cout << "Masukkan indeks untuk dihapus: ";
    std::cin >> index;
    remove(index);
    std::cout << "Priority queue after removing the element : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    return 0;
}


// Mikhael Setia Budi
// 2311110033
// copyright@MikhaelS.B
```

**Code 1**
```C++
#include <iostream>
#include <algorithm>
#include <vector>
```
kode diatas digunakan untuk mendefinisikan header file iostream yang berisi definisi objek input dan output standar seperti cin, dan cout. include stack merupakan header untuk menggunakan stack. include string digunakan untuk memanpulasi string. include algorithm digunakan untuk fungsi algoritma standar, seperti transform.
algorithm digunakan untuk mendefinisikan header untuk fungsi-fungsi algoritma seperti swap.
vector digunakan untuk mendefinisikan header untuk menggunakan struktur data dinamis vector.

**Code 2**
```C++
std::vector<int> H;
int heapSize = -1;
```
mendeklarasikan variabel global dengan H merupakan vector yang menyimpan elemen-eleme priority queue, dan heapSize merupakan variabel yang menyimpan jumlah elemen saat ini dalam priority queue.

**Code 3**
```C++
int parent(int i) {
    return (i - 1) / 2;
}

int leftChild(int i) {
    return ((2 * i) + 1);
}

int rightChild(int i) {
    return ((2 * i) + 2);
}
```
Fungsi parent(int i) digunakan untuk mengembalikan indek induk dari node ke-i dalam heap. 
leftChild(int i) digunakan untuk mengembalikan anak kiri dari node ke-i dalam heap.
rightChild(int i) digunakan untuk mengembalikan indeks anak kanan dari node ke-i dalam heap.

**Code 4**
```C++
void shiftUp(int i) {
    while (i > 0 && H[parent(i)] < H[i]) {
        std::swap(H[parent(i)], H[i]);
        i = parent(i);
    }
}
```
fungsi shifUp(int i) digunakan untuk memindahkan nde ke atas pada posisi yang sesuai dalam heap setelah penyisipan elemen baru.

**Code 5**
```C++
void shiftDown(int i) {
    int maxIndex = i;
    int l = leftChild(i);
    if (l <= heapSize && H[l] > H[maxIndex]) {
        maxIndex = l;
    }
    int r = rightChild(i);
    if (r <= heapSize && H[r] > H[maxIndex]) {
        maxIndex = r;
    }
    if (i != maxIndex) {
        std::swap(H[i], H[maxIndex]);
        shiftDown(maxIndex);
    }
}
```
fungsi shifDown(int i) digunakan untuk memindahkan node ke bawah pada posisi yang sesuai dalam heap setelah penghapusan elemen.

**Code 6**
```C++
void insert(int p) {
    heapSize = heapSize + 1;
    if (heapSize < H.size()) {
        H[heapSize] = p;
    } else {
        H.push_back(p);
    }
    shiftUp(heapSize);
}
```
fungsi insert(int P) digunakan untuk menyisipkan elemen baru dengan prioritas p ke dalam heap.

**Code 7**
```C++
int extractMax() {
    int result = H[0];
    H[0] = H[heapSize];
    heapSize = heapSize - 1;
    shiftDown(0);
    return result;
}
```
fungsi extractMax() digunakan untuk menghapus dan mengembalikan elemen dengan prioritas tertinggi (maksimum) dari heap. 

**Code 8**
```C++
void changePriority(int i, int p) {
    int oldp = H[i];
    H[i] = p;
    if (p > oldp) {
        shiftUp(i);
    } else {
        shiftDown(i);
    }
}
```
fungsi changePriority(int i, int p) digunakan untuk mengubah prioritas elemen pada indeks i menjadi p.

**Code 9**
```C++
int getMax() {
    return H[0];
}
```
fungsi getMax() digunakan untuk mengembalikan nilai elemen dengan prioritas tertinggi (maksimum) dari heap.

**Code 10**
```C++
void remove(int i) {
    H[i] = getMax() + 1;
    shiftUp(i);
    extractMax();
}
```
fungsi  remove(int i) digunakan untuk menghapus elemen pada indeks i dari heap.

**Code 11**
```C++
int main() {
    int n, value;
    std::cout << "Masukkan jumlah elemen: ";
    std::cin >> n;
    std::cout << "Masukkan elemen-elemen: ";
    for (int i = 0; i < n; ++i) {
        std::cin >> value;
        insert(value);
    }
    
    std::cout << "Priority Queue : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    std::cout << "Node with maximum priority : " << extractMax() << "\n";
    std::cout << "Priority queue after extracting maximum : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    int index, newPriority;
    std::cout << "Masukkan indeks dan prioritas baru untuk diubah: ";
    std::cin >> index >> newPriority;
    changePriority(index, newPriority);
    std::cout << "Priority queue after priority change : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    std::cout << "\n";

    std::cout << "Masukkan indeks untuk dihapus: ";
    std::cin >> index;
    remove(index);
    std::cout << "Priority queue after removing the element : ";
    for (int i = 0; i <= heapSize; ++i) {
        std::cout << H[i] << " ";
    }
    return 0;
}
```
program diatas akan meminta pengguna untuk memasukkan jumlah elemen dari elemen-elemen priority queue. melakukan penyisipan elemen-elemen ke dalam priority queue.
Menampilkan priority queue sebelum dan setelah beberapa operasi seperti ekstraksi maksimum, perubahan prioritas, dan penghapusan elemen. Meminta pengguna untuk memasukkan indeks dan prioritas baru untuk perubahan prioritas.
Mengubah prioritas elemen pada indeks yang dimasukkan oleh pengguna. Meminta pengguna untuk memasukkan indeks untuk penghapusan elemen.
Menghapus elemen pada indeks yang dimasukkan oleh pengguna. Menampilkan priority queue setelah operasi penghapusan.

#### Output:
```C++
Masukkan jumlah elemen: 10
Masukkan elemen-elemen: 1 2 3 4 5 6 7 8 9 10
Priority Queue : 10 9 6 7 8 2 5 1 4 3 
Node with maximum priority : 10
Priority queue after extracting maximum : 9 8 6 7 3 2 5 1 4 
Masukkan indeks dan prioritas baru untuk diubah: 8 11
Priority queue after priority change : 11 9 6 8 3 2 5 1 7 
Masukkan indeks untuk dihapus: 2
Priority queue after removing the element : 11 9 7 8 3 2 5 1
```
pengguna akan diminta untuk memasukkan jumlah elemen, lalu memasukkan elemen elemen ke dalam heap. lalu akan menampilkan priority queue, setelah itu menghapus nilai maksimum dan menampilkannya.
masukan indeks yang akan diubah dan masukkan prioritas baru, lalu akan menampilkan priority queue setelah perubahan pada prioritas baru. setelah itu pengguna akan diminta untuk memilih indeks berapa yang akan dihapus dan menampilkannya.

#### Full code Screenshot:
![alt text](https://github.com/MikhaelSetiaBudi/Praktikum-Algoritma-Struktur-Data-Modul-8-Priority-Queue/blob/master/Modul%208%20Alstrukdat/Code%20Unguided%201%20Priority%20Queue.png?raw=true)

#### Output Screenshot
![alt text](https://github.com/MikhaelSetiaBudi/Praktikum-Algoritma-Struktur-Data-Modul-8-Priority-Queue/blob/master/Output%20Modul%208%20Alstrukdat/Output%20Unguided%201%20Priority%20Queue.png?raw=true)

## Kesimpulan
Priority queue adalah jenis queue yang mengatur elemen berdasarkan nilai prioritasnya.  jika menambahkan elemen dengan nilai prioritas tinggi ke priority queue, elemen tersebut mungkin dimasukkan di dekat
bagian depan antrian, sementara elemen dengan nilai prioritas rendah mungkin dimasukkan di dekat bagian belakang. Ada beberapa cara untuk mengimplementasikan priority queue, termasuk
menggunakan array, linked list, heap, atau binary search tree. Heap dalam struktur data adalah struktur berbasis pohon biner (binary tree) dengan aturan tertentu.

## Referensi
[1]	M. I. Nurhadi, R. E. S. S. T, C. S. S. T, F. T. Elektro, U. Telkom, and P. Q. Algorithm, “Manajemen Dan Kendali Beban Perangkat Elektronik Berbasis Web Dengan Algoritma Priority Queue Web Based Management and Controlling for Electronic Device Loads With Priority Queue,” vol. 8, no. 2, pp. 1943–1948, 2021.
