<h1>Automatic Cloze based MCQ generation using NLP techniques</h1>
 
 
 
Kota Vinay Kumar UMBC – M.P.S. Data Science 
 
 
 
 
 
 
<h2>Abstract</h2> 
Testing the student’s ability has been a critical task on their job for most of the teachers. The topics have been evolving and coming up with ways that utilize these topics to the maximum inference to generate an evaluation metric has become a tough task. Multiple choice and the Fill in the blank questions have been in the focus of metrics from a long time. Generating efficient multiple-choice questions that can offer better understanding about the topic in hand and provide enough information for the students is an important thing to consider. In this paper, there was a method proposed to tackle this problem. The automatic generation of mcq’s and cloze based questions with some options to make the student confuse about the choices. The hypernyms and the hyponyms of the wordnet library of NLTK corpus are used for generating these distractors. Once the distractors are generated, we could establish a relation between the question and the answer.  
<h2>Introduction</h2> 
Automatic MCQ generation is a form of evaluation metric which is mapped to the correct answer and three other distractors are generated using wordnet and the disambiguate is found using the pywsd library from python.  
At first, I tried to perform this automatic generation of questions using the SQUAD v2.0 data set which is openly available as mentioned in the paper [1]. But my experimentation was unsuccessful against a BERT transformer model. The model uses the CPU power too much which cannot be handled by the machine. Also, the preprocessing of this huge data against a Bert model has received from errors which are not descriptive. So I tried this another method which does not include any machine learning training algorithms. It is a simple solution-based analogy where the sentences are selected based on the preference and a cloze based questions are generated. 
By taking advantage of the algorithm as mentioned in the [2] paper, I was able to generated the output in the form a fill in the blank questions which can be deployed into any application or website for online assessments.  
The keywords here are generated using the library called KeyBert, which is an extensive library that scores the keywords based on their relevance in the context. The keywords with maximum score are then selected and further processed for our question generations. Different libraries like nltk, pywsd, numpy, pandas are used in order to efficiently generate and map the question to the answers.  
The nltk library has been used widely with different module in it for different corpus like stop words, punctuations, wordnet etc. All these efficiently work together to generate the output we need.  
 
<h2> Related Work </h2> 
I have analyzed various research papers and past applications on the methods used for generation of automatic MCQ generation. In the paper [3] “Automatic Generation of Multiple Choice questions for E-assessment.”  Here they used webscraping techniques that could be used to search the most relevant webpages for a topic in a certain domain. These details are run against a knowledge base for question generation.  
In the paper [4] “Automatic Cloze question generation”, the authors here have performed this cloze question generation where they selected a keyword and masked the output from the keyword, which is then fed to the used in the form a question.  
In the paper [5], “Towards automatic generation of e-assessment using semantic web based antologies”, the authors proposed a novel technique where they use semantic interpretations such as annotations from a large web corpus to generate questions that are well suited for the assessment and evaluation metrics. They made use of the conceptnet corpus with an api widely available on the natural language processing domain. 
In the paper [6], “DeepQuest: A deep learning approach for automatic multiplechoice question generation”  
   
This paper aims to apply these techniques in an easy way which is selecting the keywords using parts of speech tagger and the the synsets are selected by looping through the selection list of keywords.  
 
<h2> Proposed Methodology</h2>   The proposed method is divided into four tasks in general. Task 1 is summary generation, task 2 is the keyword extraction, task3 is the distractor generation and final task is to print out the questions along with distractors.  
 
<h3> Summary generation phase:</h3> 
 
 In this phase the design takes a raw text and generate a summary of the model. In my experimentation I have done this using the harry potter book data which I found it on kaggle. A small portion of the first part has been taken into consideration since summarizing a larger text corpus requires more time and cpu power. The summary is generated using the BERTSUM model available from the library bert extractive summarization as mentioned in the paper [2]. It got down a corpus of 60000 words into a minimal length of 2000 which can be used for question generation.  
 
