# capturaYear-xsl-template

<b>This template will grab the year or range of years from various types of standaryzed spanish date strings vía XSLT 1.0</b>

* Use transform.html to test it with Javascript (<b>xslt.js</b> by <i>Johann Burkard</i>: http://johannburkard.de/software/xsltjs/)
* Use transform.php to test it with PHP (<code>$ php transform.php > dates_transformed.xml</code>)

<b>What parses:</b>

* Matches and removes <i>circa</i> (<b>ca.</b>) at the begining of the date string.
* Matches, takes acount & removes <i>antes de Cristo</i> (<b>a.c.</b>) at the end of the date string.
* Converts <i>antes de Cristo</i> (<b>a.c.</b>) date strings to  negative years.
* Avoids the year <b>0</b> and converts it to <b>1</b> or <b>-1</b> depending on the case.
* Converts centuries (<b>siglo</b>) in roman numerals to range of years.
* Generates year ranges for <i>unknown</i> date digits (<b>u</b>), eg. <b>178u</b>, <b>17uu</b>, <b>1u89</b>.

<b>Accepted input formats:</b>

    [ca.] YYYY-MM-DD [a.c.]
    siglo XX [a.c.]

<b>Will correctly output the year of following test date strings:</b>

    original  =>  year [to year]
    0  =>  1
    u  =>  1 to 9
    ca. u000 a.c.  =>  -9000 to -1000
    siglo I  =>  1 to 100
    siglo I a.c.  =>  -100 to -1
    ca. u8u-12-31 a.c.  =>  -989 to -180
    1789-12-31  =>  1789
    ca. 1789-12-31  =>  1789
    1789-12-31 a.c.  =>  -1789
    ca. 1789-12-31 a.c.  =>  -1789
    1789-12  =>  1789
    ca. 1789-12  =>  1789
    1789-12 a.c.  =>  -1789
    ca. 1789-12 a.c.  =>  -1789
    1789  =>  1789
    ca. 1789  =>  1789
    1789 a.c.  =>  -1789
    ca. 1789 a.c.  =>  -1789
    siglo XV  =>  1400 to 1500
    siglo XV a.c.  =>  -1500 to -1400
    178u  =>  1780 to 1789
    17uu  =>  1700 to 1799
    1uuu  =>  1000 to 1999
    u789  =>  1789
    uu89  =>  1089 to 1989
    uuu9  =>  1009 to 1999
    1u89  =>  1089 to 1989
    1uu9  =>  1009 to 1999
    u9  =>  19 to 99
    u89  =>  189 to 989
    uu9  =>  109 to 999
    ca. 178u  =>  1780 to 1789
    ca. 17uu  =>  1700 to 1799
    ca. 1uuu  =>  1000 to 1999
    ca. u789  =>  1789
    ca. uu89  =>  1089 to 1989
    ca. uuu9  =>  1009 to 1999
    ca. 1u89  =>  1089 to 1989
    ca. 1uu9  =>  1009 to 1999
    ca. u9  =>  19 to 99
    ca. u89  =>  189 to 989
    ca. uu9  =>  109 to 999
    178u a.c.  =>  -1789 to -1780
    17uu a.c.  =>  -1799 to -1700
    1uuu a.c.  =>  -1999 to -1000
    u789 a.c.  =>  -9789 to -1789
    uu89 a.c.  =>  -9989 to -1089
    uuu9 a.c.  =>  -9999 to -1009
    1u89 a.c.  =>  -1989 to -1089
    1uu9 a.c.  =>  -1999 to -1009
    u9 a.c.  =>  -99 to -19
    u89 a.c.  =>  -989 to -189
    uu9 a.c.  =>  -999 to -109
    ca. 178u a.c.  =>  -1789 to -1780
    ca. 17uu a.c.  =>  -1799 to -1700
    ca. 1uuu a.c.  =>  -1999 to -1000
    ca. u789 a.c.  =>  -9789 to -1789
    ca. uu89 a.c.  =>  -9989 to -1089
    ca. uuu9 a.c.  =>  -9999 to -1009
    ca. 1u89 a.c.  =>  -1989 to -1089
    ca. 1uu9 a.c.  =>  -1999 to -1009
    ca. u9 a.c.  =>  -99 to -19
    ca. u89 a.c.  =>  -989 to -189
    ca. uu9 a.c.  =>  -999 to -109
