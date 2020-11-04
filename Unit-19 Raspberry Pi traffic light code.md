.include "symbols.s"


	.global main
main:
	STMFD SP!, {LR}	    @preserve any necessary registers

	BL init
        loop:
@red
	MOV R0, #21
	BL set_pin_as_output
						
	MOV R0, #21
	MOV R1, #PIN_ON
	BL change_pin_state	@Turn on p21
	
	MOV R0, #2
	BL sleep		@wait two seconds
								
	MOV R0, #21
	MOV R1, #PIN_ON
	BL change_pin_state	@turn on p21

@PIN21 turns on and is kept on untill PIN20 is turned on.

@red&amber

MOV R0, #20
	BL set_pin_as_output
						
	MOV R0, #20
	MOV R1, #PIN_ON
	BL change_pin_state	@Turn on p20
	
	MOV R0, #2
	BL sleep		@wait two seconds
								
	MOV R0, #20
	MOV R1, #PIN_OFF
	BL change_pin_state	@turn off p20

MOV R0, #21
	BL set_pin_as_output
						
	MOV R0, #21
	MOV R1, #PIN_OFF
	BL change_pin_state	@Turn off p21
	
								
	MOV R0, #21
	MOV R1, #PIN_OFF
	BL change_pin_state	@turn off p21

@PIN20 turns on which is the Amber light and then both of them turn off, letting the green light to turn on.

@green

MOV R0, #16
	BL set_pin_as_output
						
	MOV R0, #16
	MOV R1, #PIN_ON
	BL change_pin_state	@Turn on p16
	
	MOV R0, #1
	BL sleep		@wait one second
								
	MOV R0, #16
	MOV R1, #PIN_OFF
	BL change_pin_state	@turn off p16
@amber

MOV R0, #20
	BL set_pin_as_output
						
	MOV R0, #20
	MOV R1, #PIN_ON
	BL change_pin_state	@Turn on p20

	MOV R0, #1
	BL sleep		@wait one second
									
	MOV R0, #20
	MOV R1, #PIN_OFF
	BL change_pin_state	@turn off p20


@backtoRed

MOV R0, #21
	BL set_pin_as_output
						
	MOV R0, #21
	MOV R1, #PIN_ON
	BL change_pin_state	@Turn on p21

	MOV R0, #1
	BL sleep		@wait one second
									
	MOV R0, #21
	MOV R1, #PIN_OFF
	BL change_pin_state	@turn off p21
@The @amber and @backtoRed makes it loop back to the Red light after that i created a function called 'BL loop' which makes the code loop back to the start of the code

        BL loop
	BL clean_up
  
	LDMFD SP!, {LR}	    	@restore stacked registers
	MOV R7, #1		@and bail
	SWI 0

	