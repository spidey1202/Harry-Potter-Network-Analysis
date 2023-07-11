# Harry Potter Character Network Analysis

This repository contains Python code for analyzing character networks in the 'Harry Potter' series. It includes two approaches: one utilizing Spark for distributed processing, and another using an iterative approach.



## Project motivation
- **Character Relationships:** Analyzing character networks provides insights into the relationships and dynamics among the characters in the beloved 'Harry Potter' series.
- **Understanding the Story:** Character interactions are a crucial element of the narrative, and network analysis helps uncover their significance.
- **Visualization:** Network graphs visually depict the connections and strength of relationships, offering an intuitive representation of the character network.
- **Co-occurrence and Sentiment Analysis:** Examining co-occurrence patterns and sentiment between characters reveals their associations and emotional connections.
- **Spark and Iterative Approaches:** Two different approaches are provided to accommodate varying dataset sizes and processing needs.
- **Engaging Analysis for Fans:** Fans of 'Harry Potter' can explore and appreciate the intricate web of relationships among their favorite characters.


## Usage

1. Install the required libraries mentioned in the code.
2. Place the 'Harry Potter' novels in a folder named 'novels' in the repository directory.
3. Adjust the code parameters as needed (e.g., top number of names, frequency threshold).
4. Run the code snippets (`characterNetwork-distributed.py` and `characterNetwork-iterative.py`) in a Python environment.
5. Network graphs will be generated as PNG files in the repository directory.



## Features

- Distributed processing using Spark for large-scale character network analysis
- Iterative approach for smaller datasets or without Spark
- NER (name entity recognition) for extracting character names
- Co-occurrence and sentiment analysis
- Network graph visualization
- Graph plotting for the entire series and individual seasons




## Sentiment Graph Analysis

