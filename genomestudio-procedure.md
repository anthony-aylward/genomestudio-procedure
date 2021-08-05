# Genotype processing with GenomeStudio (v2.0.5)

## Step 0: Required software tools

This procedure uses the following software tools:

### Windows (on PC)

1. [MobaXterm](https://mobaxterm.mobatek.net/) - terminal allowing SSH into gatsby/sherlock/etc., also makes it pretty easy to download/upload files
1. [7zip](https://www.7-zip.org/) - creates compressed file archives (like tarballs) that can be read by both windows and linux
1. [GenomeStudio v2.0.5](https://www.illumina.com/techniques/microarrays/array-data-analysis-experimental-design/genomestudio.html)

### Linux (on server)

1. 7zip
    - Ubuntu: `sudo apt install p7zip-full p7zip-rar`
    - CentOS: `sudo yum install p7zip p7zip-plugins`

## Step 1: Compress and download genotyping data

It is easier to download a single compressed file archive than a collection of
uncompressed files, so we'll first compress our genotyping data on the server
using 7zip. The format for the command is:

```
7z a <destination_archive.7z> <input_directory/>
```

`7z a` is short for `7zip archive`. For example:

```
7z a /nfs/lab/aaylward/pbmc_snATAC/210729.7z /nfs/lab/projects/pbmc_snATAC/data/SNParray/210729
```

On the PC, we can then navigate to the `.7z` file and download it using the
graphical interface:

---

![mobaxterm image](screenshots/moba-xterm-download.png)

---

Finally, we decompress the archive using 7zip:

---

![7zip image](screenshots/7zip-extract.png)

---

## Step 2: Download array-specific product files

Each illumina genotyping array has a corresponding set of product files that
are required for processing the data.

First we'll check which array was used by looking at the sample sheet included
with the data, in this case `210729_Gaulton_Samplesheet.csv`. It indicates that
the array used is [Infinium Omni 2.5-8 v1.5](https://support.illumina.com/array/array_kits/humanomni2_5-8_beadchip_kit/downloads.html). For a different array you'll have
to find its files on support.illumina.com.

You'll need to download the Manifest file (either BMP or CSV format) and the
Cluster file.

![sample sheet](screenshots/sample-sheet.png)

## Step 3 