CC ?= gcc
CFLAGS ?= -o3

BIN_DIR = bin
OBJ_DIR = obj

SOURCES = example.c minigzip.c
OBJ = $(patsubst %.c,$(OBJ_DIR)/%.o,$(SOURCES))
TARGETS = $(patsubst %.c,$(BIN_DIR)/%.exe,$(SOURCES))

all: create_directories $(TARGETS)

-include $(OBJ:.o=$(OBJ_DIR)/.d)

create_directories:
	mkdir -p $(BIN_DIR)
	mkdir -p $(OBJ_DIR)
	
$(BIN_DIR)/%.exe: $(OBJ_DIR)/%.o
	$(CC) -fPIC -o $@ $< -lzlib -L../library/bin
	
$(OBJ_DIR)/%.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@
	$(CC) -MM -MP -MT $@ -MF $(OBJ_DIR)/$*.d $(CFLAGS) $<

PHONY: clean create_directories
clean:
	rm -rf *.o *.d $(OBJ_DIR)/*.o $(OBJ_DIR)/*.d $(BIN_DIR)/%.exe



