==== SynthStrip dataset =======================================================

The SynthStrip dataset is a collection of full-head images, brain masks, and
label maps from 622 MRI, PET, and CT scans gathered across an array of public
sources. We created it to evaluate the SynthStrip brain-extraction tool:

    Hoopes A, Mora JS, Dalca AV, Fischl B*, Hoffmann M* (*equal contribution)
    SynthStrip: skull-stripping for any brain image
    NeuroImage, 260, 119474, 2022
    https://doi.org/10.1016/j.neuroimage.2022.119474

    Website: https://w3id.org/synthstrip


==== Dataset breakdown ========================================================

The scans in this data collection span across imaging modalities, resolutions,
and subject populations, ranging from infants to patients with glioblastoma.
Their distribution is as follows (see reference above for details).

    Dataset    Modality           Voxel size (mm^3)    Images
    =========================================================
    IXI        T1w MRI              0.9 x 0.9 x 1.2        50
               T2w MRI              0.9 x 0.9 x 1.2        50
               PDw MRI              0.9 x 0.9 x 1.2        50
               MRA                  0.5 x 0.5 x 0.8        50
               DWI                  1.8 x 1.8 x 2.0        32
    ---------------------------------------------------------
    FSM        T1w MPRAGE           1.0 x 1.0 x 1.0        38
               T2w 3D-SPACE         1.0 x 1.0 x 1.0        36
               PDw 3D-FLASH         1.0 x 1.0 x 1.0        32
               qT1 MP2RAGE          1.0 x 1.0 x 1.0        32
    ---------------------------------------------------------
    ASL        T1w MPRAGE           1.0 x 1.0 x 1.0        43
               PCASL 2D-EPI         3.4 x 3.4 x 5.0        43
    ---------------------------------------------------------
    QIN        T1w 2D-FLASH         0.4 x 0.4 x 6.0        54
               T2-FLAIR 2D-FSE      0.4 x 0.4 x 6.0        17
               T2w 2D-FSE           1.0 x 1.0 x 5.0        39
    ---------------------------------------------------------
    Infant     T1w MPRAGE           1.0 x 1.0 x 1.0        16
    ---------------------------------------------------------
    CIM (*)    FDG PET              2.0 x 2.0 x 2.0        20
               CT                   0.6 x 0.6 x 1.5        20
    ---------------------------------------------------------
                                                   Total: 622

(*) As we cannot redistribute the PET and CT images from the CERMEP-IDB-MRXFDG
dataset (CIM), we only include the corresponding brain masks in the native
space of these scans. To obtain the images, please contact the original authors
or fill out their request form:

    Ines Merida (merida@cermep.fr)
    https://framaforms.org/request-form-for-cermep-idb-mrxfdg-database-1637844711


==== Dataset structure ========================================================

Each subdirectory represents an individual scan. Subdirectory names follow a
SUBSET_MODALITY_SUBJECT format. We distribute the unmodified image from the
source dataset and a manually refined binary brain mask. For adult MPRAGE
scans, the dataset also includes a label map. All image files have the native
shape, resolution, and orientation of the respective scan:

    Filename         Scans                Content
    ====================================================================
    image.nii.gz     all except CIM       unmodified image
    mask.nii.gz      all                  binary brain mask
    labels.nii.gz    adult MPRAGE only    automatically fitted label map

The label maps include standard anatomical SynthSeg/FreeSurfer labels and six
non-brain labels of value 100-105. These non-brain labels are not necessarily
anatomically meaningful or consistent across scans: their purpose was to
generate variability outside the brain for SynthStrip training.

The specific labels are defined in the FreeSurfer colormap seg_labels.txt,
which you can use to visualize the label maps in FreeView. For example:

    cd ixi_t1_002
    freeview image.nii.gz labels.nii.gz:colormap=lut:lut=../seg_labels.txt


==== 2D subset ================================================================

The 2D subset comprises sagittal slices with approximate IA axis orientation
(inferior-anterior), extracted from the above images for all scans except CIM.
Since image geometries vary across scans, we extract sagittal slices 16 mm to
the left of the brain-mask center, without interpolating. Because the source
images have not been registered, some of the corresponding 2D label maps can
include right-hemispheric labels.


==== Validation split =========================================================

In the SynthStrip publication, we use the following scans for validation,
holding out all other images for testing (see files scans_*.txt).

    ixi_t1_016
    ixi_t1_017
    ixi_t2_016
    ixi_t2_017
    ixi_pd_016
    ixi_pd_017
    ixi_mra_016
    ixi_mra_017

    fsm_t2_02cd
    fsm_t2_24dz
    fsm_pd_02cd
    fsm_pd_24dz
    fsm_qt1_02cd
    fsm_qt1_24dz

    asl_t1_110
    asl_t1_120
    asl_epi_110
    asl_epi_120

    qin_t1_01
    qin_t1_02
    qin_flair_01
    qin_flair_02
    qin_t2_01
    qin_t2_02


