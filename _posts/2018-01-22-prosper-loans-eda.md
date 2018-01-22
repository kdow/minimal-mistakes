---
title: Prosper Loans Exploratory Data Analysis
category: r
tags: eda
date: 2018-01-22
layout: single
author_profile: true
toc: true
---

# Introduction

This report explores a dataset of 113,937 loans with 81 variables for each loan.
These variables include information about the loan such as the amount, rate,
length, and status, as well as information on the borrower, such as credit
grade, income range, and employment status.

Let's look at the structure of this dataset:


```
## 'data.frame':	113937 obs. of  81 variables:
##  $ ListingKey                         : Factor w/ 113066 levels "00003546482094282EF90E5",..: 7180 7193 6647 6669 6686 6689 6699 6706 6687 6687 ...
##  $ ListingNumber                      : int  193129 1209647 81716 658116 909464 1074836 750899 768193 1023355 1023355 ...
##  $ ListingCreationDate                : Factor w/ 113064 levels "2005-11-09 20:44:28.847000000",..: 14184 111894 6429 64760 85967 100310 72556 74019 97834 97834 ...
##  $ CreditGrade                        : Factor w/ 9 levels "","A","AA","B",..: 5 1 8 1 1 1 1 1 1 1 ...
##  $ Term                               : int  36 36 36 36 36 60 36 36 36 36 ...
##  $ LoanStatus                         : Factor w/ 12 levels "Cancelled","Chargedoff",..: 3 4 3 4 4 4 4 4 4 4 ...
##  $ ClosedDate                         : Factor w/ 2803 levels "","2005-11-25 00:00:00",..: 1138 1 1263 1 1 1 1 1 1 1 ...
##  $ BorrowerAPR                        : num  0.165 0.12 0.283 0.125 0.246 ...
##  $ BorrowerRate                       : num  0.158 0.092 0.275 0.0974 0.2085 ...
##  $ LenderYield                        : num  0.138 0.082 0.24 0.0874 0.1985 ...
##  $ EstimatedEffectiveYield            : num  NA 0.0796 NA 0.0849 0.1832 ...
##  $ EstimatedLoss                      : num  NA 0.0249 NA 0.0249 0.0925 ...
##  $ EstimatedReturn                    : num  NA 0.0547 NA 0.06 0.0907 ...
##  $ ProsperRating..numeric.            : int  NA 6 NA 6 3 5 2 4 7 7 ...
##  $ ProsperRating..Alpha.              : Factor w/ 8 levels "","A","AA","B",..: 1 2 1 2 6 4 7 5 3 3 ...
##  $ ProsperScore                       : num  NA 7 NA 9 4 10 2 4 9 11 ...
##  $ ListingCategory..numeric.          : int  0 2 0 16 2 1 1 2 7 7 ...
##  $ BorrowerState                      : Factor w/ 52 levels "","AK","AL","AR",..: 7 7 12 12 25 34 18 6 16 16 ...
##  $ Occupation                         : Factor w/ 68 levels "","Accountant/CPA",..: 37 43 37 52 21 43 50 29 24 24 ...
##  $ EmploymentStatus                   : Factor w/ 9 levels "","Employed",..: 9 2 4 2 2 2 2 2 2 2 ...
##  $ EmploymentStatusDuration           : int  2 44 NA 113 44 82 172 103 269 269 ...
##  $ IsBorrowerHomeowner                : Factor w/ 2 levels "False","True": 2 1 1 2 2 2 1 1 2 2 ...
##  $ CurrentlyInGroup                   : Factor w/ 2 levels "False","True": 2 1 2 1 1 1 1 1 1 1 ...
##  $ GroupKey                           : Factor w/ 707 levels "","00343376901312423168731",..: 1 1 335 1 1 1 1 1 1 1 ...
##  $ DateCreditPulled                   : Factor w/ 112992 levels "2005-11-09 00:30:04.487000000",..: 14347 111883 6446 64724 85857 100382 72500 73937 97888 97888 ...
##  $ CreditScoreRangeLower              : int  640 680 480 800 680 740 680 700 820 820 ...
##  $ CreditScoreRangeUpper              : int  659 699 499 819 699 759 699 719 839 839 ...
##  $ FirstRecordedCreditLine            : Factor w/ 11586 levels "","1947-08-24 00:00:00",..: 8639 6617 8927 2247 9498 497 8265 7685 5543 5543 ...
##  $ CurrentCreditLines                 : int  5 14 NA 5 19 21 10 6 17 17 ...
##  $ OpenCreditLines                    : int  4 14 NA 5 19 17 7 6 16 16 ...
##  $ TotalCreditLinespast7years         : int  12 29 3 29 49 49 20 10 32 32 ...
##  $ OpenRevolvingAccounts              : int  1 13 0 7 6 13 6 5 12 12 ...
##  $ OpenRevolvingMonthlyPayment        : num  24 389 0 115 220 1410 214 101 219 219 ...
##  $ InquiriesLast6Months               : int  3 3 0 0 1 0 0 3 1 1 ...
##  $ TotalInquiries                     : num  3 5 1 1 9 2 0 16 6 6 ...
##  $ CurrentDelinquencies               : int  2 0 1 4 0 0 0 0 0 0 ...
##  $ AmountDelinquent                   : num  472 0 NA 10056 0 ...
##  $ DelinquenciesLast7Years            : int  4 0 0 14 0 0 0 0 0 0 ...
##  $ PublicRecordsLast10Years           : int  0 1 0 0 0 0 0 1 0 0 ...
##  $ PublicRecordsLast12Months          : int  0 0 NA 0 0 0 0 0 0 0 ...
##  $ RevolvingCreditBalance             : num  0 3989 NA 1444 6193 ...
##  $ BankcardUtilization                : num  0 0.21 NA 0.04 0.81 0.39 0.72 0.13 0.11 0.11 ...
##  $ AvailableBankcardCredit            : num  1500 10266 NA 30754 695 ...
##  $ TotalTrades                        : num  11 29 NA 26 39 47 16 10 29 29 ...
##  $ TradesNeverDelinquent..percentage. : num  0.81 1 NA 0.76 0.95 1 0.68 0.8 1 1 ...
##  $ TradesOpenedLast6Months            : num  0 2 NA 0 2 0 0 0 1 1 ...
##  $ DebtToIncomeRatio                  : num  0.17 0.18 0.06 0.15 0.26 0.36 0.27 0.24 0.25 0.25 ...
##  $ IncomeRange                        : Factor w/ 8 levels "$0","$1-24,999",..: 4 5 7 4 3 3 4 4 4 4 ...
##  $ IncomeVerifiable                   : Factor w/ 2 levels "False","True": 2 2 2 2 2 2 2 2 2 2 ...
##  $ StatedMonthlyIncome                : num  3083 6125 2083 2875 9583 ...
##  $ LoanKey                            : Factor w/ 113066 levels "00003683605746079487FF7",..: 100337 69837 46303 70776 71387 86505 91250 5425 908 908 ...
##  $ TotalProsperLoans                  : int  NA NA NA NA 1 NA NA NA NA NA ...
##  $ TotalProsperPaymentsBilled         : int  NA NA NA NA 11 NA NA NA NA NA ...
##  $ OnTimeProsperPayments              : int  NA NA NA NA 11 NA NA NA NA NA ...
##  $ ProsperPaymentsLessThanOneMonthLate: int  NA NA NA NA 0 NA NA NA NA NA ...
##  $ ProsperPaymentsOneMonthPlusLate    : int  NA NA NA NA 0 NA NA NA NA NA ...
##  $ ProsperPrincipalBorrowed           : num  NA NA NA NA 11000 NA NA NA NA NA ...
##  $ ProsperPrincipalOutstanding        : num  NA NA NA NA 9948 ...
##  $ ScorexChangeAtTimeOfListing        : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ LoanCurrentDaysDelinquent          : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ LoanFirstDefaultedCycleNumber      : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ LoanMonthsSinceOrigination         : int  78 0 86 16 6 3 11 10 3 3 ...
##  $ LoanNumber                         : int  19141 134815 6466 77296 102670 123257 88353 90051 121268 121268 ...
##  $ LoanOriginalAmount                 : int  9425 10000 3001 10000 15000 15000 3000 10000 10000 10000 ...
##  $ LoanOriginationDate                : Factor w/ 1873 levels "2005-11-15 00:00:00",..: 426 1866 260 1535 1757 1821 1649 1666 1813 1813 ...
##  $ LoanOriginationQuarter             : Factor w/ 33 levels "Q1 2006","Q1 2007",..: 18 8 2 32 24 33 16 16 33 33 ...
##  $ MemberKey                          : Factor w/ 90831 levels "00003397697413387CAF966",..: 11071 10302 33781 54939 19465 48037 60448 40951 26129 26129 ...
##  $ MonthlyLoanPayment                 : num  330 319 123 321 564 ...
##  $ LP_CustomerPayments                : num  11396 0 4187 5143 2820 ...
##  $ LP_CustomerPrincipalPayments       : num  9425 0 3001 4091 1563 ...
##  $ LP_InterestandFees                 : num  1971 0 1186 1052 1257 ...
##  $ LP_ServiceFees                     : num  -133.2 0 -24.2 -108 -60.3 ...
##  $ LP_CollectionFees                  : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ LP_GrossPrincipalLoss              : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ LP_NetPrincipalLoss                : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ LP_NonPrincipalRecoverypayments    : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ PercentFunded                      : num  1 1 1 1 1 1 1 1 1 1 ...
##  $ Recommendations                    : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ InvestmentFromFriendsCount         : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ InvestmentFromFriendsAmount        : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ Investors                          : int  258 1 41 158 20 1 1 1 1 1 ...
```

