# LAPSec_companion
Companion repository for LAPSec paper
# Complete list of tested policies

|Index|Statement|Type|Associated RPs| Notes | Source |
|-----|---------------------------|---|-------------------------|---------------------------|-----------------------------------|
|1|If there is any read attempt of PMP registers from U-mode, HW should raise an IIE |TP|3,4,6,7|Applicable for all three platforms| RISC-V Privileged Spec.| 
|2|If there is any write attempt of PMP registers from U-mode, HW should raise an IIE|TP|3,4,6,7|Applicable for all three platforms|RISC-V Privileged Spec.|
|3|The CSR _mepc_ should hold the address of the instruction that raised the exception|RP|N/A|Applicable for all three platforms|RISC-V Privileged Spec.|
|4|The exception code field of the _mcause_ register should have the value of 0x2 when IIE occurs|RP|N/A|Applicable for all three platforms|RISC-V Privileged Spec.|
|5|The exception code field of the _mcause_ register should have the value of 0x1 when Instruction Access Fault occurs|RP|N/A| _mtvec_ is set by SW in Neorv32|RISC-V Privileged Spec.|
|6|The CSR _mtvec_ should be set by SW to point to the TH routine to divert the program flow to it should an exception occur|RP|N/A|Applicable for all three platforms|RISC-V Privileged Spec.|
|7|The TH should execute appropriate action as dictated by system designer|RP|N/A|IBS prints cause of exception to UART, Neorv simply skips the instruction in bare metal setup, while in FreeRTOS mode, gets diverted to FreeRTOS TH |Neorv and IBS device spec.|
|8|From U-mode application, attempting to execute instructions in protected memory regions should result in instruction access fault|TP|3,5,6,7|Applicable for all three systems|RISC-V Privileged Spec.|
|9|Attempts to read unimplemented CSRs should raise an IIE|TP|3,4,6,7|Applicable for all three platforms|RISC-V Privileged Spec.|
|10|Attempts to write to unimplemented CSRs should raise an IIE|TP|3,4,6,7|Applicable for all three platforms|RISC-V Privileged Spec.|
|11|From U-mode application, attempting to load data from protected memory regions should result in load access fault|TP|3,6,7,13|Applicable for all three systems|RISC-V Privileged Spec.|
|12|From U-mode application, attempting to store data to protected memory regions should result in store access fault|TP|3,6,7,14|Applicable for all three systems|RISC-V Privileged Spec.|
|13|The exception code field of the _mcause_ CSR should have the value of 0x5 when load access faults are raised|RP|N/A|Applicable for all three systems|RISC-V Privileged Spec.|
|14|The exception code field of the _mcause_ CSR should have the value of 0x7 when store access faults are raised|RP|N/A|Applicable for all three systems|RISC-V Privileged Spec.|
|15|U-mode application attempting to use DMA to read from protected memory regions should raise a load access fault exception|TP|3,6,7,13|Applicable to Neorv32 only as it has a DMA|RISC-V Privileged Spec.|
|16|U-mode application attempting to use DMA to write to protected memory regions should raise a store access fault exception|TP|3,6,7,14|Applicable to Neorv32 only as it has a DMA|RISC-V Privileged Spec.|
|17|U-mode application attempting to use DMA to execute instructions in protected memory regions should raise an instruction access fault|TP|3,5,6,7|Applicable to Neorv32 only as it has a DMA|Interpreted from  RISC-V Privileged Spec., CWE-1189 and CVE-2018-15383|
|18|U-mode mode should be able to read from all permitted memory regions without the raising of any exceptions|TP|3,4,5,6,7,13,14|Applicable to all three systems|Interpreted from  RISC-V Privileged Spec., CWE-1189 and CVE-2018-15383|
|19|U-mode mode should be able to write to all permitted memory regions|TP|3,4,5,6,7,13,14|Applicable to all three systems|Interpreted from  RISC-V Privileged Spec., CWE-1189 and CVE-2018-15383|
|20|Upon reset the _mstatus_ register should hold a certain value|RP|N/A|Neorv32 requires the value 0x1800 whereas IBS requires it to be 0x0080|RISC-V Privileged Spec.|
|21|Upon reset the _mtvec_ register should hold a certain value|RP|N/A|IBS requires it to be 0x01|RISC-V Privileged Spec.|
|22|If TM=0 in _mcounteren_ register, them attempting to read _time_ register from U-mode should raise an IIE|TP|3,4,6,7|Applicable to all three systems|RISC-V Privileged Spec.|
|23|If IR=0 in _mcounteren_ register, them attempting to read _instret_ register from U-mode should raise an IIE|TP|3,4,6,7|Applicable to all three systems|RISC-V Privileged Spec.|
|24-31|If HMPn=0 in _mcounteren_ register, them attempting to read _hpmcountern_ register from U-mode should raise an IIE|TP|3,4,6,7|Applicable to all three systems._n_ is an integer number. Neorv32 and IBS systems were synthesized with 8 performance counters (HPM).|RISC-V Privileged Spec.|
|32| Attempts to execute access the vector CSRs will raise an illegal instruction when mstatus.VS =0 | TP |-|Applicable to Ara only| RVV spec |
|33| Attempts to execute any vector instruction raise an illegal instruction when mstatus.VS =0 | TP |-|Applicable to Ara only| RVV spec |
|34| When mstatus.VS is set to Initial or Clean, executing any instruction that changes vector state, will change mstatus.VS to Dirty| TP |-|Applicable to Ara only| RVV spec |
|35| When mstatus.VS is set to Initial or Clean, executing any instruction that changes the vector CSRs, will change mstatus.VS to Dirty| TP |-|Applicable to Ara only| RVV spec |
|36|Prestart elements cannot raise exceptions and change destination register contents for vector arithmetic instructions such as vxor, vand, vadd, vsub, vmul| TP |-|Applicable to Ara only| RVV spec |
|37| Active elements can raise exceptions and change destination register contents for vector arithmetic instructions such as vxor, vand, vadd, vsub, vmul| TP |-|Applicable to Ara only| RVV spec |
|38| Inactive elements cannot raise exceptions nor change destination register contents for vector arithmetic instructions such as vxor, vand, vadd, vsub, vmul if vtype.vma=0 | TP |-|Applicable to Ara only| RVV spec |
|39| Inactive elements can be overwritten with all 1s in destination register contents for vector arithmetic instructions such as vxor, vand, vadd, vsub, vmulif vtype.vma=1 | RP |-|Applicable to Ara only| RVV spec |
|40| Tail elements cannot raise exceptions nor change destination register contents if for vector arithmetic instructions such as vxor, vand, vadd, vsub, vmulvtype.vta=0 | RP |-|Applicable to Ara only| RVV spec |
|41| Tail elements can be overwritten with all 1s in destination register contents if for vector arithmetic instructions such as vxor, vand, vadd, vsub, vmul vtype.vta=1 | RP |-|Applicable to Ara only| RVV spec |
|42| When vstart>=VL, there are no body elements and no elements are updated in any destination vector register group | TP |-|Applicable to Ara only| RVV spec |
|43| All elements are updated in the x and f registers, even if vstart>VL or VL=0| RP |-|Applicable to Ara only| RVV spec |
|44| A vector floating-point divide by zero (DZ) exception at any active floating-point element sets the DZ exception flag in the fflags register | TP |-|Applicable to Ara only| RVV spec |
|45| A vector floating-point invalid (NV) exception at any active floating-point element sets the NV exception flag in the fflags register  | TP |-|Applicable to Ara only| RVV spec |
|46| Low-level firmware/driver routines should have proper input validation | TP |-|Applicable to all| CWE-20 |
|47| Low-level firmware/driver routines should have proper type conversion | RP |-|Applicable to all| CWE-704 |
