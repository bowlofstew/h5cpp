#  _____________________________________________________________________________
#  Copyright (c) <2018> <copyright Steven Varga, Toronto, On>
#  Contact: Steven Varga
#           steven@vargaconsulting.ca
#           2018 Toronto, On Canada
#  _____________________________________________________________________________

CXXFLAGS =  -std=c++11  -I/usr/local/include -I/usr/local/h5cpp-llvm
LIBS =  -lhdf5  -lz -ldl -lm

test: packettable
	./packettable

# compiler assisted introspection will scan TU translation unit, which is the 
# collection of files you're compiling into an object, generates desired output
# from topologically ordered dependency graph. 
# currently POD structs, arrays and integral types are supported, in arbitrary deep
# embedding
#
# with -Dmyfile.h specifies the generated output, which must be sandwiched between
# <h5cpp/core> and <h5cpp/io>
generated.h: struct.h
	h5cpp  packettable.cpp -- $(CXXFLAGS)  -Dgenerated.h

packettable.o : packettable.cpp generated.h 
	$(CXX) -o packettable.o  $(CXXFLAGS) -c packettable.cpp

packettable: packettable.o
	$(CXX) $^ $(LIBS) -o $@	

clean:
	@$(RM) *.o *.h5 $(apps) generated.h packettable

.PHONY: test

