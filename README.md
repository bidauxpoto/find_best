# find_best

### Installation using conda:
```conda install -c molinerislab find_best```

### Description
Data analysis tool to find the rows with the highest score among those sharing the same value(s) in one or more columns identified through ID_COL.

### Usage and options:
```
find_best [OPTIONS] ID_COL[:ID_COL...] SCORE_COL[:SCORE_COL...] < TABLE

Options:
    -h, --help           show this help message and exit
    -s, --sorted         assume the input is already sorted by ID
    -r, --reverse        take the lowest SCORE(s)
    -m, --multiple       in case of ties, select all the rows with higher SCORE
    -n N, --many=N       select N rows
    -a, --absolute       sort by absolute values.
    -H, --skip_header    skip the first row and report it as is in stdout

ID_COL[:ID_COL...]: integer value(s) referring to the column(s) we want to be shared by the rows among which we want to select the one with the highest score
SCORE_COL[:SCORE_COL...]: integer value(s) referring to the column(s) with the score(s) among which we want to select the highest
TABLE: tab_separated file given as input
```

___________________________

### Example:
table.tsv
```
#myh_gene   patient  specimen     score_1     score_2
MYH4        pt_1     A            14.0        192.2
MYH4        pt_1     B            12.0        31.9
MYH3        pt_1     A            3.0         76.2
MYH3        pt_1     B            21.0        74.7
MYH7B       pt_1     A            34.0        342.6
MYH7B       pt_1     B            6.0         100.3
MYH4        pt_2     A            9.0         112.5
MYH4        pt_2     B            29.0        188.4
MYH3        pt_2     A            4.0         192.5
MYH3        pt_2     B            5.0         178.5
MYH7B       pt_2     A            78.0        111.5
MYH7B       pt_2     B            3.0         278.2
MYH4        pt_3     A            32.0        23.9
MYH4        pt_3     B            31.0        201.7
MYH3        pt_3     A            18.0        29.8
MYH3        pt_3     B            28.0        29.2
MYH7B       pt_3     A            4.0         244.3
MYH7B       pt_3     B            39.0        278.2
```

Command ```find_best -H 1:2 4 < table.tsv``` returns:
```
#myh_gene   patient  specimen     score_1     score_2
MYH3        pt_1     B            21.0        74.7
MYH3        pt_2     B            5.0         178.5
MYH3        pt_3     B            28.0        29.2
MYH4        pt_1     A            14.0        192.2
MYH4        pt_2     B            29.0        188.4
MYH4        pt_3     A            32.0        23.9
MYH7B       pt_1     A            34.0        342.6
MYH7B       pt_2     A            78.0        111.5
MYH7B       pt_3     B            39.0        278.2
```

Command ```find_best -H 1:3 5 < table.tsv``` returns:
```
#myh_gene   patient  specimen     score_1     score_2
MYH3        pt_2     A            4.0         192.5
MYH3        pt_2     B            5.0         178.5
MYH4        pt_1     A            14.0        192.2
MYH4        pt_3     B            31.0        201.7
MYH7B       pt_1     A            34.0        342.6
MYH7B       pt_2     B            3.0         278.2
```

Command ```find_best -m -H 1:3 5 < table.tsv``` returns:
```
#myh_gene   patient  specimen     score_1     score_2
MYH3        pt_2     A            4.0         192.5
MYH3        pt_2     B            5.0         178.5
MYH4        pt_1     A            14.0        192.2
MYH4        pt_3     B            31.0        201.7
MYH7B       pt_1     A            34.0        342.6
MYH7B       pt_2     B            3.0         278.2
MYH7B       pt_3     B            39.0        278.2
```