Here is a summary of this dataset:


```
##                    ListingKey     ListingNumber    
##  17A93590655669644DB4C06:     6   Min.   :      4  
##  349D3587495831350F0F648:     4   1st Qu.: 400919  
##  47C1359638497431975670B:     4   Median : 600554  
##  8474358854651984137201C:     4   Mean   : 627886  
##  DE8535960513435199406CE:     4   3rd Qu.: 892634  
##  04C13599434217079754AEE:     3   Max.   :1255725  
##  (Other)                :113912                    
##                     ListingCreationDate  CreditGrade         Term      
##  2013-10-02 17:20:16.550000000:     6          :84984   Min.   :12.00  
##  2013-08-28 20:31:41.107000000:     4   C      : 5649   1st Qu.:36.00  
##  2013-09-08 09:27:44.853000000:     4   D      : 5153   Median :36.00  
##  2013-12-06 05:43:13.830000000:     4   B      : 4389   Mean   :40.83  
##  2013-12-06 11:44:58.283000000:     4   AA     : 3509   3rd Qu.:36.00  
##  2013-08-21 07:25:22.360000000:     3   HR     : 3508   Max.   :60.00  
##  (Other)                      :113912   (Other): 6745                  
##                  LoanStatus                  ClosedDate   
##  Current              :56576                      :58848  
##  Completed            :38074   2014-03-04 00:00:00:  105  
##  Chargedoff           :11992   2014-02-19 00:00:00:  100  
##  Defaulted            : 5018   2014-02-11 00:00:00:   92  
##  Past Due (1-15 days) :  806   2012-10-30 00:00:00:   81  
##  Past Due (31-60 days):  363   2013-02-26 00:00:00:   78  
##  (Other)              : 1108   (Other)            :54633  
##   BorrowerAPR       BorrowerRate     LenderYield     
##  Min.   :0.00653   Min.   :0.0000   Min.   :-0.0100  
##  1st Qu.:0.15629   1st Qu.:0.1340   1st Qu.: 0.1242  
##  Median :0.20976   Median :0.1840   Median : 0.1730  
##  Mean   :0.21883   Mean   :0.1928   Mean   : 0.1827  
##  3rd Qu.:0.28381   3rd Qu.:0.2500   3rd Qu.: 0.2400  
##  Max.   :0.51229   Max.   :0.4975   Max.   : 0.4925  
##  NA's   :25                                          
##  EstimatedEffectiveYield EstimatedLoss   EstimatedReturn
##  Min.   :-0.183          Min.   :0.005   Min.   :-0.183  
##  1st Qu.: 0.116          1st Qu.:0.042   1st Qu.: 0.074  
##  Median : 0.162          Median :0.072   Median : 0.092  
##  Mean   : 0.169          Mean   :0.080   Mean   : 0.096  
##  3rd Qu.: 0.224          3rd Qu.:0.112   3rd Qu.: 0.117  
##  Max.   : 0.320          Max.   :0.366   Max.   : 0.284  
##  NA's   :29084           NA's   :29084   NA's   :29084   
##  ProsperRating..numeric. ProsperRating..Alpha.  ProsperScore  
##  Min.   :1.000                  :29084         Min.   : 1.00  
##  1st Qu.:3.000           C      :18345         1st Qu.: 4.00  
##  Median :4.000           B      :15581         Median : 6.00  
##  Mean   :4.072           A      :14551         Mean   : 5.95  
##  3rd Qu.:5.000           D      :14274         3rd Qu.: 8.00  
##  Max.   :7.000           E      : 9795         Max.   :11.00  
##  NA's   :29084           (Other):12307         NA's   :29084  
##  ListingCategory..numeric. BorrowerState  
##  Min.   : 0.000            CA     :14717  
##  1st Qu.: 1.000            TX     : 6842  
##  Median : 1.000            NY     : 6729  
##  Mean   : 2.774            FL     : 6720  
##  3rd Qu.: 3.000            IL     : 5921  
##  Max.   :20.000                   : 5515  
##                            (Other):67493  
##                     Occupation         EmploymentStatus
##  Other                   :28617   Employed     :67322  
##  Professional            :13628   Full-time    :26355  
##  Computer Programmer     : 4478   Self-employed: 6134  
##  Executive               : 4311   Not available: 5347  
##  Teacher                 : 3759   Other        : 3806  
##  Administrative Assistant: 3688                : 2255  
##  (Other)                 :55456   (Other)      : 2718  
##  EmploymentStatusDuration IsBorrowerHomeowner CurrentlyInGroup
##  Min.   :  0.00           False:56459         False:101218    
##  1st Qu.: 26.00           True :57478         True : 12719    
##  Median : 67.00                                               
##  Mean   : 96.07                                               
##  3rd Qu.:137.00                                               
##  Max.   :755.00                                               
##  NA's   :7625                                                 
##                     GroupKey                 DateCreditPulled
##                         :100596   2013-12-23 09:38:12:     6  
##  783C3371218786870A73D20:  1140   2013-11-21 09:09:41:     4  
##  3D4D3366260257624AB272D:   916   2013-12-06 05:43:16:     4  
##  6A3B336601725506917317E:   698   2014-01-14 20:17:49:     4  
##  FEF83377364176536637E50:   611   2014-02-09 12:14:41:     4  
##  C9643379247860156A00EC0:   342   2013-09-27 22:04:54:     3  
##  (Other)                :  9634   (Other)            :113912  
##  CreditScoreRangeLower CreditScoreRangeUpper
##  Min.   :  0.0         Min.   : 19.0        
##  1st Qu.:660.0         1st Qu.:679.0        
##  Median :680.0         Median :699.0        
##  Mean   :685.6         Mean   :704.6        
##  3rd Qu.:720.0         3rd Qu.:739.0        
##  Max.   :880.0         Max.   :899.0        
##  NA's   :591           NA's   :591          
##         FirstRecordedCreditLine CurrentCreditLines OpenCreditLines
##                     :   697     Min.   : 0.00      Min.   : 0.00  
##  1993-12-01 00:00:00:   185     1st Qu.: 7.00      1st Qu.: 6.00  
##  1994-11-01 00:00:00:   178     Median :10.00      Median : 9.00  
##  1995-11-01 00:00:00:   168     Mean   :10.32      Mean   : 9.26  
##  1990-04-01 00:00:00:   161     3rd Qu.:13.00      3rd Qu.:12.00  
##  1995-03-01 00:00:00:   159     Max.   :59.00      Max.   :54.00  
##  (Other)            :112389     NA's   :7604       NA's   :7604   
##  TotalCreditLinespast7years OpenRevolvingAccounts
##  Min.   :  2.00             Min.   : 0.00        
##  1st Qu.: 17.00             1st Qu.: 4.00        
##  Median : 25.00             Median : 6.00        
##  Mean   : 26.75             Mean   : 6.97        
##  3rd Qu.: 35.00             3rd Qu.: 9.00        
##  Max.   :136.00             Max.   :51.00        
##  NA's   :697                                     
##  OpenRevolvingMonthlyPayment InquiriesLast6Months TotalInquiries   
##  Min.   :    0.0             Min.   :  0.000      Min.   :  0.000  
##  1st Qu.:  114.0             1st Qu.:  0.000      1st Qu.:  2.000  
##  Median :  271.0             Median :  1.000      Median :  4.000  
##  Mean   :  398.3             Mean   :  1.435      Mean   :  5.584  
##  3rd Qu.:  525.0             3rd Qu.:  2.000      3rd Qu.:  7.000  
##  Max.   :14985.0             Max.   :105.000      Max.   :379.000  
##                              NA's   :697          NA's   :1159     
##  CurrentDelinquencies AmountDelinquent   DelinquenciesLast7Years
##  Min.   : 0.0000      Min.   :     0.0   Min.   : 0.000         
##  1st Qu.: 0.0000      1st Qu.:     0.0   1st Qu.: 0.000         
##  Median : 0.0000      Median :     0.0   Median : 0.000         
##  Mean   : 0.5921      Mean   :   984.5   Mean   : 4.155         
##  3rd Qu.: 0.0000      3rd Qu.:     0.0   3rd Qu.: 3.000         
##  Max.   :83.0000      Max.   :463881.0   Max.   :99.000         
##  NA's   :697          NA's   :7622       NA's   :990            
##  PublicRecordsLast10Years PublicRecordsLast12Months RevolvingCreditBalance
##  Min.   : 0.0000          Min.   : 0.000            Min.   :      0       
##  1st Qu.: 0.0000          1st Qu.: 0.000            1st Qu.:   3121       
##  Median : 0.0000          Median : 0.000            Median :   8549       
##  Mean   : 0.3126          Mean   : 0.015            Mean   :  17599       
##  3rd Qu.: 0.0000          3rd Qu.: 0.000            3rd Qu.:  19521       
##  Max.   :38.0000          Max.   :20.000            Max.   :1435667       
##  NA's   :697              NA's   :7604              NA's   :7604          
##  BankcardUtilization AvailableBankcardCredit  TotalTrades    
##  Min.   :0.000       Min.   :     0          Min.   :  0.00  
##  1st Qu.:0.310       1st Qu.:   880          1st Qu.: 15.00  
##  Median :0.600       Median :  4100          Median : 22.00  
##  Mean   :0.561       Mean   : 11210          Mean   : 23.23  
##  3rd Qu.:0.840       3rd Qu.: 13180          3rd Qu.: 30.00  
##  Max.   :5.950       Max.   :646285          Max.   :126.00  
##  NA's   :7604        NA's   :7544            NA's   :7544    
##  TradesNeverDelinquent..percentage. TradesOpenedLast6Months
##  Min.   :0.000                      Min.   : 0.000         
##  1st Qu.:0.820                      1st Qu.: 0.000         
##  Median :0.940                      Median : 0.000         
##  Mean   :0.886                      Mean   : 0.802         
##  3rd Qu.:1.000                      3rd Qu.: 1.000         
##  Max.   :1.000                      Max.   :20.000         
##  NA's   :7544                       NA's   :7544           
##  DebtToIncomeRatio         IncomeRange    IncomeVerifiable
##  Min.   : 0.000    $25,000-49,999:32192   False:  8669    
##  1st Qu.: 0.140    $50,000-74,999:31050   True :105268    
##  Median : 0.220    $100,000+     :17337                   
##  Mean   : 0.276    $75,000-99,999:16916                   
##  3rd Qu.: 0.320    Not displayed : 7741                   
##  Max.   :10.010    $1-24,999     : 7274                   
##  NA's   :8554      (Other)       : 1427                   
##  StatedMonthlyIncome                    LoanKey       TotalProsperLoans
##  Min.   :      0     CB1B37030986463208432A1:     6   Min.   :0.00     
##  1st Qu.:   3200     2DEE3698211017519D7333F:     4   1st Qu.:1.00     
##  Median :   4667     9F4B37043517554537C364C:     4   Median :1.00     
##  Mean   :   5608     D895370150591392337ED6D:     4   Mean   :1.42     
##  3rd Qu.:   6825     E6FB37073953690388BC56D:     4   3rd Qu.:2.00     
##  Max.   :1750003     0D8F37036734373301ED419:     3   Max.   :8.00     
##                      (Other)                :113912   NA's   :91852    
##  TotalProsperPaymentsBilled OnTimeProsperPayments
##  Min.   :  0.00             Min.   :  0.00       
##  1st Qu.:  9.00             1st Qu.:  9.00       
##  Median : 16.00             Median : 15.00       
##  Mean   : 22.93             Mean   : 22.27       
##  3rd Qu.: 33.00             3rd Qu.: 32.00       
##  Max.   :141.00             Max.   :141.00       
##  NA's   :91852              NA's   :91852        
##  ProsperPaymentsLessThanOneMonthLate ProsperPaymentsOneMonthPlusLate
##  Min.   : 0.00                       Min.   : 0.00                  
##  1st Qu.: 0.00                       1st Qu.: 0.00                  
##  Median : 0.00                       Median : 0.00                  
##  Mean   : 0.61                       Mean   : 0.05                  
##  3rd Qu.: 0.00                       3rd Qu.: 0.00                  
##  Max.   :42.00                       Max.   :21.00                  
##  NA's   :91852                       NA's   :91852                  
##  ProsperPrincipalBorrowed ProsperPrincipalOutstanding
##  Min.   :    0            Min.   :    0              
##  1st Qu.: 3500            1st Qu.:    0              
##  Median : 6000            Median : 1627              
##  Mean   : 8472            Mean   : 2930              
##  3rd Qu.:11000            3rd Qu.: 4127              
##  Max.   :72499            Max.   :23451              
##  NA's   :91852            NA's   :91852              
##  ScorexChangeAtTimeOfListing LoanCurrentDaysDelinquent
##  Min.   :-209.00             Min.   :   0.0           
##  1st Qu.: -35.00             1st Qu.:   0.0           
##  Median :  -3.00             Median :   0.0           
##  Mean   :  -3.22             Mean   : 152.8           
##  3rd Qu.:  25.00             3rd Qu.:   0.0           
##  Max.   : 286.00             Max.   :2704.0           
##  NA's   :95009                                        
##  LoanFirstDefaultedCycleNumber LoanMonthsSinceOrigination   LoanNumber    
##  Min.   : 0.00                 Min.   :  0.0              Min.   :     1  
##  1st Qu.: 9.00                 1st Qu.:  6.0              1st Qu.: 37332  
##  Median :14.00                 Median : 21.0              Median : 68599  
##  Mean   :16.27                 Mean   : 31.9              Mean   : 69444  
##  3rd Qu.:22.00                 3rd Qu.: 65.0              3rd Qu.:101901  
##  Max.   :44.00                 Max.   :100.0              Max.   :136486  
##  NA's   :96985                                                            
##  LoanOriginalAmount          LoanOriginationDate LoanOriginationQuarter
##  Min.   : 1000      2014-01-22 00:00:00:   491   Q4 2013:14450         
##  1st Qu.: 4000      2013-11-13 00:00:00:   490   Q1 2014:12172         
##  Median : 6500      2014-02-19 00:00:00:   439   Q3 2013: 9180         
##  Mean   : 8337      2013-10-16 00:00:00:   434   Q2 2013: 7099         
##  3rd Qu.:12000      2014-01-28 00:00:00:   339   Q3 2012: 5632         
##  Max.   :35000      2013-09-24 00:00:00:   316   Q2 2012: 5061         
##                     (Other)            :111428   (Other):60343         
##                    MemberKey      MonthlyLoanPayment LP_CustomerPayments
##  63CA34120866140639431C9:     9   Min.   :   0.0     Min.   :   -2.35   
##  16083364744933457E57FB9:     8   1st Qu.: 131.6     1st Qu.: 1005.76   
##  3A2F3380477699707C81385:     8   Median : 217.7     Median : 2583.83   
##  4D9C3403302047712AD0CDD:     8   Mean   : 272.5     Mean   : 4183.08   
##  739C338135235294782AE75:     8   3rd Qu.: 371.6     3rd Qu.: 5548.40   
##  7E1733653050264822FAA3D:     8   Max.   :2251.5     Max.   :40702.39   
##  (Other)                :113888                                         
##  LP_CustomerPrincipalPayments LP_InterestandFees LP_ServiceFees   
##  Min.   :    0.0              Min.   :   -2.35   Min.   :-664.87  
##  1st Qu.:  500.9              1st Qu.:  274.87   1st Qu.: -73.18  
##  Median : 1587.5              Median :  700.84   Median : -34.44  
##  Mean   : 3105.5              Mean   : 1077.54   Mean   : -54.73  
##  3rd Qu.: 4000.0              3rd Qu.: 1458.54   3rd Qu.: -13.92  
##  Max.   :35000.0              Max.   :15617.03   Max.   :  32.06  
##                                                                   
##  LP_CollectionFees  LP_GrossPrincipalLoss LP_NetPrincipalLoss
##  Min.   :-9274.75   Min.   :  -94.2       Min.   : -954.5    
##  1st Qu.:    0.00   1st Qu.:    0.0       1st Qu.:    0.0    
##  Median :    0.00   Median :    0.0       Median :    0.0    
##  Mean   :  -14.24   Mean   :  700.4       Mean   :  681.4    
##  3rd Qu.:    0.00   3rd Qu.:    0.0       3rd Qu.:    0.0    
##  Max.   :    0.00   Max.   :25000.0       Max.   :25000.0    
##                                                              
##  LP_NonPrincipalRecoverypayments PercentFunded    Recommendations   
##  Min.   :    0.00                Min.   :0.7000   Min.   : 0.00000  
##  1st Qu.:    0.00                1st Qu.:1.0000   1st Qu.: 0.00000  
##  Median :    0.00                Median :1.0000   Median : 0.00000  
##  Mean   :   25.14                Mean   :0.9986   Mean   : 0.04803  
##  3rd Qu.:    0.00                3rd Qu.:1.0000   3rd Qu.: 0.00000  
##  Max.   :21117.90                Max.   :1.0125   Max.   :39.00000  
##                                                                     
##  InvestmentFromFriendsCount InvestmentFromFriendsAmount   Investors      
##  Min.   : 0.00000           Min.   :    0.00            Min.   :   1.00  
##  1st Qu.: 0.00000           1st Qu.:    0.00            1st Qu.:   2.00  
##  Median : 0.00000           Median :    0.00            Median :  44.00  
##  Mean   : 0.02346           Mean   :   16.55            Mean   :  80.48  
##  3rd Qu.: 0.00000           3rd Qu.:    0.00            3rd Qu.: 115.00  
##  Max.   :33.00000           Max.   :25000.00            Max.   :1189.00  
##
```

