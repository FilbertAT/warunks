# Tugas 2
## Implementasi Checklist Tugas 2 Secara Step-By-Step.
a. Membuat sebuah proyek Django baru. 
- Membuat repositori di GitHub, membuat direktori baru secara lokal, dan menghubungkan keduanya.
- Mengakses alamat direktori lokal tersebut pada _command_ _prompt_ dan mengaktifkan _virtual_ _environment_ pada command prompt untuk mengisolasi _dependencies_ atau _requirements_ yang akan di-_install_.
- Meng-_install_ _dependencies_.
- Membuat sebuah proyek Django baru dengan nama `warunks`. Perintah yang digunakan adalah `django-admin startproject warunks .`.
- Menambahkan daftar host yang diizinkan untuk mengakses aplikasi web saya nantinya, saya bisa menjalankan server Django dan melakukan pengecekan apakah proyek Django tersebut telah berhasil dibuat (ditandai dengan adanya animasi roket pada tampilannya).

b. Membuat aplikasi dengan nama `main` pada proyek tersebut.
- Perlu memastikan untuk tetap mengaktifkan virtual environment agar dapat menggunakan dependencies yang sesuai dari proyek ini
- Jalankan perintah `python manage.py startapp main` yang akan membuat direktori baru bernama `main` dengan isinya adalah struktur awal dari aplikasi Django saya.

c. Melakukan _routing_ pada proyek agar dapat menjalankan aplikasi `main`.
- Aplikasi `main` perlu didaftarkan dalam list `INSTALLED_APPS` pada pengaturan (`settings.py`) proyek Django `warunks` sebagai salah satu aplikasi yang terinstal atau akan digunakan pada proyek nanti.
- Lalu, mendaftarkan `localhost` dan `127.0.0.1` ke dalam list `ALLOWED_HOSTS` pada file pengaturan yang sama.
- Buat folder `templates` dalam direktori `main` dan tambahkan file `main.html` sebagai visual dari `website` nantinya.

d. Membuat model pada aplikasi `main` dengan nama `Product` dan memiliki atribut wajib `name`, `price`, `description`.
- Hal yang dilakukan adalah dengan menambahkan model (_class_) baru dengan atribut-atribut sesuai ketentuan tugas.
- Saya pun menambahkan _field_-_field_ atau atribut baru yang disesuaikan dengan rencana pengembangan dari proyek ini sendiri.
- Setelah model berhasil dibuat, saya lakukan migrasi model sehingga Django juga dapat memperbarui struktur tabel dari basis data proyek. Proses migrasi dilakukan dengan dua tahapan yaitu: pembuatan migrasi modelnya `python manage.py makemigrations` dan penerapan migrasi tersebut dengan `python manage.py migrate`.

e.Membuat sebuah fungsi pada `views.py` untuk dikembalikan ke dalam sebuah template HTML yang menampilkan nama aplikasi serta nama dan kelas kamu.
- Edit `views.py` dalam direktori `main` dengan mengimpor fungsi `render` dari Django.
- Tambahkan metode `show_main` dengan parameter `request`.
- Buat dictionary yang berisi kunci dan nilai yang mewakili atribut yang dibuat pada `models.py`.
- Mengembalikan respons menggunakan return method `render` dengan parameter `request`, `'main.html'`, dan dictionary tersebut sebagai konteks.

f. Membuat sebuah routing pada `urls.py` aplikasi main untuk memetakan fungsi yang telah dibuat pada `views.py`.
- Isi `urls.py` dengan kode berikut:
    ```python
    from django.urls import path
    from main.views import show_main

    app_name = 'main'

    urlpatterns = [
        path('', show_main, name='show_main'),
    ]
    ```

- Isi juga urls.py di folder proyek dengan mengimport `include` dan menambahkan `path('', include('main.urls'))`, pada `urlpatterns`.

g.  Melakukan deployment ke PWS terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet.
- Membuat proyek baru dengan nama `warunks`.
- Menyimpan `Project` `Credentials`.
- Menambahkan URL _deployment_ PWS dalam list `ALLOWED_HOSTS` pada  `settings.py` di proyek ini.
- Menjalankan perintah yang terdapat pada informasi Project Command pada halaman PWS.

