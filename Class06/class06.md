# Class06: R functions
Bobbie Morales (A15443382)

- [A second function](#a-second-function)
- [a protein generating function](#a-protein-generating-function)

All functions in R have at least 3 things:

-A **name**, we pick this and use it to call our function, -Inout
**arguments** (there can be multiple) -The **body** lines of R code that
do the work

Our first(silly) function

Write a function to add some numbers

``` r
add <- function(x,y=1) {
  x + y
}
```

now we can call this function:

``` r
add(c(10, 10), 100)
```

    [1] 110 110

``` r
add(10,100)
```

    [1] 110

## A second function

Write a function to generate random nucleotide sequences of a user
specified length:

the `sample()` function can be helpful here.

``` r
v <- sample(c("A", "C", "G", "T"), size=50, replace = TRUE)
```

I want the a 1 element long character vector that looks like “CACAGC”

``` r
paste(v, collapse = "")
```

    [1] "TCCCTTCGAACGGCTTCACCTAATAAATATTGCTGAGGAACTGCCCCATG"

Turn this into my first wee function

``` r
generate_dna <- function(size = 50){
v <- sample(c("A", "C", "G", "T"), size = size, replace = TRUE)
paste(v, collapse = "")
}
```

Test it:

``` r
generate_dna(60)
```

    [1] "CACGCACACTTTAGTGCTGCGGCGGATTATAATAGCGAGATAGCTATGAGCAGGAGGAGG"

``` r
fasta <- TRUE
if(fasta){
  cat("HELLO You!")
} else {
  cat("No you don't")
}
```

    HELLO You!

Add the ability to return a multi-element vector or a single element
fasta like vector.

``` r
generate_fasta <- function(size = 50, fasta= FALSE) {
v <- sample(c("A", "C", "G", "T"), size = size, replace = TRUE)
s<- paste(v, collapse = "")
    if(fasta) {
  return(s)
      } else {
  return(v)
      }
}
```

\]

``` r
generate_fasta(10)
```

     [1] "A" "A" "A" "T" "G" "G" "G" "A" "G" "T"

## a protein generating function

``` r
generate_protein <- function(size = 50, fasta = TRUE) {
  aa <- c("A", "R", "N", "D", "C", "Q", "E", "G", "H", "I", 
          "L", "K", "M", "F", "P", "S", "T", "W", "Y", "V")
  v <- sample(aa, size = size, replace = TRUE)
  s <- paste(v, collapse = "")
  if (fasta) {
    return(s)
  } else {
    return(v)
  }
}
```

``` r
generate_protein(6)
```

    [1] "AMYSAG"

Use our new `generate_protein()` functin to makerandom protein sequences
of length 6 to 12 (i.e one length 6, one length7, etc. up to length 12)

one way to do this is brute force.

``` r
generate_protein(6)
```

    [1] "KTEELW"

``` r
generate_protein(7)
```

    [1] "RSNGCNY"

``` r
generate_protein(8)
```

    [1] "KYDIHPRY"

A second way is to use a `for()` loop

``` r
lengths <- 6:12
lengths
```

    [1]  6  7  8  9 10 11 12

``` r
for(i in lengths){
  cat(">",i,"\n", sep = "")
  aa <-generate_protein(i)
  cat(aa)
  cat("\n")

}
```

    >6
    TEAKPT
    >7
    IQQTTER
    >8
    WKDETFAG
    >9
    FHKYGELHE
    >10
    FLASLDYRWH
    >11
    REWDHFGQMLD
    >12
    SPVYFPFRLYWQ

a third, and better, way to solve this is to use the `apply()` family of
functions, specifically the `sapply` function in this case

``` r
sapply(6:12,generate_protein)
```

    [1] "WDGALL"       "DDTNNYD"      "DNAQRKFI"     "AYIWRFPKE"    "HKRQYQPPGF"  
    [6] "EKCQGDPPFLD"  "CSHIKDRQWWHF"
