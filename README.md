# Predictive Healthcare: Disease Detection From Clinical Notes

## Abstract

This project aims to enhance disease prediction by leveraging unstructured clinical notes, a domain traditionally overlooked in healthcare analytics. While existing approaches predominantly rely on structured data, this project explores the potential insights hidden within free-text medical records. Leveraging the publicly available MIMIC-III dataset, renowned for its comprehensive clinical data, this study proposes a streamlined approach for disease prediction. By extracting symptom-based keywords from clinical notes using Natural Language Processing (NLP) techniques and incorporating the Disease-Symptom Knowledge Database from Columbia University, this project bridges the gap between structured and unstructured healthcare data. The methodology involves data preprocessing, exploratory data analysis (EDA), clinical notes transformation, symptom identification, encoding, and disease prediction using machine learning models. Additionally, the project draws insights from previous works in healthcare analytics

Sigfried Gold, Noemie Elhadad, and James J Cimino [1] presented an innovative approach for extracting structured medication event information from discharge summaries. The method involves a sequential process starting with the definition of the targeted medication events, followed by the construction of a parser and the generation of parsing rules. To validate the effectiveness of the system, a test dataset is curated, and parsing rules are applied, with the intention of seeking input from physicians for final decision-making on medications. Testing on the created dataset yields defined scores. This method offers a systematic way to extract pertinent medication information, ensuring a comprehensive understanding. However, potential challenges may arise in cases where parsing rules may need frequent updates to adapt to variations in discharge summaries. The involvement of physicians in decision-making adds a valuable clinical perspective, but it may also introduce subjectivity into the interpretation of results.

Miotto et al. introduced DeepPatient [2], a system designed to harness raw patient data from Electronic Health Records (EHR), including information on medications, diagnoses, procedures, and lab tests. The system generates patient representations using unsupervised deep feature learning algorithms, opening the door to advanced clinical activities including medication targeting, clinical trial recruitment, and patient likeness detection. A notable strength of this research lies in its ability to leverage complex EHR data to create meaningful patient representations, allowing for sophisticated clinical applications. However, the application of deep learning algorithms might result in models that are challenging to interpret, raising concerns about data privacy and computational complexity. Despite these challenges, the system's versatility and potential for personalized clinical interventions make it a promising tool for enhancing healthcare outcomes.

With a focus on feature selection and classification methods, Jain D., Singh V.[3] offer an overview of the critical area of chronic illness prediction in healthcare. The significance of feature selection is emphasised in terms of enhancing the precision of classification algorithms through the identification and removal of superfluous features from illness datasets. The study explores traditional approaches such as filter, wrapper, and embedded methods and discusses hybrid approaches that bring together the best features of several approaches. The need of early detection for chronic conditions like diabetes, heart disease, and cancer is emphasised. The paper explores many feature selection algorithms, including their features, benefits, and drawbacks. Benefits include lower dimensionality and improved accuracy; drawbacks include possible biases and difficulties with big datasets.
Introduction

Healthcare analytics has seen significant advancements in recent years, particularly in the realm of predictive analytics for disease diagnosis and prognosis. Traditionally, these efforts have largely focused on structured data derived from electronic health records (EHR) and clinical databases. However, amidst the wealth of information contained within unstructured clinical notes, a valuable yet often overlooked resource awaits exploration.

This project aims to address the challenge of disease prediction using unstructured clinical notes, aiming to unlock the hidden insights within free-text medical records. Leveraging the Medical Information Mart for Intensive Care III (MIMIC-III) dataset, renowned for its extensive clinical data, and employing advanced Natural Language Processing (NLP) techniques, this study seeks to extract valuable insights from the narrative descriptions of patient encounters.

One of the primary objectives of this project is to bridge the gap between structured and unstructured healthcare data. While structured data provide valuable information on diagnoses, procedures, and medications, unstructured clinical notes offer a rich narrative that often captures nuanced symptoms, patient histories, and contextual details. By harnessing NLP techniques to extract symptom-based keywords from clinical notes and mapping them to diseases, this project aims to enhance the accuracy of disease prediction models.