![ezgif-5-e98e242d28ba](https://user-images.githubusercontent.com/30411828/55665266-d5e96380-586e-11e9-89af-c1a5da88d46f.gif)

The sentiment graph analysis provides valuable insights into the relationships among characters in the 'Harry Potter' series. Each node represents a character, and each edge represents the relationship between two connected characters.

- **Node Importance:** The size of each node corresponds to the importance of the character in the novel. It is measured by the frequency of their name occurrence throughout the series. Notably, characters like Harry, Ron, and Hermione, who play central roles, emerge as the top three characters in terms of importance.

- **Sentiment Relationships:** The edges in the graph are color-coded, ranging from bright (yellow) to dark (purple), representing the sentiment relationship between two connected characters. Brighter colors signify friendly or positive relationships, while darker colors indicate hostile or negative relationships. By simply observing the graph, it becomes apparent that Harry has the most bright connections with other characters, highlighting his strong bonds and alliances. Conversely, Voldemort possesses mostly dark connections, underscoring his antagonistic nature and strained relationships with others.

- **Story Progression:** The sentiment graph captures the evolving dynamics of character relationships throughout the series. The edges change as the story progresses, reflecting the shifting alliances, conflicts, and character developments that unfold across the episodes. By splitting the novel series into episodes, the graph adapts its edge parameters to illustrate the changing relationship dynamics among characters over time.

- **Plot Validation:** The sentiment graph aligns with key plot elements and memorable events from the 'Harry Potter' series. It accurately depicts the nature of character interactions, reinforcing the authenticity and reliability of the graph's representation. As a fan of the series, you can validate the graph's correctness and enjoy a deeper understanding of the intricate character dynamics.

The sentiment graph analysis provides a visually appealing and intuitive way to explore the relationships and dynamics between characters in the 'Harry Potter' series. By examining the [**graphs**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/tree/main/graphs) with node sizes, edge colors, and the changing edges throughout the story, you can gain valuable insights into the interplay of characters, their alliances, conflicts, and the overall narrative structure.



## Steps

1. **Data Preparation:**
- Before diving into the analysis, we need to prepare the necessary files. The [**novels**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/tree/main/novels) file contain the text of the 'Harry Potter' series, which will be split into sentences for further processing.
- Additionally, the [**common_words.txt**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/blob/main/common_words.txt) file includes a list of commonly used English words to filter out non-name words during the name entity recognition process.

2. **Name Entity Recognition:**

- To identify the characters in the novels, we employ name entity recognition (NER) using the pretrained **Spacy NER** classifier. Since initializing the Spacy NLP class requires substantial memory, we leverage the **PySpark distribution** to perform NER on a sentence-by-sentence basis.
- For each sentence, we extract the name entities, split multi-word names into individual words (e.g., "Harry Potter" becomes ['Harry', 'Potter']), and remove any names found in the list of common words. After aggregating the names from each sentence, we apply a user-defined threshold to filter out names with low occurrence frequency, ensuring accuracy in character identification.

3. **Character Importance:**

- From the preliminary list of character names obtained through NER, we calculate the importance of each character based on their occurrence frequency.
- Using the **Scikit-Learn** text processing function `CountVectorizer`, we generate an occurrence matrix to count the occurrences of character names in each sentence.
- We then select the top characters of interest based on their importance, in this case, the top 25 characters.

4. **Co-occurrence Matrix:**

- The co-occurrence matrix captures the interaction intensity or co-occurrence of characters in the novel.
- We start by creating a binary occurrence matrix that indicates whether a name occurs in each sentence.
- Next, we compute the co-occurrence matrix by taking the dot product of the occurrence matrix and its transpose.
- To eliminate redundancy and ensure symmetry, we triangularize the matrix and set the diagonal elements to zero.
<p align="center"><img width="220" alt="formula1" src="https://user-images.githubusercontent.com/30411828/55671792-42dc1800-58c6-11e9-973b-d66c7a726f77.png"></p>
<p align="center"><img width="600" alt="formula5" src="https://user-images.githubusercontent.com/30411828/55672777-783a3300-58d1-11e9-93fe-909d78ed01c2.png"></p>

5. **Sentiment Matrix:**

- The sentiment matrix reveals the sentiment intimacy between characters, representing the positive or negative relationships they share. To calculate the sentiment matrix, we introduce two concepts: **context sentiment score** and **sentiment alignment rate**.
- The context sentiment score is determined for each sentence using the sentiment analysis library **Afinn**. These scores are stored as a 1-D array to facilitate vectorization.
- The sentiment alignment rate adjusts the sentiment scores to account for different narrative styles and reduce skewness. It modifies the sentiment score between two characters by an amount proportional to the rate whenever a co-occurrence is observed.
- Similar to the co-occurrence matrix, the sentiment matrix is triangularized and the diagonal elements are set to zero.
- The sentiment graph analysis offers a comprehensive understanding of the relationships among characters in the 'Harry Potter' series.
- By following these steps, we can uncover valuable insights into the character importance, co-occurrence patterns, and sentiment dynamics throughout the novels.

<p align="center"><img width="400" alt="formula2" src="https://user-images.githubusercontent.com/30411828/55671901-6bb0dd00-58c7-11e9-9563-d70359835cd8.png"></p>
<p align="center"><img width="500" alt="formula3" src="https://user-images.githubusercontent.com/30411828/55671903-6e133700-58c7-11e9-8739-3df8cab2e746.png"></p>
<p align="center"><img width="560" alt="formula6" src="https://user-images.githubusercontent.com/30411828/55672693-6efc9680-58d0-11e9-9683-6029e7bd84e5.png"></p>



## Graph Parameters and Plot

Once we have the co-occurrence matrix and sentiment matrix, we can proceed to transform them into graph parameters and plot the visual representation of the character relationships.

- **Normalization:** Before plotting the graph, we first normalize the co-occurrence matrix and sentiment matrix. Normalization ensures consistent magnitudes across different novels while preserving the diversity among characters within a single novel.

- **Graph Parameters:** To generate the graph, we convert the normalized matrices into edge lists. The edge lists contain information about the weight and color of each edge in the graph. The weight represents the strength of the relationship between two characters, while the color indicates the sentiment of the relationship. Brighter colors signify more positive relationships, while darker colors indicate more negative relationships. The formulas used to calculate the graph parameters in the `matrix_to_edge_list` and `plot_graph` functions are designed to create visually appealing and aligned plots, without carrying any specific meaning.

- **Plotting:** With the graph parameters in place, we can now plot the graph using the **NetworkX** and **Matplotlib** libraries. The size of each node corresponds to the importance of the character, which is determined by their occurrence frequency. The edges connecting the nodes reflect the relationships between characters, displaying both co-occurrence and sentiment dynamics. The generated graph provides a visually captivating representation of the character network.
  ![aa](https://user-images.githubusercontent.com/30411828/55665312-b141bb80-586f-11e9-9751-274f6e5359c9.png)


## Final output
After completing all the steps outlined above, you can check the generated [**.png files**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/tree/main/graphs) in the designated folder to explore the plots showcasing the character relationships.


## Description on the 2 approaches
1. [**characterNetwork-distributed.py**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/blob/main/characterNetwork-distributed.py)
- Uses Spark for distributed processing
- Applies name entity recognition (NER) function using Spark parallelization
- Filters out names based on frequency threshold
- Calculates co-occurrence and sentiment matrices
- Converts matrices to edge lists for network graph visualization
- Plots network graphs for the entire novel and each season

2. [**characterNetwork-iterative.py**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/blob/main/characterNetwork-iterative.py)
- Performs NER iteratively on sentences
- Filters out names based on frequency threshold
- Calculates co-occurrence and sentiment matrices
- Converts matrices to edge lists for network graph visualization
- Plots network graphs for the entire novel and each season

## Which approach is better between the two?
- The main difference between the two code snippets lies in the approach used for name entity recognition (NER) and processing.
- In [**characterNetwork-distributed.py**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/blob/main/characterNetwork-distributed.py), Spark is utilized to distribute the NER function across multiple sentences, enabling parallel processing. It leverages Spark's parallelization capabilities to handle large-scale processing efficiently. *This approach can be beneficial for handling large volumes of data or when running on distributed systems.*

- On the other hand, [**characterNetwork-iterative.py**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/blob/main/characterNetwork-iterative.py) performs NER iteratively on sentences without using Spark. It processes the sentences sequentially, identifying name entities and filtering them based on a frequency threshold. *This approach is suitable for smaller datasets or when Spark is not available or necessary.*

- Both code snippets follow similar steps for calculating co-occurrence and sentiment matrices, converting them to edge lists, and visualizing network graphs for the entire novel and each season.

- Ultimately, the choice between these code snippets depends on the specific requirements of your application, the size of the dataset, and the available resources. If you have a large dataset or require distributed processing, [**characterNetwork-distributed.py**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/blob/main/characterNetwork-distributed.py) with Spark may be more suitable. Otherwise, [**characterNetwork-iterative.py**](https://github.com/spidey1202/Harry-Potter-Network-Analysis/blob/main/characterNetwork-iterative.py) can be used for sequential processing on smaller datasets.


## References
- [Spacy](https://spacy.io/)
- [NetworkX](https://networkx.org/)
- [Matplotlib](https://matplotlib.org/)
- [Spark](https://spark.apache.org/)


