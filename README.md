# How to run *ncov2019-artic-nf*
**Note:** Have `sshpass` installed using `sudo apt-get install sshpass`. 

### 1. Copying files from `GridIon` to `Storage` and `HPC1`.
  Run the script `transfer.sh` using the following command `./transfer.sh --sequence NameOfTheFolder`. </br>
  Example:
  ```
  ./transfer.sh --sequence sarscov2_geco_run52
  ```
  - The source folder is found in **GridIon**'s `/data`. </br>
  - The target directory in **Storage** is `/storage/ONT_Runs/drag_and_drop`. </br>
  - The target directory in **HPC1** is `/data/geco_proj_dir/raw/RITM`. </br>



### 2. Running the `artic-nf` pipeline.
- Run the script `runArtic.sh` using the following command `./runArtic.sh --dir path/to/data --barcode barcode.csv`. </br>
  Example: </br>
  ```
  ./runArtic.sh --dir sarscov2_geco_run52/sarscov2_geco_run52_09012022/20220901_0808_X5_FAT95592_ef9365b9 --barcode batch52_barcodes.csv
  ```
- Run the script `runPostArtic.sh` using the following command `./runPostArtic.sh --dir path/to/data`. </br>
  Example: </br>
  ```
  ./runPostArtic.sh --dir sarscov2_geco_run52/sarscov2_geco_run52_09012022/20220901_0808_X5_FAT95592_ef9365b9
  ```



### 3. Copying results to local workstation
  Run the script `copyResults.sh` using the following command `./copyResults.sh --dir path/to/data --batch number`. Make sure that the batch number is not yet present in your local directory. </br>
  Example: </br>
```
./copyResults.sh --dir sarscov2_geco_run52/sarscov2_geco_run52_09012022/20220901_0808_X5_FAT95592_ef9365b9 --batch 52
```



### 4. Uploading to REDCap
- **Dealing with repeat samples** (Skip if there is none)</br>
  Run script `dealRepeats.sh` to change the instance number in metadata and move the fasta file of the repeat samples. You need a file containing the sample number of the repeat samples in each line. `Batch52` corresponds to the directory where the results are found. </br>
  Example: </br>
  ```
  ./dealRepeats.sh --dir_input Batch52 --file_repeat repeats.csv
  ```

- **Uploading metadata for the `Sequence` and `Analysis` information** </br>
  *Step 1*: Go to the `GECO` page of RITM's [REDCap](https://geco.ritm-edc.net/) website. </br>
  *Step 2*: On the left panel under `Applications`, go to the `Data Import Tool`. </br>
  *Step 3*: Under `CSV import` tab, click `Choose File` button to upload the CSV file. </br>
  *Step 4 (`Sequence`)*: Upload the `redcap_meta_sequence.csv` file inside the `articNcovNanopore_prepRedcap_makeMeta` folder. </br>
  *Step 5 (`Analysis`)*: In the new page that loads up, upload the `meta_analysis.csv` file inside the `articNcovNanopore_prepRedcap_process_csv` folder. </br>


- **Uploading `fasta` files
