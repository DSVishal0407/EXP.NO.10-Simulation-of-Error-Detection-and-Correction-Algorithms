# EXP.NO.10-Simulation-of-Error-Detection-and-Correction-Algorithms
10.Simulation of Error Detecion and Correction Algorithms

# AIM
To simulate error detection and correction techniques, such as Parity Check and Hamming Code, and to understand their working principles using Python programming.

# SOFTWARE REQUIRED
Python

# ALGORITHMS
1. Parity Check (Error Detection)

Count the number of 1’s in the data.

Add a parity bit to make the total number of 1’s even (even parity) or odd (odd parity).

At the receiver, recount the 1’s to detect any error.

2. Hamming Code (Error Detection and Correction)

Insert parity bits at positions that are powers of 2 (1, 2, 4, etc.).

Calculate each parity bit based on a specific set of data bits.

At the receiver, recompute parity to find the error position.

If an error is found, flip the bit to correct it.

# PROGRAM
def add_parity_bit(data):
    count = data.count('1')
    if count % 2 == 0:
        return data + '0'
    else:
        return data + '1'

def detect_error(received_data):
    count = received_data.count('1')
    if count % 2 == 0:
        return "No Error Detected"
    else:
        return "Error Detected"

# Example: Parity Bit Checking
data = '1010011'
print("Original Data:", data)
transmitted_data = add_parity_bit(data)
print("Transmitted Data with Parity Bit:", transmitted_data)
received_data = transmitted_data  # Assume no error
print("Receiver Check:", detect_error(received_data))

# Hamming Code (7,4) Implementation (Single Bit Error Correction)

def encode_hamming(data_bits):
    # data_bits is a string of 4 bits
    bits = ['0'] * 7
    bits[2] = data_bits[0]
    bits[4] = data_bits[1]
    bits[5] = data_bits[2]
    bits[6] = data_bits[3]

    # Calculate parity bits
    bits[0] = str((int(bits[2]) + int(bits[4]) + int(bits[6])) % 2)  # p1
    bits[1] = str((int(bits[2]) + int(bits[5]) + int(bits[6])) % 2)  # p2
    bits[3] = str((int(bits[4]) + int(bits[5]) + int(bits[6])) % 2)  # p4

    return ''.join(bits)

def detect_and_correct(received):
    received = list(received)
    p1 = (int(received[0]) + int(received[2]) + int(received[4]) + int(received[6])) % 2
    p2 = (int(received[1]) + int(received[2]) + int(received[5]) + int(received[6])) % 2
    p4 = (int(received[3]) + int(received[4]) + int(received[5]) + int(received[6])) % 2
    error_pos = p4 * 4 + p2 * 2 + p1 * 1
    if error_pos != 0:
        print(f"Error detected at position {error_pos}")
        received[error_pos-1] = '1' if received[error_pos-1] == '0' else '0'
    else:
        print("No Error Detected")
    return ''.join(received)

# Example: Hamming Code
data_bits = '1011'
print("\nOriginal 4 Data Bits:", data_bits)
encoded_bits = encode_hamming(data_bits)
print("Encoded 7 Bits with Parity:", encoded_bits)

# Introduce an error
received = list(encoded_bits)
received[3] = '1' if received[3] == '0' else '0'  # Flip one bit
received = ''.join(received)

print("Received (with error):", received)
corrected = detect_and_correct(received)
print("Corrected Code:", corrected)

# OUTPUT

Original Data: 1010011
Transmitted Data with Parity Bit: 10100110
Receiver Check: No Error Detected

Original 4 Data Bits: 1011
Encoded 7 Bits with Parity: 0110011
Received (with error): 0111011
Error detected at position 4
Corrected Code: 0110011
 
# RESULT / CONCLUSIONS
1. The simulation of error detection using Parity Check and error detection and correction using Hamming Code was successfully performed.

2. Parity bits were able to detect single-bit errors.

3. Hamming code successfully detected and corrected single-bit errors.

Thus, the experiment successfully demonstrated basic error control techniques in digital communications.