# Univariate Plots

<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots1-1.png" class="align-center" style="width: 75%"/>

In this plot we can see that the majority of loans are current or completed.
However, it may be useful to view the categories in a different order. I'll
rearrange this variable here:


```r
#rearrange loan status

loans$LoanStatus <- factor(loans$LoanStatus,
                           levels = c("Completed", "FinalPaymentInProgress",
                                      "Current", "Past Due (1-15 days)",
                                      "Past Due (16-30 days)",
                                      "Past Due (31-60 days)",
                                      "Past Due (61-90 days)",
                                      "Past Due (91-120 days)",
                                      "Past Due (>120 days)",
                                      "Chargedoff", "Defaulted", "Cancelled"))
```


<img src="/assets/images/prosperLoanData_files/figure-html/unnamed-chunk-2-1.png" class="align-center" style="width: 75%"/>

Now this category is arranged from completed to cancelled loans.


<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots2-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots2-2.png" class="align-center" style="width: 75%"/>

These two plots show income range and stated monthly income. There are a few
issues with these plots. The income range variable is out of order and the
monthly income is being skewed by some high earners. I can adjust the graph to
leave out the top high earners, but I would also like to see this
variable converted to an annual income. I will convert this variable and
rearrange the income range variable:


```r
#rearrange income range

loans$IncomeRange <- factor(loans$IncomeRange,
                            levels = c("Not displayed","Not employed", "$0",
                                       "$1-24,999", "$25,000-49,999",
                                       "$50,000-74,999", "$75,000-99,999",
                                       "$100,000+"))
```

