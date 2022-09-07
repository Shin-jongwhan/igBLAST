# NCBI igBLAST
## 220907

### How to use
1. install
- NCBI igBLAST
```
$ wget https://ftp.ncbi.nih.gov/blast/executables/igblast/release/LATEST/ncbi-igblast-1.19.0-x64-linux.tar.gz
```

2. decompress
```
$ tar -xvf ncbi-igblast-1.19.0-x64-linux.tar.gz
```

3. reference download
```
$ wget -r -np -L https://www.imgt.org/download/V-QUEST/IMGT_V-QUEST_reference_directory/Homo_sapiens/
```

4. makeblastdb (You should make all of each three V, D, J fasta.)
- If you analyze whole IG chain or TCR, then merge each V, D, J fasta in a fasta and then do makeblastdb.
```
$ [igblast_dir]/bin/edit_imgt_file.pl [reference_dir]/Homo_sapiens/IG/IGHJ.fasta > human_gl_J.fasta
$ [igblast_dir]/bin/makeblastdb -parse_seqids -dbtype nucl -in human_gl_J.fasta
```

5. igblastn (for nucleotide)
```
[igblast_dir]/bin/igblastn -germline_db_V database/human_gl_V.fasta -germline_db_J database/human_gl_J.fasta -germline_db_D database/human_gl_D.fasta -organism human -query test/test.fasta -auxiliary_data optional_file/human_gl.aux -show_translation > igblast_test.txt
```
