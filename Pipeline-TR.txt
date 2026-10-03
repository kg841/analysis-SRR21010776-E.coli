# 1. Adım: Dosya oluşturma ve içine girme
mkdir -p analizEColi && cd analizEColi

# 2. Adım: Ham veriyi SRA veritabanından indirme (SRR..)
prefetch SRR21010776
# (Not: fastq-dump veya fasterq-dump komutu ile SRA formatındaki ham veri FASTQ'ya dönüştürülür
fasterq-dump SRR21010776.sra --split-files


# 3. Adım: Ham veriler için Kalite Kontrol (FastQC)
# (Okumaların ham kalitesini, adapter varlığını ve GC oranını raporlar)
fastqc SRR21010776_1.fastq SRR21010776_2.fastq


# 4. Adım: Kalite Kontrol ve Temizleme (fastp)
# (Düşük kaliteli bazları ve hatalı okumaları temizler, ileri analiz için filtreler)
fastp -i SRR21010776_1.fastq -I SRR21010776_2.fastq -o temiz_1.fastq -O temiz_2.fastq --html fastp_rapor.html --json fastp_rapor.json



# 5. Adım: E.coli için referans genomunu NCBI'dan indir ve aç
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_cds_from_genomic.fna.gz
gunzip GCF_000005845.2_ASM584v2_cds_from_genomic.fna.gz
mv GCF_000005845.2_ASM584v2_cds_from_genomic.fna referans.fasta


# 6. Adım: Referans genomu indexle (BWA ve Samtools için)
bwa index referans.fasta
samtools faidx referans.fasta


# 7. Adım: BWA MEM ile Referansa Hizalama (Temizlenmiş fastq dosyaları kullanılır)
bwa mem referans.fasta temiz_1.fastq > hizalama.sam


# 8. Adım: SAM formatını BAM formatına çevir, koordinata göre sırala ve indexle
samtools view -bS hizalama.sam | samtools sort -o hizalama_sirali.bam
samtools index hizalama_sirali.bam


# 9. Adım: Bcftools ile Varyant Çağırma (Variant Calling)
bcftools mpileup -f referans.fasta hizalama_sirali.bam | bcftools call -mv -Ob -o varyantlar.bcf


# 10. Adım: Tablolaştırma (BCF dosyasını CSV formatına dönüştürme)
bcftools query -f '%CHROM\t%POS\t%REF\t%ALT\t%QUAL\n' varyantlar.bcf | tr '\t' ',' > varyantlar.csv

echo "Tebrikler! Uçtan uca tüm pipeline başarıyla tamamlandı ve varyantlar.csv klasöründe hazır!"
