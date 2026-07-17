# Liquid-Batching-System-TIA-Portal
Industrial automation project using Siemens TIA Portal V17 - PLC programming, HMI design, and safety systems for liquid batching process

SEQUENCE :
IF #safety_Estop OR #pump_overload OR #stop_btn THEN
    #current_step := 99
    ;
END_IF;
// --- 2. STATE MACHINE ---
CASE #current_step OF
    0:  // IDLE (Waiting for Start)
        // Turn off all outputs to ensure safe state
        #pump1_run := FALSE;
        #MainTank_LiqA_valve := FALSE;
        #MainTank_LiqB_valve := FALSE;
        #MainTank_heater := FALSE;
        #MainTank_mixer := FALSE;
        #MainTank_drain_valve := FALSE;
        IF #start_btn THEN
            #current_step := 10;
        END_IF;
        
    10:  // Fill liquid A
        #pump1_run := TRUE;
        #MainTank_LiqA_valve := TRUE;
        IF #MainTank_Level_1 THEN
            #pump1_run := FALSE;
            #MainTank_LiqA_valve := FALSE;
            #current_step := 20;
        END_IF;
    20: // Fill liquid B
        #MainTank_LiqB_valve := TRUE;
        IF #MainTank_Level_2 THEN
            #MainTank_LiqB_valve := FALSE;
            #current_step := 30;
        END_IF;
    30: // Heating
        #MainTank_heater := TRUE;
        IF #actual_temp >= #temp_hmi_setpoint THEN
            #MainTank_heater := FALSE;
            #current_step := 40;
            ;
        END_IF;
        
        
        ;
    40: // MIXER
        #MainTank_mixer := TRUE;
        
        #time_set_point_time:= INT_TO_TIME(#mix_time_setpoint);
        
        #mix_timer.TON(IN:= TRUE,
                       PT:= #time_set_point_time );
        IF #mix_timer.Q THEN
            #mix_timer.TON(IN := FALSE, PT:= #time_set_point_time);
            #MainTank_mixer := FALSE;
            #current_step := 50;
            ;
        END_IF;
   
    50: // DRAINING
        #MainTank_drain_valve := TRUE;
        IF #MainTank_Level_low THEN
            #MainTank_drain_valve := FALSE;
            #current_step := 0;
            ;
        END_IF;
    99: // ERROR
        #pump1_run := FALSE;
        #MainTank_LiqA_valve := FALSE;
        #MainTank_LiqB_valve := FALSE;
        #MainTank_heater := FALSE;
        #MainTank_mixer := FALSE;
        #MainTank_drain_valve := FALSE;
        IF #reset_fault THEN
            #current_step := 0;
        END_IF;
        ;
END_CASE;
