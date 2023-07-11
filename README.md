# Harry Potter Character Network Analysis

This repository contains Python code for analyzing character networks in the 'Harry Potter' series. It includes two approaches: one utilizing Spark for distributed processing, and another using an iterative approach.


## Project motivation
- **Character Relationships:** Analyzing character networks provides insights into the relationships and dynamics among the characters in the beloved 'Harry Potter' series.
- **Understanding the Story:** Character interactions are a crucial element of the narrative, and network analysis helps uncover their significance.
- **Visualization:** Network graphs visually depict the connections and strength of relationships, offering an intuitive representation of the character network.
- **Co-occurrence and Sentiment Analysis:** Examining co-occurrence patterns and sentiment between characters reveals their associations and emotional connections.
- **Spark and Iterative Approaches:** Two different approaches are provided to accommodate varying dataset sizes and processing needs.
- **Engaging Analysis for Fans:** Fans of 'Harry Potter' can explore and appreciate the intricate web of relationships among their favorite characters.

## Sentiment Graph Analysis

The sentiment graph analysis provides valuable insights into the relationships among characters in the 'Harry Potter' series. Each node represents a character, and each edge represents the relationship between two connected characters.

- **Node Importance:** The size of each node corresponds to the importance of the character in the novel. It is measured by the frequency of their name occurrence throughout the series. Notably, characters like Harry, Ron, and Hermione, who play central roles, emerge as the top three characters in terms of importance.

- **Sentiment Relationships:** The edges in the graph are color-coded, ranging from bright (yellow) to dark (purple), representing the sentiment relationship between two connected characters. Brighter colors signify friendly or positive relationships, while darker colors indicate hostile or negative relationships. By simply observing the graph, it becomes apparent that Harry has the most bright connections with other characters, highlighting his strong bonds and alliances. Conversely, Voldemort possesses mostly dark connections, underscoring his antagonistic nature and strained relationships with others.

- **Story Progression:** The sentiment graph captures the evolving dynamics of character relationships throughout the series. The edges change as the story progresses, reflecting the shifting alliances, conflicts, and character developments that unfold across the episodes. By splitting the novel series into episodes, the graph adapts its edge parameters to illustrate the changing relationship dynamics among characters over time.

- **Plot Validation:** The sentiment graph aligns with key plot elements and memorable events from the 'Harry Potter' series. It accurately depicts the nature of character interactions, reinforcing the authenticity and reliability of the graph's representation. As a fan of the series, you can validate the graph's correctness and enjoy a deeper understanding of the intricate character dynamics.

The sentiment graph analysis provides a visually appealing and intuitive way to explore the relationships and dynamics between characters in the 'Harry Potter' series. By examining the node sizes, edge colors, and the changing edges throughout the story, you can gain valuable insights into the interplay of characters, their alliances, conflicts, and the overall narrative structure.


## Description

The code performs character network analysis on the 'Harry Potter' series, focusing on co-occurrence and sentiment relationships among characters. It includes two code snippets:

- `characterNetwork-distributed.py`: Utilizes Spark for distributed processing, performing name entity recognition (NER) and calculating co-occurrence and sentiment matrices. It visualizes network graphs using the Spark-based approach.

- `characterNetwork-iterative.py`: Uses an iterative approach for NER (name entity recognition), filtering names based on frequency threshold, and calculating co-occurrence and sentiment matrices. It visualizes network graphs based on the iterative approach.

## Features

- Distributed processing using Spark for large-scale character network analysis
- Iterative approach for smaller datasets or without Spark
- NER (name entity recognition) for extracting character names
- Co-occurrence and sentiment analysis
- Network graph visualization
- Graph plotting for the entire series and individual seasons

## Usage

1. Install the required libraries mentioned in the code.
2. Place the 'Harry Potter' novels in a folder named 'novels' in the repository directory.
3. Adjust the code parameters as needed (e.g., top number of names, frequency threshold).
4. Run the code snippets (`characterNetwork-distributed.py` and `characterNetwork-iterative.py`) in a Python environment.
5. Network graphs will be generated as PNG files in the repository directory.

## References

- [Spacy](https://spacy.io/)
- [NetworkX](https://networkx.org/)
- [Matplotlib](https://matplotlib.org/)
- [Spark](https://spark.apache.org/)


