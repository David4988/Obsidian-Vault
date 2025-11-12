
*Core Idea:* To explicitly command the model to ignore the fake "ghost" data we added during padding.

* *Analogy:* A cheat sheet given to the model along with the data.
* *How it works:* We create a sequence of 1s and 0s.
    * 1: "Pay attention, this is a real post."
    * 0: "Ignore this completely, it's fake padding."
* *Why?* This prevents the model from getting confused and learning from meaningless zero vectors, which would destroy its performance. It's a critical step for safely handling variable-length sequences.

*Links:* [[✂ The Photo Album - Padding & Truncating]]