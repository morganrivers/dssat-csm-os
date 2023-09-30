This is an early version of DSSAT that is compatible with the cultivar files I am working with for the mink global gridded system.

It builds the DSSAT executable file.

I fixed a couple bugs mostly having to do with errors where there was a conditional with a divide by zero in the second conditional.

So somewthing like:

```
IF (MGPP .GT. 0.0 .AND. GPP/MGPP .LT. 2.0) THEN
   GPP    = MGPP*2.0
   TGPP   = GPP - MGPP
ENDIF
```

would change to:

```
IF (MGPP .GT. 0.0) THEN
    IF (GPP/MGPP .LT. 2.0) THEN
        GPP = MGPP*2.0
        TGPP = GPP - MGPP
    ENDIF
ENDIF
```


To use it, I typically run the following:

```
# make build directory if doesn't exist
mkdir -p build

# compile
cmake .. -DCMAKE_BUILD_TYPE=DEBUG
make

# copy compiled executable to appropriate DSSAT executable file in mink
cp bin/dscsm047 ../[mink directory location here]/basics_15jun22/sge_Mink3daily/actual_program_4.7.5.11/dscsm047_debug
```