<h3> Keyword Extraction Phase: </h3> 
 	 
 The keywords are selected based on the criteria of when well it happens to be in an whole corpus. Words like Mr. Miss. Should, could, are not considered since their relevance for answer generation are minimal. In order to be consistent in my approach I have used keyBert library for selecting these keywords. 
 
  
Figure 1: Step by step algorithm for the method 
These selected keywords are then passed through a parts of speech tagger for obtaining necessary words with relevant parts of speech tokens. Once the parts of speech tokens are generated the parts of speech type with most number of occurrences are selected to perform the answer generation. This is a greedy method since most of the times, in the harry potter book, the conversations include names. For this reason in my experimentation, I was able to use only the Noun tag for the questions along with occasional verb as the keyword. After short listing the keywords from the overall list of keywords we then map the keywords to its sentence. The main reason for performing this is the use case of generating the cloze questions based on the keywords here. 
 
<h3> Distractor Generation: </h3>
 
 As mentioned in the paper [2], I used the wordnet approach for generating the keyword distractors for a given keyword. There is also an potential usage of concept net for this method, but since the text I chose was a book context with direct speeches, I used only the wordnet for this approach.  
 WORDNET is an open-source corpus available for free across the internet which was developed by the researchers at the Princeton university. The wordnet is also available in the nltk library which can be easily downloaded and accessible.  
 Before we apply the wordnet approach across each keyword in the library we make a disambiguate test on the words that are present in the keyword dictionary with the context. This is done using the most popular library for this task which is the pywsd library, whose main purpose was to sense the level of disambiguation on the given word for a given keyword.  
 I made use of the wordnet library to generate synsets based on the pos tag as we mentioned earlier. A synset is basically a different word in a different format for the given keyword. From a synset, we can access the hyponyms and the hypernyms of the word, which are our distractors in this case. Once the distractions are generated a stored for the given keyword, we make use of the dictionary from the above stage to further generate the cloze based question types.  
 
<h3>Question generation </h3>
 
 Taking the keyword for a given sentence and masking out the keyword using the replace option, we then present the user with a sentence that has a missing keyword and the options are generated from the previous are presented to the user for him/her to select from the given list of options. The user then can choose what option is right or what he/she thinks right based on the context.  
 
<h2>Results </h2>
 	 
 Since this is just a project with normal generation of text with options, I have not evaluated with any other metrics. 
 
 
<h2>Conclusion </h2>
 
 There has been wide range of increase in research in this area of generation of mcq’s using the natural language processing. With the advent of technology and gpu’s more transformer-based models are being which attain state of the art of the performances in this regard. Once the model is created, we can fine tune different aspects of it. And generated a model which could generate an mcq using the context and the summary of the given word. We could further go on with this model by creating a gui for this. 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
<h2>References </h3>
[1]	Rajpurkar, P. et al. (2016) Squad: 100,000+ questions 	for 	machine 	comprehension 	of text, arXiv.org. 	Available 	at: https://arxiv.org/abs/1606.05250 	(Accessed: December 20, 2022).  
[2]	Journal, I.R.J.E.T. (2021) Automated MCQ generator 	using 	natural 	language processing, IRJET. 	Available 	at: 
https://www.academia.edu/es/53601157/IRJET_A utomated_MCQ_Generator_using_Natural_Lang uage_Processing (Accessed: December 20, 2022).  [3] A. Santhanavijayan*, S.R. Balasundaram, S. Hari Narayanan, S. Vinod ... (no date). Available at: 
https://www.researchgate.net/profile/Balasundara m-Sr/publications 
[4]	Narendra, A., Agarwal, M. and Shah, R. (no date) Automatic Cloze-Questions Generation - 
ACL 	Anthology. 	Available 	at: https://aclanthology.org/R13-1067.pdf (Accessed: December 21, 2022).  
[5]	Cubric, M. and Tosic, M. (no date) Towards automatic generation of e-assessment using semantic 	web 	... Available 	at: 
https://uhra.herts.ac.uk/bitstream/handle/2299/778 5/904296.pdf;sequence=1 (Accessed: December 
21, 2022).   
