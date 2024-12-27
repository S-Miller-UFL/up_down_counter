This is a very simple up/down counter with preload capability.

there are 5 inputs:
1. in_input
2. in_count_direction
3. in_nres
4. in_clk
5. in_latch

and 2 outputs:
1. out_output
2. out_done

the behavior is as follows:

simply set "in_latch" to high, and an internal reference register
will capture whatever value in_input is.

This reference register is used to determine when to assert out_done as true.

if in_nres falls to a low logic level (0), then the counter
will check to see what logic level in_count_direction is.
if its '0', then that means the user wants to count down. It will
load its internal counting register with whatever value is in the internal reference register.
if its '1', then that means the user wants to count up. It will
load its internal counting register with all zeroes.

When in_clk encounters a rising edge, it will increment the internal counting register
if in_count_direction is '1'. If in_count_direction is '0', it will decrement the internal counting register.

if the internal counting register is equal to either 0, or the value of the reference register, out_done is asserted
for 1 clock cycle.

out_done, ideally, will be connected to some kind of external logic that will be notified when the count is done.