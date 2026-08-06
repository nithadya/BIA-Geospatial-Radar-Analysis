# Assessment Details

| Assessment title | Abr. | Weighting |
| :--- | :---: | :---: |
| Evaluating the Effectiveness and Efficiency of Statistical and Geospatial Tools in Generating Business Intelligence for Informed Decision-Making in the Development of the Civil Aviation Sector in Sri Lanka. | WRIT1 | 80% |

Pass marks are 40% for undergraduate work and 50% for postgraduate work unless stated otherwise.

---

## Task/assessment brief

### Purpose
This assignment is to assess student’s ability to perform business analysis using Statistical and Geographic Information Systems (GIS) related tools, techniques and methodologies to find out applicable and useful intelligence for informed decision making in private and government sector institutions in the island and different parts of the countries in the world. The relevant higher level administrative officials of the those institutions can use GIS to generate maximum efficiency and benefits on informed business decision making while eliminating discrimination, ambiguity and uncertainty.

### Tasks Introduction
Sri Lanka’s civil aviation sector plays a vital role in supporting tourism, trade, and economic development. With increasing passenger demand, evolving airline networks, and infrastructure expansion needs, decision-makers require accurate, timely, and data-driven insights to guide strategic planning. However, traditional decision-making approaches in the sector have often relied on fragmented data and limited analytical integration, reducing the effectiveness of long-term planning.

In this context, the integration of statistical tools (such as regression analysis, forecasting models, and data analytics) and geospatial technologies (such as Geographic Information Systems – GIS, spatial mapping, and location intelligence) presents a significant opportunity to enhance business intelligence generation. These tools can be used to analyze passenger demand patterns, optimize route planning, identify suitable locations for airport expansion, and assess regional connectivity.

This assignment focuses on evaluating how effectively and efficiently these statistical and geospatial methods can be applied to generate meaningful business intelligence that supports informed decision-making in Sri Lanka’s civil aviation sector. Using relevant datasets (such as passenger traffic, flight frequency, and geographic distribution of airports), students are expected to explore how integrated analytical approaches can improve planning, operational efficiency, and policy formulation.

The study aims to highlight the importance of data-driven decision-making frameworks in aviation development and to assess whether adopting advanced analytical tools can contribute to sustainable growth, improved service delivery, and enhanced competitiveness of Sri Lanka’s aviation industry.

---

This study specifically focuses on the following areas:

#### a. Decision models development
Based on passenger demand associated factors conducting a comprehensive data-driven analysis to evaluate the key determinants of passenger demand in the aviation sector in Sri Lanka.

#### b. Network analysis
During a peak tourism season, Bandaranaike International Airport (CMB) experiences a significant increase in both inbound and outbound air traffic. At the same time, an aircraft develops a technical fault upon landing, requiring immediate attention. This situation creates a high-pressure operational environment requiring coordinated action among multiple aviation stakeholders.

The aviation network consists of key entities including:
* Airports (CMB, MRIA)
* Regulatory authority (CAASL)
* Airport operator (AASL)
* Airlines (SriLankan Airlines and international carriers)
* Air Traffic Control (ATC)
* Ground Handling Units
* Maintenance & Engineering teams
* Customs & Immigration
* Sri Lanka Air Force
* Supporting organizations (Fuel suppliers, Tourism Authority, Cargo operators)

In the given scenario, Air Traffic Control (ATC) functions as the central coordinating entity, managing aircraft movements and ensuring safe separation while communicating with airlines and airport authorities. Airport & Aviation Services Sri Lanka (AASL) oversees overall airport operations and coordinates between airside and ground activities. The Civil Aviation Authority of Sri Lanka (CAASL) provides regulatory oversight, ensuring that all actions comply with aviation safety standards. Airlines, including SriLankan Airlines and international carriers, respond to ATC instructions by adjusting schedules and operations. Meanwhile, Ground Handling Units and Maintenance & Engineering teams collaborate to address the aircraft’s technical fault and manage aircraft positioning on the apron. Customs & Immigration handle passenger flow disruptions caused by delays, ensuring efficient processing despite operational challenges. Additionally, the Sri Lanka Air Force remains on standby to support security and emergency response if required. Together, these interconnected entities demonstrate a highly coordinated system where effective communication and collaboration are essential for maintaining safe and efficient airport operations during high-pressure situations.

