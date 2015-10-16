Rich document:

When post processing a note's content, we need to create chunks around various assets so that they can be added one by one.

Thus, a note with:

    # header 1
    
    hello

    ``` some sub code that generates an image ```

    good bye

We would need to:

1. Generate the image
2. Tokenize our content:


    # header 1

    hello

    <!-- img#1 -->

    goodbye

3. Create chunks:

Chunk#1:

    # header 1

    hello

Chunk #2:

    <!--img#1-->

Chunk #3:

    goodbye

We would then call:

    append text chunk #1, append attachment chunk #2, append text chunkg #3

.
Here is how a diagram would be handled, for instance:

    blah blah ```diagram blurb blurb ``` blah blah

tokenized:

    blah blah <edeninvi:attach#1> blah blah

(key: attach#1, value: blurb blurb)

run markdown; process attach#1; be ready to append as chunky chunk.