## Methodology

1.	Dataset Preparation

For this project MIMIC-III Dataset was used, employing a selection of five tables from a total of thirty available tables, as outlined in the schema provided (Figure 1). Through a systematic merging process, the resulting database comprised approximately 3.9 million records. Recognizing the constraints posed by computational limitations, a strategic refinement approach was adopted. Consequently, the focus shifted towards filtering the diagnosis and procedures tables, specifically targeting textual data and corresponding diagnoses. A deliberate curation process yielded 4000 evenly distributed data points for subsequent analysis. Notably, this analysis prioritized two key columns: 'Text', housing clinical notes, and 'Diagnosis', denoting the associated diseases.

<img width="307" alt="image" src="https://github.com/vk1309/DS5500Capstone/assets/39329373/d8e65c8c-a328-4f9b-be9e-f4c4e68603a4">
<img width="452" alt="image" src="https://github.com/vk1309/DS5500Capstone/assets/39329373/38b52aec-3dca-414c-9709-d3e9cbfc32c8">



The next data pre-processing steps included: 

    1.	Correcting spelling mistakes in disease or symptom names and their codes. 
    2.	Removing duplicate symptoms associated with the same or similar disease names. 
    3.	Separating multiple symptoms listed within the same row. 
    4.	Eliminating irrelevant codes assigned to diseases and symptoms. 
    5.	Compiling a comprehensive list of all symptoms. 
    6.	Assigning Boolean values (0 or 1) to each symptom for every disease, indicating its  presence or absence. 
    7.	Adding the corresponding disease in the final column.

2.	Exploratory Data Analysis

EDA aims to perform initial investigations on data before formal modelling and graphical representations and visualisations, in order to discover patterns, look over assumptions, and test hypothesis. The summarised information on main characteristics and hidden trends in data can help the doctor to identify concern areas and problems, and the resolution of these can boost their accuracy in diagnosing diseases. Below is the spread of diseases in the dataset.

<img width="578" alt="image" src="https://github.com/vk1309/DS5500Capstone/assets/39329373/a81df3e3-02d4-4481-865d-aac306b2e5d9">
<img width="452" alt="image" src="https://github.com/vk1309/DS5500Capstone/assets/39329373/b419a796-9c18-4634-94a9-2f8bc6010cec">
<img width="542" alt="image" src="https://github.com/vk1309/DS5500Capstone/assets/39329373/0ab3703c-7940-4b2c-a166-6685ff3b236c">


Almost all symptoms have weak linear correlations, which is indicative that these symptoms do not come hand-in-hand.
<img width="451" alt="image" src="https://github.com/vk1309/DS5500Capstone/assets/39329373/fb0c262c-52c7-4d97-80ea-7e5d83e7ca1f">


The above charts give us an idea about the patient’s ethnicity. We can see that the dataset dominated by the “White” ethnicity, and other popular ethnicities include “Black/ African American” and “Hispanic or Latino”. 


The above graphs summarize the top 5 diagnosis in the dataset. As we can observe, the most entries in the dataset are for Newborn, other meaningful diagnosis are Pneumonia, Sepsis, Congestive Heart Failure and Coronary Artery Disease. We have adequate data for analysis. 

3.	Data Modelling

The entire dataset is split into two separate sets - the training set and test set. They both consist of the same attributes, but not the same attribute values. The training set is used to train and construct the classification models. The test set is used to predict the classifications of the new unbiased data that were not used to train the model, before evaluating the model performance based on the performance metrics of accuracy, precision, recall, and F1-score of those classifications.
The target class labels for both datasets have almost even distribution. It is assumed that the training and test sets are unbiased and representative of the target classes, such as already going through the process of using a list of random numbers starting from the random selected position to perform random splitting.
The machine Learning algorithms of Support Vector Classifier (SVC), Decision Tree (DT), and Random Forest (RF), are chosen to fit to the dataset.
Support Vector Classifier is a discriminative classifier i.e. when given a labelled training data, the algorithm tries to find an optimal hyperplane that accurately separates the samples into different categories in hyperspace.