#### c. Geo Spatial Analysis for deploying PSR and SSR new radar systems
Under the Millennium Renovation Project of Bandaranaike International Airport (CMB), located in Katunayake, Sri Lanka, three modern radar systems are to be established: Primary Surveillance Radar (PSR), Secondary Surveillance Radar (SSR), and Surface Movement Radar (SMR). The PSR and SSR systems will be co-located at a single site, while the SMR system will be installed at a separate location. The SMR will be responsible for monitoring ground traffic within the airport, including runways, taxiways, and apron areas. In contrast, the PSR and SSR systems will provide surveillance for inbound and outbound air traffic within the surrounding airspace. For optimal performance and safety, specific placement criteria must be followed. 

The SMR system should be installed at an appropriate location approximately 300 m from the CMB Control Tower and about 200 m from the Runway Center Point (RCP). This ensures effective monitoring of all surface movements with minimal obstruction.

The PSR and SSR systems should be positioned at a suitable site approximately 2 km from the RCP, while remaining within a maximum of 3 km from the RCP. This placement allows for efficient long-range airspace surveillance while avoiding interference from airport infrastructure and terrain. To enhance security and operational reliability, the PSR and SSR installations should ideally be located within the Sri Lanka Air Force base premises adjacent to the airport.
* Ensuring clear line-of-sight for accurate detection
* Minimizing electromagnetic interference
* Avoiding obstructions such as buildings and terrain
* Maintaining compliance with ICAO safety and obstacle limitation standards
* Providing adequate access for maintenance and power supply

#### d. BI dashboard enables airport managers and air traffic controllers to monitor flight operations, analyze delays, track international traffic by country, and identify potential risks or bottlenecks.
Bandaranaike International Airport (CMB), the primary international gateway to Sri Lanka, is experiencing a steady increase in air traffic due to growing tourism and international connectivity. In order to improve operational efficiency and decision-making, the airport management plans to implement a Business Intelligence (BI) dashboard that provides real-time insights into flight movements, passenger flow, and operational performance.

You have been provided with an enhanced flight dataset containing detailed information on arrivals and departures, including flight schedules, delays, aircraft details, passenger counts, weather conditions, radar tracking (PSR/SSR/SMR), and geographic data such as origin and destination countries. The dataset also includes alert indicators and operational metrics such as taxi time, turnaround time, and queue position.

---

### Tasks: 1 – Report (100 Marks)

The student is required to do the following data analysis and visualizations based on datasets provided with this assignment using R, R-Studio, R-commander, QGIS, PostgreSQL, GOOGLE EARTH and other related supportive tools. All required datasets have been included within the “Data Sets” folder as separate subfolders per each question.

* **a)** Using the provided Air Transportation Regression Dataset (`Air_Transport_Data.csv`), Students are required to apply appropriate statistical techniques and analytical methods to examine the relationships between the independent variables; airport traffic, average income, fuel price, average ticket fare, flight frequency, and route distance and the dependent variable, passenger demand using provided dataset (`Air_Transport_Data.csv`).
  Based on the empirical findings, students should develop robust statistical models, supported by relevant graphical and visual representations, to generate meaningful insights that facilitate evidence-based decision-making. The analysis should culminate in a critical evaluation of the results, with particular emphasis on their practical implications for the development, efficiency, and strategic planning of Sri Lanka’s civil aviation sector. **(30 Marks)**

* **b)** Do a network analysis using provided dataset (`SriLanka_Aviation_SNA_Dataset.csv`) by constructing and visualizing the network graph representing relationships among aviation stakeholders and critically discuss the scenario by performing network analysis by calculating key metrics such as Degree Centrality, Betweenness Centrality and identify the most influential (highly connected) nodes, Critical bridge nodes within the network. Interpret the structure of the network, including: Central hubs, Clusters of interaction, Overall connectivity and efficiency.
  During your network analysis identify system vulnerabilities (e.g., failure of ATC or ground handling) and Operational efficiency during high traffic and emergency conditions. Your discussion should include recommendations to uplift Network resilience, Coordination efficiency, Risk and crisis management strategies. **(20 Marks)**