## Bagan yang berisi request client ke web aplikasi berbasis Django beserta responnya dan Penjelasan kaitan antara `urls.py`, `views.py`, `models.py`, dan berkas `html`
![Bagan](https://github.com/FilbertAT/warunks/blob/main/images/bagan.png)

**Client (Pengguna)**
   - Pengguna mengakses aplikasi web melalui browser dengan mengirimkan **HTTP Request** ke URL utama (`/`).

**urls.py**
   - Request tersebut diterima oleh `urls.py` yang bertugas mengarahkan request ke fungsi yang sesuai berdasarkan URL yang diminta. Dalam kasus ini, URL utama (`/`) diarahkan ke fungsi `show_main` di `views.py`.

**views.py**
   - Fungsi `show_main` mengelola logika untuk menyiapkan dan mengirimkan data yang diperlukan untuk ditampilkan. Fungsi ini menggunakan data yang telah didefinisikan dalam **context** untuk mengambil informasi yang relevan.

**models.py**
   - `models.py` berisi definisi model data yang digunakan untuk struktur data aplikasi dan interaksi dengan database.

**Templates**
   - Data yang telah diproses dikirim ke template `main.html` yang bertindak sebagai lapisan presentasi. `views.py` mengisi template dengan data yang relevan, yang kemudian di-render menjadi halaman HTML.

**Response**
   - Halaman HTML yang telah di-render dikirim kembali ke client sebagai **HTTP Response**, menampilkan webpage yang diminta.


## Jelaskan fungsi git dalam pengembangan perangkat lunak!
### _Version Control_
Git memungkinkan pelacakan perubahan kode secara detil, menyediakan akses mudah ke riwayat pengeditan lengkap termasuk detail siapa yang membuat perubahan dan kapan. Ini sangat berguna untuk memahami pengembangan dari proyek perangkat lunak kita dan mengelola modifikasi-modifikasinya.

### Kolaborasi
Dengan Git, pengembang dapat bekerja bersama dengan lebih efektif. Git mendukung kolaborasi yang mulus dengan memperbolehkan pengembang untuk bekerja di cabang (_branches_) terpisah tanpa mengganggu alur kerja utama, yang kemudian dapat digabungkan (_merged_) dengan aman.

### _Backup_
Dalam kasus adanya kesalahan atau kebutuhan untuk kembali ke versi sebelumnya, Git menyediakan mekanisme untuk mengembalikan kode ke status sebelumnya melalui _commit_, _reset_, dan _checkout_, sehingga berfungsi sebagai sistem pencadangan yang efisien.

### Review Kode
Git mendukung praktik review kode yang memungkinkan tim untuk memeriksa dan memberikan umpan balik terhadap perubahan kode sebelum diintegrasikan ke dalam cabang utama, sehingga dapat meningkatkan kualitas kode dan meminimalkan bug.

### _Deployment_
Git juga memfasilitasi proses deployment dengan memperbolehkan pengembang untuk mengirimkan kode mereka ke server produksi atau tahapan melalui operasi push dan pull, memastikan bahwa perubahan dapat diterapkan secara efisien.

## Menurut Anda, dari semua framework yang ada, mengapa framework Django dijadikan permulaan pembelajaran pengembangan perangkat lunak?
### Struktur Framework Django
Django menerapkan struktur Model-View-Template (MVT), yang memudahkan pemula untuk memahami pentingnya arsitektur yang terstruktur dalam pengembangan perangkat lunak. Struktur ini membantu dalam mengorganisasi kode dan memisahkan logika aplikasi dari presentasi tampilan pengguna.

### _Programmer Friendly_
Django juga dapat dibilang sebuah framework yang _programmer_ _friendly_ karena dilengkapi dengan berbagai fitur bawaan yang signifikan, seperti autentikasi, pengelolaan database, dan panel administrasi yang lengkap. Fitur-fitur ini memungkinkan bahkan untuk _programmer_ pemula untuk berfokus pada pembelajaran konsep dasar pengembangan web tanpa harus mendalaminya dari awal.

### Keamanan
Dari segi keamanan, Django menawarkan mekanisme perlindungan terhadap ancaman umum seperti _Cross_ _Site_ _Request_ _Forgery_ (CSRF), SQL _injection_, dan _Cross-Site_ _Scripting_ (XSS). Ini menunjukkan kepada pemula pentingnya aspek keamanan dalam pengembangan web.

### Skalabilitas
Django juga dirancang untuk skalabilitas, yang memungkinkan aplikasi yang dibuat dengan Django untuk tumbuh dan beradaptasi dengan kebutuhan yang lebih besar dan lebih kompleks seiring waktu. Terakhir, Django menyediakan _Object-Relational_ _Mapping_ (ORM) bawaan yang memfasilitasi interaksi dengan database secara lebih intuitif, menghindari kebutuhan untuk penulisan SQL mentah yang bisa menjadi tantangan bagi pemula. Faktor-faktor ini menjadikan Django sebagai platform yang sangat cocok untuk memulai pembelajaran dalam bidang pengembangan aplikasi web.

## Mengapa model pada Django disebut sebagai ORM?
Model pada Django disebut sebagai ORM (Object-Relational Mapping_) karena memungkinkan interaksi dengan database menggunakan objek Python, tanpa perlu menulis SQL secara langsung. ORM menjembatani perbedaan antara basis data relasional dan pemrograman berorientasi objek, memudahkan pengembang untuk fokus pada logika aplikasi sambil mengurangi kompleksitas dan kesalahan.

# Tugas 3
## Jelaskan mengapa kita memerlukan _data delivery_ dalam pengimplementasian sebuah platform?
Beberapa hal yang menjadi alasan mengapa kita memerlukan _data delivery_ dalam pengimplementasian sebuah platform adalah:
- _Data delivery_ memungkinkan platform untuk mengirimkan data dalam bentuk XML atau JSON yang kemudian akan ditampilkan atau juga diolah kembali pada aplikasi pengguna. 
- Selain mampu mengirimkan, _data delivery_ yang baik juga memastikan hanya data yang dibutuhkan (di-_request_) oleh klien yang dikirimkan ke klien, sehingga mengurangi _overhead_, mempercepat _loading time_, dan melindungi data lainnya. Hal ini juga akan meningkatkan kepuasan pengguna dan efektivitas penggunaan platform.
- _Data delivery_ memudahkan integrasi sistem dengan sistem lain, termasuk juga berkomunikasi dengan third-party _services_ dan APIs_ lainnya karena dapat memastikan bahwa data yang diperlukan dapat ditransfer antar sistem dengan lancar.
- Data delivery yang dirancang dengan baik juga akan memungkinkan pengiriman data secara aman, yang penting terutama untuk platform yang mengelola data sensitif.

## Menurutmu, mana yang lebih baik antara XML dan JSON? Mengapa JSON lebih populer dibandingkan XML?
Pemilihan antara XML (eXtensible Markup Language) dan JSON (JavaScript Object Notation) seringkali bergantung pada kebutuhan spesifik dari sebuah aplikasi atau platform. Namun, secara umum, seiring berjalannya waktu, JSON telah menjadi lebih populer daripada XML. Setelah menanyakan hal ini kepada 2 developer yang saya kenal, mereka sudah tidak lagi menggunakan XML, melainkan hanya JSON, sehingga membuat saya semakin yakin bahwa JSON lebih baik dari XML. Untuk beberapa alasan pendukungnya, saya juga akan merincikan hasil penelusuran saya di internet akan mengapa JSON lebih baik dari XML:
- JSON memiliki sintaks yang lebih sederhana dan ringkas dibandingkan XML. Bentuknya mudah dibaca dan ditulis manusia namun juga mudah untuk diparsing oleh mesin, hal ini membuat JSON menjadi format yang efisien untuk transfer data.
- Banyak teknologi modern dan API web mendukung JSON secara native. Hal ini membuatnya menjadi pilihan yang lebih mudah untuk diintegrasikan dalam berbagai platform dan bahasa pemrograman. Salah satunya, JSON sudah secara alami terintegrasi dengan JavaScript, sehingga menjadikannya pilihan yang sangat baik untuk pengembangan web.

## Jelaskan fungsi dari method `is_valid()` pada form Django dan mengapa kita membutuhkan method tersebut?
Method `is_valid()` pada form Django adalah fungsi yang digunakan untuk melakukan validasi data yang dikirimkan pengguna melalui form. Fungsi ini memeriksa apakah data yang masuk sesuai dengan kriteria yang telah ditentukan dalam definisi form, seperti tipe data, lalu apakah _field_ tersebut wajib diisi atau tidak (required fields), dan batasan - batasan lain yang kita (_developer_) tetapkan dalam validasi. `is_valid()` sangat penting karena ia memastikan bahwa data yang masuk ke dalam sistem aman dan dapat diproses tanpa menimbulkan error.

## Mengapa kita membutuhkan `csrf_token` saat membuat form di Django? Apa yang dapat terjadi jika kita tidak menambahkan `csrf_token` pada form Django? Bagaimana hal tersebut dapat dimanfaatkan oleh penyerang?
Kita membutuhkan `csrf_token` saat membuat form di Django untuk mencegah serangan Cross-Site Request Forgery (CSRF), di mana penyerang bisa memanipulasi pengguna yang sah untuk melakukan aksi tidak diinginkan di aplikasi web saat pengguna tersebut masih terautentikasi. Jika `csrf_token` tidak ditambahkan pada form Django, aplikasi menjadi rentan terhadap serangan tersebut. Penyerang dapat membuat permintaan berbahaya, seperti mengubah kata sandi atau mengirim email palsu, yang tampak berasal dari pengguna yang sah, karena aplikasi kita tidak dapat memverifikasi bahwa permintaan tersebut benar-benar berasal dari pengguna tersebut.

## Step-by-step Implementasi Checklist Tugas 3
1) Saya membuat direktori bernama `templates` di direktori utama proyek dan menambahkan sebuah berkas HTML baru yang saya namakan `base.html`. Berkas `base.html` ini saya isi sebagai template dasar yang berfungsi sebagai kerangka untuk halaman - halaman web lain dalam proyek `warunks` saya. Hal ini memungkinkan konsistensi dan efisiensi dalam pengembangan halaman web selanjutnya, karena semua halaman dapat mengadopsi struktur dan desain yang serupa dengan mengacu pada template dasar ini.
   ```python
   {% load static %}
   <!DOCTYPE html>
   <html lang="en">
   <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      {% block meta %} {% endblock meta %}
   </head>

   <body>
      {% block content %} {% endblock content %}
   </body>
   </html>
   ```

   Saya juga memasukkan template HTML dasar tersebut ke dalam pengaturan TEMPLATES di `/warunks/settings.py` agar Django dapat me-_recognize_ template tersebut. Kemudian, saya memodifikasi `main.html` yang berada di `/main/templates` untuk meng-extend `base.html`. Langkah ini bertujuan untuk mempersingkat kode HTML yang perlu saya tulis di setiap halaman web, mempercepat proses pengembangan dan memastikan konsistensi tampilan seluruh halaman.

