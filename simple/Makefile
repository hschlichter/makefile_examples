CC = clang
CFLAGS = -std=c17 -O0 -g -Wall -MMD -fPIC
LDFLAGS = 
INCLUDE = -I.
BUILDDIR = ./build
LDINCLUDE = 

SRCS = $(wildcard *.c **/*.c)
OBJS = $(foreach obj, $(SRCS:.c=.o), $(BUILDDIR)/$(obj))

$(OBJS): $(BUILDDIR)/%.o: %.c
	@mkdir -p $(dir $@)
	$(CC) -c $(CFLAGS) -o $@ $< $(INCLUDE)

-include $(OBJS:%.o=%.d)

.PHONY: all
all: $(OBJS)
	$(CC) $^ -o $(BUILDDIR)/main $(CFLAGS) $(INCLUDE) $(LDINCLUDE) $(LDFLAGS)

.PHONY: clean
clean:
	@rm -rf $(BUILDDIR)

print-%  : ; @echo $* = $($*)
