CC = clang
CFLAGS = -std=c17 -O0 -g -Wall -MMD -fPIC
LDFLAGS = 
INCLUDE = -I. -Ihello/include
BUILDDIR = ./build
LDINCLUDE = -L. -L$(BUILDDIR)

SRCS = $(wildcard hello/src/*.c hello/src/**/*.c)
OBJS = $(foreach obj, $(SRCS:.c=.o), $(BUILDDIR)/$(obj))

.PHONY: all
all: test

$(OBJS): $(BUILDDIR)/%.o: %.c
	@mkdir -p $(dir $@)
	$(CC) -c $(CFLAGS) -o $@ $< $(INCLUDE)

-include $(OBJS:%.o=%.d)

$(BUILDDIR)/libhello.so: $(OBJS)
	clang -shared -o $(BUILDDIR)/libhello.so $^

test: test/main.c $(BUILDDIR)/libhello.so
	$(CC) $< -o $(BUILDDIR)/test $(CFLAGS) $(INCLUDE) $(LDINCLUDE) $(LDFLAGS) -lhello

.PHONY: clean
clean:
	@rm -rf $(BUILDDIR)

print-%  : ; @echo $* = $($*)
