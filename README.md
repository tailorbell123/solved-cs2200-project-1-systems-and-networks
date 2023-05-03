Download Link: https://assignmentchef.com/product/solved-cs2200-project-1-systems-and-networks
<br>
<h1>1      Requirements</h1>

<ul>

 <li>Download the proper version of CircuitSim. A copy of CircuitSim is available under Files on Canvas. You may also download it from the CircuitSim website (https://ra4king.github.io/CircuitSim/). In order to run CircuitSim, Java must be installed. If you are a Mac user, you may need to right-click on the JAR file and select “Open” in the menu to bypass Gatekeeper restrictions.</li>

 <li>CircuitSim is still under development and may have unknown bugs. Please back up your work using some form of version control, such as a local/private git repository or Dropbox. <strong>Do not use public git repositories; it is against the Georgia Tech Honor Code</strong>.</li>

 <li>The LC-900 assembler is written in Python. If you do not have Python 2.6 or newer installed on your system, you will need to install it before you continue.</li>

</ul>

<h1>2         Project Overview and Description</h1>

Project 1 is designed to give you a good feel for exactly how a processor works. In Phase 1, you will design a datapath in CircuitSim to implement a supplied instruction set architecture. You will use the datapath as a tool to determine the control signals needed to execute each instruction. In Phases 2 and 3, you are required to build a simple finite state machine (the “control unit”) to control your computer and actually run programs on it.

<strong>Note: </strong>You will need to have a working knowledge of CircuitSim. Make sure that you know how to make basic circuits as well as subcircuits before proceeding. The TAs are always here if you need help.

<h1>3          Phase 1 – Implement the Datapath</h1>

<h2>Figure 1: Datapath for the LC-900 Processor</h2>

In this phase of the project, you must learn the Instruction Set Architecture (ISA) for the processor we will be implementing. Afterwards, we will implement a complete LC-900 datapath in CircuitSim using what you have just learned.

<strong>You must do the following:</strong>

<ol>

 <li>Learn and understand the LC-900 ISA. The ISA is fully specified and defined in Appendix A: LC-900</li>

</ol>

Instruction Set Architecture. <strong>Do not move on until you have fully read and understood the ISA specification</strong>. <em>Every single detail </em>will be relevant to implementing your datapath in the next step.

<ol start="2">

 <li>Using CircuitSim, implement the LC-900 datapath. To do this, you will need to use the details of the LC-900 datapath defined in Appendix A: LC-900 Instruction Set Architecture. You should model your datapath on Figure 1.</li>

</ol>

<h2><strong>3.1     Hints</strong></h2>

<h3>3.1.1       Subcircuits</h3>

CircuitSim enables you to break create reusable components in the form of subcircuits. <strong>We highly recommend that you break parts of your design up into subcircuits. </strong>At a minimum, you will want to implement your ALU in a subcircuit. The control unit you implement in Phase 2 is another prime candidate for a subcircuit.

<h3>3.1.2       Debugging</h3>

As you build the datapath, you should consider adding functionality that will allow you to operate the whole datapath by hand. This will make testing individual operations quite simple. We suggest your datapath include devices that will allow you to put arbitrary values on the bus and to view the current value of the bus. Feel free to add any additional hardware that will help you understand what is going on.

<h3>3.1.3        Memory Addresses</h3>

Because of CircuitSim limitations, the RAM module is limited to no more than 16 address bits. Therefore, per our ISA, any 32-bit values used as memory addresses will be truncated to 16 bits (with the 16 most significant bits disregarded). We would like you to implement this (i.e. truncate the most significant bits) before feeding the address value from the MAR (Memory Address Register) to the RAM.

<h3>3.1.4        Comparison Logic</h3>

The “comparison logic” box in Figure 1 is responsible for performing the comparison logic associated with the SKP instructions. The comparison logic should read the current value on the bus plus the mode bits (CmpSel) from the IR. When executing the SKP instructions, you should compute <em>A</em>−<em>B </em>using the ALU. While this result of the ALU is being driven on the bus, the comparison logic should read the result <em>A</em>−<em>B </em>and output a single “true” or “false” bit for the selected condition (CmpSel).

Your comparison logic should be purely combinational. Feel free to use any CircuitSim components you wish to aid in your implementation. Note that the three outputs of a comparator are gt, eq, lt which correspond to bits 2, 1, and 0 in the SKP instruction. Also note that bits 0:2 can be obtained from the value chosen by RegSel.

<h3>3.1.5        Register File</h3>

You must implement your own register file. That is to say, you cannot use CircuitSim’s built-in RAM to create the register file. Consider what logic components you may want to use to implement addressing functionality (multiplexers, demultiplexers, decoders, etc). Your zero register must be implemented such that writes to it are ineffective, i.e., attempting to write a non-zero value to the zero register will do nothing. <strong>Do not forget to do this or you will lose points!</strong>

<h3>3.1.6        Register Select</h3>

From lecture and the textbook, you should be familiar with the “register select” (RegSel) multiplexer. The mux is responsible for feeding the register number from the correct field in the instruction into the register file. See Table 4 for a list of inputs your mux should have.

<h1>4          Phase 2 – Implement the Microcontrol Unit</h1>

In this phase of the project, you will use CircuitSim to implement the microcontrol unit for the LC-900 processor. This component is referred to as the “Control Logic” in the images and schematics. The microcontroller will contain all of the signal lines to the various parts of the datapath.

<strong>You must do the following:</strong>

<ol>

 <li>Read and understand the microcontroller logic:

  <ul>

   <li>Please refer to Appendix B: Microcontrol Unit for details.</li>

   <li><strong>Note: </strong>You will be required to generate the control signals for each state of the processor in the next phase, so make sure you understand the connections between the datapath and the microcontrol unit before moving on.</li>

  </ul></li>

 <li>Implement the Microcontrol Unit using CircuitSim. The appendix contains all of the necessary information. Take note that the input and output signals on the schematics directly match the signals marked in the LC-900 datapath schematic (see Figure 1).</li>

</ol>

<h1>5         Phase 3 – Microcode and Testing</h1>

In this final stage of the project, you will write the microcode control program that will be loaded into the microcontrol unit you implemented in Phase 2. Then, you will hook up the control unit you built in Phase 2 of the project to the datapath you implemented in Phase 1. Finally, you will test your completed computer using a simple test program and ensure that it properly executes.

<strong>You must do the following:</strong>

<ol>

 <li>Open and fill out microcode.xlsx file we’ve provided you (note: the formulas in the provided file will <strong>not </strong>work with Numbers, but work with Excel and Google Sheets). You will need to mark which control signal is high (that is 1) for each of the states.</li>

 <li>After you have completed all the microstates, convert the binary strings you just computed into hex and move them into the main ROM. You can just copy and paste the hex column (highlighted yellow) from the spreadsheet directly into the ROM component in Circuitsim. Do the same for the sequencer and condition ROMs.</li>

 <li>Connect the completed control unit to the datapath you implemented in Phase 1. Using Figures 1 and 2, connect the control signals to their appropriate spots.</li>

 <li>Finally, it is time to test your completed computer. Use the provided assembler (found in the “assembly” folder) to convert a test program from assembly to hex. For instructions on how to use the assembler and simulator, see README.txt in the “assembly” folder. <strong>Note: The simulator does not test your project, it simply provides a model. To test your design, you must load the assembled HEX into CircuitSim. </strong>We recommend using test programs that contain a single instruction since you are bound to have a few bugs at this stage of the project. Once you have built confidence, test your processor with the provided <strong>s </strong>program as a more comprehensive test case.</li>

</ol>

<h1></h1>

<h1>7            Appendix A: LC-900 Instruction Set Architecture</h1>

The LC-900 is a simple, yet capable computer architecture. The LC-900 combines attributes of both ARM and the LC-2200 ISA defined in the Ramachandran &amp; Leahy textbook for CS 2200.

The LC-900 is a <strong>word-addressable</strong>, <strong>32-bit </strong>computer. <strong>All addresses refer to words</strong>, i.e. the first word (four bytes) in memory occupies address 0x0, the second word, 0x1, etc.

All memory addresses are truncated to 16 bits on access, discarding the 16 most significant bits if the address was stored in a 32-bit register. This provides roughly 64 KB of addressable memory.

<h2><strong>7.1     Registers</strong></h2>

The LC-900 has 16 general-purpose registers. While there are no hardware-enforced restraints on the uses of these registers, your code is expected to follow the conventions outlined below.

<h3>Table 1: Registers and their Uses</h3>

<table width="426">

 <tbody>

  <tr>

   <td width="115">Register Number</td>

   <td width="50">Name</td>

   <td width="174">Use</td>

   <td width="88">Callee Save?</td>

  </tr>

  <tr>

   <td width="115">0</td>

   <td width="50">$zero</td>

   <td width="174">Always Zero</td>

   <td width="88">NA</td>

  </tr>

  <tr>

   <td width="115">1</td>

   <td width="50">$at</td>

   <td width="174">Assembler/Target Address</td>

   <td width="88">NA</td>

  </tr>

  <tr>

   <td width="115">2</td>

   <td width="50">$v0</td>

   <td width="174">Return Value</td>

   <td width="88">No</td>

  </tr>

  <tr>

   <td width="115">3</td>

   <td width="50">$a0</td>

   <td width="174">Argument 1</td>

   <td width="88">No</td>

  </tr>

  <tr>

   <td width="115">4</td>

   <td width="50">$a1</td>

   <td width="174">Argument 2</td>

   <td width="88">No</td>

  </tr>

  <tr>

   <td width="115">5</td>

   <td width="50">$a2</td>

   <td width="174">Argument 3</td>

   <td width="88">No</td>

  </tr>

  <tr>

   <td width="115">6</td>

   <td width="50">$t0</td>

   <td width="174">Temporary Variable</td>

   <td width="88">No</td>

  </tr>

  <tr>

   <td width="115">7</td>

   <td width="50">$t1</td>

   <td width="174">Temporary Variable</td>

   <td width="88">No</td>

  </tr>

  <tr>

   <td width="115">8</td>

   <td width="50">$t2</td>

   <td width="174">Temporary Variable</td>

   <td width="88">No</td>

  </tr>

  <tr>

   <td width="115">9</td>

   <td width="50">$s0</td>

   <td width="174">Saved Register</td>

   <td width="88">Yes</td>

  </tr>

  <tr>

   <td width="115">10</td>

   <td width="50">$s1</td>

   <td width="174">Saved Register</td>

   <td width="88">Yes</td>

  </tr>

  <tr>

   <td width="115">11</td>

   <td width="50">$s2</td>

   <td width="174">Saved Register</td>

   <td width="88">Yes</td>

  </tr>

  <tr>

   <td width="115">12</td>

   <td width="50">$k0</td>

   <td width="174">Reserved for OS and Traps</td>

   <td width="88">NA</td>

  </tr>

  <tr>

   <td width="115">13</td>

   <td width="50">$sp</td>

   <td width="174">Stack Pointer</td>

   <td width="88">No</td>

  </tr>

  <tr>

   <td width="115">14</td>

   <td width="50">$fp</td>

   <td width="174">Frame Pointer</td>

   <td width="88">Yes</td>

  </tr>

  <tr>

   <td width="115">15</td>

   <td width="50">$ra</td>

   <td width="174">Return Address</td>

   <td width="88">No</td>

  </tr>

 </tbody>

</table>

<ol>

 <li><strong>Register 0 </strong>is always read as zero. Any values written to it are discarded. <strong>Note: </strong>for the purposes of this project, you must implement the zero register. Regardless of what is written to this register, it should always output zero.</li>

 <li><strong>Register 1 </strong>is used to hold the target address of a jump. It may also be used by pseudo-instructions generated by the assembler.</li>

 <li><strong>Register 2 </strong>is where you should store any returned value from a subroutine call.</li>

 <li><strong>Registers 3 – 5 </strong>are used to store function/subroutine arguments. <strong>Note: </strong>registers 2 through 8 should be placed on the stack if the caller wants to retain those values. These registers are fair game for the callee (subroutine) to trash.</li>

 <li><strong>Registers 6 – 8 </strong>are designated for temporary variables. The caller must save these registers if they want these values to be retained.</li>

 <li><strong>Registers 9 – 11 </strong>are saved registers. The caller may assume that these registers are never tampered with by the subroutine. If the subroutine needs these registers, then it should place them on the stack and restore them before they jump back to the caller.</li>

 <li><strong>Register 12 </strong>is reserved for handling interrupts. While it should be implemented, it otherwise will not have any special use on this assignment.</li>

 <li><strong>Register 13 </strong>is your anchor on the stack. It keeps track of the top of the activation record for a subroutine.</li>

 <li><strong>Register 14 </strong>is used to point to the first address on the activation record for the currently executing process.</li>

 <li><strong>Register 15 </strong>is used to store the address a subroutine should return to when it is finished executing.</li>

</ol>

<h2><strong>7.2      Instruction Overview</strong></h2>

The LC-900 supports a variety of instruction forms, only a few of which we will use for this project. The instructions we will implement in this project are summarized below.

<h3>Table 2: LC-900 Instruction Set</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0000</td>

   <td width="47">DR</td>

   <td width="47">SR1</td>

   <td width="187">unused</td>

   <td colspan="2" width="47">SR2</td>

  </tr>

  <tr>

   <td width="47">0001</td>

   <td width="47">DR</td>

   <td width="47">SR1</td>

   <td width="187">unused</td>

   <td colspan="2" width="47">SR2</td>

  </tr>

  <tr>

   <td width="47">0010</td>

   <td width="47">DR</td>

   <td width="47">SR1</td>

   <td width="187">immval20</td>

   <td colspan="2" width="47"></td>

  </tr>

  <tr>

   <td width="47">0011</td>

   <td width="47">DR</td>

   <td width="47">BaseR</td>

   <td width="187">offset20</td>

   <td colspan="2" width="47"></td>

  </tr>

  <tr>

   <td width="47">0100</td>

   <td width="47">SR</td>

   <td width="47">BaseR</td>

   <td width="187">offset20</td>

   <td colspan="2" width="47"></td>

  </tr>

  <tr>

   <td width="47">0101</td>

   <td colspan="2" width="94">unused</td>

   <td width="187">offset20</td>

   <td colspan="2" width="47"></td>

  </tr>

  <tr>

   <td width="47">0110</td>

   <td width="47">RA</td>

   <td width="47">AT</td>

   <td width="187">unused</td>

   <td colspan="2" width="47"></td>

  </tr>

  <tr>

   <td width="47">0111</td>

   <td colspan="2" width="94"></td>

   <td width="187">unused</td>

   <td colspan="2" width="47"></td>

  </tr>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="187">unused</td>

   <td width="12"></td>

   <td width="35">001</td>

  </tr>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="187">unused</td>

   <td width="12"></td>

   <td width="35">011</td>

  </tr>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="187">unused</td>

   <td width="12"></td>

   <td width="35">010</td>

  </tr>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="187">unused</td>

   <td width="12"></td>

   <td width="35">101</td>

  </tr>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="187">unused</td>

   <td width="12"></td>

   <td width="35">100</td>

  </tr>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="187">unused</td>

   <td width="12"></td>

   <td width="35">110</td>

  </tr>

  <tr>

   <td width="47">1001</td>

   <td width="47">DR</td>

   <td width="47">unused</td>

   <td width="187">PCoffset20</td>

   <td colspan="2" width="47"></td>

  </tr>

 </tbody>

</table>

ADD

NAND

ADDI

LW

SW

BR

JALR

HALT

SKPLT

SKPLE

SKPEQ

SKPNE

SKPGT

SKPGE

LEA

<h4>7.2.1        Conditional Branching</h4>

Branching in the LC-900 ISA is a bit different than usual. We have one branch instruction: the BR instruction, which, if executed, unconditionally jumps/changes the PC. Then, we have a series of instructions known as the skip-instructions, or SKP instructions. These instructions use the comparison operators, comparing the values of two source registers. If the comparisons are true (for example, with the SKPGT instruction, if SR1 <em>&gt; </em>SR2), then we skip over the next line of code – we increment PC by 1 (remember that at the time of execution, PC has already been incremented by 1, so this is an additional increment).

These SKP instructions all have the same opcode and use bits 2:0 to determine the comparison type (CmpSel). Bit 0 controls less then, bit 1 controls equals, and bit 2 controls greater than. For example, if you wanted to do a SKPGE (skip greater than or equal), you would set the CmpSel bits as: 110 (high for greater than and high for equals.)

Branching can then be accomplished by using the SKP instructions to do comparison-checking, and using BR instructions below those SKP instructions. Particular BR instructions are taken if a particular comparison result is reached.

<h2><strong>7.3       Detailed Instruction Reference</strong></h2>

<strong>7.3.1       ADD</strong>

<strong>Assembler Syntax</strong>

ADD           DR, SR1, SR2

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0000</td>

   <td width="47">DR</td>

   <td width="47">SR1</td>

   <td width="187">unused</td>

   <td width="47">SR2</td>

  </tr>

 </tbody>

</table>

<strong>Operation</strong>

DR = SR1 + SR2;

<h3>Description</h3>

The ADD instruction obtains the first source operand from the SR1 register. The second source operand is obtained from the SR2 register. The second operand is added to the first source operand, and the result is stored in DR.

<strong>7.3.2        NAND</strong>

<strong>Assembler Syntax</strong>

NAND        DR, SR1, SR2

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0001</td>

   <td width="47">DR</td>

   <td width="47">SR1</td>

   <td width="187">unused</td>

   <td width="47">SR2</td>

  </tr>

 </tbody>

</table>

<strong>Operation</strong>

DR = ~(SR1 &amp; SR2);

<h3>Description</h3>

The NAND instruction performs a logical NAND (AND NOT) on the source operands obtained from SR1 and SR2. The result is stored in DR.

<table width="623">

 <tbody>

  <tr>

   <td width="623"><strong>HINT: </strong>A logical NOT can be achieved by performing a NAND with both source operands the same.For instance,NAND DR, SR1, SR1…achieves the following logical operation: <em>DR</em>←<em>SR</em>1.</td>

  </tr>

 </tbody>

</table>

<strong>7.3.3       ADDI</strong>

<strong>Assembler Syntax</strong>

ADDI           DR, SR1, immval20

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0010</td>

   <td width="47">DR</td>

   <td width="47">SR1</td>

   <td width="234">immval20</td>

  </tr>

 </tbody>

</table>

<strong>Operation</strong>

DR = SR1 + SEXT(immval20);

<h3>Description</h3>

The ADDI instruction obtains the first source operand from the SR1 register. The second source operand is obtained by sign-extending the immval20 field to 32 bits. The resulting operand is added to the first source operand, and the result is stored in DR.

<strong>7.3.4      LW</strong>

<strong>Assembler Syntax</strong>

LW             DR, offset20(BaseR)

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0011</td>

   <td width="47">DR</td>

   <td width="47">BaseR</td>

   <td width="234">offset20</td>

  </tr>

 </tbody>

</table>

<strong>Operation</strong>

DR = MEM[BaseR + SEXT(offset20)];

<h3>Description</h3>

An address is computed by sign-extending bits [19:0] to 32 bits and then adding this result to the contents of the register specified by bits [23:20]. The 32-bit word at this address is loaded into DR.

<strong>7.3.5       SW</strong>

<strong>Assembler Syntax</strong>

SW             SR, offset20(BaseR)

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0100</td>

   <td width="47">SR</td>

   <td width="47">BaseR</td>

   <td width="234">offset20</td>

  </tr>

 </tbody>

</table>

<strong>Operation</strong>

MEM[BaseR + SEXT(offset20)] = SR;

<h3>Description</h3>

An address is computed by sign-extending bits [19:0] to 32 bits and then adding this result to the contents of the register specified by bits [23:20]. The 32-bit word obtained from register SR is then stored at this address.

<strong>7.3.6       BR</strong>

<strong>Assembler Syntax</strong>

BR           offset20

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0101</td>

   <td width="94">unused</td>

   <td width="234">offset20</td>

  </tr>

 </tbody>

</table>

<strong>Operation</strong>

PC = incrementedPC + offset20

<h3>Description</h3>

A branch is unconditionally taken. The PC will be set to the sum of the incremented PC (since we have already undergone fetch) and the sign-extended offset[19:0].

<strong>7.3.7        JALR</strong>

<strong>Assembler Syntax</strong>

JALR          RA, AT

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0110</td>

   <td width="47">RA</td>

   <td width="47">AT</td>

   <td width="234">unused</td>

  </tr>

 </tbody>

</table>

<h3>Operation</h3>

RA = PC;

PC = AT;

<h3>Description</h3>

First, the incremented PC (address of the instruction + 1) is stored into register RA. Next, the PC is loaded with the value of register AT, and the computer resumes execution at the new PC.

<strong>7.3.8        HALT</strong>

<strong>Assembler Syntax</strong>

HALT

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">0111</td>

   <td width="328">unused</td>

  </tr>

 </tbody>

</table>

<strong>Description</strong>

The machine is brought to a halt and executes no further instructions.

<strong>7.3.9        SKPLT</strong>

<strong>Assembler Syntax</strong>

SKPLT SR1, SR2

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="199">unused</td>

   <td width="35">001</td>

  </tr>

 </tbody>

</table>

<h3>Operation</h3>

if (SR1 &lt; SR2) {

PC = incrementedPC + 1

}

<strong>Description</strong>

The incrementedPC is further incremented by 1 if SR1 is less than SR2.

<strong>7.3.10        SKPLE</strong>

<strong>Assembler Syntax</strong>

SKPLE SR1, SR2

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="199">unused</td>

   <td width="35">011</td>

  </tr>

 </tbody>

</table>

<h3>Operation</h3>

if (SR1 &lt;= SR2) {

PC = incrementedPC + 1

}

<strong>Description</strong>

The incrementedPC is further incremented by 1 if SR1 is less than or equal to SR2.

<strong>7.3.11        SKPEQ</strong>

<strong>Assembler Syntax</strong>

SKPEQ SR1, SR2

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="199">unused</td>

   <td width="35">010</td>

  </tr>

 </tbody>

</table>

<h3>Operation</h3>

if (SR1 == SR2) {

PC = incrementedPC + 1

}

<strong>Description</strong>

The incrementedPC is further incremented by 1 if SR1 is equal to SR2.

<strong>7.3.12        SKPNE</strong>

<strong>Assembler Syntax</strong>

SKPNE SR1, SR2

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="199">unused</td>

   <td width="35">101</td>

  </tr>

 </tbody>

</table>

<h3>Operation</h3>

if (SR1 != SR2) {

PC = incrementedPC + 1

}

<strong>Description</strong>

The incrementedPC is further incremented by 1 if SR1 is not equal to SR2.

<strong>7.3.13        SKPGT</strong>

<strong>Assembler Syntax</strong>

SKPGT SR1, SR2

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="199">unused</td>

   <td width="35">100</td>

  </tr>

 </tbody>

</table>

<h3>Operation</h3>

if (SR1 &gt; SR2) {

PC = incrementedPC + 1

}

<strong>Description</strong>

The incrementedPC is further incremented by 1 if SR1 is greater than SR2.

<strong>7.3.14        SKPGE</strong>

<strong>Assembler Syntax</strong>

SKPGE SR1, SR2

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">1000</td>

   <td width="47">SR1</td>

   <td width="47">SR2</td>

   <td width="199">unused</td>

   <td width="35">110</td>

  </tr>

 </tbody>

</table>

<h3>Operation</h3>

if (SR1 &gt;= SR2) {

PC = incrementedPC + 1

}

<strong>Description</strong>

The incrementedPC is further incremented by 1 if SR1 is greater or equal to SR2.

<strong>7.3.15       LEA</strong>

<strong>Assembler Syntax</strong>

LEA            DR, label

<h3>Encoding</h3>

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

<table width="375">

 <tbody>

  <tr>

   <td width="47">1001</td>

   <td width="47">DR</td>

   <td width="47">unused</td>

   <td width="234">PCoffset20</td>

  </tr>

 </tbody>

</table>

<strong>Operation</strong>

DR = PC + SEXT(PCoffset20);

<h3>Description</h3>

An address is computed by sign-extending bits [19:0] to 32 bits and adding this result to the incremented PC (address of instruction + 1). It then stores the computed address into register DR.

<h1>8         Appendix B: Microcontrol Unit</h1>

You will make a microcontrol unit which will drive all of the control signals to various items on the datapath. This Finite State Machine (FSM) can be constructed in a variety of ways. You could implement it with combinational logic and flip flops, or you could hard-wire signals using a single ROM. The single ROM solution will waste a tremendous amount of space since most of the microstates do not depend on the opcode or the conditional test to determine which signals to assert. For example, since the condition line is an input for the address, every microstate would have to have an address for condition = 0 as well as condition = 1, even though this only matters for one particular microstate.

To solve this problem, we will use a three ROM microcontroller. In this arrangement, we will have three ROMs:

<ul>

 <li>the main ROM, which outputs the control signals,</li>

 <li>the sequencer ROM, which helps to determine which microstate to go at the end of the FETCH state,</li>

 <li>and the condition ROM, which helps determine whether or not to skip during the SKP instructions.</li>

</ul>

Examine the following:

<h2>Figure 2: Three ROM Microcontrol Unit</h2>

As you can see, there are three different locations that the next state can come from: part of the output from the previous state (main ROM), the sequencer ROM, and the condition ROM. The mux controls which of these sources gets through to the state register. If the previous state’s “next state” field determines where to go, neither the OPTest nor ChkCmp signals will be asserted. If the opcode from the IR determines the next state (such as at the end of the FETCH state), the OPTest signal will be asserted. If the comparison circuitry determines the next state (such as in the SKP instruction), the ChkCmp signal will be asserted. Note that these two signals should never be asserted at the same time since nothing is input into the “11” pin on the MUX.

The sequencer ROM should have one address per instruction, and the condition ROM should have one address for condition true and one for condition false.

Before getting down to specifics you need to determine the control scheme for the datapath. To do this examine each instruction, one by one, and construct a finite state bubble diagram showing exactly what control signals will be set in each state. Also determine what are the conditions necessary to pass from one state to the next. You can experiment by manually controlling your control signals on the bus you’ve created in Phase 1 – Implement the Datapath to make sure that your logic is sound.

Once the finite state bubble diagram is produced, the next step is to encode the contents of the Control Unit ROM using MCGen. Then you must design and build (in CircuitSim) the Control Unit circuit which will contain the three ROMs, a MUX, and a state register. Your design will be better if it allows you to single step and ensure that it is working properly. Finally, you will load the Control Unit’s ROMs with the hexadecimal generated by MCGen’s export feature.

Note that the input address to the ROM uses bit 0 for the lowest bit of the current state and 5 for the highest bit for the current state.

<h2>Table 3: ROM Output Signals</h2>

<table width="536">

 <tbody>

  <tr>

   <td width="34">Bit</td>

   <td width="90">Purpose</td>

   <td width="36">Bit</td>

   <td width="66">Purpose</td>

   <td width="36">Bit</td>

   <td width="65">Purpose</td>

   <td width="36">Bit</td>

   <td width="72">Purpose</td>

   <td width="36">Bit</td>

   <td width="68">Purpose</td>

  </tr>

  <tr>

   <td width="34">0</td>

   <td width="90">NextState[0]</td>

   <td width="36">6</td>

   <td width="66">DrREG</td>

   <td width="36">12</td>

   <td width="65">LdIR</td>

   <td width="36">18</td>

   <td width="72">WrMEM</td>

   <td width="36">24</td>

   <td width="68">ChkCmp</td>

  </tr>

  <tr>

   <td width="34">1</td>

   <td width="90">NextState[1]</td>

   <td width="36">7</td>

   <td width="66">DrMEM</td>

   <td width="36">13</td>

   <td width="65">LdMAR</td>

   <td width="36">19</td>

   <td width="72">RegSelLo</td>

   <td width="36"></td>

   <td width="68"></td>

  </tr>

  <tr>

   <td width="34">2</td>

   <td width="90">NextState[2]</td>

   <td width="36">8</td>

   <td width="66">DrALU</td>

   <td width="36">14</td>

   <td width="65">LdA</td>

   <td width="36">20</td>

   <td width="72">RegSelHi</td>

   <td width="36"></td>

   <td width="68"></td>

  </tr>

  <tr>

   <td width="34">3</td>

   <td width="90">NextState[3]</td>

   <td width="36">9</td>

   <td width="66">DrPC</td>

   <td width="36">15</td>

   <td width="65">LdB</td>

   <td width="36">21</td>

   <td width="72">ALULo</td>

   <td width="36"></td>

   <td width="68"></td>

  </tr>

  <tr>

   <td width="34">4</td>

   <td width="90">NextState[4]</td>

   <td width="36">10</td>

   <td width="66">DrOFF</td>

   <td width="36">16</td>

   <td width="65">LdCmp</td>

   <td width="36">22</td>

   <td width="72">ALUHi</td>

   <td width="36"></td>

   <td width="68"></td>

  </tr>

  <tr>

   <td width="34">5</td>

   <td width="90">NextState[5]</td>

   <td width="36">11</td>

   <td width="66">LdPC</td>

   <td width="36">17</td>

   <td width="65">WrREG</td>

   <td width="36">23</td>

   <td width="72">OPTest</td>

   <td width="36"></td>

   <td width="68"></td>

  </tr>

 </tbody>

</table>

<h2>Table 4: Register Selection Map</h2>

<table width="242">

 <tbody>

  <tr>

   <td width="69">RegSelHi</td>

   <td width="70">RegSelLo</td>

   <td width="103">Register</td>

  </tr>

  <tr>

   <td width="69">0</td>

   <td width="70">0</td>

   <td width="103">RX (IR[27:24])</td>

  </tr>

  <tr>

   <td width="69">0</td>

   <td width="70">1</td>

   <td width="103">RY (IR[23:20])</td>

  </tr>

  <tr>

   <td width="69">1</td>

   <td width="70">0</td>

   <td width="103">RZ (IR[3:0])</td>

  </tr>

  <tr>

   <td width="69">1</td>

   <td width="70">1</td>

   <td width="103">unused</td>

  </tr>

 </tbody>

</table>

<h2>Table 5: ALU Function Map</h2>

<table width="188">

 <tbody>

  <tr>

   <td width="58">ALUHi</td>

   <td width="63">ALUlLo</td>

   <td width="67">Function</td>

  </tr>

  <tr>

   <td width="58">0</td>

   <td width="63">0</td>

   <td width="67">ADD</td>

  </tr>

  <tr>

   <td width="58">0</td>

   <td width="63">1</td>

   <td width="67">SUB</td>

  </tr>

  <tr>

   <td width="58">1</td>

   <td width="63">0</td>

   <td width="67">NAND</td>

  </tr>

  <tr>

   <td width="58">1</td>

   <td width="63">1</td>

   <td width="67">A + 1</td>

  </tr>

 </tbody>

</table>