<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots3-1.png" class="align-center" style="width: 75%"/>


```r
#create annual income variable from stated monhly income

loans$StatedAnnualIncome <- loans$StatedMonthlyIncome * 12

qplot(data = loans, x = StatedAnnualIncome)
```

<img src="/assets/images/prosperLoanData_files/figure-html/unnamed-chunk-4-1.png" class="align-center" style="width: 75%"/>

```r
summary(loans$StatedAnnualIncome)
```

```
##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max.
##        0    38400    56000    67300    81900 21000000
```

```r
#adjust plot so we can see annual income without top 1% of earner

qplot(data = loans, x = StatedAnnualIncome) +
  scale_x_continuous(lim = c(0, quantile(loans$StatedAnnualIncome, 0.99)))
```

<img src="/assets/images/prosperLoanData_files/figure-html/unnamed-chunk-4-2.png" class="align-center" style="width: 75%"/>

<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots4-1.png" class="align-center" style="width: 75%"/>

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
##    1000    4000    6500    8337   12000   35000
```

Here we can see that the shape of orignal loan amount is right skewed, with
many peaks around roughly $5k intervals.

<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots5-1.png" class="align-center" style="width: 75%"/>

Most borrowers are employed in some manner, with full-time employment being the
largest category. However, there are a few groups that I think would be best
combined into one "NA" level: "", "Not Available", and "Other".


```r
#adjust employment status variable

