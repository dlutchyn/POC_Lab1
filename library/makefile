CC ?= gcc
CFLAGS ?= -o3
LIBEXT ?= .dll

BIN_DIR = bin
OBJ_DIR = obj

HEADERS = $(wildcard *.h)
SOURCES = $(wildcard *.c)
OBJ = $(patsubst %.c,$(OBJ_DIR)/%.o,$(SOURCES))

PROGRAM_NAME = libzlib
BIN_DIR = bin
OBJ_DIR = obj

ST_EXTENTION = .a
DYN_EXTENTION = $(LIBEXT)

all: create_directories $(BIN_DIR)/$(PROGRAM_NAME)$(ST_EXTENTION) $(BIN_DIR)/$(PROGRAM_NAME)$(DYN_EXTENTION)

create_directories:
	mkdir -p $(BIN_DIR)
	mkdir -p $(OBJ_DIR)

-include $(OBJ:.o=$(OBJ_DIR)/.d)

$(BIN_DIR)/$(PROGRAM_NAME)$(ST_EXTENTION): $(OBJ)
	ar rcs $@ -o $^

$(BIN_DIR)/$(PROGRAM_NAME)$(DYN_EXTENTION): $(OBJ)
	$(CC) -shared -fPIC -o $@ $^
	
$(OBJ_DIR)/%.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@
	$(CC) -MM -MP -MT $@ -MF $(OBJ_DIR)/$*.d $(CFLAGS) $<

.PHONY: clean create_directories
clean:
	rm -rf *.o *.d $(OBJ_DIR)/*.o $(OBJ_DIR)/*.d $(BIN_DIR)/$(PROGRAM_NAME)$(ST_EXTENTION) $(BIN_DIR)/$(PROGRAM_NAME)$(DYN_EXTENTION)
