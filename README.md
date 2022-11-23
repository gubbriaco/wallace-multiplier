# wallace-multiplier
8-bit and 16-bit Wallace Multiplier implemented in VHDL


> This thesis work aims to design and analyze a 16 and 8 bit Wallace Multiplier. Furthermore, the results obtained will be compared with a standard multiplier.

# WALLACE MULTIPLIER
> The Wallace multiplier is a fast tree multiplier of serial-parallel type. Compared to other types of multiplier, it has a greater number of gates and digital components. It must be specified that, in the face of this greater area of occupation on the chip, there are significant gains in terms of calculation speed. So much so that it is defined as a fast tree multiplier since the structure that characterizes it means that the addition operation, having the calculated partial products as operands, is actually faster than the other types of binary multipliers. In fact, considering FA and HA, it is possible to considerably reduce the number of operands which will characterize the final sum. To be precise, a Full-Adder will be associated to each triad of bits corresponding to three different partial products, while a Half-Adder will be associated to each pair of bits corresponding to two different partial products. The corresponding sum and carry bits will be placed respectively in the current position and in the next position in the following iteration. It can be seen how an output pair is generated from the input triad to the Full-Adder. Therefore, the next iteration will surely have fewer partial products than the current one and, therefore, a lower height. Therefore, in the final iteration, having a height equal to 2, it will be possible to carry out the final sum of the remaining partial products. This is because the compression process would always produce torque output and, therefore, the relative height would remain equal to 2.
> The final sum has been designed so that the generated delay is minimal. Therefore, the choice, regarding the VMA , fell on the Ripple-Carry adder which, for the devices used, appears to be the one that is managed in the most efficient way for the reasons mentioned in the previous chapter.
> As regards the generation of partial products, the multiplier has the usual structure adopted by other digital multipliers: the and between the i-th bit of the multiplier and the j-th bit of the multiplicand is calculated.
> It should be noted that the total delay of the multiplier depends on the number of logical components instantiated. Typically, the total delay associated with the Wallace Multiplier is equal to:

n∙τ(FA) + n∙τ(HA) + τ(VMA)

> where τ(VMA) is the delay associated with the Vector-Merging Adder, τ(FA) is the delay associated with the Full-Adder, τ(HA) is the delay associated with the Half-Adder and n is the number of iterations in which components FA and HA were used. Obviously, the delay associated with the VMA is equal to the delay corresponding to the adder used, i.e. the signed Ripple-Carry Adder. Furthermore, considering the unsigned Ripple-Carry Adder used for sign management, the total delay of the designed Wallace Multiplier will be equal to:

τ(RCAu) + n∙τ(FA) + n∙τ(HA) + τ(RCAs)= 
= N∙τ(FA) + n∙τ(FA) + n∙τ(HA) + M∙τ(FA)

> where τ(RCAu) is the delay associated with the unsigned Ripple-Carry Adder, τ(RCAs) is the delay associated with the signed Ripple-Carry Adder, N is the number of bits of the RCAu operands and M is the number of bits of the operands of the RCAs.

***********************************************************************************************************************************************************************
***********************************************************************************************************************************************************************
> For the analysis of the structures of Wallace's Multipliers, the following legend must be referred to:
> 
![image](https://user-images.githubusercontent.com/101352023/203648587-94666faf-d108-4d17-a654-6f5a03053f74.png)
***********************************************************************************************************************************************************************

***********************************************************************************************************************************************************************
# 8-BIT WALLACE MULTIPLIER
> The 8-bit Wallace multiplier has 56 logical and gates for generating partial products and 36 Full-Adder and 24 Half-Adder for compressing PPs. Furthermore, an unsigned Ripple-Carry Adder was used to calculate the partial product corresponding to the last bit of the multiplier and a signed Ripple-Carry Adder to calculate the final sum.
> Therefore, it is possible to define the following 8-bit Wallace Multiplier structure:

![image](https://user-images.githubusercontent.com/101352023/203646180-08d242c0-fb4f-4e0d-84fc-c72885f5bcc9.png)

> It can be seen that during the iterations, the height has decreased significantly. By plotting the height trend, it is possible to observe how it decreased from the initial value of 8, the moment in which the partial products were generated, up to the value of 2, the moment in which the final sum is calculated using the Vector Merging Adder.

![image](https://user-images.githubusercontent.com/101352023/203649307-bb4b7313-fb80-4fb7-bceb-853caf75e719.png)

> So much so that, observing the designed structure, it can be seen that, for example, in iteration 1, in correspondence with the column that contains the largest number of bits, there are two Full-Adders, which, each having a triad as input, generate one pair of outputs each by decreasing the height by 2 units.

***********************************************************************************************************************************************************************
# 16-BIT WALLACE MULTIPLIER
> The 16-bit Wallace Multiplier has 240 logic and gates for generating partial products and 196 Full-Adder and 81 Half-Adder for compressing PPs. Furthermore, an unsigned Ripple-Carry Adder was used to calculate the partial product corresponding to the last bit of the multiplier and a signed Ripple-Carry Adder to calculate the final sum.
> Therefore, it is possible to define the following 16-bit Wallace Multiplier structure:

![image](https://user-images.githubusercontent.com/101352023/203646739-9042fae1-5c94-4dd2-9736-dcd2710bd884.png)

> It can be seen that starting from a height of 16, after 6 compressions, the number of partial products decreased by as much as 14 units.
> By plotting the height of the multiplier in question, it is possible to notice how, thanks to the presence of the Full-Adders and the Half-Adders, the height has decreased considerably.

![image](https://user-images.githubusercontent.com/101352023/203649413-8c64e864-4049-4489-bb42-30fe249d0682.png)

> So much so that, observing the designed structure, it can be seen that, for example, in iteration 1, in correspondence with the column that contains the largest number of bits, there are 5 Full-Adders, which, each having a triad as input, generate a pair of outputs each by decreasing the height by 5 units.

***********************************************************************************************************************************************************************
# STANDARD MULTIPLIER
> The standard multiplier, used as a comparison for the 8-bit Wallace Multiplier, is a digital electronic circuit that implements standard multiplication via cascaded adders. Therefore, considering N-bit operands, this circuit provides for the instantiation of N adders each having two N-bit operands. Therefore, it can be deduced that the total delay of the multiplier, neglecting the delay introduced by the initial logic and gates, turns out to be τ(N) precisely because each subsequent adder will have to wait for the result of the adder preceding it. This circuit turns out to be one of the simplest multipliers to design and implement using a hardware descriptive language.
> Considering the following legend:

![image](https://user-images.githubusercontent.com/101352023/203649811-9018b4a7-89f5-4ea2-b732-21d6cc822eb2.png)

> it is possible to define the following structure of the Standard Multiplier:

![image](https://user-images.githubusercontent.com/101352023/203647457-b42cd581-aeff-4e6d-96e7-451fb828407b.png)

> It can be seen how the first operand of the first adder has a 0 as the most significant bit. This is due to the fact that the least significant bit of the first operand turns out to be the least significant bit of the result of the multiplication. Therefore, it will not be considered in the subsequent cascading sums but will be directly propagated as the zero-position bit of the result. Furthermore, the second operand is shifted to the left by one bit being the second partial product calculated. So much so that each partial product calculated will be shifted to the left by one bit as happens in standard decimal multiplication.

***********************************************************************************************************************************************************************
***********************************************************************************************************************************************************************
***********************************************************************************************************************************************************************
