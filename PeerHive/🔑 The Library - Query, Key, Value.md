
*Core Idea:* The "attention" mechanism is like looking something up in a library.

* *Query:* Your question. The information you have.
    * Example: A text token, like the embedding for the word "cat."
* *Key:* The "titles" on the spines of the books. The information you scan to find a match.
    * Example: The summary "titles" of all the image patches. The "cat" query looks for the patch whose Key is most similar.
* *Value:* The content inside the book. The information you retrieve once you find a match.
    * Example: The actual content/features of the best-matching image patch.

In our model, for an image patch, its "title" (Key) and its "content" (Value) are the same thing: its collection of visual features (color, texture, etc.).

*Links:* [[🧠The Brains - Cross-Attention]]

---
