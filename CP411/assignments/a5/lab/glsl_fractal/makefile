
# Makefile for glsl_fractal
# Build each example in src/ into an executable and link shared glsl sources.

SRC_DIR := src

CXX := g++
CXXFLAGS := -O0 -g -Wall
LDLIBS := -lfreeglut -lopengl32 -lglu32 -lglew32

SRCS := $(wildcard $(SRC_DIR)/*.cpp)
PROGS := $(patsubst $(SRC_DIR)/%.cpp,%.exe,$(SRCS))

.PHONY: all clean run-%

all: $(PROGS)

# Build rule: foo.exe from src/foo.cpp and link any shared glsl sources
%.exe: $(SRC_DIR)/%.cpp $(SRC_DIR)/glsl/*.cpp
	$(CXX) $(CXXFLAGS) -o $@ $^ $(LDLIBS)

# Run helper: make run-julia_bitmap_f7
run-%: %.exe
	./$<

clean:
	rm -f $(PROGS)

