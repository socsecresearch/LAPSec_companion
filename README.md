# LAPSec_companion
Companion repository for LAPSec paper
# Complete list of tested policies

|Index|Statement|Type|Associated RPs| Notes |
|-----|---------------------------|---|-------------------------|---------------------------|
|1|If there is any read attempt of PMP registers from U-mode, HW should raise an IIE |TP|3,4,5,6,7|Applicable for both platforms|
|2|If there is any write attempt of PMP registers from U-mode, HW should raise an IIE|TP|3,4,5,6,7|Applicable for both platforms|
|3|The CSR _mepc_ should hold the address of the instruction that raised the exception|RP|N/A|Applicable for both platforms|
|4|The exception code field of the _mcause_ register should have the value of 0x2 when IIE occurs|RP|asd|Applicable for both platforms|
|5|The CSR _mtvec_ should be set by SW to point to the TH routine to divert the program flow to it should an exception occur|RP|asd| _mtvec_ is set by SW in Neorv32|
|6|The CSR _mtvec_ should be set by SW to point to the TH routine to divert the program flow to it should an exception occur|RP|asd|Applicable for both platforms|
|7|The TH should execute appropriate action as dictated by system designer|RP|asd|IBS prints cause of exception to UART, Neorv simply skips the instruction in bare metal setup, while in FreeRTOS mode, gets diverted to FreeRTOS TH |
|8|From U-mode application, attempting to execute instructions in protected memory regions should result in instruction access fault|TP|asd|Applicable for both systems|
|9|Attempts to read unimplemented CSRs should raise an IIE|TP|asd|Applicable for both platforms|
|10|Attempts to write to unimplemented CSRs should raise an IIE|TP|asd|Applicable for both platforms|
|11|From U-mode application, attempting to load data from protected memory regions should result in load access fault|TP|asd|Applicable for both systems|
|12|From U-mode application, attempting to store data to protected memory regions should result in store access fault|TP|asd|Applicable for both systems|
|13|The exception code field of the _mcause_ CSR should have the value of 0x5 when load access faults are raised|TP|asd|Applicable for both systems|
|14|The exception code field of the _mcause_ CSR should have the value of 0x7 when store access faults are raised|TP|asd|Applicable for both systems|
|15|U-mode application should not be able to use DMA to read from protected memory regions|TP|asd|Applicable to both systems|
|16|U-mode application should not be able to use DMA to write to protected memory regions|TP|asd|Applicable to both systems|
|17|U-mode application should not be able to use DMA to write to protected memory regions|TP|asd|Applicable to both systems|
|18|U-mode mode should be able to read from all permitted memory regions|TP|asd|Applicable to both systems|
|19|U-mode mode should be able to write to all permitted memory regions|TP|asd|Applicable to both systems|
|20|Upon reset the _mstatus_ register should hold a certain value|RP|asd|Neorv32 requires the value 0x1800 whereas IBS requires it to be 0x0080|
|21|Upon reset the _mtvec_ register should hold a certain value|RP|asd|IBS requires it to be 0x01|
|22|If TM=0 in _mcounteren_ register, them attempting to read _time_ register from U-mode should raise an IIE|TP|asd|Applicable to both systems|
|23|If IR=0 in _mcounteren_ register, them attempting to read _instret_ register from U-mode should raise an IIE|TP|asd|Applicable to both systems|
|24-31|If HMPn=0 in _mcounteren_ register, them attempting to read _hpmcountern_ register from U-mode should raise an IIE|TP|asd|Applicable to both systems._n_ is an integer number. Both system HW were synthesized with 8 performance counters (HPM).|
