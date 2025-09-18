*Core Idea:* To condense a detailed sequence of information into a single, fixed-size summary.

* *Analogy:* A talent show judge summarizing a 3-minute performance into a single score.
* *Why?* The next layer of the model (the MLP Head) needs a fixed-size input. It can't handle a variable number of tokens or patches.
* *How?* We simply take the mean of all the token/patch embeddings after the attention step.

This creates a smart summary vector (z_fused) that represents the entire post, ready for the final decision.

*Links:* [[👩‍⚕The Specialist Doctor - MLP Head]]