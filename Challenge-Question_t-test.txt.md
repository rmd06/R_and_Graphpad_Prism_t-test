Optional Challenge questions:
1) Yes, the data is normally distributed.  You can check this by plotting the data to determine if it fits a normal curve, or selecting "Analyze", "Column Statistics", and then running the Shapiro-Wilk Normality test.
[See this very good explanation of what the test describes](https://www.graphpad.com/guides/prism/7/statistics/index.htm?stat_howto_columnstatistics.htm), and [also see here](https://www.graphpad.com/guides/prism/7/statistics/index.htm?)
2) In GraphPad Prism, select "No, use nonparametric test" under "Assume Gaussian Distribution".  In R, run this command instead:

    wilcox.test(t$Male,t$Female)
