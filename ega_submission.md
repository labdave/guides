# EGA Submission

The guide provides all the details to submit the research study data to the [EGA].

## What is EGA?
The European Genome-phenome Archive (EGA) is a service for permanent archiving and sharing of all types of personally identifiable genetic and phenotypic data resulting from biomedical research projects. (copied from the EGA website directly).

For more information about EGA, please follow this [link](https://ega-archive.org/).

The account for the lab has already been set up on EGA. You can find the information below:
```
Username: ega-box-611
Password: *******
Centre name: DAVELAB
Submission ID: EGAB00000001134
```
Please contact [Tushar Dave] for the password.

## How to submit the data to EGA?
Please follow the steps listed below to submit the data to `EGA`.

1. Go to [EGA submission website]
2. Login to the Dave Lab account using the credential provided above
3. Click on the New Submission Tab <br>
**Note:** Registering new study, samples, read data consider as a new submission every time. Once, you are done with one of their submission, hit New Submission button to initiate submission for the next one.
4. Register the study (project). In this step, you are required to have following items handy:
    * Study Title (aka manuscript title)
    * Study abstract <br>
**Note:** After you successfully register the study, EGA will generate the accession number for your study. Please record that accession number for your reference as you will require that in the future. If possible, please record the EGA generated Thank you message.
5. Register the samples. In this step, you are required to upload the sample sheet. Please follow the format of this 
   file to make sample file for your study. Please make sure the file is in tab-delimited format and has extension ".
   tsv". <br>
**Note:** After you successfully register the sample/s, EGA will generate the accession number/s for your sample/s. Please record that accession number for your reference as you will require that in the future. If possible, please record the EGA generated Thank you message.
6. Submit Data Access Agreement (DAA) and Data Access Committee (DAC). You are not required to create a new DAC as 
   it has already been created. To make DAA, please refer to this DAA. Make study specific changes and upload it. <br>
**Note:** For your record, please record the EGA generated Thank you message.
7. Encrypt the BAM files.
    * Compile list of BAM files to encrypt in a text file
    * Build a custom script tp encrypt the BAM file with `egacryptor` - an encryption software provided by EGA
    * Create `MD5SUM` for both the encrypted and raw BAM files
    * Create a `TSV` file with name `experiment_bam_details.tsv` containing following three columns:
        1. BAM file name
        2. `MD5SUM` check for encrypted BAM files with extenstion `.gpg.md5`
        3. `MD5SUM` check for BAM file with extension `.md5`
8. Upload the encrypted BAM and `MD5SUM` check files. Use the following command line as reference.
```bash
#command line to upload encrypted BAM file/s
ASPERA_SCP_PASS=GHpGCYI2 /home/thd7/.aspera/cli/bin/ascp -P33001 -QT -l300M -L- *.bam.gpg ega-box-611@fasp.ega.ebi.ac.uk:/.
  
#command line to upload MD5SUM file/s for BAM/s
ASPERA_SCP_PASS=GHpGCYI2 /home/thd7/.aspera/cli/bin/ascp -P33001 -QT -l300M -L- *.md5 ega-box-611@fasp.ega.ebi.ac.uk:/.
 
#command line to upload MD5SUM file/s for encrypted BAM/s
ASPERA_SCP_PASS=GHpGCYI2 /home/thd7/.aspera/cli/bin/ascp -P33001 -QT -l300M -L- *.gpg.md5 ega-box-611@fasp.ega.ebi.ac.uk:/.
```
9. Check `Submit sequence reads and experiments` option on EGA website and press next. Select the corresponding 
   study from the list. Skip the next step as you already registered the samples in Step - 5. Please select the BAM 
   and upload the file with sample/s, BAM/s, and their MD5SUM. Please refer the [sequence reads file] to make one file 
   for your upload. Please make sure the file is in tab-delimited format and has extension `.tsv`. <br>
   **CAUTION:** If you have many samples to upload, please divide the file into small chunks (of 200) and upload them 
   individually. If you try to upload all of them in one file, you may experience `Time Out` error. <br>
   **Note:** After you successfully register the run/s, EGA will generate the accession number/s for your run/s. Please record that accession number/s for your reference as you will require that in future. If possible, please record the EGA generated Thank you message.
10. Check "Submit dataset". In this step you are required to provide the following thing:
   * DAC (just select the DAC for the list)
   * Select appropriate study policy
   * Provide all the run accession numbers delimited by the comma (e.g. `EGARxxxx`, `EGARxxxx`, ...). <br>
     **Note:** If you received `EGAXxxxx` numbers, please contact EGA HelpDesk to provide corresponding `EGARxxxx` 
     numbers. <br>
   **Note:** After you successfully submit the dataset, EGA will generate the accession number/s for it. Please record that accession number/s for your reference as you will require that in future. If possible, please record the EGA generated Thank you message.

[EGA]:https://ega-archive.org/
[EGA submission website]:https://www.ebi.ac.uk/ena/submit/sra/#ega
[Tushar Dave]:<mailto:tushar.dave@duke.edu>
[sequence reads file]:https://www.dropbox.com/s/u51ua57aq075f3d/experiment_bam_spreadsheet_1KDLBCL_uploaded.tsv?dl=0