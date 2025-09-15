# Winning Solution for STEM GAMES – M Arena

**Team:**
*   Roko Čubrić
*   Borna Gojšić
*   David Janjić
*   Roko Karničić

**Institution:** University of Zagreb, Faculty of Electrical Engineering and Computing

---

## About the Competition

STEM Games is a student competition that gives students from STEM fields (Science, Technology, Engineering, and Mathematics) an opportunity to showcase their knowledge and skills in solving real-world engineering problems. The Math Arena (M Arena) is specifically focused on mathematical modeling and computational problem-solving.

## Project Summary

This repository contains the winning solution for the M Arena competition at STEM Games. The project addresses the critical problem of data protection in digital communication channels, with a special focus on its application in banking transactions. Our team developed a comprehensive solution that leverages advanced error correction coding techniques to ensure the integrity and reliability of data throughout the transaction process.

## Core Concepts

Our solution is grounded in information and coding theory, utilizing fundamental concepts such as entropy, channel coding, and perfect codes.

### Entropy as a Measure of Information

Entropy is a key concept in information theory that quantifies the amount of uncertainty or information in a data source. We used entropy as a foundational measure to analyze the characteristics of the communication channel and the information being transmitted.

### Error Correction Codes

To protect data from errors caused by noise and interference in the channel, we implemented a multi-layered coding strategy.

*   **Hamming Codes:** These are a class of linear error-correcting codes capable of detecting up to two-bit errors or correcting one-bit errors. We designated their use for protecting data at rest, such as on SSDs and HDDs.
*   **Golay Codes:** The Golay code is a type of perfect code known for its powerful error-correcting capabilities. In our solution, we used the binary Golay code as part of a strategy to protect a 100-bit data block.
*   **Reed-Solomon Codes:** These codes are exceptionally effective at correcting burst errors (i.e., a sequence of consecutive bit errors). This makes them ideal for a wide range of applications, including:
    *   CDs/DVDs (correcting scratches)
    *   QR Codes (reading damaged codes)
    *   NASA Deep Space Communication (overcoming cosmic noise)
    *   DVB-S2 (satellite TV)

## Application in Banking Transactions

We analyzed a typical banking transaction to identify critical points where data integrity is at risk.

#### Transaction Stages:
1.  **Initialization:** Starting the transaction.
2.  **Validation & Authorization:** Verifying credentials and funds.
3.  **Database Processing:** Committing the transaction to the ledger.
4.  **Confirmation & Completion:** Finalizing the transaction.

#### Potential Physical Layer Errors:
*   **Bit-flips (Single Event Upset - SEU):** Spontaneous bit changes caused by radiation or interference.
*   **Network Infrastructure Failures:** Errors during data transmission.
*   **Data Storage Failures (SSD/HDD):** Bit rot or corruption of data at rest.
*   **Hardware Security Module (HSM) Issues:** Errors within the secure processing hardware.

## The Proposed Solution

Our solution is a hybrid error correction system tailored to protect different parts of the transaction lifecycle. The ultimate goal is to achieve maximum **efficiency** by ensuring both the **speed** and **security** of the transaction.

### 1. Protecting Data in Transit
To guard against bit-flips (SEUs) and burst errors common in network communication, we propose using **Reed-Solomon** and **Golay codes**. These robust codes can handle both single-bit and multi-bit burst errors, making them ideal for securing data as it moves through the network. We also recommend prioritizing optical fiber over copper (Ethernet) and wireless channels to reduce the frequency of errors.

### 2. Protecting Data at Rest
To prevent corruption in stored data on SSDs and HDDs, we recommend the implementation of **Hamming codes**. They are computationally efficient and highly effective at correcting the single-bit errors that are a common failure mode in storage devices.

By applying the right code to the right problem, our solution creates a resilient and reliable system for handling sensitive financial transactions.
