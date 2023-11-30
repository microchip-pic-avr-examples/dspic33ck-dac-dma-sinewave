<picture>
    <source media="(prefers-color-scheme: dark)" srcset="images/microchip_logo_white_red.png">
	<source media="(prefers-color-scheme: light)" srcset="images/microchip_logo_black_red.png">
    <img alt="Microchip Logo." src="images/microchip_logo_black_red.png">
</picture>

## Sine Wave Demo using the DMA, DAC and PWM drivers

![Sine Wave reading on an oscilloscope](images/SineWaveReading.png)

# Summary

The dspic33ck DAC DMA PWM sine wave Demo shows an example configuration of the DMA driver to iterate through a 256 point sine look up table to generate a 100 Hz sine wave using the PWM driver.

## Related Documentation

[DMA Driver Documentation](https://onlinedocs.microchip.com/v2/keyword-lookup?keyword=DMA_16BIT_MELODY_DRIVER&version=latest&redirect=true)

[DMA FRM Documentation](https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ProductDocuments/ReferenceManuals/dsPIC33-PIC24-FRM-Direct-Memory-Access-Controller-%28DMA%29-DS30009742C.pdf)

[DAC Driver Documentation](https://onlinedocs.microchip.com/v2/keyword-lookup?keyword=CMP_DAC_Melody_Driver&version=latest&redirect=true)

[PWM Driver Documentation](https://onlinedocs.microchip.com/v2/keyword-lookup?keyword=PWM_16BIT_MELODY_DRIVER&version=latest&redirect=true)

# Software Used 
- MPLAB® X IDE  **6.15** or newer (https://www.microchip.com/MPLABXIDE)
- MPLAB® XC16 Compiler **2.10** or a newer compiler (https://www.microchip.com/xc16) 
- MPLAB® Code Configurator (MCC) **5.3.7** or newer (https://www.microchip.com/mcc)
- MPLAB® Code Configurator (MCC) Melody **2.6.3** or newer (https://www.microchip.com/melody)

# Hardware Used
- Debugging tool: MPLAB® PICkit™ 4 In-Circuit Debugger (https://www.microchip.com/PICkit4) **or** PKOB (PICkit On-Board)
#### With either of the selected boards:
- dsPIC33CK Curiosity Development Board (https://www.microchip.com/dsPIC33CKCuriosity)
- Explorer 16/32 Development Board (https://www.microchip.com/Explorer1632)
    - dsPIC33CK256MP508 General Purpose Plug-in Module (https://www.microchip.com/MA330042)

# Setup

The dspic33ck sine wave demo uses the Explorer 16/32 Development board or the dsPIC33CK Curiosity Development board.  The boards are plugged in for programming through PKOB(PICkit On-Board) or the PicKit 4. 

The setup for each board is slightly different:
- Explorer 16/32 Development Board
    - dsPIC33CK256MP508 PIM inserted into the designated slot
    - The Sine Wave signal (DACOUT) can be read in on P25
- dsPIC33CK Curiosity Development board
    - The Sine Wave signal (DACOUT) can be read in on RA3

## Software Setup
### Peripheral Configurations

System/Clock SettingsDefault Clock settings are used for this demo
- DMA Driver
    - DMA Channel 0 Settings:
        |Setting|Value|Explaination|
        |--------------|----|-------------------------------------------------------------------------------------------------------|
        |Enable Channel|True| Enables the Channel.|
        |Enable Reload|True|The registers are reloaded to previous values at the next start.|
        |Transfer Mode|Repeated One-Shot|This allows the DMA to iterate to the Transfer Count value then start over repeatedly.|
        |Trigger Sources|SCCP1 Timer/OC/IC Event|This allows for an event of the SCCP1 compare event. (Triggered by the PWM driver) |
        |Source Address Mode|Incremented|Increments the Source Address value by the Data Size|
        |Source Address|0|This is set within the applicaiton code to use the address of the first sine wave point.|
        |Destination Address Mode|Unchanged|This means the destination address will not be affected by the DMA iteration.|
        |Destination Address|0|This is set within the applicaiton code.|
        |Data Size|16 bit|Sets that transaction size.|
        |Transfer Count|0x100|The number of times to iterate in one-shot. (256 times)|
- DAC Driver

- PWM Driver
### Programming the Device
1. Open the dspic33ck_dac_dma_pwm_sinewave.X project in MPLAB® X IDE.
2. Right click the project in "Projects" tab of MPLAB® X IDE and select "Set as Main Project".
3. Plug in the PKOB (PICkit On-Board) or the PICKit 4 from the board to the PC.
4. Program the device by selecting the "Make and Program Device (Project dspic33ck_dac_dma_pwm_sinewave)" button on the menu bar.
5. The project should build and program successfully.

# Operation
After programming the device and connecting an Oscilloscope to the pin described before a 100 Hz sinewave will be present. 


