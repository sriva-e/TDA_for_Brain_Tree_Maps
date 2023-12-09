# TDA_for_Brain_Tree_Maps
Topological Data Analysis of MRA Scans Brain Images (Patient vs. control)

This project is investigating if topology can help us better understand the brain tree maps, 
the project is divided into two pipelines <br />
--Data preprocessing (vessel segmentation)<br />
--TDA pipeline(future work)<br />

Notes on the data preprocessing pipeline are as follows:<br/>
DATASET: Lausanne_TOF-MRA_Aneurysm_Cohort(https://openneuro.org/datasets/ds003949/versions/1.0.1) <br />
         --code<br />
         --derivatives<br />
          &nbsp; --N4_bias_field_corrected (files are located in anat folder which is inside the ses folder which is inside subfolder)<br/>
          &ensp;  --sub folders<br/>
          &emsp;  --ses folders<br/>
           &emsp;   -- anat folders<br/>
                &emsp; --angio_N4bfc_brain_mask.nii.gz<br/>
                &emsp; --angio_N4bfc_mask.nii.gz<br/>
            &nbsp;--manual_masks</br>
          &nbsp; --registrations<br/>
(outside derivates and code we have subfolders)<br/>
        &nbsp; --subfolders (files are located in anat folder which is inside the ses folder which is inside subfolder)<br/>
         &ensp;   --ses folders<br/>
            &emsp;   -- anat folders<br/>
             &emsp;    -- _T1w.nii.gz<br/>
              &emsp;   -- _angio.nii.gz<br/>

PIPELINE INFO: RUN THESE 3 STEPS FOR EACH CASE TO GET .tre FILE FOR ALL THE CASES IN THE DATA <br/>

Segment Brain from MRIs<br/>
                     &emsp;   &emsp; Input in our program<br/>
                                  &emsp;              (these images need to be in .mha format)<br/>
takes: <br/>
       -- mra.mha    &ensp;              =     &ensp;        -- _N4_bfc_mask.nii.gz file  (located in subfolders of N4_bfc)                       |      <br/> 
       --mri_t1_sag.mha     &ensp;       =     &ensp;        -- _T1w.nii.gz file  (located in subfolders outside code and derivatives folder)     | <br/>
      --Normal-FLASH.mha     &ensp;     =    &ensp;         -- _ angio.nii.gz file (located in subfolders outside code and derivatives folder) __|<br/>
      --Normal-FLASH-Brain.mha &ensp;   =     &ensp;        -- angio_N4bfc_brain_mask.nii.gz (located in subfolders in N4_bias_field_corrected folder) <br/>


Output<br/>
   &nbsp;    -- MRA-ISo.mha<br/>                      
   &nbsp;    -- MRT1-Iso.mha<br/>
   &nbsp;    -- MRA-Brain.mha<br/>
   &nbsp;    -- MRT1-Brain.mha<br/>


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
 
 This is what the final output will look like: <br/>
 ![alt text](https://github.com/sriva-e/TDA_for_Brain_Tree_Maps/blob/main/segmented_vessels.png)<br/>
 
 These brain vessels are interpreted as topological structures, we then use Persistent Homology to analyze these netwrorks, <br/>
 Following is a persistence diagram of one of the brains: <br/>
![alt text](https://github.com/sriva-e/TDA_for_Brain_Tree_Maps/blob/main/Persistence%20diagram.png)
 
 
 REFERENCES:<br />
https://geometry.stanford.edu/papers/zc-cph-05/zc-cph-05.pdf <br />
https://towardsdatascience.com/exploring-brain-artery-trees-with-giotto-tda-688a44c00f59  <br />
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7753013/ <br />
https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.102.7885 <br />
https://github.com/giesekow/deepvesselnet/wiki/Datasets  <br />
https://www.frontiersin.org/articles/10.3389/fnins.2020.592352/full  <br />
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6472360/  <br />
https://physionet.org/content/ct-ich/1.3.1/ <br />
https://www.semanticscholar.org/paper/PERSISTENT-HOMOLOGY-ANALYSIS-OF-BRAIN-S.-Marron/d4f95f114dd8b0333fa1c8754d36ebc4ffb1e52d#references <br />
https://link.springer.com/article/10.1007/s12021-022-09597-0 <br />
https://github.com/InsightSoftwareConsortium/ITKTubeTK <br /> 
https://persim.scikit-tda.org/en/latest/notebooks/Differentiation%20with%20Persistence%20Landscapes.html. <br />
https://arxiv.org/abs/1310.7467 <br />
https://arxiv.org/abs/2204.13799 <br />
https://arxiv.org/pdf/1501.00179.pdf 

