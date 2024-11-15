# Traffic Light Controller using Verilog HDL and Testbench Verification

## Aim

To design and simulate a traffic light controller using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 simulation environment. The objective is to control the traffic lights for a junction with a specific time-based sequence for Red, Yellow, and Green lights.

## Apparatus Required

Vivado 2023.1 or equivalent Verilog simulation tool.
Computer system with a suitable operating system.
FPGA board (optional for hardware verification).

## Procedure

Launch Vivado 2023.1:

Open Vivado and create a new project.
Design the Traffic Light Controller Verilog Code:

Write the Verilog code for the traffic light controller, using an FSM (Finite State Machine) to transition between Green, Yellow, and Red lights based on timing intervals.
Create the Testbench:

Write a testbench to simulate the traffic light controller. The testbench will check the sequence of light transitions based on time.
Add the Verilog Files:

Add the traffic light controller Verilog code and the testbench file to the project.
Run Simulation:

Run the behavioral simulation in Vivado to verify the correct sequence of the traffic lights.
Observe the Waveforms:

Examine the waveform output to verify that the traffic light transitions through the Green, Yellow, and Red lights in the correct sequence.
Save and Document Results:

Capture screenshots of the waveform and save the simulation logs to include in your report.

Verilog Code for Traffic Light Controller
```
// Inputs to the module (reg type in testbench)
reg clk;
reg reset;

// Outputs from the module (wire type in testbench)
wire [2:0] lights;

// Instantiate the traffic_light_controller module
traffic_light_controller uut (
    .clk(clk),
    .reset(reset),
    .lights(lights)
);

// Clock generation: 10ns period
always begin
    #5 clk = ~clk;  // Toggle clock every 5 time units (10 ns clock period)
end

// Initial block to apply stimulus (inputs)
initial begin
    // Initialize inputs
    clk = 0;
    reset = 1;  // Start with reset active
    
    // Wait for a few cycles with reset asserted
    #20;
    reset = 0;  // Release reset after 20ns

    // Let the simulation run for a while
    #1000;

    // End simulation
    $finish;
end

// Monitor the outputs during the simulation
initial begin
    // Print header
    $display("Time\tReset\tLights");
    $monitor("%d\t%b\t%b", $time, reset, lights);
end
endmodule
```
Testbench for Traffic Light Controller
```
// Inputs to the module (reg type in testbench)
reg clk;
reg reset;

// Outputs from the module (wire type in testbench)
wire [2:0] lights;

// Instantiate the traffic_light_controller module
traffic_light_controller uut (
    .clk(clk),
    .reset(reset),
    .lights(lights)
);

// Clock generation: 10ns period
always begin
    #5 clk = ~clk;  // Toggle clock every 5 time units (10 ns clock period)
end

// Initial block to apply stimulus (inputs)
initial begin
    // Initialize inputs
    clk = 0;
    reset = 1;  // Start with reset active
    
    // Wait for a few cycles with reset asserted
    #20;
    reset = 0;  // Release reset after 20ns

    // Let the simulation run for a while
    #1000;

    // End simulation
    $finish;
end

// Monitor the outputs during the simulation
initial begin
    // Print header
    $display("Time\tReset\tLights");
    $monitor("%d\t%b\t%b", $time, reset, lights);
end
endmodule
```
## output:
![image](https://github.com/user-attachments/assets/eedfed08-b5ff-4d2c-977d-bb8a611a492a)



## Conclusion

In this experiment, a traffic light controller was successfully designed and simulated using Verilog HDL. The design controlled the traffic lights to switch between Green, Yellow, and Red in a cyclic manner based on timing intervals. The testbench verified that the traffic lights followed the correct sequence and timing. The simulation results confirm the correct functionality of the traffic light controller, demonstrating the effectiveness of Verilog HDL in designing FSM-based controllers for real-world applications.
