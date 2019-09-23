CXX ?= g++
CXXFLAGS += -O3 -march=native -std=c++11 -pthread -fPIC -I../include/
OPENMP := 0

ifeq ($(shell $(CXX) --version | grep "Apple"),)
	OPENMP := 1
endif

ifeq ($(OPENMP), 1)
	CXXFLAGS += -fopenmp
	LDFLAGS += -fopenmp
else
	CXXFLAGS += -DSINGLE_THREADED
endif

LDFLAGS += -lpthread

all: shared_lib

shared_lib: libn2.so

libn2.so: base.o hnsw.o hnsw_node.o distance.o heuristic.o mmap.o
	$(CXX) $(CXXFLAGS) -shared -o $@ $(LDFLAGS) $?

static_lib: libn2.a

libn2.a: base.o hnsw.o hnsw_node.o distance.o heuristic.o mmap.o
	ar rvs $@ $?

clean:
	rm -f *.o n2.so n2.a
