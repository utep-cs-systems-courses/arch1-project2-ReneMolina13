#makefile configuration
COMMON_OBJECTS = initToy.o adjustPWM.o toyCtrl.o main.o
CPU	       = msp430g2553
CFLAGS         = -mmcu=${CPU} -I../demos/h
LDFLAGS        = -L/opt/ti/msp430_gcc/include

#switch the compiler (for the internal make rules)
CC             = msp430-elf-gcc
AS             = msp430-elf-as

all: led-c.elf led-s.elf

#additional rules for files
led-c.elf: ${COMMON_OBJECTS} buzzerAdjust-c.o
	${CC} ${CFLAGS} ${LDFLAGS} -o $@ $^
led-s.elf: ${COMMON_OBJECTS} buzzerAdjust-s.o
	${AS} ${CFLAGS} ${LDFLAGS} -o $@ $^

load-c: led-c.elf
	$msp430loader.sh
load-s: led-s.elf
	$msp430loader.sh

clean: $^
	rm -f *. *.elf

main.o: libTimer.h led.h toyCtrl.h
toyCtrl.o: led.h toyCtrl.h adjustPWM.h
adjustPWM.o: led.h toyCtrl.h adjustPWM.h
initToy.o: led.h initToy.h toyCtrl.h
buzzerAdjust-c.o: toyCtrl.h adjustPWM.h
buzzerAdjust-s.o: toyCtrl.h adjustPWM.h
