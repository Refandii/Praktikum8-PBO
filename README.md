<H1 align="center"> LAPORAN PRAKTIKUM PEMROGAMAN BERORIENTASI OBJEK </H1>
<H1 align="center"> Laporan Praktikum 008: Polimorfisme, Abstract, dan Interface </H1>

<br>

<p align="center">
  <img width="500" height="500" alt="UNS No  Bckg" src="https://github.com/user-attachments/assets/58f18451-ea1e-40e7-af70-23081dc27263" />
</p>

<br>

<div>
  <p align="center">
    <b>Disusun oleh:</b><br>
    Nama: Re'fandi Indra Maulana<br>
    NIM: L0325011</p><br>
</div>

<div>
  <p align="center">
    <b>Asisten Praktikum:</b><br>
    AZFA RAHMA PUTRA SUSANTO<br>
    INDRA FATA AZHARI<br>
</div>

---

Program Java untuk implementasi polimorfisme, Abstract, dan Interface

---

## Tujuan Praktikum
Setelah menyelesaikan modul praktikum ini, mahasiswa diharapkan mampu:
- Mahasiswa mampu memahami dan mengimplementasikan konsep Polymorphism (polimorfisme) pada tingkat runtime (Method Overriding).
- Mahasiswa mampu merancang Abstract Class dan Abstract Method sebagai kerangka dasar dari sebuah hierarki kelas.
- Mahasiswa mampu mengimplementasikan Interface untuk menciptakan kontrak arsitektur perangkat lunak dan menyimulasikan pewarisan ganda (multiple inheritance).
---

## Dasar Teori
- **Polymorphism**: Berasal dari bahasa Yunani yang berarti "banyak bentuk". Dalam OOP, sebuah objek dapat memiliki berbagai bentuk perilaku meskipun dipanggil dari referensi kelas induk yang sama. Terdapat dua jenis polimorfisme: Compile-time (Method Overloading) dan Runtime (Method Overriding).
- **Abstract Class**: Sebuah kelas yang dideklarasikan dengan kata kunci abstract. Kelas ini tidak dapat diinstansiasi (tidak bisa dibuat objeknya menggunakan new), namun dapat diwariskan ke subclass. Kelas ini biasanya berisi satu atau lebih abstract method (metode tanpa isi/bodi) yang wajib di-override oleh subclass-nya.
- **Interface**: Sebuah cetak biru murni (pure abstraction) dari kelas yang hanya berisi tanda tangan metode (method signatures) dan konstanta. Berbeda dengan class yang hanya bisa mewarisi (extends) satu kelas lain, sebuah kelas di Java dapat mengimplementasikan (implements) lebih dari satu Interface.

---

## Kegiatan Praktikum

<h2>Kegiatan 1:</h2><br>Implementasi Polymorphism (Method Overriding)
Pada kegiatan ini, kita membuat hierarki kelas Hewan beserta subclass Kucing dan Anjing untuk mendemonstrasikan polimorfisme runtime.<br>

**1. Hewan.java**<br>
```package com.praktikum8;

public class Hewan {
    public void bersuara() {
        System.out.println("Hewan ini mengeluarkan suara yang tidak spesifik.");
    }
}
<br>
```
Penjelasan: Kelas Hewan merupakan superclass (induk) yang memiliki satu metode bersuara(). Metode ini mendefinisikan perilaku dasar yang nantinya akan dimodifikasi (di-override) oleh kelas turunannya.

---

**2. Kucing.java**<br>
```package com.praktikum8;

public class Kucing extends Hewan {
    @Override
    public void bersuara() {
        System.out.println("Kucing: Meow meow!");
    }
}
<br>
```
Penjelasan: Kelas Kucing mewarisi kelas Hewan. Anotasi @Override digunakan untuk mengganti implementasi metode bersuara() dari superclass dengan suara spesifik kucing.

---

**3. Anjing.java**<br>
```package com.praktikum8;

public class Anjing extends Hewan {
    @Override
    public void bersuara() {
        System.out.println("Anjing: Guk guk!");
    }
}
<br>
```
Penjelasan: Sama seperti Kucing, kelas Anjing juga mewarisi Hewan dan mengganti metode bersuara() dengan suara spesifik anjing.

---

**4. PoliTester.java**<br>
```public class PoliTester {
    public static void main(String[] args) {
        // Deklarasi array dari tipe Superclass, tetapi diisi dengan objek Subclass
        Hewan[] daftarHewan = new Hewan[3];
        daftarHewan[0] = new Hewan();
        daftarHewan[1] = new Kucing(); // Upcasting
        daftarHewan[2] = new Anjing(); // Upcasting

        // Polimorfisme: Pemanggilan method yang sama menghasilkan output berbeda
        for (Hewan h : daftarHewan) {
            h.bersuara();
        }
    }
}
<br>
```
Penjelasan: Kelas ini menguji polimorfisme (Dynamic Binding). Kita membuat array bertipe Hewan, namun mengisinya dengan objek Hewan, Kucing, dan Anjing (Upcasting). Saat metode bersuara() dipanggil di dalam loop, Java secara dinamis menentukan metode mana yang akan dieksekusi berdasarkan wujud asli objek tersebut saat runtime, bukan tipe referensinya.

