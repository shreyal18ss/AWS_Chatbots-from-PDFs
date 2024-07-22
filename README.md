# Chatbots-from-PDFs
•	All companies conduct AGM for their shareholders. While the purpose of AGM is to throw light onto companies’ future agendas and fundamentals, a lot of figurative information is also provided as public data in the form of annual reports.  
•	The proposed model attempts to create an automated cognitive chatbot from small/large pdfs (company annual report in this PoC) that can answer users’ questions without them having to read the reports thoroughly. This solution is expected to be achieved using AWS cloud services.  
•	Given that the model is fulfilling the basic expectations, it will probably be a breakthrough in the way the developers may the realize formation of chatbots, as PDF data as such is difficult to be analyzed through data mining techniques, when accuracy levels are increased with additional layers of fuzzy matching and/or expansion of raw data structure into databases and knowledge graphs.

Key Words:   
Chatbot, bot, NLP, Information Retrieval, AWS, Reports, Large Files, Annual Report, AGM, cognitive, PDF, data mining. 


Business/Process flow: 
1.	The admin will upload the Annual Report (Object and large PDF file) in S3 bucket and questions in the form of a .csv file.
2.	A lambda function will be triggered on S3 “Put Object” Event and will split the large file into smaller chunks. The smaller files (10 pages each, which is the processing size limit of Textract based on its performance and documentation analysis) will then be stored in a different bucket. 
3.	Another Lambda function will then fetch each file to Textract, from where an SNS notification will trigger yet another lambda function once the file is processed in order to store it in a new S3 bucket.  
4.	The outputs in the form of raw text, tables, key-value pairs and query-answers will be stored back into in the S3 bucket.
5.	A static website, acting as the user interface for questions will compare the queries with the backend output query-answer file using a fuzzy-matching script and return the answer. In case the query isn’t already present in the backend file, a fresh textract analyse job can be called for the valid topic selection and the answer can be fetched at that point.


