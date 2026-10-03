# analysis-SRR21010776-E.coli

##E. coli Whole-Genome Variant Analysis
Bu proje, E. coli genomuna ait SRR21010776 numaralı ham dizileme verisinin kullanılarak kalite kontrolü, temizlenmesi, referans genoma hizalanması ve varyantların belirlenmesi amacıyla gerçekleştirilmiştir.
Çalışmada ham dizileme verisinden başlayarak varyant sonuçlarının CSV formatında elde edilmesine kadar uzanan temel bir biyoinformatik analiz pipeline'ı uygulanmıştır.

 Çalışmanın Amacı
Bu çalışmanın temel amacı, SRR21010776 accession numarasıyla tanımlanan E. coli dizileme verisini analiz ederek referans genomdan farklı olan nükleotid bölgelerini belirlemektir.

Analiz genel olarak şu aşamalardan oluşmaktadır:

Ham veri → Kalite kontrol → Veri temizleme → Referans genom → Hizalama → BAM oluşturma → Varyant çağırma → Sonuçların CSV formatına aktarılması

Kullanılan Veri Analizde NCBI SRA veritabanında bulunan:
SRA Accession: SRR21010776
Organizma: Escherichia coli
Veri tipi: Illumina paired-end dizileme verisi kullanılmıştır.

Ham veri SRA formatından FASTQ formatına dönüştürülerek analizde kullanılmıştır
