# Drug Discovery Project (Erdős Institute Data Science Boot Camp)



Overview: This project attempts to build a pipeline for ADME (Absorption, Distribution, Metabolism, Excretion) property prediction of candidate drug molecules. The ADME properties of a drug molecule is essential to determine the viability of a drug during lead optimization in the pharmaceutical industry. Build models that can generalize the prediction on an unseen drug can save valuable time during clinical trials. Essentially, this project can be broken down into four models targeting accurate predictions for each of the ADME properties. 

Data collection and preparation: The dataset used in the models were obtained from the TDC website using the PyTDC API. Although the dataset was relatively ‘clean’, some N/A and ‘null’ values were present when molecular descriptors were generated. This is due to improper generation of the molecular object from RDkit. Since only a handful of datapoints had this discrepancy (<10), we decided to drop them from the dataset. We used a scaffold split implemented from the TDC’s API. 

Caco2 permeability prediction: Caco2 is an intestinal cell that is responsible for absorption of certain drugs when ingested into our body. If a drug has poor absorption, it is an unlikely candidate and identifying it prior to clinical trials using a machine learning (ML) model can help save valuable time. To predict the Caco2 permeability, we used the Caco2-wang dataset from TDC website which has about 910 datapoints. These datapoints contain molecular ‘Simplified Molecular Input Line Entry System’ (SMILES) strings along with the target property (Y) - log(apparent permeability), logPapp. The target property is in the range of -3 to -8. 

Featurization: The features were generated using the RDkit and DeepChem packages. There are two main classes of features- molecular descriptors (MD) and molecular fingerprints (FP). Several models (namely, Random Forest, Linear regression and XGBoost) was considered with only MD, only FP and both MD + FP as feature vectors.   

Model performance: Random Forest was used to classify molecules based on the Lipinski’s rule of 5, a binary classification problem that achieved true positive rate of 98%. However, rule of 5 is not the best approach to classifying a molecule to have good absorption properties. XGBoost regressor overperformed Linear regression for all three types of featurizations. The MAE of XGBoost was 0.55, 0.49 and 0.33 for MD, FP, and MD+FP respectively. Feature engineering approaches like similarity profiles using Tanimoto coefficients can likely improve the model performance. 

In addition to this work, please check this page for CYP inhibition predictions: https://github.com/sonjoydasphd/FunSimpleProjects/blob/65a9962a4f6891284a5907f04b22c24ffe742da7/DrugDiscovery_CYP.ipynb