==== License ==================================================================

You can use the IXI images under a Creative Commons Attribution-ShareAlike 4.0
International Licence (CC BY-SA 4.0). We distribute all other content of the
SynthStrip dataset under a Creative Commons Attribution 4.0 International
License (CC BY 4.0).

    https://creativecommons.org/licenses/by-sa/4.0/
    https://creativecommons.org/licenses/by/4.0/


==== References ===============================================================

If you find this dataset useful, please cite the SynthStrip reference at the
top and any relevant references below to credit the original authors of the
source datasets we obtained the images from.

    Information eXtraction from Images (IXI):

        IXI Dataset
        Biomedical Image Analysis Group, Imperial College London
        https://brain-development.org/ixi-dataset

    FreeSurfer Maintenance (FSM):

        A deep learning toolbox for automatic segmentation of subcortical
            limbic structures from MRI images
        Greve DN, Billot B, Cordero D, Hoopes A, Hoffmann M, Dalca AV,
            Fischl B, Iglesias JE, Augustinack JC
        NeuroImage, 244, 118610, 2021
        https://doi.org/10.1016/j.neuroimage.2021.118610

    In-house HCP-A pseudo-continuous arterial spin labeling (ASL):

        Extending the Human Connectome Project across ages: Imaging protocols
            for the Lifespan Development and Aging projects
        Harms MP, Somerville LH, Ances BM, Andersson J, Barch DM, et al.
        NeuroImage, 183, 972-84, 2018
        https://doi.org/10.1016/j.neuroimage.2018.09.060

        Characterizing cerebral hemodynamics across the adult lifespan with
            arterial spin labeling MRI data from the Human Connectome
            Project-Aging
        Juttukonda MR, Li B, Almaktoum R, Stephens KA, Yochim KM, Yacoub E,
            Buckner RL, Salat DH
        NeuroImage, 230, 117807, 2021
        https://doi.org/10.1016/j.neuroimage.2021.117807

    QIN GBM Treatment Response from The Cancer Imaging Archive (QIN):

        Mamonov AB, Kalpathy-Cramer J
        Data From QIN GBM Treatment Response
        The Cancer Imaging Archive
        https://doi.org/10.7937/K9/TCIA.2016.nQF4gpn2

        Prah MA, Stufflebeam SM, Paulson ES, Kalpathy-Cramer J, Gerstner ER,
            Batchelor TT, Barboriak DP, Rosen BR, Schmainda KM
        Repeatability of Standardized and Normalized Relative CBV in Patients
            with Newly Diagnosed Glioblastoma
        American Journal of Neuroradiology, 36 (9), 1654-61, 2015
        https://doi.org/10.3174/ajnr.A4374

        Clark K, Vendt B, Smith K, Freymann J, Kirby J, Koppel P, Moore S,
            Phillips S, Maffitt D, Pringle M, Tarbox L, Prior F
        The Cancer Imaging Archive (TCIA): Maintaining and Operating a Public
            Information Repository
        Journal of Digital Imaging, 26 (6), 1045-57, 2013
        https://doi.org/10.1007/s10278-013-9622-7

    Infant subjects from Boston Children's Hospital (Infant):

        De Macedo Rodrigues K, Ben-Avi E, Sliva DD, Choe MS, Drottar M, Wang R,
            Fischl B, Grant PE, Zollei L
        A FreeSurfer-compliant consistent manual segmentation of infant brains
            spanning the 0-2 year age range
        Frontiers in Human Neuroscience, 9, 21, 2015
        https://doi.org/10.3389/fnhum.2015.00021

    CERMEP-IDB-MRXFDG (CIM):

        Merida I, Jung J, Bouvard S, Le Bars D, Lancelot S, Lavenne F, Bouillot
            C, Redoute J, Hammers A, Costes N
        CERMEP-IDB-MRXFDG: a database of 37 normal adult human brain [18F]FDG
            PET, T1 and FLAIR MRI, and CT images available for research
        EJNMMI Research, 11, 91, 2021
        https://doi.org/10.1186/s13550-021-00830-6


==== Changes ==================================================================

2022-03-16 (v1.0):

    * Released initial dataset.

2022-03-17 (v1.1):

    * Updated README and data subsets included.

2022-07-26 (v1.2):

    * Added the Infant data.
    * Listed the validation scans used in the publication.

2022-12-16 (v1.3):

    * Added the FSM data and CIM masks.
    * Added missing asl_epi_115 image.
    * Specified license.

2023-09-07 (v1.4):
    * Added label maps for adult MPRAGE scans.
    * Released a 2D version of the dataset.
    * Included FreeView colormap and subject lists.

2024-06-20 (v1.5):
    * Extracted largest CC and filled holes to clean up brain masks.