loans$EmploymentAdjusted<- factor(loans$EmploymentStatus,
                                  levels = c("Employed", "Full-time",
                                             "Part-time", "Self-employed",
                                             "Not employed", "Retired"))
```


<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots6-1.png" class="align-center" style="width: 75%"/>


<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots7-1.png" class="align-center" style="width: 75%"/>

This plot of listing category shows that some categories are much more popular
than others. However, we would need to reference the variable dictionary to see
what these are. I will create a new variable which stores the category names as
factors.



```r
#convert numeric categories
loans$ListingCategory <- cut(loans$ListingCategory..numeric.,
                             breaks = c(0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,
                                        16,17,18,19,20,21),
                             labels = c("Not Available", "Debt Consolidation",
                                        "Home Improvement", "Business",
                                        "Personal Loan", "Student Use", "Auto",
                                        "Other", "Baby&Adoption", "Boat",
                                        "Cosmetic Procedure", "Engagement Ring",
                                        "Green Loans", "Household Expenses",
                                        "Large Purchases", "Medical/Dental",
                                        "Motorcycle", "RV", "Taxes", "Vacation",
                                        "Wedding Loans"), right = FALSE)
```


```
##  [1] "Not Available"      "Debt Consolidation" "Home Improvement"  
##  [4] "Business"           "Personal Loan"      "Student Use"       
##  [7] "Auto"               "Other"              "Baby&Adoption"     
## [10] "Boat"               "Cosmetic Procedure" "Engagement Ring"   
## [13] "Green Loans"        "Household Expenses" "Large Purchases"   
## [16] "Medical/Dental"     "Motorcycle"         "RV"                
## [19] "Taxes"              "Vacation"           "Wedding Loans"
```

<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots8-1.png" class="align-center" style="width: 75%"/>

This plot shows that debt consolidation is by far the largest category. The next
two categories are not available, and other. Of the other names categories, the
next largest are home improvement and business.



```r
#create loan origination year and month variables from loan origination date

