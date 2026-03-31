# Laporan Programming Assignment 1: Basic C++
## Putra Nasa Anang Marello 5024251081

### Deskripsi Program
 
Program ini dibuat menggunakan bahasa C++ untuk menghitung **usia seseorang** berdasarkan tanggal lahir yang diinputkan. Program menerima input berupa tanggal lahir dalam format `DD/MM/YYYY`, kemudian menghasilkan tiga informasi utama:
 
1. **Usia dalam tahun**
2. **Usia dalam bulan**
3. **Nama hari dari tanggal lahir tersebut** (dalam Bahasa Indonesia)
 
---
 
### Fungsi-Fungsi yang Diimplementasikan
 
### 1. `yearsOld(tm* inputTgl, tm* currentTgl)`
 
Menghitung usia dalam **tahun penuh**. Caranya dengan mengurangkan tahun lahir dari tahun sekarang, lalu dikurangi 1 apabila ulang tahun di tahun ini belum terjadi (bulan atau hari belum terlewati).
 
```cpp
int yearsOld(tm* inputTgl, tm* currentTgl)
{
    int years = (currentTgl->tm_year + 1900) - (inputTgl->tm_year + 1900);
 
    if (currentTgl->tm_mon < inputTgl->tm_mon ||
       (currentTgl->tm_mon == inputTgl->tm_mon && currentTgl->tm_mday < inputTgl->tm_mday))
    {
        years--;
    }
 
    return years;
}
```
 
### 2. `monthsOld(tm* inputTgl, tm* currentTgl)`
 
Menghitung usia dalam **total bulan**. Selisih tahun dikonversi ke bulan (dikali 12), ditambah selisih bulan, lalu dikurangi 1 apabila hari ulang tahun di bulan ini belum tercapai.
 
```cpp
int monthsOld(tm* inputTgl, tm* currentTgl)
{
    int months = ((currentTgl->tm_year + 1900) - (inputTgl->tm_year + 1900)) * 12;
    months += (currentTgl->tm_mon) - (inputTgl->tm_mon);
 
    if (currentTgl->tm_mday < inputTgl->tm_mday)
    {
        months--;
    }
 
    return months;
}
```
 
### 3. `dayOfDate(tm* inputTgl)`
 
Mengembalikan **nama hari** dari tanggal lahir yang diinputkan. Fungsi `mktime()` digunakan untuk mengisi field `tm_wday` secara otomatis, kemudian dipetakan ke nama hari dalam Bahasa Indonesia.
 
```cpp
string dayOfDate(tm* inputTgl)
{
    inputTgl->tm_hour = 0;
    inputTgl->tm_min  = 0;
    inputTgl->tm_sec  = 0;
    inputTgl->tm_isdst = -1;
    mktime(inputTgl);
 
    string hariList[] = {"Minggu", "Senin", "Selasa", "Rabu", "Kamis", "Jumat", "Sabtu"};
    return hariList[inputTgl->tm_wday];
}
```
 
---
 
### Contoh Input dan Output
 
Format input: `DD/MM/YYYY`  
Format output: `[usia tahun] [usia bulan] [nama hari tanggal lahir]`
 
| Input (Tanggal Lahir) | Output             | Keterangan                          |
|-----------------------|--------------------|-------------------------------------|
| `01/01/2000`          | `26 314 Sabtu`     | Lahir 1 Januari 2000, hari Sabtu    |
| `17/08/1945`          | `80 967 Jumat`     | Lahir 17 Agustus 1945, hari Jumat   |
| `29/02/2000`          | `26 313 Selasa`    | Lahir 29 Februari 2000, hari Selasa |
| `31/12/1999`          | `26 315 Jumat`     | Lahir 31 Desember 1999, hari Jumat  |
 
> **Catatan:** Output di atas dihitung berdasarkan tanggal sistem saat program dijalankan.
 
---
 
### Library yang Digunakan
 
| Library       | Kegunaan                                              |
|---------------|-------------------------------------------------------|
| `<iostream>`  | Input/output standar (`cin`, `cout`)                  |
| `<string>`    | Tipe data dan operasi string                          |
| `<ctime>`     | Struktur `tm`, fungsi `time()`, `localtime()`, `mktime()` |
| `<sstream>`   | Parsing string input tanggal dengan `stringstream`    |
 
---
 
### Cara Menjalankan
 
```bash
# Kompilasi
g++ -o program src/main.cpp
 
# Jalankan
echo "DD/MM/YYYY" | ./program
# atau
./program
# kemudian ketik tanggal dalam format DD/MM/YYYY
```
 
