CXX = g++
CXX_FLAGS  = -O2 -march=native -fpermissive -Wno-write-strings
LINK_FLAGS = -lpthread -ldl

THREADS = 4
WORDS   = 1000000
INPUT   = ../input/voc-1M.txt

# File names
EXEC = stem_porter
SOURCES = main.cpp porter.cpp ../../utils/timer.cpp
OBJECTS = $(SOURCES:.cpp=.o)

.PHONY: all test

all : $(EXEC)
$(EXEC): $(OBJECTS) Makefile
	$(CXX) $(CXX_FLAGS) $(OBJECTS) -o $(EXEC) $(LINK_FLAGS)

# To obtain object files
%.o: %.cpp Makefile
	$(CXX) -c $(CXX_FLAGS) $(EXTRA_FLAGS) $< -o $@

# test
test: CXX_FLAGS += -DTESTING
test: all
	@./$(EXEC) $(THREADS) $(WORDS) $(INPUT)
	-@diff -q ../input/$(EXEC).baseline ../input/$(EXEC).pthread

# To remove generated files
clean:
	$(RM) -f $(EXEC) $(OBJECTS) *.o ../input/$(EXEC).pthread
