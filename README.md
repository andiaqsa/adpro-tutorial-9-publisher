a. How much data your publisher program will send to the message broker in one run?
Program publisher akan mengirimkan total 5 buah pesan (UserCreatedEventMessage) ke message broker dalam satu kali jalan. Hal ini dikarenakan terdapat 5 baris pemanggilan fungsi p.publish_event di dalam fungsi main().

b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
Hal ini berarti Publisher dan Subscriber terhubung ke Message Broker (RabbitMQ) yang sama. Agar komunikasi event-driven berhasil, pengirim dan penerima harus menggunakan broker yang sama sebagai perantara pengiriman pesan.

**c. RabbitMQ Management Interface**
Berikut adalah *screenshot* dari RabbitMQ yang sudah berhasil berjalan di komputer saya menggunakan Docker:

![img.png](img.png)

**d. Sending and Processing Event**
Berikut adalah *screenshot* dari terminal saat program dijalankan:

![img_1.png](img_1.png)

**Penjelasan:**
Gambar di atas menunjukkan komunikasi sukses antara *publisher* dan *subscriber* melalui RabbitMQ. Saat saya menjalankan perintah `cargo run` di direktori `publisher`, program tersebut mengirimkan 5 buah event secara beruntun ke RabbitMQ. Karena program `subscriber` sudah saya jalankan sebelumnya dan sedang "mendengarkan" antrean pesan, ia langsung menerima kelima event tersebut secara *real-time* dan mencetaknya di layar konsol, lengkap dengan identitas saya (Andi - 2306275046).

**e. Monitoring Chart Based on Publisher**
Berikut adalah *screenshot* dari grafik "Message rates" pada RabbitMQ setelah *publisher* dijalankan secara berulang:

![img_2.png](img_2.png)

**Penjelasan Lonjakan (Spike):**
Lonjakan (*spike*) tajam yang terlihat pada grafik "Message rates" memiliki korelasi langsung dengan eksekusi program *publisher*. Setiap kali perintah `cargo run` dijalankan, *publisher* secara instan menembakkan 5 *event/message* sekaligus ke *exchange/queue* di RabbitMQ.

RabbitMQ mencatat masuknya paket data secara tiba-tiba ini dan memvisualisasikannya sebagai lonjakan (biasanya terlihat pada garis kuning/Publish). Karena program *subscriber* kita juga sedang aktif merespons (*listening*), RabbitMQ langsung meneruskan pesan tersebut, yang divisualisasikan oleh grafik ungu (Deliver/Consumer ack). Setelah 5 pesan tersebut selesai dikirim dan diterima dalam hitungan milidetik, aktivitas kembali kosong (0.0/s), sehingga grafiknya kembali turun hingga eksekusi `cargo run` berikutnya dilakukan.

