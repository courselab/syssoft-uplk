run: preload.so
	LD_PRELOAD=./preload.so ../docrypt ../sample.cry easy >> answer.out


preload.so:
	gcc -m32 -c -fPIC preload.c -o preload.o
	gcc -m32 -shared -o preload.so preload.o

