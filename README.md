CHIP DisplayCounterDecorder8 {
    IN inc, reset;
    OUT a, b, c, d, e, f, g;

    PARTS:
    // A 4-bit register to hold the current count
    Register(in=nextCount, load=load, out=currentCount);

    // Increment the current count
    Inc16(in=currentCount, out=incrementedCount);

    // Logic to determine whether to increment or reset
    Mux16(a=incrementedCount, b=false, sel=reset, out=nextCount);
    Or(a=inc, b=reset, out=load);

    // Decoder to drive the 7-segment display
    YourDecoder(in=currentCount, out[0]=a, out[1]=b, out[2]=c, out[3]=d, out[4]=e, out[5]=f, out[6]=g);
}
