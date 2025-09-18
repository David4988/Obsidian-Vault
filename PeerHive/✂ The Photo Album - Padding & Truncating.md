
*Core Idea:* To force every user's post history into the same fixed length for the sequence model.

* *Analogy:* A machine with a conveyor belt that has exactly 20 slots.
* *Short Sequences (<20 posts):* We fill the empty slots with blank, zero-filled "ghost" posts. This is *Padding*.
* *Long Sequences (>20 posts):* We only take the most recent 20 posts and ignore the rest. This is *Truncating*.

This ensures the model's input is always the same shape.

*Links:* [[🎭 The Cheat Sheet - Attention Masking]]