# Magang-IRIS
###

# Rangkuman Pointer (Intern 13/04/2021)
**Pointer** adalah variabel yang menunjuk suatu alamat memori. Pointer sendiri tidak berisi nilai dari suatu data, hanya alamat memori dari data tersebut. 
## Alamat Memori
### Operator Address-Of (&)
Setiap variabel atau objek lain di dalam suatu program memiliki lokasi memori masing-masing yang disimpan dalam alamat memori tertentu.
**Contoh**
variabel yang bernama `myVariable` dapat diketahui alamat memorinya dengan _Operator Address-Of_
```c
int myVariable=1;
printf("%d\n", myVariable);
printf("%p\n", &myVariable);
```
**Output:**
```c
1
000000000065FE1C
```
000000000065FE1C merupakan alamat memori dari variabel `myVariable`
## Pointer
Pointer ditujukan kepada alamat memori (untuk menyimpan alamat memori). 
### Deklarasi Pointer
Pointer dapat dideklarasikan dengan format sebagai berikut
<br>
`type *name;`
Sehingga, penulisan pointer bisa berupa
```c
int * number;
char * character;
double * decimals;
```
Sebagai contoh untuk penempatan `*` menggunakan tipe `int`, ialah
```c
int *pointer;
```
atau 
```c
int* pointer;
```
atau 
```c
int * pointer;
```
Sementara untuk pendeklarasian pointer yang berjumlah lebih dari satu secara tidak terpisah, dapat digunakan:
```c
int *pointer1,*pointer2;
```
Kode di atas berbeda dengan kode di bawah ini
```c
int *pointer1, pointer2;
```
Di mana `pointer2` pada contoh yang ada di bawah bukanlah variabel pointer, di mana variabel `pointer2` bertipe `int`, bukan `int*`.
<br>
### Inisialisasi Variabel Pointer
Variabel `pointer` adalah variabel pointer yang bertipe int dan menyimpan alamat memori. Inisialisasi variabel pointer harus berupa alamat memori, bisa dari variabel lain. 
Contohnya ialah sebagai berikut menggunakan variabel `myVariable` dan variabel pointer `pointer`
```c
int myVariable = 2;
int *pointer = &myVariable; //menggunakan alamat dari myVariable
```
Namun, ada pula contoh salah penggunaan dalam inisialisasi variabel pointer, yaitu sebagai berikut
```c
// ERROR
int *pointer1  = 3;
// UNDEFINED BEHAVIOUR
int *pointer2 = 0x7fffdeb3ed84;
```
Hal di atas menyebabkan hasil ERROR atau _Undefined behaviour_
### Assignment Variabel Pointer
Cara melakukan _assignment_ pada variabel pointer tidak sama dengan inisialisasinya.
```c
int myVariable, *pointer;
myVariable = 4;
pointer = &myVariable; // Assignment pada variabel pointer menggunakan alamat dari variabel myVariable
```
###  Operator Deference
Digunakan untuk mengakses nilai dari sebuah variabel pointer. Penggunaan operator dereference di depan nama variabel pointer. 
Sebagai contoh dengan variabel `myVariable` dan variabel pointer `pointer`
```c
int myVariable  = 5;
int *pointer = &myVariable; //Inisialisasi variabel pointer

printf("%d\n", *pointer); //Mencetak isi dari alamat variabel yang berasal dari proses inisialisasi
*pointer = 6; //Mengubah nilai (isi) dari alamat variabel yang berasal dari proses inisialisasi

printf("%d\n", *pointer);
printf("%d\n", myVariable);
```
**Output**
```c
5
6
6
```
## Double Pointer
Variabel pointer juga dapat menunjuk variabel pointer lainnya. Hal ini disebut dengan double pointer (pointer to pointer).  Kegunaan paling umum dari variabel double pointer adalah untuk membuat array dua dimensi secara dinamis.
```
int **doublePointer;
```