* **c)** Develop a fully geo referenced digitized informative aerial map with suitable information about CMB and its suburbs using provided dataset. *(Note: It is mandatory to do the image geo-referencing before initiation of the digitization. Every vector layer attribute table should contain suitable data in columns id, name, type, and size)* (CRS:EPSG:5234). The map should visualize suitable areas / Locations with GPS data to deploy PSR, SSR and SMR radar systems using geo spatial data processing with the support of geo processing and analysis tools in QGIS. The map development process should be supported by Geo Spatial Database named as “`SL_BIA_Aerial_Info`” to store spatial and non-spatial data generated and required GPS data should be extracted using KML/KMZ files with the aid of Google Earth and find below information.
  * Total number of buildings situated within the suitability area(s) at present
  * Total land area occupied by the buildings within the suitability area(s)
  * Total land area available for the Radar Deployment project.
  
  The map should be incorporated by a critical discussion highlighting the importance of the aforesaid radar systems for BIA along with the findings of the aforementioned geo spatial data processing and analysis. **(30 Marks)**

* **d)** Using the provided dataset (`BIA_CMB_Dataset.csv`), your task is to develop a comprehensive BI dashboard that enables airport managers and air traffic controllers to monitor flight operations, analyze delays, track international traffic by country, and identify potential risks or bottlenecks. The dashboard should support data-driven decision-making by providing clear visualizations such as flight status summaries, delay analysis, country-based traffic patterns, and real-time alerts for critical events. **(20 Marks)**

---

**Word count (or equivalent): 3000**  
This is a reflection of the effort required for the assessment. Word counts will normally include source code, any text, tables, calculations, figures, subtitles and citations. Reference lists and contents of appendices are excluded from the word count. Contents of appendices are also considered as evidences of work when determining your final assessment grade.

---

### Academic or technical terms explained:
* **ABI** – Analytics and Business Intelligence
* **GIS** – Geographical Information Systems
* **GPS** – Global Positioning System
* **GCP** – Ground Controlling Points
* **MOFAFET** – Ministry of Foreign Affairs, Foreign Employment and Tourism
* **Demonstrate** – Apply subject knowledge gained in business analytics tools, techniques and methods for real world problem solving or opportunity improving.
* **Evaluate** – Using statistical and geospatial processing and analyzing data make and defend judgements based on internal evidence or external criteria.
* **Explore** – Find out latest tools, techniques and methods found in the field of data science / Business analytics for providing more precise and quality result for durable, efficient and effective decision making.
* **BA** – Business Analytics done through statistical tools, techniques and methods.
* **BI** – Business Intelligence generated through BA; this encompasses narrative descriptions, Graphs and Formulas.
* **Describe** – Demonstrate an understanding of the facts based on previously learned information in BA module.
* **Hypothesis** – Null and alternative hypothesis written for supporting research questions for statistical use.
* **Use** – Apply BA knowledge to actual situations to generate new knowledge.
* **Explain** – Demonstrate an understanding of the facts based on the BA and the scenario.
* **Analyse** – Break down data into simpler parts and find evidence to support generalizations.
* **Discuss** – Demonstrate an understanding of the facts based on the BA and the scenario along with suitable real world examples.
* **Justify** – Make and defend judgments based on internal evidence through findings of the statistical analysis.
* **Conclude** – Make and defend judgments based on internal evidence through findings of the statistical analysis.

---

## Submission Details

| Submission Deadline | Estimated Feedback Return Date | Submission Time |
| :--- | :--- | :--- |
| This will be provided on the Moodle submission point. | This will normally be 20 working days after initial submission. | By 2.00pm on the deadline day. |

* **Moodle/Turnitin:** Any assessments submitted after the deadline will not be marked and will be recorded as a non-attempt unless you have had an extension request agreed or have approved mitigating circumstances. See the School Moodle pages for more information on extensions and mitigating circumstances.
* **File Format:** The assessment must be submitted as a pdf document (save the document as a pdf in your software) and submit through the Turnitin submission point in Moodle.  
  Your assessment should be titled with your: **student ID number, module code and assessment ID**, e.g., `st12345678 CSE5013 WRIT1`
* **Feedback:** Feedback for the assessment will be provided electronically via Moodle. Feedback will be provided with comments on your strengths and the areas which you can improve. View the guidance on how to access your feedback. All marks are provisional and are subject to quality assurance processes and confirmation at the programme Examination Board.

