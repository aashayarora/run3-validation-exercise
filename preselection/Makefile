CXX = g++
CPPFLAGS = -g -Wall -O2
MYINCLUDES = -I include/
ROOTFLAGS = $(shell root-config --libs --cflags) -lRooFit -lRooFitCore -lRooStats -lMinuit -lFoam -lMathMore
CORRECTIONLIBFLAGS = -I $(shell correction config --incdir --ldflags --rpath)

MAKEFLAGS := --jobs=8

SRCS = $(wildcard src/*.cpp)
OBJS = $(patsubst src/%.cpp,build/%.o,$(SRCS))

TARGET = runAnalysis

BUILD_DIR = build/

all: oogabooga

oogabooga: $(OBJS)
	$(CXX) $(CPPFLAGS) $(MYINCLUDES) $(ROOTFLAGS) $(CORRECTIONLIBFLAGS) $(OBJS) -o bin/$(TARGET)

build/%.o: src/%.cpp | $(BUILD_DIR)
	$(CXX) $(CPPFLAGS) $(MYINCLUDES) $(ROOTFLAGS) $(CORRECTIONLIBFLAGS) -c $< -o $@

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

.DELETE_ON_ERROR:

clean:
	$(RM) $(OBJS) bin/$(TARGET)

clearplots:
	$(RM)

.PHONY: all oogabooga clean clearplots
