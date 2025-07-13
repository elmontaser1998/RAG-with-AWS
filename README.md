# RAG-with-AWS

<img width="2000" height="905" alt="image" src="https://github.com/user-attachments/assets/9512e581-e9b3-463c-b465-3837566d509c" />

### Introduction
This tutorial provides a step-by-step guide to setting up a **Retrieval-Augmented Generation (RAG)** system using **Amazon Bedrock**, leveraging the following components:

- Documents stored in **Amazon S3**
- A vector engine powered by **OpenSearch Serverless**
- An embedding model: **Titan Text Embeddings V2**
- A Bedrock-hosted LLM (e.g., **Anthropic Claude**) to query the knowledge base


### Create an IAM User

> ⚠**Important**: Using Amazon Bedrock requires an **IAM user**, not the root user.

1. Go to the **IAM** service in the AWS Management Console.  
   <img width="1261" height="671" alt="image" src="https://github.com/user-attachments/assets/614142bd-f507-4876-b52d-a540fbeb8a0d" />

2. Click on **"Users"**, then **"Create user"**.  
   <img width="2530" height="1351" alt="image" src="https://github.com/user-attachments/assets/f82244b0-e929-4819-9458-18bc70978fe2" />
   <img width="1269" height="673" alt="image" src="https://github.com/user-attachments/assets/41ec1702-d41b-4bde-8a4e-fc3a5c9a85ef" />

3. Choose a username and enable **"Provide user access to the AWS Management Console"**. Then set a custom password.  
   <img width="1267" height="673" alt="image" src="https://github.com/user-attachments/assets/8d99b30f-5304-48e7-8510-4eae707ca7f5" />

4. Attach the policy **`AdministratorAccess`** to the user.  
   <img width="1268" height="676" alt="image" src="https://github.com/user-attachments/assets/6b85f4ea-508b-4823-8d91-6499acacb546" />

5. Create the user and use the provided sign-in URL to log in with your new credentials.  
   <img width="1276" height="679" alt="image" src="https://github.com/user-attachments/assets/334c754b-b6ab-415a-a7b6-8f9712e86577" />
   <img width="1265" height="672" alt="image" src="https://github.com/user-attachments/assets/58ca93b6-5eda-49ea-bb4d-cbde4397eceb" />


###  Create a Knowledge Base in Bedrock

1. Go to **Amazon Bedrock** → **Knowledge Bases** → click **Create** → select **"Knowledge base with vector store"**.  
   <img width="1268" height="675" alt="image" src="https://github.com/user-attachments/assets/952deb73-9bd5-444d-88ec-a398b58c3344" />

2. Provide a name for your knowledge base.

3. In the **IAM permissions** section, select:  
   **"Create and use a new service role"**

4. In the **Data source** section, choose:  
   **Amazon S3** as the source.  
   <img width="1244" height="650" alt="image" src="https://github.com/user-attachments/assets/d7276e5a-d0e8-45b2-b752-d2431e04519d" />

> **Note**: You can also use other data sources such as:
> - A **web crawler** (to ingest webpage content)
> - **Confluence**, **Salesforce**, or **SharePoint** for enterprise document access

pour configuer s3 il fqut cree s3 bucket 


<img width="1274" height="370" alt="image" src="https://github.com/user-attachments/assets/75b151ad-4d9f-4fdb-985c-f33343add768" />
etre sur que tu est dans la region us-east-1
donner un nom au bucket et puis clickaue sur creqte bucket
<img width="1276" height="570" alt="image" src="https://github.com/user-attachments/assets/24ed9117-c7ba-4d67-b261-4308b52473fd" />


notre bucket est cree 
<img width="1268" height="631" alt="image" src="https://github.com/user-attachments/assets/b8d593af-f58d-43cf-8ab7-ffbb5eabe44e" />

cliecker sur le bucket 
puis uploader


<img width="1268" height="483" alt="image" src="https://github.com/user-attachments/assets/2b5716b0-3ea6-40f5-aac4-e93039890b37" />

pour ajouter des objets 

<img width="1274" height="625" alt="image" src="https://github.com/user-attachments/assets/3ac6c8c9-cfa5-473d-a5b4-b710781d0faa" />

exemple j ajouter artile attention is qll you need puis cliquer sur upload

<img width="1262" height="346" alt="image" src="https://github.com/user-attachments/assets/aa3464cb-41c6-4c00-8a44-0ca6210116f4" />
maintenat on a le bucket avec l object uploader dedant

<img width="1262" height="544" alt="image" src="https://github.com/user-attachments/assets/2d947619-944a-4f57-a854-c15cde54e63b" />
retourner au confugueration de s3
<img width="1277" height="664" alt="image" src="https://github.com/user-attachments/assets/f11ce147-cc1b-4ae0-887a-51a9ed9810b4" />
clicker sur borzse S3 
tu trouve le bucket deja cre

<img width="1253" height="484" alt="image" src="https://github.com/user-attachments/assets/4894c118-2667-467f-a4a7-660dfb1f9561" />


puis next pour choisir embedding model

<img width="1265" height="635" alt="image" src="https://github.com/user-attachments/assets/ca1984c9-6175-4ade-952d-ae8c6ca3a534" />

pou le vector store je coisir d utilise opensearch servless 


<img width="1268" height="674" alt="image" src="https://github.com/user-attachments/assets/498ea6a0-5bef-4cd2-9ea0-bef7a76f442e" />


puis create knozledge base une remarque vous avez des erreurs si vous  utilise pas IAM user
apres quelque temps base de connaisqnce est available

<img width="1241" height="649" alt="image" src="https://github.com/user-attachments/assets/60317156-beab-4274-a295-eaa78ae3cb62" />

cliquer sur bqse de connaissonce et sync our voire si il y a des probleme

<img width="1255" height="662" alt="image" src="https://github.com/user-attachments/assets/35fbe377-c9c2-4d74-bd9e-4b4b311a6a4c" />

puis clicer sur test knowledge bqse

<img width="1268" height="679" alt="image" src="https://github.com/user-attachments/assets/350dbdeb-8d4a-4c68-b178-b93c4870dc6f" />


and resultat

<img width="1248" height="668" alt="image" src="https://github.com/user-attachments/assets/0ce9f660-0650-48a2-875d-2eddd9e94d53" />