---

## Assessment Criteria

### Learning outcomes assessed
* Demonstrate understanding of the leading technologies relating to business intelligence, data analysis, predictive and other analytical technologies (e.g., geospatial, social), and be able to apply them appropriately in real world scenarios.
* Demonstrate understanding of and application of specialist technologies used to harvest, analyze and visualize business data in an intelligent way.
* Critically evaluate, design, prototype and implement business intelligence from data harvesting, processing visualizations to business analysis and storytelling.
* Explore the latest visualization techniques, business-IT project governance and related industry certifications.

### Learning Outcomes covered from the course work
LO2, LO3, LO4
* **a)** LO2, LO3
* **b)** LO2, LO3, LO4
* **c)** LO2, LO3, LO4
* **d)** LO2, LO3, LO4

### Other skills/attributes developed
This includes elements of the Cardiff Met EDGE (Ethical, Digital, Global and Entrepreneurial skills) and other attributes developed in students through the completion of the module and assessment. These will also be highlighted in the module guidance, which should be read by all students completing the module. Assessments are not just a way of auditing student knowledge. They are a process which provides additional learning and development through the preparation for and completion of the assessment.

* **ETHICAL:** Understanding the importance of adhering to the formal ethical practices when different sources data is extracted, processed and disseminate. This is achieved via university ethical guidelines and procedures.
* **DIGITAL:** Making use of vector and raster data models for geospatial analysis and processing. Surveyed datasets for statistical signification process.
* **GLOBAL:** Usage of Surveyed data generated in various parts of the world for statistical and geospatial analysis and processing. Localizing findings based on globally collected and analyzed data.
* **ENTREPRENEURIAL:** Involvement of business analytics and business intelligence; motivate students to initiate their own organizations for providing various services for corporate and individual customers.

---

### Guidelines for the report format
* Paper: A4
* Margins: 1.5” left, 1” right, top and bottom
* Page numbers: bottom, right
* Line spacing: 1.5
* Font face: Times New Roman
* Headings: 14pt, Bold
* Normal: 12pt
* Referencing and in-text citation should be done strictly using Harvard Referencing System.

### Guidelines for the practical work
* Students are strictly required to submit created all data and scripts files (Ex: `.CSV`, `R`, `PostgreSQL`), Database backups and include screenshots showing important and major steps of the practical work related to each task in separate appendixes. Ex: Appendix A for Task a, Appendix B for Task b etc.
* All Supportive materials should be labeled as per the task name. DO NOT submit the dataset provided for your practical work.
* Task 1, Task 2 should be completed using R / RStudio and Task 3 Should be completed using QGIS, POSTGRESQL and Google Earth. Task 4 should be completed using Power BI tools.
* For each task a separate dataset has been provided under a folder labeled by task name.

---

### Marking/Assessment Criteria