loans$LoanOriginationYear <- as.factor(year(loans$LoanOriginationDate))
loans$LoanOriginationMonth <- as.factor(month(loans$LoanOriginationDate))


#remove year from loan origination quarter variable
loans$LoanQuarter <- substr(loans$LoanOriginationQuarter,1-2,2)
```

I created a few more variables. We have a loan origination date variable which
has the day, month, and year for each loan. I've created a variable that has
just the year, and one that has just the month. I've also created a variable
that will have just the quarter of the loan, without the year.


<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots9-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots9-2.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots9-3.png" class="align-center" style="width: 75%"/>

These three plots show when each loan started, broken down by each year, month,
and quarter. There are very few loans started in 2005, so it is likely that
Prosper either started with a small number of loans at the end of 2005, or that
the data collection for this dataset started at the end of 2005. We can see a
dropoff in loans in 2009 (which could be correlated with the recession), then
the number of loans builds up each year to a high in 2013. This year has way
more loans than any other year; it may be interesting to look at this year more
in depth as it has the most data.

On average, April has the lowest number of loans started, and
January the highest. The second quarter has the least amount of loans, and the
fourth quarter the highest.

<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots10-1.png" class="align-center" style="width: 75%"/>

In this plot we can see that the number of homeowners is only slighly higher
than non homeowners.


```r
#create credit score mean variable
loans$CreditScoreMean <- (loans$CreditScoreRangeLower +
                            loans$CreditScoreRangeUpper)/2

#create credit score category variable
loans$CreditScoreCategory <- cut(loans$CreditScoreMean,
                                 breaks = c(0, 550, 650, 700, 750, 900),
                                 labels = c("Bad", "Poor", "Fair", "Good",
                                            "Excellent"),
                                 include.lowest = TRUE,
                                 right = FALSE)
```

There is a credit score range lower variable, and a credit score range upper
variable. I've created a new variable which takes the mean of these two numbers,
so we can use this one variable in our analysis. I've then created another
variable which breaks up the mean credit scores into categories: Bad - Under
550, Poor - 550-650, Fair - 650-700, Good - 700-750, and Excellent - 750
and higher.

<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots11-1.png" class="align-center" style="width: 75%"/>

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's
##     9.5   669.5   689.5   695.1   729.5   889.5     591
```

