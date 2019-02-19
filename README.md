# SolsTiS-Tuning

Stripped down version of the Labview Code used for tuning the SolsTiS M2 Laser with a High Precision wavemeter. This program uses both the built-in SolsTiS tuning for tuning larger than 1 MHz and for high precision steps (<1 MHz) uses the slow and fast resonator analog inputs


Files will need the wavemeter .dll to be executable

Program is oriented in stages that loop until endpoint is reached

1.  Init - Initializes variables and sets the modulation analog modulation voltages to zero.  Then proceeds to first lock
2.  First Lock - Uses the SolsTiS software to tune to the desired frequency.  There is the option to round this tune frequency command to a value.  This is useful to get around the fact that at the point this code was written the SolsTiS tune command was truncated based on the JSON library 6 digit limitation (single MHz).  The finer tuning will be done on the next step.
3.  Second Lock - Stops the SolsTiS lock control.  Uses the fast and slow modulation inputs on the SolsTis and a PID algorithm using the wavemeter reading as the control variable to lock to desired frequency.  This will continue until the Jump! command occures from either this program or is received from another program from the global variable.  Reaching designated stopping wavelengths will also stop the lock loop.  
4.  Jump - This step will set the desired frequency to the current frequency + stepsize and then use the SolsTiS software to tune to this frequnecy just as in the First lock step.  This step also keeps track of several variables such as jump number.  
