# Compiler
CXX = g++
CXXFLAGS = -std=c++17 -g -I.

# Source files
SRC_FILES = TemplateClassTests.cpp
OBJ_FILES = $(SRC_FILES:.cpp=.o)

# Executable
TARGET = test

# Google Test
GTEST_LIB = -lgtest -lgtest_main -pthread

# Build rules
all: $(TARGET)

$(TARGET): $(OBJ_FILES)
	$(CXX) $(OBJ_FILES) -o $@ $(GTEST_LIB)

%.o: %.cpp
	 $(CXX) $(CXXFLAGS) -c $< -o $@

clean:
	 rm -f $(OBJ_FILES) $(TARGET)

.PHONY: all clean