## Pointer dan Array
Array adalah kumpulan data yang disusun secara berurutan. Oleh karena itu, lamat-alamat memori tiap elemen array juga tersusun secara berurutan.
Contoh dari penggunaan pointer pada variabel array `array` adalah sebagai berikut
```c
int array[5] = {1, 2, 3, 4, 5};
int i;
for (i = 0; i < 5; ++i) {
printf("&array[%d] => %p\n", i, &array[i]);
    }
    printf("Address of array => %p\n", array);
    return 0;
```
**Output**
```c
&array[0] => 000000000065FE00
&array[1] => 000000000065FE04
&array[2] => 000000000065FE08
&array[3] => 000000000065FE0C
&array[4] => 000000000065FE10
Address of array => 000000000065FE00
```
Alamat dari `array[0]` sama dengan alamat dari `array`. Dari hal ini dapat diketahui bahwa nama array menunjuk ke elemen pertama dari array tersebut. Karena `&arrray[0]` = `array`, maka dapat disimpulkan bahwa `array[0]` = `*array`, atau nilai dari elemen pertama dapat diakses dengan `*array` atau `*(array + 0)`.
Sehingga, berlaku: <br>
`array[0]` = `*(array + 0)` <br>
`array[1]` = `*(array + 1)` <br>
`array[2]` = `*(array + 2)` <br>
dst. <br>
Atas dasar tersebut, berlaku pula
```c
    int array[5] = {1, 2, 3, 4, 5}, i;
    int *pointer = array;

    for (int i = 0; i < 5; ++i) {
        printf("%d ", *(pointer+i));
    }
    return 0;
```
**Output**
```
1 2 3 4 5
```
Terdapat pula contoh lain penggunaan gabungan pointer dan array di mana nilai dari bagian array ditentukan menggunakan `*p`, yaitu sebagai berikut
```
int numbers[5];
int *p;
p = numbers;  *p = 10;
p++;  *p = 20;
p = &numbers[2];  *p = 30;
p = numbers + 3;  *p = 40;
p = numbers;  *(p+4) = 50;
   for (int n=0; n<5; n++)
   printf ("%d ", numbers[n]);
  return 0;
```
**Output**
```
10 20 30 40 50
```
## Pointer dan Fungsi
Terdapat dua cara untuk _passing_ argumen pada fungsi, yaitu **Pass by value** dan **Pass by reference**
### Pass by Value
Yaitu saat _passing_ argumen pada fungsi, nilai dari argumen tersebut akan disalin ke variabel yang berada pada parameter fungsi. Karena hanya menerima nilainya saja, perubahan yang terjadi pada variabel parameter fungsi tidak akan berpengaruh terhadap variabel asalnya. Sebagai contoh:
```
#include <stdio.h>

void change(int a, int b)
{
    a = a + 5;
    b = b + 5;
}

int main()
{
    int x = 10, y = 6;
    change(x, y);
    printf("%d %d\n", x, y);

    return 0;
}
```
**Output**
```
10 6
```
Nilai variabel `x` dan `y` tidak akan berubah karena menggunakan metode _pass by value_
### Pass by Reference
berarti argumen yang dimasukkan ke parameter fungsi adalah alamat memori variabel. Segala perubahan yang terjadi pada variabel tersebut, juga mempengaruhi langsung ke variabel asalnya karena argumennya langsung berupa alamat memori. Sebagai contoh:
```
#include <stdio.h>

void change(int *a, int *b)
{
    *a = *a + 5;
    *b = *b + 5;
}

int main()
{
    int x = 10, y = 6;
    change(&x, &y);
    printf("%d %d\n", x, y);

    return 0;
}
```
**Output**
```
15 11
```

