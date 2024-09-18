# LAPSec_companion
Companion repository for LAPSec paper
# Tested Policies

|Index|Statement|Type|Associated TP/RP| Notes |
|-----|---------------------------|---|-------------------------|---------------------------|
|1|Attempts to read unimplemented CSRs should raise an IIE|TP|asd|Applicable for both platforms|
|2|Attempts to write to unimplemented CSRs should raise an IIE|TP|asd|Applicable for both platforms|
|3|The CSR _mepc_ should hold the address of the instruction that raised the exception|RP|asd|Applicable for both platforms|
|4|The exception code field of the _mcause_ register should have the value of 0x2 when IIE occurs|RP|asd|Applicable for both platforms|
|5|The CSR _mtvec_ should be set by SW to point to the TH routine to divert the program flow to it should an exception occur|RP|asd| _mtvec_ is set by HW in IBS|
|6|The CSR _mtvec_ should be set by SW to point to the TH routine to divert the program flow to it should an exception occur|RP|asd|Applicable for both platforms|
|7|The TH should execute appropriate action as dictated by system designer|RP|asd|IBS prints cause of exception to UART, Neorv simply skips the instruction in bare metal setup, while in FreeRTOS mode, gets diverted to FreeRTOS TH |