| Task | Poor (< 40) | Satisfactory (40 - 49) | Good (50 - 59) | Very Good (60 - 69) | Excellent (70 - 100) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Task a**<br>(30 Marks) | No or Very poor reporting and statistical testing has been done based on subject matter. Ordinary discussion included based on the findings. No citations or referencing included. | Basic reporting with hypothesis based normality and correlation testing has been done for the subject matter while selecting most suitable variables. Full scale of regression analysis (simple linear and multiple linear) has been done for the subject matter. Basic discussion included based on the findings. Citations and referencing included but contains some errors. | Good reporting with hypothesis based normality and correlation testing has been done for the subject matter while selecting most suitable variables. Scatterplot graphical simulation has been supported with the findings. Basic discussion included based on the findings. Full scale of regression analysis (simple linear and multiple linear) has been done for the subject matter. Scatter plot graphical simulation has been supported with the findings. Precise statistical model(s) has been developed. Good discussion included based on the findings. | Very good reporting with hypothesis based normality and correlation testing has been done for the subject matter while selecting most suitable variables. Scatterplot graphical simulation has been supported with the findings. Basic discussion included based on the findings. A full scale of regression analysis (simple linear and multiple linear) has been done for the subject matter. Scatter plot graphical simulation has been supported with the findings. Precise statistical model(s) has been developed. Very good discussion included based on the findings. Proper citations and referencing included. | Excellent reporting with full scale of hypothesis based normality and correlation tests have been done for the subject matter. Scatter plot graphical simulations have been supported with the findings. Excellent critical discussion included based on the findings. Full scale of regression analysis (simple linear and multiple linear) has been done for the subject matter. Scatter plot graphical simulation has been supported with the findings. Precise statistical model(s) has been developed. Excellent discussion included based on the findings. Proper citations and referencing included. |
| **Task b**<br>(20 Marks) | No or Very poor network graph has been included. Ordinary discussion included based on the Social Network Analysis findings. No citations or referencing included. | Basic network graph has been included to visualize information clearly. Suitable screen shots of the work have been included in appendix. Basic discussion included based on the Social Network Analysis findings. Citations and referencing included but contains some errors. | Good network graph with all required information has been included. All standard graph have been included to easily read the map. Suitable screen shots of the work have been included in appendix. Good discussion included based on the Social Network Analysis findings. Proper citations and referencing included. | Very good network graph with all required information has been included. All standard graph elements have been included to easily read the map. Suitable screen shots of the work have been included in appendix. Very good discussion included based on the Social Network Analysis findings. Proper citations and referencing included. | Excellent network graph with all required information has been included. All standard graph elements have been included to easily read the map. A suitable base map has been included. The graph has been properly captioned. Suitable screen shots of the work have been included in appendix. Excellent critical discussion included based on the Social Network Analysis findings. Proper citations and referencing included. |
| **Task c**<br>(30 Marks) | No or Very poor ordinary map has been included. Ordinary discussion included based on the findings. No citations or referencing included. | Basic map with some required digitized information has been included. The aerial image has been georeferenced and then digitized. A suitable geo-processing tools such as buffering, clipping and intersection etc. has been used. Suitable screen shots of the work have been included in appendix. Basic discussion included. Citations and referencing included but contains some errors. | Good map with all required digitized information has been included. All standard map elements (North Arrow, Map Scale-Graphic, Map Scale-numeric, Map title, Map legends) have been included to easily read the map. The aerial image has been georeferenced and then digitized. A suitable geo-processing tools such as buffering, clipping and intersection etc. has been used. KML/KMZ file(s) included using Google Earth. A Geo spatial database has been developed using PostgreSQL spatial DBMS and populated with required data. A suitable base map has been included and area found. Suitable screen shots of the work have been included in appendix. Good discussion included. Proper citations and referencing included. | Very good map with all required digitized information has been included. All standard map elements (North Arrow, Map Scale-Graphic, Map Scale-numeric, Map title, Map legends) have been included to easily read the map. The aerial image has been georeferenced and then digitized. A suitable geo-processing tools such as buffering, clipping and intersection etc. has been used. KML/KMZ file(s) included using Google Earth. A Geo spatial database has been developed using PostgreSQL spatial DBMS and populated with required data. A suitable base map has been included. Suitable screen shots of the work have been included in appendix. Very good discussion included. Proper citations and referencing included. | Excellent map with all required digitized information has been included. All standard map elements (North Arrow, Map Scale-Graphic, Map Scale-numeric, Map title, Map legends) have been included to easily read the map. The aerial image has been georeferenced and then digitized. A suitable geo-processing tools such as buffering, clipping and intersection etc. has been used. KML/KMZ file(s) included using Google Earth. A Geo spatial database has been developed using PostgreSQL spatial DBMS and populated with required data. A suitable base map has been included. The map has been properly captioned. Suitable screen shots of the work have been included in appendix. Excellent critical discussion included. Proper citations and referencing included. |
| **Task d**<br>(20 Marks) | No or Very poor BI Dashboard has been included. Ordinary discussion included based on the findings. No citations or referencing included. | Basic BI Dashboard with some required information has been included. Suitable screen shots of the work have been included in appendix. Basic discussion included. Citations and referencing included but contains some errors. | Good BI Dashboard with all required information has been included. All standard Dashboard elements have been included to easily read the Dashboard. A suitable base map has been included. KML/KMZ file(s) included using Google Earth. Suitable screen shots of the work have been included in appendix. Good discussion included. Proper citations and referencing included. | Very good BI Dashboard with all required information has been included. All standard Dashboard elements have been included to easily read the Dashboard. Suitable screen shots of the work have been included in appendix. Very good critical discussion included. Proper citations and referencing included. | Excellent BI Dashboard with all required information has been included. All standard Dashboard elements have been included to easily read the map. Suitable screen shots of the work have been included in appendix. Excellent critical discussion included. Proper citations and referencing included. |

