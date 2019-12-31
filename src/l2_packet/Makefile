all: libl2_packet.a

clean:
	rm -f *~ *.o *.d *.gcno *.gcda *.gcov libl2_packet.a

install:
	@echo Nothing to be made.

include ../lib.rules

ifdef CONFIG_L2_PACKET
ifdef CONFIG_DNET_PCAP
ifdef CONFIG_L2_FREEBSD
LIBS += -lpcap
LIB_OBJS += l2_packet_freebsd.o
else
LIBS += -ldnet -lpcap
LIB_OBJS += l2_packet_pcap.o
endif
else
LIB_OBJS += l2_packet_linux.o
endif
else
LIB_OBJS += l2_packet_none.o
endif

libl2_packet.a: $(LIB_OBJS)
	$(AR) crT $@ $?

-include $(OBJS:%.o=%.d)