<img src="/assets/images/prosperLoanData_files/figure-html/Univariate_Plots11-2.png" class="align-center" style="width: 75%"/>

In the first plot we can see that the mean credit score for a small amount of
borrowers is 0. The rest of the borrowers scores start at 450, with most
borrowers having mean credit scores ranging between 625 and 725. The largest
group by far appears to be about 680 - 710.

When we look at the credit score category graph, we can see the largest groups
are Fair and Good.

# Univariate Analysis

For this report, the main features of interest in this dataset will be loan
status, income, and credit score. Other features of interest are loan
origination year, whether or not the borrower is a homeowner, and listing
category.

To aid my analysis, I have created a few new variables from the existing
variables in this dataset. I made ListingCategory..numeric. into a categorical
variable with the categories listed as factors. I  made loan origination month
and year variables from loan origination date. I made a variable for loan
quarter which just has the quarter without the year. I made a credit score mean
variable from the credit score upper range and lower range variables. From this
credit score mean, I made a credit score category. I made a stated annual income
variable from the stated monthly income variable. I made an adjusted employment
variable which combines the "", "Not available", and "Other" levels of
employment status into one NA level.

I rearranged the order of loan status and income range so that they will appear
in a logical fashion when graphed.


# Bivariate Plots

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots1-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots1-2.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots1-3.png" class="align-center" style="width: 75%"/>

In the first plot we can see that the final payment in progress group has a
slightly higher median stated annual income than the other groups, while the
cancelled group has the lowest. The IQR for the loans that are past due over 120
days is smaller.

The second plot shows the credit score mean is much lower for the chargedoff,
defaulted, and cancelled groups. There are a number of outliers in the completed
group with low credit scores.

In the third plot, there is a slight upward trend for the past due groups, where
the borrower rate increases. The current and completed groups have similar
borrower rates.

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots2-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots2-2.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots2-3.png" class="align-center" style="width: 75%"/>

In these plots we can see that the median borrower rate is highest for cosmetic
procedures and lowest for personal loans, however the stated annual
income median and IQR is similar for these two groups. Student use has the
lowest stated annual income, whereas taxes have the highest. The personal loan
and student use groups have the largest IQR and lowest medians, after the not
available group.

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots3-1.png" class="align-center" style="width: 75%"/>

Although there is a trend of less current delinquencies as credit score
increases, there is a drop around 600.

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots4-1.png" class="align-center" style="width: 75%"/>

The median original loan amount for homeowners is higher, along with the IQR.

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots5-1.png" class="align-center" style="width: 75%"/>

In this plot, we can see that the not employed group has a higher credit score
mean than the groups who earn less than $75k.

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots6-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots6-2.png" class="align-center" style="width: 75%"/>

In the first plot, we can see that the stated annual income rises slightly each
year from 2006-2014. The income for 2005 is noticeably higher than the other
groups. We saw earlier that there are very few loans from 2005 in this dataset.
Due to this small sample size, it isn't as representative of the data as a whole
compared to the other groups which contain many more loans.

In the second plot, we can see the loan amounts rising overall, but there is a
dip in 2008 and 2009 before it starts rising again. As we saw previously, this
is likely due to the recession. We can also see that it looks like loans were
limited to \$25,000 until 2013, when the limit rose to \$35,000.

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots7-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots7-2.png" class="align-center" style="width: 75%"/>

In the first plot, we can see that stated annual income and loan origination
month are about the same throughout the year.

In the second plot, we can see that loan amounts are about the same from April
to August. They start rising in September and are highest in January and
February.

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots8-1.png" class="align-center" style="width: 75%"/>

This plot shows a few noticeable peaks. The excellent credit score group has a
high amount of borrowers with a low rate around 0.08. The bad credit score group
has a high peak around 0.29, and a few smaller peaks at 0.24 and 0.35.

<img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots9-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Bivariate_Plots9-2.png" class="align-center" style="width: 75%"/>

These two plots are using a subsetted version of the dataset which only
includes loans started in 2013. In the first plot we can see that Green Loans
have the highest median mean credit score. Some of the lowest median mean credit
scores are for Auto, Other, Engagement Ring, Household Expenses, and Vacation.

The second plot shows that the highest median stated annual income is for the RV
category, followed by Taxes and Baby&Adoption. Some of the lowest are Auto,
Other, Cosmetic Procedure, Household Expenses, Motocycle, and Vacation.

# Bivariate Analysis

In this section, we've seen that there is a strong relationship between credit
score category and borrower rate. We also saw that loans that were chargedoff,
defaulted, or cancelled had borrowers with lower credit scores that other loan
status groups. Another observation is that homeowners took out bigger loans than
non-homeowners.


# Multivariate Plots

<img src="/assets/images/prosperLoanData_files/figure-html/unnamed-chunk-9-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/unnamed-chunk-9-2.png" class="align-center" style="width: 75%"/>

In the first plot we can see that the debt consolidation group has the most and
highest amount of loans. In 2008 and 2009, there are a large number of personal
loans and loans for student use. From 2012 on, there are a large number of loans
in other categories, which could indicate that these categories were introduced
at that time, and there may have been fewer listing categories available
previously.

In the second plot, loan amount and listing category are shown by quarter. We
can more clearly see the categories that have smaller loans on average. We can
also see that some loan categories don't have any loans higher than $25,000,
which appeared to be the loan limit up until 2013. There's a good chance that
some of the categories that do not have loans over $25,000 were not part of the
list of loan categories after 2012.