2) Lalu, saya membuat sebuah input form dengan nama `ProductEntryForm` untuk menambahkan objek model `Product` pada app saya, `warunks`.
   ```python
   class ProductEntryForm(ModelForm):
      class Meta:
         model = ProductEntry
         fields = ["name", "price", "category", "description"]
   ```

   Di `views.py`, `ProductEntryForm` yang telah saya buat akan saya gunakan untuk merender form ke halaman `/create-product-entry`. Ini memastikan bahwa form tersebut dapat diakses dan digunakan untuk membuat data produk baru ke dalam _database_.
   ```python
   def create_product_entry(request):
      form = ProductEntryForm(request.POST or None)

      if form.is_valid() and request.method == "POST":
         form.save()
         return redirect('main:show_main')

      context = {'form': form}
      return render(request, "create_product_entry.html", context)
   ```

   Saya telah membuat sebuah file HTML baru yang bernama `create_product_entry.html` dalam direktori `/main/templates` untuk halaman `/create-product-entry`. Ini memfasilitasi pembuatan halaman web yang akan digunakan untuk menambahkan produk baru melalui form yang disediakan.
   ```python
   {% extends 'base.html' %} 
   {% block content %}
   <h1>Add New Product Entry</h1>

   <form method="POST">
   {% csrf_token %}
   <table>
      {{ form.as_table }}
      <tr>
         <td></td>
         <td>
         <input type="submit" value="Add Product Entry" />
         </td>
      </tr>
   </table>
   </form>

   {% endblock %}
   ```

   Kemudian, saya memasukkan url `create-product-entry` ke dalam `urls.py` yang terletak di direktori `/main`, sehingga form tersebut dapat ditampilkan pada halaman `/create-product-entry`. Ini mengatur jalur akses untuk memastikan bahwa form dapat diakses melalui URL yang ditentukan.

