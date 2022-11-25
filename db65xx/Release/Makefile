#SRCS = \
#	6502_decimal_test.ca65 \
#	6502_functional_test.ca65 \
#	65C02_extended_opcodes_test.ca65
#
#OBJS = $(SRCS:%.ca65=%.bin)
#
#all: $(OBJS)
#
#%.bin: %.ca65
#	ca65 -l $*.lst $<
#	ld65 $*.o -o $@ -m $*.map -C example.cfg

E = c:\cc65
W = $(MAKEDIR)
R = $W\Release
O = $R\obj
S = $W\src
L = $R\listing
TARGETS = $R\6502_tests.bin \
	$R\65C02_tests.bin \
	$R\decimal_tests.bin
SOURCES = $S\6502_functional_test.s \
	$S\65C02_extended_opcodes_test.s \
	$S\6502_decimal_test.s
OBJECTS = $O\6502_functional_test.o \
	$O\65C02_extended_opcodes_test.o \
	$O\6502_decimal_test.o

all : $(TARGETS)

$(TARGETS) : $(OBJECTS) $(SOURCES) $R\Makefile $R\tests.cfg
	$E\ca65 --cpu 65C02 -g -l $L\6502_functional_test.lst -o $O\6502_functional_test.o $S\6502_functional_test.s
	$E\ca65 --cpu 65C02 -g -l $L\65C02_extended_opcodes_test.lst -o $O\65C02_extended_opcodes_test.o $S\65C02_extended_opcodes_test.s
	$E\ca65 --cpu 65C02 -g -l $L\6502_decimal_test.lst -o $O\6502_decimal_test.o $S\6502_decimal_test.s
	$E\ld65 -o $R\6502_tests.bin -m $L\6502_tests.map -Ln $L\6502_tests.sym -C $R\tests.cfg --dbgfile $L\6502_tests.dbg $O\6502_functional_test.o
	$E\ld65 -o $R\65C02_tests.bin -m $L\65C02_tests.map -Ln $L\65C02_tests.sym -C $R\tests.cfg --dbgfile $L\65C02_tests.dbg $O\65C02_extended_opcodes_test.o
	$E\ld65 -o $R\decimal_tests.bin -m $L\decimal_tests.map -Ln $L\decimal_tests.sym -C $R\tests.cfg --dbgfile $L\decimal_tests.dbg $O\6502_decimal_test.o
	copy "$L\6502_tests.dbg" "$R\6502_tests.dbg"
	copy "$L\65C02_tests.dbg" "$R\65C02_tests.dbg"
	copy "$L\decimal_tests.dbg" "$R\decimal_tests.dbg"
