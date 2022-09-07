# NCBI igBLAST
## 220907


### link
1. NCBI igBLAST
- description : https://ncbi.github.io/igblast/
- install : https://ftp.ncbi.nih.gov/blast/executables/igblast/release/LATEST/

2. IMGT reference 
- https://www.imgt.org/vquest/refseqh.html#VQUEST

### <br/><br/><br/>

### How to use
1. install
- NCBI igBLAST
```
$ wget https://ftp.ncbi.nih.gov/blast/executables/igblast/release/LATEST/ncbi-igblast-1.19.0-x64-linux.tar.gz
```

### <br/><br/>

2. decompress
```
$ tar -xvf ncbi-igblast-1.19.0-x64-linux.tar.gz
```

### <br/><br/>

3. reference download
```
$ wget -r -np -L https://www.imgt.org/download/V-QUEST/IMGT_V-QUEST_reference_directory/Homo_sapiens/
```

### <br/><br/>

4. makeblastdb (You should make all of each three V, D, J fasta.)
- If you analyze whole IG chain or TCR, then merge each V, D, J fasta in a fasta and then do makeblastdb.
```
$ [igblast_dir]/bin/edit_imgt_file.pl [reference_dir]/Homo_sapiens/IG/IGHJ.fasta > human_gl_J.fasta
$ [igblast_dir]/bin/makeblastdb -parse_seqids -dbtype nucl -in human_gl_J.fasta
```

### <br/><br/>

5. igblastn (for nucleotide)
```
[igblast_dir]/bin/igblastn -germline_db_V database/human_gl_V.fasta -germline_db_J database/human_gl_J.fasta -germline_db_D database/human_gl_D.fasta -organism human -query test/test.fasta -auxiliary_data optional_file/human_gl.aux -show_translation > igblast_test.txt
```
#### test.fasta
```
>IGHV1-18*01_test
caggttcagctggtgcagtctggagctgaggtgaagaagcctggggcctcagtgaag
gtctcctgcaaggcttctggttacacctttaccagctatggtatcagc
tgggtgcgacaggcccctggacaagggcttgagtggatgggatggatcagcgcttac
aatggtaacacaaactatgcacagaagctccagggcagagtcaccatgaccaca
gacacatccacgagcacagcctacatggagctgaggagcctgagatctgacgacacggcc
gtgtattactgtgcgagaga
```

### <br/><br/>

