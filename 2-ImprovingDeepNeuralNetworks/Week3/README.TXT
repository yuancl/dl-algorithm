- Tensorflow is a programming framework used in deep learning
- The two main object classes in tensorflow are **Tensors and Operators**.
- When you code in tensorflow you have to take the following steps:
    - Create a graph containing **Tensors** (Variables, Placeholders ...) and **Operations** (tf.matmul, tf.add, ...)
    - Create a session
    - Initialize the session
    - Run the session to execute the graph
- You can execute the graph multiple times as you've seen in model()

- The backpropagation and optimization is automatically done when running the session on the "optimizer" object



**Writing and running programs in TensorFlow has the following steps:**
-   Create Tensors (variables) that are not yet executed/evaluated.
-   Write operations between those Tensors.
-   Initialize your Tensors.
-   Create a Session.
-   Run the Session. This will run the operations you'd written above.

**computation graph**
