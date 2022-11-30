E = c:\cc65
W = $(MAKEDIR)
R = $W\Release
O = $R\obj
S = $W\src
L = $R\listing
TARGETS = $R\6502_functional_test.bin \
	$R\65C02_extended_opcodes_test.bin \
	$R\6502_decimal_test.bin
SOURCES = $S\6502_functional_test.s \
	$S\65C02_extended_opcodes_test.s \
	$S\6502_decimal_test.s
OBJECTS = $O\6502_functional_test.o \
	$O\65C02_extended_opcodes_test.o \
	$O\6502_decimal_test.o

.SUFFIXES: .s .o

!IF !EXIST($O)
!IF [cmd /c mkdir $O] == 0
!MESSAGE Created $O
!ENDIF
!ENDIF

!IF !EXIST($L)
!IF [cmd /c mkdir $L] == 0
!MESSAGE Created $L
!ENDIF
!ENDIF

all : $(TARGETS)

{$S}.s{$O}.o:
	$E\ca65 --cpu 65C02 -g -l $L\$(@B).lst -o $@ $<

$(TARGETS) : $(OBJECTS) $(SOURCES) $R\Makefile $R\tests.cfg
	$E\ld65 -o $@ -m $L\$(@B).map -Ln $L\$(@B).sym -C $R\tests.cfg --dbgfile $L\$(@B).dbg $O\$(@B).o
	copy "$L\$(@B).dbg" "$R\$(@B).dbg"
