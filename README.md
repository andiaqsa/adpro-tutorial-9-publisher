a. How much data your publisher program will send to the message broker in one run?
Program publisher akan mengirimkan total 5 buah pesan (UserCreatedEventMessage) ke message broker dalam satu kali jalan. Hal ini dikarenakan terdapat 5 baris pemanggilan fungsi p.publish_event di dalam fungsi main().

b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
Hal ini berarti Publisher dan Subscriber terhubung ke Message Broker (RabbitMQ) yang sama. Agar komunikasi event-driven berhasil, pengirim dan penerima harus menggunakan broker yang sama sebagai perantara pengiriman pesan.