Linux_devmem2
=============

Learning source code of utility "devmem2"


Refer to "AMDM37x Multimedia Device Silicon Revision 1.x Technical Reference Manual___sprugn4m.pdf"
 
Page 2434: For OMAP37x (Beagle Board's processor), its pin gpmc_ncs4 (Mode 0, CONTROL_PADCONF_GPMC_NCS3[31:16]) can also be switched to gpt9_pwm_evt (Mode 3), whose physical address is 0x4800 20B4.
 
 
I run below command on Beagle Board(OMAP ):
ubuntu@omap:~/tom/test$ sudo devmem2 0x480020b4 w
/dev/mem opened.
Memory mapped at address 0xb6f4b000.
Value at address 0x480020B4 (0xb6f4b0b4): 0x180018
 
Refer to page 2428: 0x18 (high 16 bits) means mode 0 = gpmc_ncs4. So to turn it to PWM functionality, (means mode 0 to mode 3 at high 16 bits), 0x18 -> 0x18+0x3=0x1b
ubuntu@omap:~/tom/test$ sudo devmem2 0x480020b4 w 0x1b0018
/dev/mem opened.
Memory mapped at address 0xb6f31000.
Value at address 0x480020B4 (0xb6f310b4): 0x180018
Written 0x1B0018; readback 0x1B0018
ubuntu@omap:~/tom/test$ sudo devmem2 0x480020b4 w
/dev/mem opened.
Memory mapped at address 0xb6fa7000.
Value at address 0x480020B4 (0xb6fa70b4): 0x1B0018