---

## Further Information

### Who can answer questions about my assessment?
Questions about the assessment should be directed to the staff member who has set the task/assessment brief. This will usually be the Module Leader. They will be happy to answer any queries you have.

Staff members can often provide feedback on an assignment plan but cannot review any drafts of your work prior to submission. The only exception to this rule is for Dissertation Supervisors to provide feedback on a draft of your dissertation.

### Referencing and independent learning
Please ensure you reference a range of credible sources, with due attention to the academic literature in the area. The time spent on research and reading from good quality sources will be reflected in the quality of your submitted work.

Remember that what you get out of university depends on what you put in. Your teaching sessions typically represent between 10% and 30% of the time you are expected to study for your degree. A 20-credit module represents 200 hours of study time. The rest of your time should be taken up by self-directed study.

Unless stated otherwise you must use the **HARVARD** referencing system. Further guidance on referencing can be found in the Study Smart area on Moodle and at www.citethemrightonline.com (use your university login details to access the site). Correct referencing is an easy way to improve your marks and essential in achieving higher grades on most assessments.

### Technical submission problems
It is strongly advised that you submit your work at least 24 hours before the deadline to allow time to resolve any last minute problems you might have. If you are having issues with IT or Turnitin you should contact the IT Helpdesk on (+44) 2920 417000. You may require evidence of the Helpdesk call if you are trying to demonstrate that a fault with Moodle or Turnitin was the cause of a late submission.

### Extensions and mitigating circumstances
Short extensions on assessment deadlines can be requested in specific circumstances. If you are encountering particular hardship which has been affecting your studies, then you may be able to apply for mitigating circumstances. This can give the teachers on your programme more scope to adapt the assessment requirements to support your needs. Extensions and mitigating circumstances policies and procedures are regularly updated. You should refer to your degree programme or school Moodle pages for information on extensions and mitigating circumstances.

### Unfair academic practice
Cardiff Met takes issues of unfair practice extremely seriously. The University has procedures and penalties for dealing with unfair academic practice. These are explained in full in the University's Unfair Practice regulations and procedures under Volume 1, Section 8 of the Academic Handbook. The Module Leader reserves the right to interview students regarding any aspect of their work submitted for assessment.

#### Types of Unfair Practice, include:
1. **Plagiarism**, which can be defined as using without acknowledgement another person’s words or ideas and submitting them for assessment as though it were one’s own work, for instance by copying, translating from one language to another or unacknowledged paraphrasing. Further examples include:
   * Use of any quotation(s) from the published or unpublished work of other persons, whether published in textbooks, articles, the Web, or in any other format, where quotations have not been clearly identified as such by being placed in quotation marks and acknowledged.
   * Use of another person’s words or ideas that have been slightly changed or paraphrased to make it look different from the original.
   * Summarising another person’s ideas, judgments, diagrams, figures, or computer programmes without reference to that person in the text and the source in a bibliography/reference list.
   * Use of assessment writing services, essay banks and/or any other similar agencies (NB. Students are commonly being blackmailed after using essay mills).
   * Use of unacknowledged material downloaded from the Internet.
   * Re-use of one’s own material except as authorised by your degree programme.
2. **Collusion**, which can be defined as when work that has been undertaken with others is submitted and passed off as solely the work of one person. Modules will clearly identify where joint preparation and joint submission are permitted, in all other cases they are not.
3. **Fabrication of data**, making false claims to have carried out experiments, observations, interviews or other forms of data collection and analysis, or acting dishonestly in any other way.

### How is my work graded?
Assessment grading is subject to thorough quality control processes. You can view a summary of these processes on the Assessment Explained Infographic. Grading of work at each level of Cardiff Met degree courses is benchmarked against a set of general requirements set out in Volume 1, Section 4.3 of our Academic Handbook. A simplified version of these Grade Band Descriptors (GBDs) with short videos explaining some of the academic terminology used can be accessed via the Facilitation of Learning resource page.

We would strongly recommend looking at the Study Smart area of Moodle to find out more about assessments and key academic skills which can have a significant impact on your grades. Always check your work thoroughly before submission.