***
# Latihan Soal
## Soal
1. Buat fungsi untuk menukar nilai dari 2 variabel menggunakan pointer!
```
int a = 5, b = 3;

tukar();
```
2. Buat fungsi untuk membalik sebuah array menggunakan pointer !
```
int arr[5] = {1,2,3,4,5,6}

balik();
```
3. Cari soal tentang penerapan pointer dan kerjakan ! <br>
[Sumber soal, nomor 15](https://www.geeksforgeeks.org/c-language-2-gq/pointers-gq)
## Jawaban
1. Menukar nilai pada variabel `a` dan `b`
```
#include <stdio.h>

void tukar (int *a, int *b)
{
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}

int main (){
    int a=5, b=3;
    tukar (&a, &b);
    printf ("%d %d", a, b);

}
```
**Output**
```
a=3 b=5
```
2. Menukar urutan dari isi array `arr`
```
#include <stdio.h>

void balik (int *arr)
{
    int arrSimpan[5], i, j;
    for (i=0 ; i <5; i++)
    {
        arrSimpan[i] = *(arr + i);
    }
    for (i=0, j=4 ;i<5; i++)
    {
        *(arr+i) = arrSimpan[j];
        j--;
    }
}

int main (){
    int arr[] = {1, 2, 3, 4, 5};
    balik (arr);
    for (int i =0; i < 5; i++)
    {printf ("%d ", arr[i]);}

}
```
**Output**
```
5 4 3 2 1
```
3. Mencari satu soal mengenai penerapan pointer 
What are the outputs>
```
#include<stdio.h>
 
void swap (char *x, char *y)
{
    char *t = x;
    x = y;
    y = t;
}
 
int main()
{
    char *x = "geeksquiz";
    char *y = "geeksforgeeks";
    char *t;
    swap(x, y);
    printf("(%s, %s)", x, y);
    t = x;
    x = y;
    y = t;
    printf("\n(%s, %s)", x, y);
    return 0;
}
```
**Outputs**
```
geeksquiz, geeksforgeeks)
(geeksforgeeks, geeksquiz)
```
Pada soal ini, fungsi `swap` menggunakan metode passing _pass by value_ sehingga nilai `x` dan `y` tidak tertukar.
###
# OOP

## Soal 1
```
#include<bits/stdc++.h>
using namespace std;

class Shape{ 
    public: 
    int width, height; 
    void numbers(int x, int y) { 
        width=x; 
        height=y; 
    }
};

class Rectangle: public Shape{ 
    public: 
    float area () {
        return width*height; 
    }

};

class Triangle: public Shape { 
    public:
    float area () {
        return width*height/2; 
    }
};

int main (){
    Rectangle kotak; 
    Triangle segitiga;
    kotak.numbers (10, 5); 
    segitiga.numbers (9, 4); 
    cout << kotak.area() << "\n" <<  segitiga.area();
    return 0;

}
```
**Output**
```
50
18
```
## Soal 2
```
include<bits/stdc++.h>
using namespace std;

class Mother{ 
 public: 
 void display () 
 {cout << "Mom! /n";} 
};

class Daughter: public Mother { 
    public:
    void display () 
    {cout << "Daughter! \n";}
};

int main (){
    Daughter x; 
    x.display(); 
    return 0;
}
```
**Output**
```
Daughter!

```
## Soal 3
```
#include<bits/stdc++.h>
using namespace std;

class Animal { 
    public:
    int age; 
    string name, origin, movement; 
    void set_value(string x, int y, string z, string aa){ 
        name = x; 
        age = y; 
        origin =z; 
        movement=aa; 
    }
};

class Zebra: public Animal { 
    public:
    void zeb(){ 
        cout << name << " the zebra is " << age << " years old, from " <<  origin <<". It moves by " << movement << endl;
    }
    
};

class Dolphin: public Animal { 
    public:
    void dolphin(){ 
        cout << name << " the dolphin is " << age << " years old, from " <<  origin <<". It moves by " << movement << endl;
    }
   
};

int main (){
    string na1 , na2; 
    string or1 , or2 ;  
    string m1 , m2 ; 
    int o1,o2; 
    cin >> na1 >> o1 >> or1 >> m1; 
    cin >> na2 >> o2 >> or2 >> m2; 
    Zebra a; 
    Dolphin b; 
    a.set_value(na1, o1, or1, m1); 
    b.set_value(na2, o2, or2, m2);
    a.zeb(); 
    cout << "\n";
    b.dolphin(); 
    return 0;
}
```
**Output**
```
(Sesuai dengan input)
```

## Soal 3(2)

```
#include<bits/stdc++.h>
using namespace std;

class Animal { 
    public:
    int age;
    string name, origin, movement;
    void set_value(string x, int y, string z, string aa){ 
        name = x; 
        age = y; 
        origin =z; 
        movement=aa; 
    }
};

class Zebra: public Animal { 
    public:
    void zeb(){ 
        cout << name << " the zebra is " << age << " years old, from " <<  origin <<". It moves by " << movement << endl;
    }
    
};

class Dolphin: public Animal { 
    public:
    void dolphin(){ 
        cout << name << " the dolphin is " << age << " years old, from " <<  origin <<". It moves by " << movement << endl;
    }
    
};

int main (){
    string na1 = "Lala", na2 = "Lili"; 
    string or1 = "Africa", or2 = "worldwide";  
    string m1 = "walking", m2 = "swimming"; 
    Zebra a;
    Dolphin b; 
    a.set_value(na1, 20, or1, m1); 
    b.set_value(na2, 30, or2, m2);
    a.zeb(); 
    cout << "\n";
    b.dolphin();
    return 0;
}  
```
**Output**
```
Lala the zebra is 20 years old, from Africa. It moves by walking

Lili the dolphin is 30 years old, from worldwide. It moves by swimming

```
