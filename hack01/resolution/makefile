CC := gcc

SRC_F := preload.c
OBJ := preload.o
SHRD_LIB := preload.so




OUTPUT := answer.out





run: $(SHRD_LIB)
	LD_PRELOAD=$(shell pwd)/$(SHRD_LIB) ../docrypt $(FILE) $(KEY)


$(OBJ): $(SRC_F)
	$(CC) -m32 -c -fPIC $(SRC_F) -o $(OBJ)



$(SHRD_LIB): $(OBJ)
	$(CC) -m32 -shared -o $(SHRD_LIB) $(OBJ)

