
# E. coli Whole-Genome Variant Analysis
### <ins>Çalışma Hakkında </ins>
Bu proje, E. coli genomuna ait [SRR21010776](https://www.ncbi.nlm.nih.gov/sra/?term=SRR21010776) numaralı ham dizileme verisinin kullanılarak kalite kontrolü, temizlenmesi, referans genoma hizalanması ve varyantların belirlenmesi amacıyla gerçekleştirilmiştir.
Çalışmada ham dizileme verisinden başlayarak varyant sonuçlarının CSV formatında elde edilmesine kadar uzanan temel bir biyoinformatik analiz pipeline'ı uygulanmıştır.

### <ins>Çalışmanın Amacı</ins>
Bu çalışmanın temel amacı, [SRR21010776](https://www.ncbi.nlm.nih.gov/sra/?term=SRR21010776) accession numarasıyla tanımlanan E. coli dizileme verisini analiz ederek referans genomdan farklı olan nükleotid bölgelerini belirlemektir.<br>
Analiz genel olarak şu aşamalardan oluşmaktadır:

Ham veri → Kalite kontrol → Veri temizleme → Referans genom → Hizalama → BAM oluşturma → Varyant çağırma → Sonuçların CSV formatına aktarılması
Ham veri → Kalite kontrol → Veri temizleme → Referans genom → Hizalama → BAM oluşturma → Varyant çağırma → CSV


| 1. Veri indirme | Ham verinin SRA'dan alınıp FASTQ formatına çevrilmesi | SRA Toolkit |<br>
| 2. Kalite kontrol | Ham okumaların kalitesinin değerlendirilmesi | FastQC |<br>
| 3. Veri temizleme | Düşük kaliteli okumaların ve adaptörlerin temizlenmesi | fastp |<br>
| 4. Hizalama | Temizlenmiş okumaların referans genoma hizalanması | BWA-MEM |<br>
| 5. BAM işleme | SAM dosyasının BAM'e çevrilmesi, sıralanması ve indekslenmesi | SAMtools |<br>
| 6. Varyant çağırma | Referanstan farklı bölgelerin belirlenmesi ve işlenmesi | BCFtools |<br>


Veri : Analizde [NCBI](https://www.ncbi.nlm.nih.gov/) SRA veritabanında bulunan SRA Accession [SRR21010776](https://www.ncbi.nlm.nih.gov/sra/?term=SRR21010776) numarası<br>
Organizma: Escherichia coli<br>
Veri tipi: Illumina paired-end dizileme verisi kullanılmıştır.<br>

### <ins>Çalışmanın Çıktısı</ins>
Pipeline'ın sonunda E. coli örneğine ait varyantlar belirlenmiş ve [varyantlar.csv](varyantlar.csv) dosyasında tablo halinde sunulmuştur.

### <ins>Kullanılan Araçlar</ins>
**NCBI SRA** — Ham dizileme verisinin elde edilmesi<br>
**SRA Toolkit** — SRA verisinin FASTQ formatına dönüştürülmesi<br>
**FastQC** — Ham veri kalite kontrolü<br>
**fastp** — Okuma temizleme ve kalite kontrolü<br>
**BWA-MEM** — Referans genoma hizalama<br>
**SAMtools** — SAM/BAM dosyalarının işlenmesi<br>
**BCFtools** — Varyant çağırma ve varyant sonuçlarının işlenmesi<br>

<br><br>
**Analiz komutları (Pipeline Aşamaları) [pipline.sh]( pipline.sh) dosyasında yer almaktadır.** <br><br>
[fastp_rapor.html](fastp_rapor.html) dosyası, veri temizleme aşamasında fastp tarafından üretilen kalite raporudur. Temizleme sonrası okumaların %98,17'si korunmuş, Q30 oranı %95,35'ten %96,01'e yükselmiştir.
