# TDA_for_Brain_Tree_Maps
Topological Data Analysis of Brain(Patient vs control)

This project is dedicated to investigate if topology can help us better understand the brain tree maps, 
the project is divided in two pipelines <br />
--Data preprocessing (vessel segmentation)<br />
--TDA pipeline(future work)<br />

Notes on data preprocessing pipeline are as follows 
DATASET: Lausanne_TOF-MRA_Aneurysm_Cohort(https://openneuro.org/datasets/ds003949/versions/1.0.1) <br />
         --code<br />
         --derivatives<br />
          &nbsp; + space   --N4_bias_field_corrected (files are located in anat folder which is inside ses folder which is inside sub folder)
          &nbsp; + space +space   --sub folders
           &nbsp; + space +space   --ses folders
            &nbsp; + space +space +space  -- anat folders
               &nbsp; + space +space +space+space      -- -angio_N4bfc_brain_mask.nii.gz
                 &nbsp; + space +space +space +space     -- -angio_N4bfc_mask.nii.gz
         &nbsp; + space   --manual_masks
          &nbsp; + space  --registrations
(outside derivates and code we have sub folders)
         --sub folders (files are located in anat folder which is inside ses folder which is inside sub folder)
            --ses folders
              -- anat folders
                 -- _T1w.nii.gz
                 -- _angio.nii.gz

PIPELINE INFO : RUN THESE 3 STEPS FOR EACH CASE TO GET .tre FILE FOR ALL THE CASES IN THE DATA 

Segment Brain from MRIs
                          Input in our program
                                                (these images need to be in .mha format)
takes -- mra.mha                  =             -- _N4_bfc_mask.nii.gz file  (loacted in sub folders of N4_bfc)                       |                                       
      --mri_t1_sag.mha            =             -- _T1w.nii.gz file  (loacted in sub folders outside code and derivatives folder)     | 
      --Normal-FLASH.mha          =             -- _ angio.nii.gz file (loacted in sub folders outside code and derivatives folder) __|
      --Normal-FLASH-Brain.mha    =             -- angio_N4bfc_brain_mask.nii.gz (loacted in sub folders in N4_bias_field_corrected folder) 
Output
     -- MRA-ISo.mha     #can save these outputs by image names for each case                         
     -- MRT1-Iso.mha
     -- MRA-Brain.mha
     -- MRT1-Brain.mha


Compute Vessel Probability Image From Brain MRIs
Input in the program: (Input in this program is the output we got from running Segment Brain from MRIs)
 takes  --MRA-Iso.mha
        --MRA-Brain.mha
        --MRT1-Iso.mha
        --MRT1-Brain.mha
Output
       --MRA-VesselEnhanced.mha
       --MRA-Brain-VesselEnhanced.mha

Segment Vessels Using Vessel Probability Image(This is the file that does segmentation)

Input in the program:(Input in this program is the output we got from running Compute Vessel Probability Image From Brain MRIs)
 takes: --MRA-VesselEnhanced.mha
        --MRA-Brain-VesselEnhanced.mha
output: 
       --MRA-vessels.tre (Important # this .tre file is the one we will be using for TDA)
 
