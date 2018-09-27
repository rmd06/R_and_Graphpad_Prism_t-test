## Common Statistical Tests in R and and Graphpad® Prism: Student's t-test

### Synopsis
The student's t-test was first created by William Gosset, while doing analyses on beer in the Guiness Brewery in Dublin [[citation needed]()].  Gosset used the pseudonym "Student" on the paper that he published with the results, and the test that he developed became known as the "Student's T-test", or simply a "t-test".

There are a few different ways to run the t-test, but the methods to perform the test on each variant is similar in GraphPad Prism and R.  Briefly, the tails for the t-test refer to how the data should be measured, meaning [does the data go in one direction, or two](https://stats.idre.ucla.edu/other/mult-pkg/faq/general/faq-what-are-the-differences-between-one-tailed-and-two-tailed-tests/).  Nearly all biological experiments should use a two-tailed t-test.  A paired t-test is typically used for datasets that are linked to each other in some way, such as treating cells at timepoint 1, then treating the same cells at timepoint 2, and testing whether the results are statistically significant. An unpaired t-test tests whether two unrelated datasets, such as if cells treated with Chemical X versus cells treated with Chemical Y have results that are statistically significantly different.  

If you are uncertain about which test to use, typically a two-tailed, unpaired t-test is what you want. 

The files for this are attached, as well as the Challenge Question Solutions.

#### Example Data

        Male	Female
        54	43
        23	34
        45	65
        54	77
        45	46
        33	65

#### Unpaired t-test using Graphpad Prism

1) Select "Column", and the radio button for "Enter replicate values, stacked into columns"
2) Copy and paste the data, then select "Analyze", and under Column analyses, select "t-tests (and non-parametric tests).
3) Under Experimental Design, make sure the following is selected:
* Unpaired
* "Yes, use parametric test"
* Unpaired t-test, assume both populations have the same SD.
4) Click OK.  The results should look like this:

        "Table Analyzed"	"Unpaired t test data"
        	
        "Column B"	Female
        vs.	vs.
        "Column A"	Male
        	
        "Unpaired t test"	
        "  P value"	0.1607
        "  P value summary"	ns
        "  Significantly different (P < 0.05)?"	No
        "  One- or two-tailed P value?"	Two-tailed
        "  t, df"	"t=1.515 df=10"
        	
        "How big is the difference?"	
        "  Mean ± SEM of column A"	"42.33 ± 4.991, n=6"
        "  Mean ± SEM of column B"	"55 ± 6.708, n=6"
        "  Difference between means"	"12.67 ± 8.361"
        "  95% confidence interval"	"-5.963 to 31.3"
        "  R squared (eta squared)"	0.1867
        	
        "F test to compare variances"	
        "  F, DFn, Dfd"	"1.806, 5, 5"
        "  P value"	0.5321
        "  P value summary"	ns
        "  Significantly different (P < 0.05)?"	No

#### Unpaired t-test using R

1) import the table into R:

        t <- read.csv('t-test_exampleData.csv')

2) type the following command:

        t.test(t$Male, t$Female, var.equal = TRUE)

3) You should get the following output:


		Two Sample t-test
		
		data:  t$Male and t$Female
		t = -1.5149, df = 10, p-value = 0.1607
		alternative hypothesis: true difference in means is not equal to 0
		95 percent confidence interval:
		-31.296774   5.963441
		sample estimates:
		mean of x mean of y 
		42.33333  55.00000 

Comments: specifying "var.equal = TRUE" forces R to run an equal variance t-test.  In the Experimental Design step in Graphpad Prism, this would be the same as selecting "Unpaired t-test, assume both populations have the same SD".  The default in R is 

        t.test(t$Male, t$Female, var.equal = FALSE)

which runs a t-test and does not assume equal SD.  This is the same in Graphpad Prism as selecting "Unpaired t-test with Welch's correction. Do not assume equal SD".  

Optional Challenge questions:
1) Are the data normally distributed?
2) How would you run a non-parametric test using Graphpad Prism and R?
