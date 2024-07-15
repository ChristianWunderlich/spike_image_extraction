# Experiments

This post provides an overview of a series of experiments conducted to evaluate the performance and accuracy of different strategies for data extraction from tables, images, and graphs. The experiments aimed to assess the effectiveness of various techniques in extracting information from different types of data.

For tables, three strategies were employed: extracting raw text data, using markdown formatting for extraction, and utilizing image-based techniques instead of text. The goal was to compare the accuracy and efficiency of these strategies in extracting data from tables.

For images, the experiment focused on utilizing image analysis with gpt-4o for extraction. The objective was to evaluate the effectiveness of this technique in generating accurate descriptions of images and compare it to human interpretation.

The experiments were designed to provide insights into the performance and suitability of different strategies for data extraction in various scenarios. The results obtained from these experiments can help inform the selection of appropriate techniques for specific data extraction tasks.

## Experiment 1: 01-experiment-simpleTable

**Description:** \
This experiment utilized a simple table for analysis. The table, shown below, contains basic information, with a nested table in the Results column. Despite the nested structure, the table is considered to be straightforward.

![Table](../01-experiment-simpleTable/table.png)

Two strategies were employed for analysis. The first strategy involved sending the PDF content to Azure Document Intelligence for document reading. The resulting document was then sent to gpt-4o without any post-processing.

The second strategy involved directly feeding the LLM a screenshot of the table. A PNG file was created from the aforementioned table and processed by the code before being sent to the LLM.

**Goal:** \
The objectives of this experiment were to extract the following information:
- Accuracy in the Results Column for Low Vision, ideally obtaining both results in that row.
- Time to complete in the Results column for Low Vision.
- Total number of participants across all disability categories.

**Result:** 
- **Strategy 1 (raw text):** 
    - The overall accuracy and retrieved data were highly accurate across all test cases. The table structure was well understood, allowing for easy summarization of all participants.
- **Strategy 2 (image extraction):** 
    - The overall accuracy and retrieved data were highly accurate across all test cases. The table structure was well understood, allowing for easy summarization of all participants.

The LLM demonstrated the ability to comprehend the structure and content of simple tables. It was capable of extracting information from different rows and columns, as well as summarizing numbers across rows.

**Extra-curriculum:** \
As an additional test, the latest version of gpt-4-turbo was evaluated for its accuracy in reading raw text from tables. The results were highly accurate in terms of the retrieved data. However, the execution time was significantly longer compared to the gpt-4o model.

## Experiment 2: 02-experiment-complexTable

**Description:** 

This experiment involved the analysis of a more complex table. The table, displayed below, contains the extracted data from Microsoft's annual financial report. 

![Table](../02-experiment-complexTable/msft.png)

Three strategies were employed for analysis. The first strategy involved sending the PDF content to Azure Document Intelligence for document reading. The resulting document was then sent to gpt-4o without any post-processing.

The second strategy involved directly feeding the LLM a screenshot of the table. A PNG file was created from the aforementioned table and processed by the code before being sent to the LLM.

The final strategy utilized Azure Document Intelligence's table recognition and data extraction capabilities. Document Intelligence has a built-in functionality to locate tables and store them in an array. Each object represents a table in the document and provides information such as the row count, column count, cell details, bounding boxes, and more. This information can be used to provide context and structure to the LLM.

This table is significantly more complex than the one in *Experiment 1*, highlighting the differences in results obtained from the strategies. To accurately extract information from this table, understanding its structure, dependencies, and data is crucial.


**Goal:**  
The objectives of this experiment were to extract the following information:
- The exact number of recorded basis for equity investments of level 1 in 2023.
- The exact number of recorded basis for equity investments of level 1 in 2022.
- The recorded basis for Corporate notes and bonds of Level 3 in 2023.
- The recorded basis for Corporate notes and bonds of Level 3 in 2022.
- The total number of unrealized gains of total debt investments for 2023 and 2022.

**Result:** 
The highlighted numbers in the provided screenshot were expected to be retrieved from the image/document.

![](../02-experiment-complexTable/msft_result_1.png)
![](../02-experiment-complexTable/msft_result_2.png)

- **Strategy 1 (raw text):** 
    - The question regarding the exact number of recorded basis for equity investments of level 1 in 2023 was answered incorrectly. Instead of 10.138, it retrieved 2.692. 
    - The question regarding the exact number of recorded basis for equity investments of level 1 in 2022 was answered incorrectly. Instead of 1.590, it retrieved 456.
    - Both questions about the recorded basis for Corporate notes and bonds were answered correctly.
    - The overall numbers were retrieved correctly.
- **Strategy 2 (image extraction):** 
    - The question regarding the exact number of recorded basis for equity investments of level 1 in 2023 was answered correctly.
    - The question regarding the exact number of recorded basis for equity investments of level 1 in 2022 was answered correctly.
    - However, both questions about Corporate notes and bonds were sometimes answered correctly and sometimes returned 0 (which is the value next to the desired one).
    - The overall numbers were retrieved correctly.
- **Strategy 3 (di table detection):** 
    - All questions were answered correctly!

For more complex tables, utilizing di table detection and data extraction is recommended. Among the three strategies, di table extraction demonstrates high precision.

## Experiment 3: 03-experiment-imageDescriptions

**Description:**  
This experiment was specifically designed to explore the extraction of information from images. The main objective of this experiment was to replace images in documents with descriptive text, thereby enabling semantic searching of images. Throughout the experiment, a variety of image types were tested, including basic illustrations, flowcharts, and architectural images. The purpose of this testing was to evaluate the effectiveness of different techniques in accurately extracting information from these images. 
![](../03-experiment-imageDescriptions/aspirine.jpg)
![](../03-experiment-imageDescriptions/flowchart.png)
![](../03-experiment-imageDescriptions/rag.png)


**Goal:**  
The goal was to assess the accuracy of image descriptions generated by gpt-4o in comparison to human interpretation of each image.

**Result:**  
The generation of image descriptions using gpt-4o proved to be highly effective. The process was efficient, and the descriptions provided were precise and informative. The example of the rag pattern demonstrated the LLM's ability to interpret the image in the correct sequence, even without explicit step numbering.

## Experiment 3: 04-experiment-graphDataExtraction
**Description:**  
This experiment focused on extracting information from graphs, with the primary objective of replacing graphs in documents with descriptive text. The aim was to enable semantic searching of graphs and improve accessibility.
I have tested more basic graphs as well as more advanced graphs.
![](../04-experiment-graphDataExtraction/graph1.png)
![](../04-experiment-graphDataExtraction/graph3.png)

**Goal:**  
The goal of this experiment was to evaluate the accuracy of graph descriptions generated by gpt-4o, comparing them to human interpretation. The objective was to assess the effectiveness of gpt-4o in accurately describing graphs and providing meaningful information.

**Result:**  
The results of this experiment demonstrated that gpt-4o was highly effective in generating accurate and informative descriptions of graphs. It was able to interpret both basic and complex graphs with precision. Additionally, tests were conducted to evaluate the usability of the generated descriptions for answering follow-up questions. The descriptions were saved as text and provided to another gpt-4o call, which successfully answered the follow-up questions based on the retrieved descriptions. This indicates the potential for using gpt-4o-generated graph descriptions for further analysis and decision-making processes. I have observed that the resolution of images and graphs significantly impacts the quality of the generated answers.