We've previously seen that debt consolidation is the largest loan category, and
that the largest loans are taken out in the first and fourth quarter of the
year. In this plot, we can see that the median loan for debt consolidation is
around $10,000 in the first and fourth quarters, and observably lower in the
second and third quarters. We see this same pattern in home improvement,
business, wedding loans, baby and adoption. In green loans, we see a similar
pattern, but with a distinct increase in the fourth quarter.


Let's look at just 2013:

<img src="/assets/images/prosperLoanData_files/figure-html/unnamed-chunk-10-1.png" class="align-center" style="width: 75%"/>

We can see that a couple of the categories are not present in this plot
(Personal loan and Student Use), and there are fewer "Not Available", so we can
see loans broken down into more specific categories in this plot. It is
interesting to see the different loan amounts per quarter for each category.

In this plot, the median loan amount for debt consolidation is the same
throughout the year. Green loans continues its trend of having high loan
original amounts in the fourth quarter.


<img src="/assets/images/prosperLoanData_files/figure-html/Multivariate_Plots2-1.png" class="align-center" style="width: 75%"/>

Overall, it appears homeowners have a lower borrower rate.


<img src="/assets/images/prosperLoanData_files/figure-html/Multivariate_Plots3-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Multivariate_Plots3-2.png" class="align-center" style="width: 75%"/>

In the first plot, we can see that homeowners have higher credit scores and
higher stated annual income. Borrowers with lower incomes and credit scores tend
not to be homeowners.

In the second plot, we can more clearly see the disparity in median credit
scores between homeowners and non homeowners.

If we test the correlation between just credit score mean and stated annual
income, we see that there is not a linear relationship:


```
## [1] 0.1079008
```


<img src="/assets/images/prosperLoanData_files/figure-html/Multivariate_Plots4-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Multivariate_Plots4-2.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Multivariate_Plots4-3.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Multivariate_Plots4-4.png" class="align-center" style="width: 75%"/>

These plots show loan status and stated annual income grouped by credit
score category and whether or not the borrower is a homeowner. The first two
plots include the whole dataset, whereas the last two plots only show borrowers
who started loans in 2013. One interesting difference is that the 2013 plots
have two less credit score categories. The "Bad" and "NA" groups are not
included. This could mean that Prosper no longer allows borrowers with bad
credit or no credit to create loans, or that lenders chose not to lend to those
groups. As observed earlier, homeowners tend to have higher credit
scores. There is an observable low number of chargedoff and defaulted loans in
the excellent credit score group in 2013, however, for all years there are a
large number of chargedoff and defaulted loans in the excellent credit score
group when we look at all years.

One interesting observation is that the median annual income for homeowners is
almost always higher than non-homeowners. An exception is for chargedoff loans
and loans 61-120 days past due for borrowers with Excellent credit in 2013.
Another observation is homeowners with fair credit who defaulted on their loan
have a relatively high median income.


<img src="/assets/images/prosperLoanData_files/figure-html/Multivariate_Plots5-1.png" class="align-center" style="width: 75%"/>

This plot looks at the borrower rate, original loan amount and credit score
category, broken down by loan status for loans originating in 2013. We can see
that borrowers with good credit have more loans for higher amounts and lower
rates.

Let's look at the correlation for borrower rate, original loan amoun, and credit
score mean for loans overall, and in just 2013.


```
## [1] -0.3289599
```

```
## [1] -0.4071593
```

There is a weak negative linear relationship for borrower rate and loan original
amount, but it is almost a moderate relationship in 2013.


```
## [1] 0.3408745
```

```
## [1] 0.2999042
```

We see a weak positive linear relationship for credit score mean and loan
original amount, and it a little stronger overall than for just 2013.



```
## [1] -0.4615667
```

```
## [1] -0.5597953
```

Here we see a moderate negative linear relationship for credit score mean and
borrower rate, with the relationship being stronger in 2013.






# Multivariate Analysis

In this section we saw that homeowners tend to have higher credit scores and
stated annual income. I found it interesting that even borrowers with excellent
credit scores had many defaulted and chargedoff loans.


------

# Final Plots and Summary

### Plot One
<img src="/assets/images/prosperLoanData_files/figure-html/Plot_One-1.png" class="align-center" style="width: 75%"/>

### Description One

This plot shows that homeowners tend to have higher incomes and credit scores.
I chose this plot to feature because there is a distinct difference visible
based on homeownership.

### Plot Two
<img src="/assets/images/prosperLoanData_files/figure-html/Plot_Two-1.png" class="align-center" style="width: 75%"/>

### Description Two

This plot shows a breakdown in loan categories by quarter. In previous plots,
we saw that debt consolidation has the highest number of loans. We also saw that
the most loans and the biggest loans are taken out in the first and fourth
quarters. These observations are also reflected in this plot. I chose to include
this plot because it's easy to see how the range in loan amount and median loan
amounts differ between categories and quarters.


### Plot Three
<img src="/assets/images/prosperLoanData_files/figure-html/Plot_Three-1.png" class="align-center" style="width: 75%"/><img src="/assets/images/prosperLoanData_files/figure-html/Plot_Three-2.png" class="align-center" style="width: 75%"/>

### Description Three

I chose to show this as both scatterplots and boxplots so that amount of loans
as well as median and IQR could be displayed by homeownership. These charts
reinforce that homeowners tend to have better credit as well as higher stated
incomes. We can also see that they tend to have less chargedoff and defaulted
loans. Thus we could conclude that homeowners with higher incomes are better
loan candidates.




------

# Reflection

For me, a difficulty with a dataset of this size (number of variables and
observations), was deciding which data to use and where to put my focus. As I
began to explore the data, I began to find interesting patterns that warranted
further exploration such as the high number of loans in 2013, and the patterns
of homeownershp. I was able to find patterns in the data through visualizations.

For future work on this dataset, it would be interesting to explore the
BorrowerState variable to see how the variables I've explored are related
geographically.
