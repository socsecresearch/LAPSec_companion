# LAPSec_companion
Companion repository for LAPSec paper
# Complete list of tested policies

|Index|Statement|Type|Associated RPs| Notes | Source |
|-----|---------------------------|---|-------------------------|---------------------------|-----------------------------------|
|1|If there is any read attempt of PMP registers from U-mode, HW should raise an IIE |TP|3,4,6,7|Applicable for both platforms| RISC-V Privileged Spec.| 
|2|If there is any write attempt of PMP registers from U-mode, HW should raise an IIE|TP|3,4,6,7|Applicable for both platforms|RISC-V Privileged Spec.|
|3|The CSR _mepc_ should hold the address of the instruction that raised the exception|RP|N/A|Applicable for both platforms|RISC-V Privileged Spec.|
|4|The exception code field of the _mcause_ register should have the value of 0x2 when IIE occurs|RP|N/A|Applicable for both platforms|RISC-V Privileged Spec.|
|5|The exception code field of the _mcause_ register should have the value of 0x1 when Instruction Access Fault occurs|RP|N/A| _mtvec_ is set by SW in Neorv32|RISC-V Privileged Spec.|
|6|The CSR _mtvec_ should be set by SW to point to the TH routine to divert the program flow to it should an exception occur|RP|N/A|Applicable for both platforms|RISC-V Privileged Spec.|
|7|The TH should execute appropriate action as dictated by system designer|RP|N/A|IBS prints cause of exception to UART, Neorv simply skips the instruction in bare metal setup, while in FreeRTOS mode, gets diverted to FreeRTOS TH |Neorv and IBS device spec.|
|8|From U-mode application, attempting to execute instructions in protected memory regions should result in instruction access fault|TP|3,5,6,7|Applicable for both systems|RISC-V Privileged Spec.|
|9|Attempts to read unimplemented CSRs should raise an IIE|TP|3,4,6,7|Applicable for both platforms|RISC-V Privileged Spec.|
|10|Attempts to write to unimplemented CSRs should raise an IIE|TP|3,4,6,7|Applicable for both platforms|RISC-V Privileged Spec.|
|11|From U-mode application, attempting to load data from protected memory regions should result in load access fault|TP|3,6,7,13|Applicable for both systems|RISC-V Privileged Spec.|
|12|From U-mode application, attempting to store data to protected memory regions should result in store access fault|TP|3,6,7,14|Applicable for both systems|RISC-V Privileged Spec.|
|13|The exception code field of the _mcause_ CSR should have the value of 0x5 when load access faults are raised|RP|N/A|Applicable for both systems|RISC-V Privileged Spec.|
|14|The exception code field of the _mcause_ CSR should have the value of 0x7 when store access faults are raised|RP|N/A|Applicable for both systems|RISC-V Privileged Spec.|
|15|U-mode application attempting to use DMA to read from protected memory regions should raise a load access fault exception|TP|3,6,7,13|Applicable to Neorv32 only as it has a DMA|RISC-V Privileged Spec.|
|16|U-mode application attempting to use DMA to write to protected memory regions should raise a store access fault exception|TP|3,6,7,14|Applicable to Neorv32 only as it has a DMA|RISC-V Privileged Spec.|
|17|U-mode application should not be able to use DMA to write to protected memory regions|TP|asd|Applicable to both systems|RISC-V Privileged Spec.|
|18|U-mode mode should be able to read from all permitted memory regions|TP|asd|Applicable to both systems|RISC-V Privileged Spec.|
|19|U-mode mode should be able to write to all permitted memory regions|TP|asd|Applicable to both systems|RISC-V Privileged Spec.|
|20|Upon reset the _mstatus_ register should hold a certain value|RP|asd|Neorv32 requires the value 0x1800 whereas IBS requires it to be 0x0080|RISC-V Privileged Spec.|
|21|Upon reset the _mtvec_ register should hold a certain value|RP|asd|IBS requires it to be 0x01|RISC-V Privileged Spec.|
|22|If TM=0 in _mcounteren_ register, them attempting to read _time_ register from U-mode should raise an IIE|TP|asd|Applicable to both systems|RISC-V Privileged Spec.|
|23|If IR=0 in _mcounteren_ register, them attempting to read _instret_ register from U-mode should raise an IIE|TP|asd|Applicable to both systems|RISC-V Privileged Spec.|
|24-31|If HMPn=0 in _mcounteren_ register, them attempting to read _hpmcountern_ register from U-mode should raise an IIE|TP|asd|Applicable to both systems._n_ is an integer number. Both system HW were synthesized with 8 performance counters (HPM).|RISC-V Privileged Spec.|