---



## Output Program
**Output Kegiatan 1**<br>
```Hewan ini mengeluarkan suara yang tidak spesifik.
Kucing: Meow meow!
Anjing: Guk guk!
```

---


<h2>Kegiatan 2:</h2>h2>:<br>Implementasi Abstract Class
Pada kegiatan ini, kita membuat kerangka dasar bangun datar yang belum memiliki rumus luas spesifik.<br>

**1. BangunDatar.java**<br>
```package com.praktikum8;

public abstract class BangunDatar {
    String warna;

    public BangunDatar(String warna) {
        this.warna = warna;
    }

    // Abstract method: Tidak memiliki isi, wajib di-override subclass
    public abstract double hitungLuas();

    // Concrete method: Punya isi, bisa langsung dipakai
    public void cetakWarna() {
        System.out.println("Warna bangun ini adalah: " + warna);
    }
}
<br>
```
Penjelasan: Deklarasi kelas BangunDatar menggunakan keyword abstract. Kelas ini memiliki concrete method (cetakWarna()) yang langsung bisa dipakai, dan abstract method (hitungLuas()) yang tidak memiliki bodi (kurung kurawal) dan memaksa subclass untuk mengimplementasikannya.

---

**2. Lingkaran.java**<br>
```package com.praktikum8;

public class Lingkaran extends BangunDatar {
    private double jariJari;

    public Lingkaran(String warna, double jariJari) {
        super(warna); // Memanggil constructor superclass
        this.jariJari = jariJari;
    }

    @Override
    public double hitungLuas() {
        return Math.PI * jariJari * jariJari;
<br>
```
- extends BangunDatar: Kata kunci ini menunjukkan bahwa kelas Lingkaran adalah subclass yang mewarisi (inherit) kelas abstrak BangunDatar.   
- private double jariJari;: Mendeklarasikan variabel spesifik milik kelas Lingkaran untuk menyimpan nilai jari-jari.   
- public Lingkaran(String warna, double jariJari): Konstruktor kelas untuk menginisialisasi objek Lingkaran saat dibuat.
- super(warna);: Kata kunci super digunakan untuk memanggil konstruktor dari kelas induk (BangunDatar) agar atribut warna dapat diinisialisasi secara benar.
- this.jariJari = jariJari;: Menyimpan nilai parameter jariJari ke dalam atribut kelas.
- @Override public double hitungLuas(): Karena BangunDatar memiliki abstract method hitungLuas() yang tidak memiliki bodi, maka Lingkaran wajib mengimplementasikan (melakukan override) metode tersebut agar IDE tidak error.
- return Math.PI * jariJari * jariJari;: Mengembalikan nilai perhitungan luas lingkaran menggunakan konstanta bawaan Java Math.PI dikalikan kuadrat jari-jari.   

---



<h2>Kegiatan 3:</h2>h2><br>Implementasi Interface (Multiple Implementation)
Pada kegiatan ini, kita membuat antarmuka (interface) untuk menyimulasikan pewarisan ganda (multiple inheritance) di mana satu kelas dapat mengimplementasikan lebih dari satu interface.<br>

**1. AlatElektronik.java**<br>
```public interface AlatElektronik {
    void nyalakan();
    void matikan();
}
<br>
```
Penjelasan: Interface ini bertindak sebagai cetak biru murni yang mendefinisikan kontrak bahwa setiap alat elektronik harus memiliki metode nyalakan() dan matikan().

---

**2. Kamera.java**<br>
```public interface Kamera {
    void ambilFoto();
}
<br>
```
Penjelasan: Interface kedua yang mendefinisikan fitur kamera melalui metode ambilFoto().

---

**3. Smartphone.java**<br>
```public class Smartphone implements AlatElektronik, Kamera {
    private String merk;

    public Smartphone(String merk) {
        this.merk = merk;
    }

    @Override
    public void nyalakan() {
        System.out.println(merk + " menyala, Booting OS...");
    }

    @Override
    public void matikan() {
        System.out.println(merk + " dimatikan. Goodbye.");
    }

    @Override
    public void ambilFoto() {
        System.out.println("Cekrek! Foto berhasil disimpan di galeri " + merk);
    }
}
<br>
```
Penjelasan: Kelas Smartphone mengimplementasikan dua interface sekaligus (AlatElektronik dan Kamera) menggunakan kata kunci implements. Oleh karena itu, kelas ini wajib melakukan override dan memberikan isi implementasi pada seluruh metode dari kedua interface tersebut. (Catatan: Typo hasil pemindaian pada modul asli seperti "05" telah disesuaikan menjadi "OS" dan "Cokrok" menjadi "Cekrek!").

---
