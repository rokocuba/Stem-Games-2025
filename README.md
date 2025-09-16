# Winning Solution - STEM Games 2025 M Arena

**Team:**
*   Roko Čubrić
*   Borna Gojšić
*   David Janjić
*   Roko Karničić

**Institution:** University of Zagreb, Faculty of Electrical Engineering and Computing

<p align="center">
  <img src="images/pic1.jpg" alt="Team Structure" width="700"/>
  <br>
  <em>The Winning photo with (from left to right): Myself, Borna and David</em>
</p>
---

## Project Overview

This repository contains the winning solutions for the M Arena at STEM Games 2025. The competition was divided into theoretical and programming tasks rooted in information theory and error-correcting codes.

*   **Theoretical Tasks:** Required the mathematical derivation of formulas related to channel capacity, entropy, and coding theory.
*   **Programming Tasks:** Involved designing and implementing custom error-correcting codes for several "exotic" communication channels, each with unique error characteristics.

This README focuses on the programming solutions, particularly our implementation of a hybrid Golay-Hamming code.

## Core Achievement: Hybrid Golay & Hamming Code

The most significant part of our solution was a robust hybrid coding scheme designed for a channel that could introduce up to **10 random bit errors** in a **100-bit message**. Our full implementation, including the encoder, decoder, and syndrome lookup table, can be found in<br> `day 3/Golay_implementation.ipynb`.

### The Challenge

The task was to devise a protective code for a 100-bit message. The channel's noise was significant, capable of flipping up to 10 bits in the original message. A simple, single coding scheme was unlikely to be efficient or effective enough.

### Our Solution: A Hybrid Approach

We partitioned the 100-bit message and applied the best available code for each segment's size.

1.  The 100-bit message is split into **eight 12-bit blocks** and **one 4-bit block**.
2.  Each of the eight 12-bit blocks is encoded using the **Extended Binary Golay Code [24, 12, 8]**.
3.  The final 4-bit block is encoded using the **Hamming Code [7, 4, 3]**.

This results in a final message of `(8 * 24) + 7 = 199` bits being sent through the channel.

### Implementation Details (`day 3/Golay_implementation.ipynb`)

Our Python implementation in the Jupyter Notebook handles the entire process:

*   **Matrices:** Defines the generator and parity-check matrices for both the Golay `G(24,12)` and Hamming `H(7,4)` codes.
*   **Syndrome Hash Map:** A key feature is the `return_syndrome_hash_map` function. It pre-calculates the error pattern corresponding to every possible syndrome for the given code. This creates a highly efficient lookup table (a dictionary in Python) that allows for near-instantaneous decoding.
    *   The Golay code has a minimum distance of 8, allowing it to correct any combination of up to `floor((8-1)/2) = 3` errors within its 24-bit block.
    *   The Hamming code has a minimum distance of 3, allowing it to correct any single-bit error within its 7-bit block.
*   **Encoder (`ENCODE_CHANNEL_MESSAGE`):** Takes a 100-bit message, performs the 8+1 block split, and encodes each block using the appropriate generator matrix.
*   **Decoder (`DECODE_CHANNEL_MESSAGE`):** Takes the 199-bit received message, splits it back into encoded blocks, calculates the syndrome for each, and uses the pre-computed hash map to find and flip the erroneous bits, thereby correcting the message.

## Additional Solution: 2D Parity Code

Another task involved protecting a 100-bit message using exactly 20 protection bits against scattered, non-consecutive errors. Our solution for this can be found in `prvi.ipynb`.

### The Challenge (1st Channel)

-   **Message bits (n):** 100
-   **Protection bits (k):** 20
-   **Max errors (t):** 10
-   **Error type:** Uniformly random, non-bursty.

### Our Solution (`prvi.ipynb`)

We implemented a heuristic, 2D parity check code. The 100 message bits are treated as a 10x10 grid.

*   **Parity Set 1 (10 bits):** Parity bits are calculated for each of the 10 columns.
*   **Parity Set 2 (10 bits):** A second set of 10 parity bits is calculated along diagonals (using a stride of 11 through the 1D array) to provide a second dimension for error location.

When an error occurs, it will trip one parity check in the first set and one in the second. The intersection of these failing checks can be used to locate and correct single-bit errors. This custom, lightweight approach was designed to fit the specific constraints of the problem.
