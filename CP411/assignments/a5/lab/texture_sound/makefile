
SRC_DIR := src

CXX := g++
LDLIBS := -lfreeglut -lopengl32 -lglu32 -lwinmm

SRCS := $(SRC_DIR)/texture_sound.cpp
# Produce program names: src/glsl_cube1.cpp -> cube1.exe
TARGET := texture.exe

.PHONY: all clean run

all: $(TARGET)

# Pattern rule: compile cubeN.exe from src/glsl_cubeN.cpp and link with glsl/*.cpp
$(TARGET): 
	$(CXX) $(SRCS) -o $(TARGET) $(LDLIBS)

# run helper: make run-1
run: $(TARGET)
	./$(TARGET)

clean:
	rm -f $(TARGET)