Decision tree is constructed based on parameters of best split strategy, and the criterion of entropy which utilises information gain to iteratively select the next node according to higher feature importance to optimise the quality of splits. The minimum number of leaves are restricted to 2. The outputs are the classification rules as extracted from the decision tree. These are determined by the flow sequence from the root node and the corresponding branches to the internal or decision nodes, then stopping when the leaf node representing the class label is reached.


The symptom of 'fatique' is found to have the significantly largest predictive power of 0.1579.
Random Forest classifier will combine multiple base models of Decision Trees during its training period, using the strategy of ensemble machine learning methods. This will construct a single optimal predictive model, with the criterion of entropy which utilises information gain to iteratively select the next node according to higher feature importance to optimise the quality of splits. The minimum number of leaves are restricted to 2. The final output may be the mode class or the mean prediction of individual trees.

## Conclusion
In conclusion, this project represents a significant advancement in healthcare analytics by leveraging unstructured clinical notes for disease prediction. By using Natural Language Processing (NLP) techniques and machine learning algorithms, this project has successfully bridged the gap between structured and unstructured healthcare data, unlocking valuable insights hidden within free-text medical records.

Through dataset preparation, exploratory data analysis, and clinical notes transformation, this project has demonstrated the feasibility and efficacy of extracting symptom-based information from unstructured clinical narratives. This process not only enriches the dataset but also enhances the predictive capabilities of our models by incorporating nuanced symptomatology.

## Future Work
Expanding the predictors beyond the 140 symptoms currently utilized presents a promising avenue for refinement. By integrating additional symptoms and clinical indicators into the model design, we can capture a more comprehensive spectrum of patient presentations, thereby enhancing the model's predictive capabilities. Leveraging extensive symptom databases and medical literature, we can identify and incorporate potent predictors of disease prognosis, augmenting the richness and granularity of our predictive models.
The integration of Large Language Models (LLMs) represents a cutting-edge approach to disease prediction, offering the potential to glean insights from unstructured clinical narratives in unprecedented ways. By harnessing the power of LLMs, such as transformer-based architectures like BERT or GPT, our model can learn to discern intricate patterns and associations within textual medical data. This enables the model to not only mimic existing disease-symptom relationships but also extrapolate and predict entirely novel disease manifestations based on latent linguistic structures. By leveraging the contextual understanding encoded in LLMs, our predictive framework can adapt and evolve alongside emerging medical knowledge, facilitating the discovery of previously unrecognized disease patterns and symptom associations.
Iterative refinement and validation of our predictive models are essential for ensuring their robustness and generalizability across diverse clinical contexts. Continuous evaluation against real-world clinical data, including external validation on independent datasets, serves to validate the reliability and efficacy of our predictive framework. Furthermore, incorporating feedback from healthcare practitioners and domain experts enables us to refine and calibrate our models in alignment with clinical insights and evolving medical standards.

## References 
[1] D. Singh, V. Kumar, and R. G. Qiu, "Patients’ Disease Risk Predictive Modeling using MIMIC Data”, Procedia Computer Science, vol. 170, pp. 401-408, 2020. [Online]. Available: https://doi.org/10.1016/j.procs.2020.02.271.

[2] M. Saeed, M. Villarroel, A. T. Reisner, G. Clifford, L. Lehman, G. Moody, T. Heldt, T. Kyaw, B. Moody, R. G. Mark. (2016). "Multiparameter Intelligent Monitoring in Intensive Care III (MIMIC-III): A public-access intensive care unit database," [Online]. Available: https://physionet.org/content/mimiciii/1.4/.

[3] M. Friedman, "Disease Symptom Knowledge Base," Columbia University Department of Biomedical Informatics, [Online]. Available: https://people.dbmi.columbia.edu/~friedma/Projects/DiseaseSymptomKB/.

<img width="1189" alt="Screenshot 2024-04-09 at 12 22 33 AM" src="https://github.com/vk1309/DS5500Capstone/assets/39329373/3a7959e3-1e8c-4774-a222-32a5e082fe3c">


