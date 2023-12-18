# IEEE Floating Point Number Conversion

## Form
Source: [Geeks For Geeks](https://www.geeksforgeeks.org/ieee-standard-754-floating-point-numbers/)

There are several ways to represent floating point number but IEEE 754 is the most efficient in most cases. IEEE 754 has 3 basic components:

1. **The Sign of Mantissa –**  
    This is as simple as the name. 0 represents a positive number while 1 represents a negative number.
2. **The Biased exponent –**  
    The exponent field needs to represent both positive and negative exponents. A bias is added to the actual exponent in order to get the stored exponent.
3. **The Normalised Mantissa –**  
    The mantissa is part of a number in scientific notation or a floating-point number, consisting of its significant digits. Here we have only 2 digits, i.e. O and 1. So a normalised mantissa is one with only one 1 to the left of the decimal.

## Example
Source: [Geeks for Geeks](https://www.geeksforgeeks.org/ieee-standard-754-floating-point-numbers/)

```
85.125
85 = 1010101
0.125 = 001
85.125 = 1010101.001
       =1.010101001 x 2^6 
sign = 0 

1. Single precision:
biased exponent 127+6=133
133 = 10000101
Normalised mantisa = 010101001
we will add 0's to complete the 23 bits

The IEEE 754 Single precision is:
= 0 10000101 01010100100000000000000
This can be written in hexadecimal form **42AA4000**

2. Double precision:
biased exponent 1023+6=1029
1029 = 10000000101
Normalised mantisa = 010101001
we will add 0's to complete the 52 bits

The IEEE 754 Double precision is:
= 0 10000000101 0101010010000000000000000000000000000000000000000000
This can be written in hexadecimal form **4055480000000000**
```

## In Pseudocode
Source: GPT-4

==**BEGIN AI-GENERATED CONTENT**==

Converting a floating point number into its IEEE 754 binary representation involves several steps. Let's consider the 32-bit single-precision format for the example of pi (approximately 3.14159). The IEEE 754 single-precision standard represents a floating-point number with 32 bits, consisting of:

- Sign bit: 1 bit
- Exponent: 8 bits
- Mantissa (or significand): 23 bits

Here's an outline of the process in pseudocode:

```pseudocode
function ConvertToIEEE754(floatValue)
    // Step 1: Determine the sign bit.
    if floatValue is negative then
        signBit = 1
        floatValue = -floatValue  // Convert to positive for further processing
    else
        signBit = 0
    endif

    // Step 2: Normalize the float value to binary.
    binaryValue = ConvertToBinary(floatValue)  // Convert the float to a binary string
    
    // Step 3: Find the position of the binary point, and ensure the number is in the form of 1.xxxxx
    normalizedValue, exponent = NormalizeBinary(binaryValue)
    
    // Step 4: Adjust the exponent to be biased by adding the bias (127 for single-precision).
    biasedExponent = exponent + 127
    
    // Step 5: Extract the mantissa, which is the part after the binary point (drop the leading 1).
    mantissa = ExtractMantissa(normalizedValue)
    
    // Step 6: Convert the biased exponent and the mantissa to binary.
    exponentBits = ConvertToBinary(biasedExponent, 8 bits)
    mantissaBits = ConvertToBinary(mantissa, 23 bits)
    
    // Step 7: Assemble the IEEE 754 representation.
    ieee754Bits = ConcatenateBits(signBit, exponentBits, mantissaBits)
    
    return ieee754Bits
endfunction
```

1. **Determine the sign bit**: If the number is negative, the sign bit is 1; otherwise, it's 0. For positive numbers (like pi), the sign bit is 0.
2. **Normalize the float value to binary**: Convert the absolute value of the floating-point number to its binary representation.
3. **Normalize the binary value**: Shift the binary point to just after the first 1 (making it a number in the range \[1,2) ). The number of shifts is the exponent, which needs to be stored.
4. **Adjust the exponent**: IEEE 754 uses a biased exponent, which for single-precision is 127. Add the bias to the actual exponent.
5. **Extract the mantissa**: The mantissa is the part of the number after the binary point. Since in normalized form the number always starts with 1, this leading 1 is not stored (it's implicit).
6. **Convert to binary and pad**: Convert the biased exponent and the mantissa to binary. The mantissa needs to be rounded or truncated to fit into 23 bits.
7. **Assemble the IEEE 754 representation**: Combine the sign bit, the 8 bits of the biased exponent, and the 23 bits of the mantissa to create the 32-bit IEEE 754 representation.

Please note, the `ConvertToBinary`, `NormalizeBinary`, `ExtractMantissa`, and `ConcatenateBits` functions are not defined in this pseudocode, as they are placeholders for the processes that would need to be implemented for the algorithm to work. These functions would handle the specific tasks of converting a floating-point number to binary, normalizing it, extracting the mantissa, and assembling the final binary string, respectively.

==**END AI-GENERATED CONTENT**==

### Rewritten in TACL, by me

```tacl
<ConvertToIEEE754>[DefineAction]{
	<Input>{InputFloatValue}
	<Default>0
	<Body>{
		# Step 1: Determine the sign bit.
		[If]{
			(c)<>[IsNegative]{InputFloatValue}
			(t)<>{
				<SignBit>1 
				<InputFloatValue>[ReverseSign]{InputFloatValue}
			}
			(f)<SignBit>0
		}
		# Step 2: Normalize the float value to binary.
		<BinaryValue>[ConvertToBinary]{InputFloatValue}
		# Step 3: Find the position of the binary point, and ensure the number is in 
		#   the form of 1.xxxxx, or in the range of [1 2)
		<NormalizedValue>[NormalizeBinary]{BinaryValue}
		<Exponent>[CountShiftsRequiredToNormalizeBinary]{BinaryValue}
		# Step 4: Adjust the exponent to be biased by adding the bias (127 for single-precision).
		<BiasedExponent>[Add]{Exponent, 127}
		# Step 5: Extract the mantissa, which is the part after the binary point (drop the leading 1).
		<Mantissa>[ExtractMantissa]{NormalizedValue}
		# Step 6: Convert the biased exponent and the mantissa to binary.
		<ExponentBits>[ConvertToBinaryWithLength]{BiasedExponent, 8}
		<MantissaBits>[ConvertToBinaryWithLength]{Mantissa, 23}
		# Step 7: Assemble the IEEE 754 representation.
		<Output>[ConcatenateBinary][SignBit, ExponentsBits, MantissaBits]
		
		<Return>{Output}
	}
}

```

### Rewritten in TACL, by GPT-4

==**BEGIN AI-GENERATED CONTENT**==

```tacl
<ConvertToIEEE754>[DefineAction]{
    <Input>{floatValue}
    <Default><Error>"An error has occurred."
    <Body>{
        # Step 1: Determine the sign bit.
        [If]{
            (c)[LessThan]{floatValue, 0}
            (t)<signBit>1
                <floatValue>[Multiply]{floatValue, -1}
            (f)<signBit>0
        }

        # Step 2: Normalize the float value to binary.
        <binaryValue>[ConvertToBinary]{floatValue}

        # Step 3: Find the position of the binary point, and ensure the number is in the form of 1.xxxxx
        <normalizedValue, exponent>[NormalizeBinary]{binaryValue}

        # Step 4: Adjust the exponent to be biased by adding the bias (127 for single-precision).
        <biasedExponent>[Add]{exponent, 127}

        # Step 5: Extract the mantissa, which is the part after the binary point (drop the leading 1).
        <mantissa>[ExtractMantissa]{normalizedValue}

        # Step 6: Convert the biased exponent and the mantissa to binary.
        <exponentBits>[ConvertToBinary]{biasedExponent, 8}
        <mantissaBits>[ConvertToBinary]{mantissa, 23}

        # Step 7: Assemble the IEEE 754 representation.
        <ieee754Bits>[ConcatenateBits]{signBit, exponentBits, mantissaBits}

        <Return>{ieee754Bits}
    }
}
```

Please note that TACL assumes that actions like `ConvertToBinary`, `NormalizeBinary`, `ExtractMantissa`, and `ConcatenateBits` are predefined or will be defined in the same manner as `ConvertToIEEE754` is defined here.

==**END AI-GENERATED CONTENT**==