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
          &nbsp; --N4_bias_field_corrected (files are located in anat folder which is inside ses folder which is inside sub folder)<br/>
          &ensp;  --sub folders<br/>
          &emsp;  --ses folders<br/>
           &emsp;   -- anat folders<br/>
                &emsp; --angio_N4bfc_brain_mask.nii.gz<br/>
                &emsp; --angio_N4bfc_mask.nii.gz<br/>
            &nbsp;--manual_masks</br>
          &nbsp; --registrations<br/>
(outside derivates and code we have sub folders)<br/>
        &nbsp; --sub folders (files are located in anat folder which is inside ses folder which is inside sub folder)<br/>
         &ensp;   --ses folders<br/>
            &emsp;   -- anat folders<br/>
             &emsp;    -- _T1w.nii.gz<br/>
              &emsp;   -- _angio.nii.gz<br/>

PIPELINE INFO : RUN THESE 3 STEPS FOR EACH CASE TO GET .tre FILE FOR ALL THE CASES IN THE DATA <br/>

Segment Brain from MRIs<br/>
                     &emsp;   &emsp; Input in our program<br/>
                                  &emsp;              (these images need to be in .mha format)<br/>
takes: </br>
       -- mra.mha    &ensp;              =     &ensp;        -- _N4_bfc_mask.nii.gz file  (loacted in sub folders of N4_bfc)                       |      <br/> 
       --mri_t1_sag.mha     &ensp;       =     &ensp;        -- _T1w.nii.gz file  (loacted in sub folders outside code and derivatives folder)     | <br/>
      --Normal-FLASH.mha     &ensp;     =    &ensp;         -- _ angio.nii.gz file (loacted in sub folders outside code and derivatives folder) __|<br/>
      --Normal-FLASH-Brain.mha &ensp;   =     &ensp;        -- angio_N4bfc_brain_mask.nii.gz (loacted in sub folders in N4_bias_field_corrected folder) <br/>

Output<br/>
   &nbsp;    -- MRA-ISo.mha <br/>                      
   &nbsp;    -- MRT1-Iso.mha<br/>
   &nbsp;   -- MRA-Brain.mha<br/>
   &nbsp;   -- MRT1-Brain.mha<br/>


Compute Vessel Probability Image From Brain MRIs<br/>
Input in the program: (Input in this program is the output we got from running Segment Brain from MRIs)<br/>
 takes: <br/>
     &nbsp;  --MRA-Iso.mha<br/>
     &nbsp;    --MRA-Brain.mha<br/>
     &nbsp;   --MRT1-Iso.mha<br/>
     &nbsp;  --MRT1-Brain.mha<br/>
Output<br/>
    &nbsp;    --MRA-VesselEnhanced.mha<br/>
    &nbsp;   --MRA-Brain-VesselEnhanced.mha<br/>

Segment Vessels Using Vessel Probability Image(This is the file that does segmentation)<br/>

Input in the program:(Input in this program is the output we got from running Compute Vessel Probability Image From Brain MRIs)<br/>
 takes:</br>
 &nbsp; --MRA-VesselEnhanced.mha<br/>
 &nbsp;--MRA-Brain-VesselEnhanced.mha<br/>
output: <br/>
 &nbsp; --MRA-vessels.tre (Important # this .tre file is the one we will be using for TDA)<br/>
 
