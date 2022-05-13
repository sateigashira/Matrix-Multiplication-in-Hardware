# Matrix-Multiplication-in-Hardware
Implementing matrix multiplication in hardware allows us to take advantage of parallelism and  high  memory  bandwidth  to  improve  the  performance  significantly. This project utilizes the DE-10 Lite FPGA board for the implementation.

# Design
The basic high level design of this project looks as follows:

![image](https://user-images.githubusercontent.com/91091795/168397371-e0a29424-b64b-4bbf-9f02-11f48202796f.png)

                  ||image credit: UCD Department of Engineering||
                  
                  
                  
The MAC's (Multiply-Accumulate) operate in parallel. Each MAC alternates which value of the resulting matrix C they are calculating and send those value to the buffer which then ensures they are in the right order. The finite machine controls this circuit.
After ensuring proper functionality of this design, it is further optimized to maximize throughput via parallelism and pipelining. Instead of just making RAMA dual ported, I made RAMB dual ported as well so that we are running 4 MAC’s in parallel and calculating 4 values of the output in parallel. This reduced our clock cycle run time by half. I had to redesign the buffer a bit to take into account the extra 2 values that needed to be written. There were issues with the output address since the values would just write back over themselves so I had to manually restrict the address by using two counters and assigning the address to one of those counters depending on which value we were writing to the output.
You can see the output and reduced clock cycles below:

![image](https://user-images.githubusercontent.com/91091795/168398307-6e605cd4-aec9-44c1-bc23-4be20b5e4435.png)

The code as well as testbench is included with this project.
