CC = gcc
CPPFLAGS = -I./include
CFLAGS = `pkg-config --cflags glib-2.0`
LIBS = `pkg-config --libs glib-2.0`

RM = rm -rf
MKDIR = mkdir -p

TARGET = demo


SRCS = 
OBJS = 

SRCS += $(wildcard *.c)
OBJS += $(patsubst %.c, %.o, $(SRCS))

TARGET:$(OBJS)
	$(CC) -o $(TARGET) $(OBJS) $(LIBS)

$(OBJS):%.o:%.c
	$(CC) -c $(CPPFLAGS) $(CFLAGS) -o $@ $<

.PHONY:fmt clean cleanall
clean:
	-$(RM) $(TARGET) $(OBJS)

cleanall:
	-$(RM) $(TARGET) $(OBJS)  %.o