3) Saya juga memperbarui `main.html` yang terletak di `/main/templates` dengan menambahkan sebuah tombol yang mengarah ke halaman `/create-product-entry` agar form tersebut mudah diakses. Selain itu, saya menambahkan sebuah tabel yang menampilkan data dari model Product yang sudah tersimpan di _database_. Untuk memastikan data tersebut dapat ditampilkan di tabel, saya mengubah context di fungsi `show_main` yang ada di `views.py`.
   ```python
   context = {
      'name': 'Filbert',
      'class': 'PBP C',
      'npm': '2306152336',
      'product_entries': ProductEntry.objects.all()
   }
   ```

   Produk-produk ini akan ditangkap oleh `main.html` dan diiterasi untuk ditampilkan dalam bentuk tabel, di mana saya menggunakan looping untuk menambahkan setiap baris data ke dalam tabel tersebut.
   ```python
   {% for product_entry in product_entries %} ... {% endfor %}
   ```

4) Akhirnya, saya menambahkan empat fungsi baru di `views.py` yang bertujuan untuk mengirimkan response dalam format XML dan JSON, baik untuk data keseluruhan maupun data spesifik berdasarkan ID. Fungsi-fungsi ini memungkinkan penggunaan endpoint seperti `xml/[id]` dan `json/[id]` selain yang paling sederhana `/xml` dan `/json` untuk mengakses data sesuai dengan format yang diinginkan.
   ```python
   def show_xml(request):
      data = ProductEntry.objects.all()
      return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

   def show_json(request):
      data = ProductEntry.objects.all()
      return HttpResponse(serializers.serialize("json", data), content_type="application/json")

   def show_xml_by_id(request, id):
      data = ProductEntry.objects.filter(pk=id)
      return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

   def show_json_by_id(request, id):
      data = ProductEntry.objects.filter(pk=id)
      return HttpResponse(serializers.serialize("json", data), content_type="application/json")
   ```

   Selanjutnya, saya mengatur _routing_ untuk masing-masing fungsi tersebut di `urls.py` yang terletak di direktori `/main`, untuk memastikan bahwa setiap fungsi dapat diakses melalui URL yang sesuai.
   ```python
   urlpatterns = [
      path('', show_main, name='show_main'),
      path('create-product-entry', create_product_entry, name='create_product_entry'),
      path('xml/', show_xml, name='show_xml'),
      path('json/', show_json, name='show_json'),
      path('xml/<str:id>/', show_xml_by_id, name='show_xml_by_id'),
      path('json/<str:id>/', show_json_by_id, name='show_json_by_id'),
   ]
   ```

   ## Screenshot Postman
   ### `/xml`
   ![xml](https://github.com/FilbertAT/warunks/blob/main/images/xml.png)

   ### `/json`
   ![json](https://github.com/FilbertAT/warunks/blob/main/images/json.png)

   ### `xml/[id]`
   ![xml/[id]](https://github.com/FilbertAT/warunks/blob/main/images/xml_id.png)

   ### `json/[id]`
   ![json/[id]](https://github.com/FilbertAT/warunks/blob/main/images/json_id.png)


# Tugas 4
## Apa perbedaan antara `HttpResponseRedirect()` dan `redirect()`
Dalam pengembangan web menggunakan Django, terdapat dua cara yang umum digunakan untuk mengarahkan pengguna ke halaman lain dari halaman yang sedang mereka berada yaitu `HttpResponseRedirect()` dan `redirect()`. `HttpResponseRedirect()` merupakan kelas di Django yang digunakan secara eksplisit untuk mengirim respons HTTP 302, yang memberi tahu browser untuk mengarahkan ke URL yang ditentukan, sehingga <u>diperlukan URL lengkap sebagai inputnya</u>. Sebaliknya, `redirect()` adalah cara yang lebih fleksibel dan sederhana untuk melakukan _redirecting_ atau pengalihan halaman dalam aplikasi Django. Fungsi ini dapat menerima objek model, nama view, atau URL sebagai argumen dan secara otomatis menghasilkan HttpResponseRedirect atau HttpResponsePermanentRedirect sesuai pada kebutuhan.

## Jelaskan cara kerja penghubungan model `Product` dengan `User`!
Pada file `models.py` di folder `main`, dalam model `ProductEntry`, terdapat atribut bernama `user` yang menggunakan `ForeignKey(User, on_delete=models.CASCADE)`. Foreign key ini menghubungkan setiap `ProductEntry` dengan satu `User`, sehingga setiap produk yang dibuat akan menyimpan referensi ke pengguna terkait melalui foreign key tersebut. Dengan demikian, satu produk hanya dapat dimiliki oleh satu pengguna, sementara satu pengguna dapat memiliki banyak produk (`ProductEntry`).


## Apa perbedaan antara authentication dan authorization, apakah yang dilakukan saat pengguna login? Jelaskan bagaimana Django mengimplementasikan kedua konsep tersebut.
1. <b>Authentication (Otentikasi)</b> adalah proses untuk memverifikasi identitas pengguna. Ini biasanya dilakukan dengan meminta kredensial seperti username dan password. Dengan kata lain, authentication menjawab pertanyaan: <em>"Apakah Anda benar-benar adalah orang yang Anda klaim?"</em>

   Contoh: Saat seseorang memasukkan email dan password ke dalam form login, sistem akan memeriksa apakah data tersebut sesuai dengan yang ada di database.

2. <b>Authorization (Otorisasi)</b> adalah proses yang terjadi setelah identitas pengguna terverifikasi melalui authentication, authorization menentukan hak akses yang dimiliki oleh pengguna tersebut. Ini menjawab pertanyaan: <em>"Apakah Anda memiliki izin untuk mengakses sumber daya ini?"</em>

   Contoh: Setelah login berhasil (authenticated), sistem memeriksa apakah pengguna tersebut diperbolehkan untuk mengakses halaman admin atau melakukan perubahan data (authorized).

Ketika pengguna login, hal yang pertama terjadi adalah proses _authentication_. Ini melibatkan verifikasi identitas pengguna dengan mencocokkan username dan password yang mereka masukkan dengan yang tersimpan di database. Jika cocok, pengguna akan dianggap "_authenticated_" dan _session_ akan dibuatkan untuk mereka, yang berfungsi sebagai tanda bahwa pengguna telah terverifikasi. Setelah pengguna "_authenticated_", sistem kemudian melakukan _authorization_ untuk menentukan halaman atau fungsi apa saja yang bisa diakses oleh pengguna tersebut berdasarkan perannya atau level hak akses yang dimilikinya.

_Authentication_ di Django diimplementasikan melalui modul bawaan yang disebut `django.contrib.auth`. Modul ini menyediakan segala yang dibutuhkan untuk mengelola proses otentikasi, seperti User Model yang akan menyimpan informasi pengguna seperti username, password (yang dienkripsi), email, serta informasi lainnya, lalu modul ini juga menyediakan fungsi-fungsi bawaan lainnya seperti `authenticate()` dan `login()`.

## Bagaimana Django mengingat pengguna yang telah login? Jelaskan kegunaan lain dari cookies dan apakah semua cookies aman digunakan?
Django menggunakan <b>session-based authentication</b> untuk mengingat pengguna yang login. Setelah pengguna berhasil login, Django membuat sesi di server dan mengirimkan <b>session ID</b> melalui _cookies_ ke browser pengguna. Setiap kali pengguna mengakses halaman, _cookies_ ini dikirim kembali ke server, memungkinkan Django memverifikasi pengguna yang telah login. Jika sesi valid, pengguna dianggap masih login.

Selain untuk membantu proses login dari User, beberapa kegunaan _cookies_ lainnya adalah:
- Menyimpan _preferences_ pengguna seperti kami para programmer yang sangat menyukai _dark_ _theme_, preferensi lainnya seperti bahasa.
- Melacak aktivitas pengguna untuk analitik dan pemasaran (Biasanya kita dapat memiliki untuk tidak mengaktifkan _cookies_ ini)
- Fitur "Remember Me" yang dapat mengizinkan pengguna untuk tetap login setelah menutup browser
_
Tidak semua penggunaan _cookies_ juga aman, karena bisa saja _cookies_ yang tidak dienkripsi dan tidak memiliki pengaturan keamanan seperti `HttpOnly` dan `Secure` beresiko diekspos ke serangan seperti XSS (_Cross-Site Scripting_) dimana penyerang dapat mencuri _cookies_ dengan menanamkan skrip (JavaScript biasanya) berbahaya di halaman web. Kemudian jika cookies tidak dienkripsi atau dikirim melalui koneksi HTTP biasa, penyerang dapat mengintip dan mencuri informasi tersebut. Dan jika session ID dalam cookie dicuri, penyerang bisa menggunakan session ID tersebut untuk mengakses akun pengguna yang sedang login.

## Step-by-step Implementasi Checklist Tugas 4
a. Mengimplementasikan fungsi registrasi, login, dan logout untuk memungkinkan pengguna untuk mengakses aplikasi sebelumnya dengan lancar.
- Memodifikasi views.py dengan menambahkan impor `UserCreationForm` dan `messages` untuk menangani form registrasi dan pesan. Lalu, membuat fungsi `register` dan laman templatenya yaitu `register.html` sebagai form registrasi dan tidak lupa menambahkan alamat URL nya pada `urls.py`.
- Memodifikasi `views.py` dengan menambahkan impor `authenticate`, `login`, dan `AuthenticationForm` untuk menangani proses autentikasi dan login. Lalu, membuat fungsi `login_user` dan laman templatenya yaitu `login.html` sebagai form login, serta menambahkan path URL untuk login pada `urls.py`.
- Lagi-lagi memodifikasi `views.py` dengan menambahkan impor `logout` untuk menangani proses logout. Lalu, membuat fungsi `logout_user` dan menambahkan tombol logout pada `main.html`. Terakhir, menambahkan path URL untuk logout pada `urls.py`.

b. Membuat **dua** akun pengguna dengan masing-masing **tiga** dummy data menggunakan model yang telah dibuat pada aplikasi sebelumnya untuk setiap akun **di lokal**.
- Jalankan `python manage.py runserver` di terminal.
- Akses http://localhost:8000/ melalui browser.
- Klik "Register Now" dan buat dua akun pengguna secara terpisah.
- Buat tiga _dummy_ data (_product_ dalam `warunks`) sesuai yang diminta pada kedua akun yang sudah dibuat.

c. Menghubungkan model `Product` dengan `User`.
- Tambahkan impor `User` di `models.py` dan hubungkan `ProductEntry` dengan pengguna menggunakan `ForeignKey` ke `User`.
- Perbarui fungsi `create_product_entry` di `views.py` agar setiap product entry terkait dengan pengguna yang sedang login.
- Ubah fungsi `show_main` di `views.py` untuk hanya menampilkan product entries milik pengguna yang sedang login.
- Simpan perubahan dan jalankan `python manage.py makemigrations`. Pilih opsi 1 saat diminta untuk menetapkan nilai default user dan jalankan `python manage.py migrate` untuk menerapkan perubahan.
- Perbarui `settings.py` dengan menambahkan impor `os` dan ubah variabel `DEBUG` untuk environment production.
- Jalankan server menggunakan `python manage.py runserver`, buat akun baru, dan pastikan hanya product entries pengguna yang login yang ditampilkan.

d. Menampilkan detail informasi pengguna yang sedang _logged in_ seperti _username_ dan menerapkan `cookies` seperti `last login` pada halaman utama aplikasi.
- Tambahkan impor `HttpResponseRedirect`, `reverse`, dan `datetime` ke `views.py`.
- Perbarui fungsi `login_user` untuk menambahkan cookie `last_login` saat pengguna berhasil login.
- Tambahkan `last_login` ke variabel context di fungsi `show_main` untuk menampilkan waktu login terakhir.
- Perbarui fungsi `logout_user` untuk menghapus cookie `last_login` saat logout.
- Tambahkan kode di `main.html` untuk menampilkan detail informasi pengguna yang sedang _logged in_ seperti _username_.
- Jalankan proyek, login, dan cek apakah data `last_login` muncul di halaman utama dan cookie di browser.