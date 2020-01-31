---
layout: project 
type: project
image: images/huffman.gif
title: "Huffman Tree Code"
permalink: projects/huffman-tree-code
# All dates must be YYYY-MM-DD format!
date: 2020-01-21
labels:
  - Huffman
  - Problem Solving
summary: Learned how to decide what data structure to use for certain situations.
---
<img class="ui medium right floated rounded image" src="../images/huffman.gif">
  This project's purpose was to continue to use binary trees and learning how the system works as well as how to use it.  I was to create the body of the functions decode, encode, and decompress.  Learning outcomes for this project were to use Huffman trees to encode and decode files and write a program that decompresses files that were compressed using Huffman encoding.  This project helped me be more comfortable with Binary Trees/Huffman Trees, reading binary data using java, and reading/understanding/modifying existing java code using Eclipse.  
The code for the constructor, decode, and decompress functions is shown below: 
```js
  /**
   * Builds a Huffman tree as read from the given input bit stream.
   * <p>The stream must be at the start of the tree data, after the byte count header.
   * Reads from the stream until the end of the tree, which leaves the given BitReader
   * at the start of the encoding data.</p>
   *
   * @param input a BitReader at the start of the pre-order traversal of the Huffman.
   * @throws IOException If cannot read from stream.
   */
  public Huffman(BitReader input) throws IOException {
   //visit the node
    this.root = preOrder(input);
  }


/**
  * Helper method for the decode method
  * @param temp
  * @param bytes
  * @param in
  * @param out
  * @throws IOException
  */
  private void decode(HuffmanNode<Byte> temp, int bytes, BitReader in, OutputStream out) throws IOException {
      if (temp.isLeaf()) {
        out.write(temp.getData());
      } else if (in.read()) {
        decode(temp.getRight(), bytes, in, out);
    //0 means traverse to the left
      } else {
        decode(temp.getLeft(), bytes, in ,out);
      }
  }


  /**
   * Decompresses the given input stream, writing to the given output stream.
   *
   * @param in the InputStream.
   * @param out the OutputStream.
   * @throws IOException If there are any read/write error.
   */
  public static void decompress(InputStream in, OutputStream out) throws IOException {
    BitReader bite = new BitReader(in);
    // read in byte count from BitReader
    int b = bite.readInt();
    // build a tree = new Huffman(BitReader)
      //create an instance of Huffman from a BitReader
    Huffman huff = new Huffman(bite);
    // use tree to decode given number of byte from bitreader
    huff.decode(b, bite, out);
  }
}
```

  Attached at the bottom of this paragraph is the link to our assignment outline.  It will show all the requirements we had to meet for our programming.  This was a moderate level in terms of difficulty because it was using methods we had done all semester, but I was also just learning what Huffman Trees were.  I developed better problem-solving skills with this project because I kept getting a null-pointer exception and it took a lot of collaboration to figure out what the problem was.  I did many debugs and step-by-step evaluating to see where the problem rooted.  
For more information on te requirements: [click here](http://courses.ics.hawaii.edu/ics211f18/morea/120.trees/experience-H11.html).

