# analysis-SRR21010776-E.coli

// <ins> </ins>

## E. coli Whole-Genome Variant Analysis
### <ins>Çalışma Hakkında </ins>
Bu proje, E. coli genomuna ait SRR21010776 numaralı ham dizileme verisinin kullanılarak kalite kontrolü, temizlenmesi, referans genoma hizalanması ve varyantların belirlenmesi amacıyla gerçekleştirilmiştir.
Çalışmada ham dizileme verisinden başlayarak varyant sonuçlarının CSV formatında elde edilmesine kadar uzanan temel bir biyoinformatik analiz pipeline'ı uygulanmıştır.

### <ins>Çalışmanın Amacı</ins>
Bu çalışmanın temel amacı, [SRR21010776](https://www.ncbi.nlm.nih.gov/sra/?term=SRR21010776) accession numarasıyla tanımlanan E. coli dizileme verisini analiz ederek referans genomdan farklı olan nükleotid bölgelerini belirlemektir.<br>
Analiz genel olarak şu aşamalardan oluşmaktadır:

Ham veri → Kalite kontrol → Veri temizleme → Referans genom → Hizalama → BAM oluşturma → Varyant çağırma → Sonuçların CSV formatına aktarılması

Kullanılan Veri : Analizde [NCBI](https://www.ncbi.nlm.nih.gov/) SRA veritabanında bulunan SRA Accession [SRR21010776](https://www.ncbi.nlm.nih.gov/sra/?term=SRR21010776)<br>
Organizma: Escherichia coli<br>
Veri tipi: Illumina paired-end dizileme verisi kullanılmıştır.<br>

### <ins>Çalışmanın Çıktısı</ins>
Pipeline'ın sonunda E. coli örneğine ait varyantlar belirlenmiş ve varyantlar.csv dosyasında tablo halinde sunulmuştur.

### <ins>Kullanılan Araçlar</ins>
**NCBI SRA** — Ham dizileme verisinin elde edilmesi<br>
**SRA Toolkit** — SRA verisinin FASTQ formatına dönüştürülmesi<br>
**FastQC** — Ham veri kalite kontrolü<br>
**fastp** — Okuma temizleme ve kalite kontrolü<br>
**BWA-MEM** — Referans genoma hizalama<br>
**SAMtools** — SAM/BAM dosyalarının işlenmesi<br>
**BCFtools** — Varyant çağırma ve varyant sonuçlarının işlenmesi<br>