6. result
```
Database: human_gl_V.fasta; human_gl_D.fasta; human_gl_J.fasta
           479 sequences; 125,262 total letters



Query= IGHV1-18*01_test

Length=296
                                                                                                      Score     E
Sequences producing significant alignments:                                                          (Bits)  Value

IGHV1-18*01                                                                                           463     1e-132
IGHV1-18*03                                                                                           459     1e-131
IGHV1-18*04                                                                                           459     1e-131


Domain classification requested: imgt


V-(D)-J rearrangement summary for query sequence (Top V gene match, Top D gene match, Top J gene match, Chain type, stop codon, V-J frame, Productive, Strand, V Frame shift).  Multiple equivalent top matches, if present, are separated by a comma.
IGHV1-18*01	N/A	N/A	VH	No	N/A	N/A	+	N/A

V-(D)-J junction details based on top germline gene matches (V end, V-D junction, D region, D-J junction, J start).  Note that possible overlapping nucleotides at VDJ junction (i.e, nucleotides that could be assigned to either rearranging gene) are indicated in parentheses (i.e., (TACT)) but are not included under the V, D, or J gene itself
AGAGA	N/A	N/A	N/A	N/A	

Alignment summary between query and top germline V gene hit (from, to, length, matches, mismatches, gaps, percent identity)
FR1-IMGT	1	75	75	75	0	0	100
CDR1-IMGT	76	99	24	24	0	0	100
FR2-IMGT	100	150	51	51	0	0	100
CDR2-IMGT	151	174	24	24	0	0	100
FR3-IMGT	175	288	114	114	0	0	100
CDR3-IMGT (germline)	289	296	8	8	0	0	100
Total	N/A	N/A	296	296	0	0	100


Alignments

                                       <--------------------------------FR1-IMGT---------------------------------><-------CDR1-IM
                                        Q  V  Q  L  V  Q  S  G  A  E  V  K  K  P  G  A  S  V  K  V  S  C  K  A  S  G  Y  T  F  T 
                     Query_1      1    CAGGTTCAGCTGGTGCAGTCTGGAGCTGAGGTGAAGAAGCCTGGGGCCTCAGTGAAGGTCTCCTGCAAGGCTTCTGGTTACACCTTTACC  90
V  100.0% (296/296)  IGHV1-18*01  1    ..........................................................................................  90
                                        Q  V  Q  L  V  Q  S  G  A  E  V  K  K  P  G  A  S  V  K  V  S  C  K  A  S  G  Y  T  F  T 
V  99.7% (295/296)   IGHV1-18*03  1    ..........................................................................................  90
V  99.7% (295/296)   IGHV1-18*04  1    ..........................................................................................  90

                                       GT------><--------------------FR2-IMGT---------------------><-------CDR2-IMGT------><-----
                                        S  Y  G  I  S  W  V  R  Q  A  P  G  Q  G  L  E  W  M  G  W  I  S  A  Y  N  G  N  T  N  Y 
                     Query_1      91   AGCTATGGTATCAGCTGGGTGCGACAGGCCCCTGGACAAGGGCTTGAGTGGATGGGATGGATCAGCGCTTACAATGGTAACACAAACTAT  180
V  100.0% (296/296)  IGHV1-18*01  91   ..........................................................................................  180
                                        S  Y  G  I  S  W  V  R  Q  A  P  G  Q  G  L  E  W  M  G  W  I  S  A  Y  N  G  N  T  N  Y 
V  99.7% (295/296)   IGHV1-18*03  91   ..........................................................................................  180
V  99.7% (295/296)   IGHV1-18*04  91   .....C....................................................................................  180

                                       -----------------------------------------------FR3-IMGT-----------------------------------
                                        A  Q  K  L  Q  G  R  V  T  M  T  T  D  T  S  T  S  T  A  Y  M  E  L  R  S  L  R  S  D  D 
                     Query_1      181  GCACAGAAGCTCCAGGGCAGAGTCACCATGACCACAGACACATCCACGAGCACAGCCTACATGGAGCTGAGGAGCCTGAGATCTGACGAC  270
V  100.0% (296/296)  IGHV1-18*01  181  ..........................................................................................  270
                                        A  Q  K  L  Q  G  R  V  T  M  T  T  D  T  S  T  S  T  A  Y  M  E  L  R  S  L  R  S  D  D 
V  99.7% (295/296)   IGHV1-18*03  181  ..........................................................................................  270
V  99.7% (295/296)   IGHV1-18*04  181  ..........................................................................................  270

                                       ----------------->        
                                        T  A  V  Y  Y  C  A  R   
                     Query_1      271  ACGGCCGTGTATTACTGTGCGAGAGA  296
V  100.0% (296/296)  IGHV1-18*01  271  ..........................  296
                                        T  A  V  Y  Y  C  A  R   
V  99.7% (295/296)   IGHV1-18*03  271  .T........................  296
V  99.7% (295/296)   IGHV1-18*04  271  ..........................  296


Lambda      K        H
    1.10    0.333    0.549 

Gapped
Lambda      K        H
    1.08    0.280    0.540 

Effective search space used: 30154093

Total queries = 1
Total identifiable CDR3 = 0
Total unique clonotypes = 0



  Database: human_gl_V.fasta
    Posted date:  Sep 7, 2022  11:08 AM
  Number of letters in database: 123,491
  Number of sequences in database:  422

  Database: human_gl_D.fasta
    Posted date:  Sep 7, 2022  11:12 AM
  Number of letters in database: 1,070
  Number of sequences in database:  44

  Database: human_gl_J.fasta
    Posted date:  Sep 7, 2022  11:13 AM
  Number of letters in database: 701
  Number of sequences in database:  13



Matrix: blastn matrix 1 -1
Gap Penalties: Existence: 4, Extension: 1

```
