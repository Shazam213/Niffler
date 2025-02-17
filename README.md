# Niffler: A DICOM Framework for Machine Learning and Processing Pipelines.

Niffler is a lightweight framework to facilitate executing machine learning pipelines and processing workflows on DICOM images and metadata. Niffler facilitates efficient transfer of DICOM images on-demand and real-time from PACS to the research environments. Niffler is also integrated with the radiology information system (RIS) to get clinical data in real-time. The DICOM images from the PACS and clinical data retrieved from the RIS can be used in conjunction in real-time as well as retrospectively on-demand.

The Niffler framework consists of:
- On-demand and real-time retrieval and processing of DICOM images from the PACS environment configured to accept requests from a deployment of Niffler.
- Acquisition and processing of clinical data from a RIS, to enable real-time analytics (RTA).
- Supportive utility functions such as DICOM → PNG conversion, DICOM → NifTi conversion, DICOM anonymization, and the workflows module.
- Scanner Usage Visualization with PACS And RIS data algorithm (modules/suvpar).
- Sample applications of the Niffler modules (modules/app-layer).

Niffler enables receiving DICOM images real-time as a data stream from PACS as well as specific DICOM data based on a series of DICOM C-MOV queries. The Niffler real-time DICOM receiver extracts the metadata free of PHI as the images arrive, store the metadata in a Mongo database, and deletes the images nightly. The on-demand extractor reads a CSV file provided by the user (consisting of a list of values for PatientID, AccessionNumber, or other DICOM keywords), and performs a series of DICOM C-MOVE requests to receive them from the PACS, without manually querying them. Niffler also provides additional features such as converting DICOM images into PNG images, and perform additional computations such as computing scanner utilization and finding scanners with misconfigured clocks.


# Configure Niffler

Niffler consists of multiple modules, inside the modules folder. Here we will look into the common configuration and installation steps of Niffler. An introduction to Niffler can be found [here](https://emory-hiti.github.io/Niffler/).


## Install Niffler

To deploy Niffler, checkout Niffler source code and run the installation script.
```
$ git clone https://github.com/Emory-HITI/Niffler.git

$ cd Niffler
```
The master branch is stable whereas the dev branch has the bleeding edge.

You might want to use the dev branch for the latest updates. For more stable version, skip the below step:
```
$ git checkout dev
```
Finally, run the installation script for a quick installation of dependencies. 

```
$ sh install.sh
```

This script is written for Centos. If you are using another operating system, please go through the script and make necessary changes as the script is easy to follow.

Please refer to each module's individual README for additional instructions on configuring, deploying, and using Niffler for each of its modules.


## Configure PACS

Both meta-extraction and cold-extraction modules require proper configuration of a PACS environment to allow data transfer and query retrieval to Niffler, respectively.

* If you plan to use meta-extraction and cold-extraction modules, please make sure to configure the PACS to send data to Niffler meta-extraction module's host, port, and AE_Title. 

* Niffler cold-extraction won't receive data unless the PACS allows the requests from Niffler cold-extraction (host/port/AE_Title). Please go through your PACS framework's documentation on configuring host/port/AE_Tiles for a new AE to accept queries from (Query AET). Those instructions should prepare your PACS to receive queries from Niffler as the Query AET.



# Citing Niffler

If you use Niffler in your research, please cite the below papers:

* Pradeeban Kathiravelu, Puneet Sharma, Ashish Sharma, Imon Banerjee, Hari Trivedi, Saptarshi Purkayastha, Priyanshu Sinha, Alexandre Cadrin-Chenevert, Nabile Safdar, and Judy Wawira Gichoya. **A DICOM Framework for Machine Learning Pipelines against Real-Time Radiology Images.** Journal of Digital Imaging (JDI). August 2021. https://doi.org/10.1007/s10278-021-00491-w

* Pradeeban Kathiravelu, Ashish Sharma, and Puneet Sharma. **Understanding Scanner Utilization With Real-Time DICOM Metadata Extraction.** IEEE Access, 9 (2021): 10621-10633. https://doi.org/10.1109/ACCESS.2021.3050467

* Pradeeban Kathiravelu, Nan Li, Nishchal Singi, Ananth Reddy Bhimireddy, Ryan Birmingham, Judy Wawira Gichoya, Hari Trivedi, Nabile Safdar, Ashish Sharma, and Puneet Sharma. **Visualizing Scanner Utilization from MRI Metadata and Clinical Data.** IEEE Computer. Accepted. 2022 December.
