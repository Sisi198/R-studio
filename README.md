<img width="407" height="109" alt="image" src="https://github.com/user-attachments/assets/411b1660-c5e3-4efa-8480-124dea0af371" /><img width="403" height="133" alt="image" src="https://github.com/user-attachments/assets/f8507221-71d4-4527-a7a0-76cf4feb1ecc" /><img width="880" height="168" alt="Screenshot 2026-05-12 at 10 17 59 pm" src="https://github.com/user-attachments/assets/7b0d7d50-4b6f-45cb-b71f-5a919732759c" /># R-studio

<Likert scale>

#package install

library(psych) 

# read data

load("SDQ.RData") 

# selecting variables

items_emotion<-c("somatic","worries","unhappy","clingy","afraid") 

# Computing test score

rowSums(SDQ[items_emotion]) ( SDQ = data file name) / computes the sum of specified variables for each row

rowSums(SDQ[items_emotion], na.rm=TRUE) (removing NA data (missing data) )

rowMeans(SDQ[items_emotion], na.rm=TRUE)*5 ( 5: likert scale number)

SDQ$S_emotion <- rowMeans(SDQ[items_emotion], na.rm=TRUE)*5 -set the name of removed missing data

hist(SDQ$S_emotion) -histogram 

<img width="452" height="335" alt="image" src="https://github.com/user-attachments/assets/bdf9792c-3eac-400b-8fa8-ad68f3a4e84e" />


describe(SDQ$S_emotion) - mean, sd, median (min max range skew kurtosis) 

<img width="452" height="216" alt="image" src="https://github.com/user-attachments/assets/a1092f66-a02a-44e3-9e72-4127b994ef67" />


# Norm referencing

FIRST!!

Check the cutoff: 

EX: 

Normal: 0-5

Borderline: 6

Abnormal: 7-10

table(SDQ$S_emotion<=5) (<= :  ≤ / >= : ≥ / == : = )


<img width="452" height="302" alt="image" src="https://github.com/user-attachments/assets/fcf9c12f-6b3f-4383-b614-d70a3978003d" />

<img width="452" height="273" alt="image" src="https://github.com/user-attachments/assets/c4c25ebc-25ef-4072-993b-c72894cdda63" />



 
# <Classical test theory: Classical Test Theory analysis of a scale compiled from binary items>

# package install

library(psych)

EPQ <- read.delim(file="EPQ_N.dat") - import the data into into a new object (data frame) called EPQ

describe(EPQ) -mean, median, SD …

lowerCor(EPQ) - compute the product -moment (Pearson) correlations

lowerCor(EPQ, use="pairwise") - missing values will be treated in the pairwise fashion

tetrachoric(EPQ) -tetrachoric correlations; These would be more appropriate for binary items on which a NO/YES dichotomy was forced

N_score <- rowMeans(EPQ, na.rm=TRUE)*23 - compute the average score from non-missing item responses (removing ‘NA’ values from calculation, na.rm=TRUE / 23 (the number of items in the Neuroticism scale)  

<img width="452" height="317" alt="image" src="https://github.com/user-attachments/assets/819cf7c9-d995-434a-b561-b18627eda908" />

<img width="452" height="100" alt="image" src="https://github.com/user-attachments/assets/68c4125d-6770-4045-ab35-79940e483ae3" />

<img width="452" height="119" alt="image" src="https://github.com/user-attachments/assets/4308f18f-7524-475f-b045-124804e7d9d5" />


 describe(N_score) -mean, median, SD …  

 <img width="452" height="209" alt="image" src="https://github.com/user-attachments/assets/0eb63a9d-dabe-4628-bdc7-f2d5b65ba3cf" />

 
hist(N_score) -histogram

# Internal consistency reliability
alpha(EPQ) -“internal consistency reliability” (Cronbach’s alpha) of the total score (average score)

<img width="452" height="35" alt="image" src="https://github.com/user-attachments/assets/15a05cd0-3418-49b1-a696-6005360cca03" />
<img width="452" height="159" alt="image" src="https://github.com/user-attachments/assets/e1af1295-d1bd-41bb-ba96-febcf265f068" />


  
alpha(EPQ, cumulative=TRUE)  -To obtain the mean and SD for the sum score

<img width="418" height="106" alt="image" src="https://github.com/user-attachments/assets/b4fd5a43-fca3-464a-9092-a64de2dd8b51" />

 
EX Q: Which item has the highest correlation with the remaining items (r.drop value)? Look up this item’s content in the EPQ questionnaire on Moodle.

*EPQtetr <- tetrachoric(EPQ)* -to compute the tetrachoric correlations for the EPQ items

*alpha(EPQtetr$rho)*  - the function the correlations rather than the raw scores, no statistics for the “test score” can be computed and you cannot specify the type of score using cumulative option 

<img width="452" height="160" alt="image" src="https://github.com/user-attachments/assets/b1fb9ba0-56c2-4347-b724-ba9f5d945977" />


EX Q: What is the tetrachoric-based alpha? 

# Computing the Standard Error of measurement for the total score

SEm(y) = SD(y)*sqrt(1-alpha) 

↳ (refer. describe(N_score);5.53)*sqrt(1-0.93)

Or { SEm <- sd(N_score)*sqrt(1-0.93) } 

<img width="452" height="196" alt="image" src="https://github.com/user-attachments/assets/b0584222-fed5-4636-b22e-7599ffa04452" />

 
# Computing the Confidence Interval around a score

N_score[1]-2*SEm

N_score[1]+2*SEm

 
# < Testing homogeneity of a psychometric scale>

# package install
library(psych) 
# read data

load("SDQ.RData") 

# selecting variables 

items_conduct <- c("tantrum","obeys","fights","lies","steals")

# full correlation matrix

lowerCor(SDQ[items_conduct])  

<img width="408" height="118" alt="image" src="https://github.com/user-attachments/assets/7ea4d2ce-21a8-4aa6-90ca-e01c4edf012f" />

# Kaiser-Meyer-Olkin (KMO) index – the measure of sampling adequacy (MSA)

KMO(SDQ[items_conduct])

<img width="346" height="123" alt="image" src="https://github.com/user-attachments/assets/2ffb12b7-5bcd-48cc-a183-53a9a92eee86" />
<img width="452" height="190" alt="image" src="https://github.com/user-attachments/assets/dbde6e6a-fd4f-4557-949a-40bbf19188f9" />

  
# Parallel Analysis Scree

fa.parallel(SDQ[items_conduct], fa="pc")	
 
<img width="452" height="42" alt="image" src="https://github.com/user-attachments/assets/fc5a247a-2862-4d74-81b0-934ad9fa00ab" />

 <img width="452" height="401" alt="image" src="https://github.com/user-attachments/assets/ebd886c2-1023-41b1-ad87-ac6ada0930a5" />

 <img width="452" height="177" alt="image" src="https://github.com/user-attachments/assets/081da4e8-19b9-4dc1-8a9a-599a266b3c26" />

# Fitting and interpreting a single-factor model

>> fa(SDQ[items_conduct],nfactors=1) 

EX Q: 

- Examine the Standardised factor loadings. How do you interpret them? What is the “marker item” for the Conduct Problems scale? [In the “Standardized loadings” output, the loadings are printed in “MR1” column. “MR” stands for the estimation method, “Minimum Residuals”, and “1” stands for the factor number. Here we have only 1 factor, so only one column.]
  
-Examine communalities and uniquenesses (look at “h2” and “u2” values in the table of “Standardized loadings”, respectively). What is communality and uniqueness and how do you interpret them?

A: between 20% and 51% of variance in the items is due to the common factor; communality is the proportion of variance in the item due to the factor, and uniqueness is the remaining proportion (1-communality).

- What is the proportion of variance explained by the factor in the overall set of five items (total variance explained)? To answer this question, look for “Proportion Var” entry in the output (in a small table beginning with “SS loadings”).

   <img width="1282" height="560" alt="Screenshot 2026-05-12 at 10 07 42 pm" src="https://github.com/user-attachments/assets/f15e051b-094f-4ecc-b0e4-6f9d8444ea9c" />

<img width="452" height="248" alt="image" src="https://github.com/user-attachments/assets/3f0b03d6-daad-4c6c-8d2b-23851f18956d" />

-Is the chi-square for the tested model significant? Do you accept or reject the single-factor model? [Look for “Likelihood Chi Square” in the output.]  

<img width="452" height="171" alt="image" src="https://github.com/user-attachments/assets/82eee3ce-5cb9-4a0a-9450-ed8700495942" />


<img width="452" height="246" alt="image" src="https://github.com/user-attachments/assets/e6f835da-5c64-4fe7-a06a-72ce16edc104" />


## The hypothesis cannot be rejected{=accept} (prob > 0.05); the scale is homogeneous


# Residuals 

F_conduct <- fa(SDQ[items_conduct], nfactors=1)

# without removing diagonal

residuals.psych(F_conduct)  
<img width="375" height="123" alt="image" src="https://github.com/user-attachments/assets/fcedaf0c-3ca1-44b9-a038-b67f31510506" />

# removing diagonal

residuals.psych(F_conduct, diag=FALSE)

 <img width="363" height="123" alt="image" src="https://github.com/user-attachments/assets/6234558d-1cf4-4abe-8fe8-58691f837116" />

-Standards are the same as correlation; therefore, consider r < 0.3: small, r < 0.5: medium, r < 0.7: large. Consider that the error rate is high, if exceeding 0.3 or closer to that number

# reverse coding

* Obey the negative sign in the correlation matrix, need to reverse coding

>> R_conduct <- reverse.code(c(1,-1,1,1,1), SDQ[items_conduct])
>> 
>>alpha(R_conduct)

<img width="452" height="160" alt="image" src="https://github.com/user-attachments/assets/1db2d441-49dc-4333-9948-5304db5f8bcf" />

 
# install package

library(GPArotation) 

# omega total

>> omega(R_conduct, nfactors=1)
 
 <img width="452" height="169" alt="image" src="https://github.com/user-attachments/assets/671e32db-a433-4bc2-8b5a-c8ab18f25a8d" />

# <Exploratory Factor Analysis of personality test scores>

# package install

library(psych)

# read data

load("neo.RData") 

# measure of sampling adequacy (MSA)

>> KMO(neo)

 <img width="452" height="96" alt="image" src="https://github.com/user-attachments/assets/121acdd6-2373-4bf4-b6bf-7f629c9a487c" />

# scree plots

>> fa.parallel(neo, n.obs=1000, fm="ml", fa="pc")
 
 
<img width="452" height="24" alt="image" src="https://github.com/user-attachments/assets/2a544e5e-5e1c-47ec-aa5d-379e3bf9eac5" />
<img width="452" height="291" alt="image" src="https://github.com/user-attachments/assets/73d9d318-28c7-4291-b967-1161e7399025" />


* if you don’t need the n.observation:

<img width="452" height="154" alt="image" src="https://github.com/user-attachments/assets/f6687672-a130-46ea-b036-972667a3aba2" />


# result of chi-square statistic testing the 5-factor model, Fitting an exploratory 5-factor model

## {NEED GPA rotation package}

>> fa(neo, nfactors=5, n.obs=1000, fm="ml")

↳ nfactors : neo have 5 factors in their survey script 


QUESTION: Find the result of the chi-square statistic testing the 5-factor model (look for “Likelihood Chi Square”). How many degrees of freedom are there? What is the chi square statistic, and p value, for the tested model? Would you retain or reject this model based on the chi-square test? Why?


<img width="452" height="82" alt="image" src="https://github.com/user-attachments/assets/5423575f-877c-4244-ae8d-75d2ac403375" />

 
Chi-square=1443.45 on DF=295 (p=1.8E-150). {reject}


# model residuals, evaluate the root mean square of the residuals (RMSR), which is a summary of all residuals

<img width="452" height="54" alt="image" src="https://github.com/user-attachments/assets/a6fe7da8-e776-485f-81f2-842f623785c1" />
 
∴ The RMSR of 0.03 is a very small value, indicating that the 5-factor model reproduces the observed correlations well.


# to get the actual residuals

>> FA_neo <- fa(neo, nfactors=5, n.obs=1000, fm="ml") 

<img width="440" height="27" alt="image" src="https://github.com/user-attachments/assets/f9e00907-67c5-4134-b3f4-9e052d177d58" />


>> residuals.psych(FA_neo)
>> residuals.psych(FA_neo, diag=FALSE)

 <img width="452" height="476" alt="image" src="https://github.com/user-attachments/assets/bc0ac4f1-1a78-438a-b50e-bddf20cf4976" />

∴ All residuals are very small (close to zero), and none are above 0.1 in absolute value. 

# Examine the standardised factor loadings (pattern matrix)

  ## Interpreting the 5-factor exploratory model_ factor loadings, unique variances and correlations between factors.
  
>> print.psych(FA_neo, cut=0.3)
>>
>> 
### QUESTION 6. Examine the standardised factor loadings (pattern matrix), and name the factors you obtained based on which facets load on them.
= ML1=Neuroticism; ML4=Conscientiousness, ML3=Agreeableness, ML2=Extraversion, ML5=Openness (see the salient loadings marked in Q7) 

- When you see Neo PI Description, ordered in neuroticisim -> extraversion -> agreeableness -> conscientiousness -> openness

<img width="452" height="134" alt="image" src="https://github.com/user-attachments/assets/68986b60-b728-45e7-99a4-d918b555dfc6" />
<img width="452" height="94" alt="image" src="https://github.com/user-attachments/assets/eab46901-1b5b-4fd9-8d83-fa42e93a844d" />



### QUESTION 7. Examine the factor loadings again, this time looking for cross-loading facets (facets with loadings greater than 0.32 on factor(s) other than its own). Refer to the NEO facet descriptions in the supplementary document to hypothesise why these cross-loadings may have occurred.

<img width="259" height="342" alt="image" src="https://github.com/user-attachments/assets/ae4be032-5078-4cb5-b345-e0b351371c79" />


 
* ML2: Extraversion and E4 is extraversion question, so when you compared {correlation between ML4 and E4}, {correlation between ML3 and E4}, and {correlation between ML2 and E4} correlation between ML2 and E4 need to be largest, but it isn’t


∴ There are several cross-loadings for facets of Agreeableness (factor ML3) and Extraversion (factor ML2) - see the loadings below. For instance, E4 (Activity), described as ‘pace of living’ loads on Extraversion as expected (0.36) but even slightly stronger on Conscientiousness (0.39) and negatively on Agreeableness (-0.38). Perhaps the need to meet deadlines and achieve (part of Conscientiousness) has an effect on the ‘pace of living’, as well as the need to ‘get ahead’ (the low end of Agreeableness).



### QUESTION 8. Examine the columns h2 and u2 of the factor loadings (pattern matrix). The h2 column is the facet’s communality (proportion of variance due to all of the common factors), and u2 is the uniqueness (proportion of variance unique to this facet). The communality and uniqueness must sum to 1. Based on communalities, which facets are the least explained by the factor model we just tested? Which are the best explained? 

<img width="452" height="439" alt="image" src="https://github.com/user-attachments/assets/1e4a9bdb-e1eb-4837-b611-0f3e073fe331" />



∴ Facets O6 (Values) and O4 (Ideas) are worst explained by the factors in this model. Their communalities (see column “h2”) are only 15% and 28% respectively. O6 Values is an unusual scale, quite different from other NEO scales. It has attitudinal rather than behavioural statements, such as “I believe letting students hear controversial speakers can only confuse and mislead them’.

Facets N3 (Depression) and C5 (Self-Discipline) are best explained by the factors in this model.



### QUESTION 9. Find and interpret the factor correlation matrix. Which factors correlate the strongest? 

<img width="298" height="140" alt="image" src="https://github.com/user-attachments/assets/2878b789-efac-4ee8-ad70-2c72ac05d91a" />


∴ Overall, the five factors correlate quite weakly, but they are not orthogonal. ML1 (Neuroticism) correlates negatively with all other factors; the rest of the factors correlate positively with each other. The strongest correlation is between ML1 (Neuroticism) and ML4 (Conscientiousness) (r=–.41).
 
# <Confirmatory Factor Analysis> 

# package install

library(psych)
library(lavaan)

# read data

load("Thurstone.RData")

# Specifying and fitting a measurement model
<img width="452" height="113" alt="image" src="https://github.com/user-attachments/assets/bfaa1cb1-8964-455f-af27-2174c7dcc444" />
<img width="403" height="133" alt="image" src="https://github.com/user-attachments/assets/5d839934-5a19-4543-ab7b-1e337cfe2831" />

<img width="880" height="168" alt="Screenshot 2026-05-12 at 10 17 59 pm" src="https://github.com/user-attachments/assets/8730fbe9-7268-4b66-a0d0-6543f46760aa" />


             
# fit the model with default scaling, and ask for summary output 

>> fit <- cfa(model=T.model, sample.cov=Thurstone, sample.nobs=215)
>> summary(fit)
>>
-factor loading, Std.Err, z-values or p-values, latent variables, parameters 


<img width="452" height="209" alt="image" src="https://github.com/user-attachments/assets/1ca5034d-6fde-4d2e-97e2-e947be77d27b" />

# Factor loading, Std.Err, z-values or p-values
  
∴ The factor loadings for s1, s4 and s7 were not actually estimated; instead, they were fixed to 1 to set the scale of the latent factors (latent factors then simply take the scale of these particular measured variables). That is why there is no usual estimation statistics reported for these. Factor loadings for the remaining 6 subtests (9-3=6) are free parameters in the model to estimate.

 <img width="452" height="359" alt="image" src="https://github.com/user-attachments/assets/9688e04e-e878-4d99-92fc-ded5f8d5dadc" />

# Latent variables
  
∴ There are 12 unobserved (latent) variables – 3 common factors (Verbal, WordFluency and Reasoning), and 9 unique factors /errors (these are labelled by the prefix ‘.’ in front of the observed variable to which this error term is attached, for example .s1, .s2, etc. It so happens that in this model, all the latent variables are exogenous (independent), and for that reason variances for them are estimated. In addition, covariances are estimated between the 3 common factors (3 covariances, one for each pair of factors). Of course, the errors are assumed uncorrelated (remember the local independence assumption in factor analysis?), and so their covariances are fixed to 0 (not estimated and not printed in the output).

<img width="452" height="130" alt="image" src="https://github.com/user-attachments/assets/47077349-af1b-4c77-b55a-340b963f4b04" />

# Parameters

∴ You can look this up in lavaan output. It says: “Number of free parameters 21”. To work out how this number is derived, you can look how many rows of values are printed in ‘Parameter Estimates’ under each category. The model estimates: 6 factor loadings (see Q1) + 3 factor variances (see Q2) + 3 factor covariances (see Q2) + 9 error variances (see Q2). That’s it. So we have 6+3+3+9=21 parameters.

* ‘Sample moments’ refers to the number of variances and covariances in our observed data
  
: m(m+1)/2 = ex: 9 observed variables, therefore there are 9(9+1)/2=45


<img width="452" height="87" alt="image" src="https://github.com/user-attachments/assets/9016bcb7-661a-412f-ae99-d872231e8822" />

 # chi-square
 
∴ Chi-square is 38.737 (df=24). We have to reject the model, because the test indicates that the probability of this factor model holding in the population is less than .05 (P = .029).

# extended output

>> summary(fit, fit.measures=TRUE)- SRMR, CFI and RMSEA.  

 <img width="452" height="72" alt="image" src="https://github.com/user-attachments/assets/ed628340-c34f-476c-8fa6-309a604276f0" />

 <img width="436" height="78" alt="image" src="https://github.com/user-attachments/assets/fd586f3e-7760-4fe7-b718-8c5a505fcbf4" />
 
<img width="420" height="138" alt="image" src="https://github.com/user-attachments/assets/a50693b8-6b44-4289-b487-5e55e360f72a" />

∴ Comparative Fit Index (CFI) = 0.986, which is larger than 0.95, indicating good fit. Root Mean Square Error of Approximation (RMSEA) = 0.053, just outside of the cut-off .05 for close fit. The 90% confidence interval for RMSEA is (0.017, 0.083), which just includes the cut-off 0.08 for adequate fit. Overall, RMSEA indicates close to adequate fit. Standardized Root Mean Square Residual (SRMR) = 0.044 is small as we would hope for a well-fitting model. All indices indicate close fit of this model, despite the significant chi-square.


# Alternative scaling of latent factors
>> fit.2 <- cfa(T.model, sample.cov=Thurstone, sample.nobs=215, std.lv=TRUE)
>> summary(fit.2)

-factor loading, factor covariances, error variances.

<img width="442" height="256" alt="image" src="https://github.com/user-attachments/assets/1976e107-fb6b-402f-afd9-d24aa67ef52b" />

 
# factor loading

∴ All factor loadings are positive as would be expected with ability variables, since ability subtests should be positive indicators of the ability domains. The SEs are low (magnitude of 1/SQRT(N), as they should be in a properly identified model). All factor loadings are significantly different from 0 (p-values are very small).
 
 <img width="441" height="150" alt="image" src="https://github.com/user-attachments/assets/e90f3f33-e2d3-4a53-aaac-c32ddc32b9ee" />


# factor covariance

∴ The factor covariances are easy to interpret in terms of size, because we set the factors’ variances =1, and therefore factor covariances are correlations. The correlations between the 3 ability domains are positive and large, as expected.

<img width="452" height="174" alt="image" src="https://github.com/user-attachments/assets/4a3e4538-37b2-40f7-8296-272b170df092" />

 
# error variance

∴ The error variances are certainly quite small – considering that the observed variables had variance 1 (remember, we analysed the correlation matrix, with 1 on the diagonal?), the error variance is less than half that for most subtests. The remaining proportion of variance is due to the common factors. For example, for s1, error variance is 0.18 and this means 18% of variance is due to error and the remaining 82% (1-0.18) is due to the common factors.


# standised solution (in which EVERYTHING is standardised - the latent and observed variables)

>> summary(fit.2, standardized=TRUE)


- factor loading, covariance, error variance

# Examining residuals and local areas of misfit

>> fitted(fit.2)

>> residuals(fit.2)


# standised residuals

>> residuals(fit.2, type="standardized")

# modification indices

>> modindices(fit.2)


# <Path analysis>
  
# read data

load("Wellbeing.RData")

# package install

library(lavaan)

# Specifying and fitting the model
 <img width="403" height="133" alt="image" src="https://github.com/user-attachments/assets/bc1c792f-b3dd-4792-8330-d643a3082ca8" />

>> W.model <- '
>> # regressions
   WA ~ PS + DH
   CT ~ PS + DH
   SWB ~ WA + CT
>> # covariance of IVs
   PS ~~ DH
>> # residual covariance of DVs
   WA ~~ CT '

   <img width="496" height="474" alt="Screenshot 2026-05-12 at 10 23 56 pm" src="https://github.com/user-attachments/assets/e19f8163-aa8c-4657-9fa2-d824c4416956" />

#  Number of model parameters  

>> sem(W.model, sample.cov=Wellbeing, sample.nobs=149)

- number of free parameters(number of model parameters)

<img width="452" height="224" alt="image" src="https://github.com/user-attachments/assets/c46ac114-1948-4ec3-bc86-36a5044c7970" />

fit <- sem(W.model, sample.cov=Wellbeing, sample.nobs=149)

summary(fit, fit.measures=TRUE) 

- regressions, covariances, variances

<img width="452" height="204" alt="image" src="https://github.com/user-attachments/assets/a946ccdd-e2e5-40ec-af73-264e1baf2a36" />

 
## QUESTION 3. Interpret the chi-square. Do you retain or reject the model?

∴ The chi-square test (Chi-square = 10.682, Degrees of freedom = 2, P-value = .005) suggests rejecting the model because the test is significant (p-value is very low). In this case, we cannot “blame” the poor chi-square result on the large sample size (our sample is not that large).

# residuals covariance

>> residuals(fit)

<img width="335" height="196" alt="image" src="https://github.com/user-attachments/assets/f6605cf0-c327-4cc1-b428-4718ce494703" />

 
>> residuals(fit, type="standardized")

<img width="396" height="194" alt="image" src="https://github.com/user-attachments/assets/0bcd6e09-6bc9-4a8d-83a8-b0a0760e8319" />

 
* (We usually interpret a correlation of 0.1 as small; and correlations below 0.1 trivial. Use the same logic for interpreting the residual correlations.) The residuals for these omitted paths are small in magnitude (just under 0.1), but one borderline residual PS/SWB (=0.096) is significantly different from zero (stdz value = 2.051 is larger than the critical value 1.96).



# Computing indirect and total effects

 <img width="452" height="186" alt="image" src="https://github.com/user-attachments/assets/71c207ea-0366-4c06-82cb-1e74cc593095" />


>> W.model.label <- '
>> # regressions - now with parameter labels assigned
   WA ~ a1*PS + DH
   CT ~ a2*PS + DH
   SWB ~ b1*WA + b2*CT
   # covariance of IVs (same as before)
   PS ~~ DH
   # residual covariance of DVs (same as before)
  WA ~~ CT 
  # Here we describe new indirect effects
   ind.WA := a1*b1    # indirect via WA
   ind.CT := a2*b2    # indirect via CT
   ind.total := ind.WA + ind.CT 
   '
>> sem(W.model.label, sample.cov=Wellbeing, sample.nobs=149)
>> fit2 <- sem(W.model.label, sample.cov=Wellbeing, sample.nobs=149)
>> summary(fit2, fit.measures=TRUE)


  <img width="1294" height="896" alt="Screenshot 2026-05-12 at 10 27 45 pm" src="https://github.com/user-attachments/assets/94bdb084-ddf2-486a-baa2-89c4c3053e93" />
<img width="452" height="195" alt="image" src="https://github.com/user-attachments/assets/b2c8df09-47c4-47a3-bea6-17e6749a6ae6" />
<img width="407" height="109" alt="image" src="https://github.com/user-attachments/assets/48f7ac17-3cbe-41f0-bfb2-7af192b48208" />

QUESTION 7. What is the indirect effect of PS on SWB via WA? What is the indirect effect of PS on SWB via CT? What is the total indirect effect of PS on SWB (the sum of the indirect paths via WA and CT)? How do the numbers correspond to the observed covariance of PS and SWB?
The total indirect effect of PS on SWB is –.216. Let’s see how it is computed. Look at the regression weights in the answer to Q5. The route from PS to SWB via WA: (–0.339)0.328=–0.111. The route from PS to SWB via CT: (–0.191)0.550=–0.105. Adding these two routes, we get the indirect effect = –0.216. This shows you how to compute the effects from given parameter values by hand, but we obtained the same answers through parameter labels.

<Structural models for repeated measures>

#Creating project and examining data

#reading data
SDQ <- read.csv(file="SDQ_repeated.csv")
library(psych)
describe(SDQ)  - full descriptive statistics for all variables
library(lavaan)
#Fitting a basic structural model for repeated measures


Model0 <- '
# Time 1 measurement model
   External1 =~ p1_conduct + p1_hyper + p1_prosoc
# Time 2 measurement model
   External2 =~ p2_conduct + p2_hyper + p2_prosoc
# Structural model
   External2 ~ External1 '

fit0 <- sem(model = Model0, data = SDQ, meanstructure=TRUE)

# ask for summary output including fit indices
summary(fit0, fit.measures=TRUE) -chi-square test, SRMR, CFI and RMSE)
    
#modification indices
modindices(fit0)  
EX Q: What do the modification indices tell you? Which two changes in the model would produce the greatest decrease in the chi-square? How do you interpret these model changes?
A: Two largest modification indices (MI) by far can be found in the covariance ~~ statements: p1_hyper~~p2_hyper (mi=248.422) and p1_prosoc~~p2_prosoc (mi=156.286).
The first MI tells you that if you repeat the analysis allowing p1_hyper and p2_hyper correlate (actually, because these are DVs, the correlation will be between their errors/unique factors), the chi square will fall by about 248. But is this reasonable to allow errors/unique factors for the same measures at Time 1 and Time 2 correlate? Consider how the variance on the Hyperactivity facet is explained by both, the common Externalising factor, and the remaining unique content of the facet (the unique factor). Because the same Hyperactivity scale was administered on two different occasions, its unique content not explained by the common Externalising factor would be still shared between the occasions. Therefore, the unique factors at Time 1 and Time 2 cannot be considered independent. The correlated errors will correct for this lack of local independence. Similarly, we should allow correlated errors across time for the Pro-social construct (p1_prosoc and p2_prosoc). A correlated error for p1_conduct and p2_conduct is not needed since M.I. did not suggest it.

#modify the model allowing the unique factors (errors) of p1_hyper and p2_hyper, and errors of p1_prosoc and p2_prosoc correlate.

Model1 <- '
# Time 1 measurement model
   External1 =~ p1_conduct + p1_hyper + p1_prosoc
# Time 2 measurement model
   External2 =~ p2_conduct + p2_hyper + p2_prosoc
# Structural model
   External2 ~ External1 
   
# MODIFIED PART:  correlated errors for repeated measures
   p1_hyper ~~ p2_hyper
   p1_prosoc ~~ p2_prosoc '

fit1 <- sem(model = Model1, data = SDQ, meanstructure=TRUE)
summary(fit1)
Q; chi-square for the model with correlated errors for repeated measures (Model1). 
# Fitting a full measurement invariance model for repeated measures

Model2 <- '
# Time 1 measurement model with labels
    External1 =~ p1_conduct + lh*p1_hyper + lp*p1_prosoc
# error variances
    p1_conduct ~~ ec*p1_conduct
    p1_hyper ~~ eh*p1_hyper
    p1_prosoc ~~ ep*p1_prosoc
# intercepts
    p1_conduct ~ ic*1
    p1_hyper ~ ih*1
    p1_prosoc ~ ip*1

# Time 2 measurement model with labels
    External2 =~ p2_conduct + lh*p2_hyper + lp*p2_prosoc
# error variances
    p2_conduct ~~ ec*p2_conduct
    p2_hyper ~~ eh*p2_hyper
    p2_prosoc ~~ ep*p2_prosoc
# intercepts
    p2_conduct ~ ic*1
    p2_hyper ~ ih*1
    p2_prosoc ~ ip*1 

# Structural model
    External2 ~ External1

#correlated errors for repeated measures
    p1_hyper ~~ p2_hyper
    p1_prosoc ~~ p2_prosoc '
fit2 <- sem(model = Model2, data = SDQ, meanstructure=TRUE)
summary(fit2, fit.measures=TRUE) -chi-square test, SRMR, CFI and RMSE)
 
modindices(fit2) 
=> 24, 25

#Carry out the chi-square difference test to compare nested models Model2 and Model3. Report the chi-square difference statistic here as a number. 

HINT. Use function anova(fit2,fit3) as explained in the lecture.

  
<Fitting measurement models to multiple groups>
#Creating project and examining data
#reading data
library(lavaan)
library(psych)
data(HolzingerSwineford1939): A new object HolzingerSwineford1939 should appear in your Environment tab
sample <- HolzingerSwineford1939[HolzingerSwineford1939$school=="Grant-White", ] : a new object called sample with only children from school Grant-White included
# give value labels for sex variable
sample$sex <- factor(sample$sex,
                    levels = c(1,2),
                    labels = c("boy", "girl"))  
# descriptives by sex
describeBy(sample, group="sex"): Descriptive statistics by group

Ex QUESTION 1. Examine the means of the six test variables for boys and girls. Note the mean differences for x3 (spatial orientation), and all verbal tests (x4-x6). Who score higher on what tests?
: Boys scored higher than girls on x3, but girls scored higher than boys on all verbal tests (x4, x5 and x6).
  
# Fitting a baseline measurement model to two subgroups (boys and girls)

# Describe the measurement (confirmatory factor analysis, or CFA) model
HS.model <- ' Spatial =~ x1 + x2 + x3
              Verbal =~ x4 + x5 + x6 '
# Fitting Baseline (Configural) model
fit.b <- cfa(HS.model, data = sample, group = "sex")
summary(fit.b, fit.measures=TRUE): chi-square, df, p-value, CFI, RMSEA,SRMR

QUESTION 2. How many sample moments are there in the data? Why? {Hint. When counting sample moments, do not forget that we split the data into 2 groups, so observed means, variances and covariances are available for both groups}.
 = There are 6 observed variables, therefore 6 means, plus 6(6+1)/2=21 variances and covariances; 27 moments in total for each group. So we have 27*2=54 sample moments in both groups.

QUESTION 3. How many parameters does the baseline (configural) model estimate? What are they? {Hint. You can look up the total number of parameters in the output, but try to work out how these are made up. The output will help you, if you look in ‘Parameter Estimates’. Remember that values printed there are parameters.}
Baseline model estimates 38 parameters in total. Boys and girls groups estimate the same parameters (i.e. there are 19 parameters in each group)
 
QUESTION 4. Interpret the chi-square, and SRMR. Do we retain or reject the baseline model?
Chi-square for the baseline model is insignificant (chisq = 16.710; Degrees of freedom = 16; p = .405). The SRMR is 0.040 – nice and small.

# Fitting a full measurement invariance model to subgroups
The baseline model does not allow us to compare the Spatial and Verbal factor scores between boys and girls, because each group has its own metric for these factors.

# Fitting Measurement Invariance model
fit.mi <- cfa(HS.model, data = sample, group = "sex",
           group.equal = c("loadings", "intercepts", "residuals"))
summary(fit.mi, fit.measures=TRUE): chi-square, df, p-value, CFI, RMSEA,SRMR
-> What you have just done is fitted a full measurement invariance model. The model tests the following combined hypothesis:
H1. The measure is fully invariant across groups. Factor loadings, intercepts and error variances for corresponding indicators are equal.
QUESTION 5. Interpret the chi-square and SRMR. Do we retain or reject the full measurement invariance model?
= Chi-square for the measurement invariance model is again insignificant (chisq = 27.482, Degrees of freedom = 30, P-value = 0.598). The SRMR is 0.058 – small again. The almost equal chi-square values for both groups (boy chisq = 13.693, girl chisq = 13.789) indicate that the measurement invariance model is equally appropriate for boys and girls.

  
QUESTION 6. How many parameters does the measurement invariance model estimate? What are they? {Hint. Again, look up the total number of parameters in the output, and then try to work out how these are made up. The ‘Parameter Estimates’ output and the above explanation will help you.}
= The output says that ‘Number of free parameters’ is 40, and ‘Number of equality constraints’ is 16. This means that 40-16=24 unique parameters are estimated 

# Testing Equality of means of latent factors : All you need to do is to add one more group equality constraint, for latent variable "means"

fit.mi.e <- cfa(HS.model, data = sample, group = "sex",
   group.equal = c("loadings", "intercepts", "residuals", "means"))

summary(fit.mi.e, fit.measures=TRUE)
EX Q: Now fit the HS.model separately to boys and girls of Pasteur school, imposing equality constraints on the factor loadings only (i.e. fit a Metric invariance model).  
What is the chi-square statistic for the boy subgroup? Report it here.
The correct answer is: 18.081
 

# Because the two models are nested (one is a special case of the other), you can conduct the chi-square difference test using the R base function anova(), which will compute the difference of the models’ chi-square statistics and the difference of their degrees of freedom, and print out the resulting p-value.
anova(fit.mi, fit.mi.e)

QUESTION 8. Conduct the chi-square difference test of models with and without the equality constraints as described above, and interpret the results. Are the models significantly different? Which model will you retain?
The model with additional constraints (fit.mi.e) has the Chi-square = 35.786; Degrees of freedom = 32. Testing the difference between this model and the previous model (fit.mi), we obtain Diff(Chi-square) = 35.786–27.482= 8.304 and Diff(DF) = 32–30 = 2.
Chi-square of 8.304 on 2 degrees of freedom is significant at the 0.05 level, with the p-value=0.016. Restricting the model with additional equality constraints resulted in significantly different (worse) fit. The fit is worse is because the chi-square is greater (and constraining some free parameters cannot make the fit better!). We conclude that the means for boys and girls on the Spatial and Verbal tests are significantly different, and that our measurement invariance model with free means is better than the model with means constrained equal.
You may wonder how the fit can be ‘significantly worse’ if it is still very good according to the chi-square test (the SRMR, not being a ‘significance’ measure but an ‘effect size’ measure picked up the worsening fit). Here the small sample works against us – there is not enough power to reject the ‘wrong’ model (it has too many parameters), but just enough power to detect the elements of the model that make a difference.
 

<Logistic regression – application to DIF analysis>

#Data set - preliminary examination
EPQ <- read.delim(file="EPQ_N_demo.txt", header=TRUE)
#Screening EPQ Neuroticism items for gender DIF
#Creating the trait (matching) variable, and the grouping variable
Compute the Neuroticism trait score (call it Nscore), and append it to the dataset as a new variable
EPQ$Nscore <- rowMeans(EPQ[ ,4:26], na.rm=TRUE)*23 -item responses are located in columns 4 to 26
#The variable sex is coded as 0 = female; 1 = male. ATTENTION: this means that “male” is the focal group
EPQ$sex <- factor(EPQ$sex,
                  levels = c(0,1),
                  labels = c("female", "male"))
library(psych)
describeBy(EPQ, group="sex")-Descriptive statistics by group
EX Q: Who has the higher proportion of endorsing item N_19 – males or females? (Hint. Remember that for binary items coded 0/1, the item mean is also the proportion of endorsement.) Who score higher on the Neuroticism scale (Nscore) on average – males or females?
Interpret the means for N_19 in the light of the Nscore means.

Females endorse item N_19 more frequently (0.70 or 70% of them endorse it) than males (0.36 or 36%). Females also have higher Nscore (mean=13.30) than males (mean=10.16). Knowing this, the differences in the item endorsement rates are actually expected, as they may be explained by the difference in Neuroticism levels. The question is whether the differences in responses are fully explained by the trait level.

  
  

#Specifying logistic regression models

# Baseline model 
Baseline <- glm(N_19 ~ Nscore, data = EPQ, family = binomial(link="logit"))
# Uniform DIF model 
dif.U <- glm(N_19 ~ Nscore + sex, data = EPQ, family = binomial(link="logit"))
# Non-Uniform DIF model
dif.NU <- glm(N_19 ~ Nscore + sex + Nscore:sex, data = EPQ, family = binomial(link="logit"))
#Testing for significance of uniform and non-uniform effects of sex

anova(dif.NU, test= "Chisq")
 

QUESTION 2. Is the Baseline model (with Nscore as the only predictor) significant? Try to report the chi-square statistic for this model using the template below: Baseline – NULL: diff.chi-square (df= __ , N=__ ) = _______, p = _______.
; The Baseline model predicts the item response significantly (as we would expect); chi-square (1, N = 1377)=622.32, p < .001.

QUESTION 3. Does sex add significantly over and above Nscore? What is the increment in chi-square compared to the Baseline model? What does this mean in terms of testing for Uniform DIF? dif.U – Baseline: diff.chi-square (df= __ , N=__ ) = _______, p = _______.
: Sex adds significantly to prediction. The increment is diff.chi-square (1, N = 1377) =57.42, p < .001. This means that Uniform DIF might be present (to judge its effect size, we will need to look at the Nagelkerke R2).

QUESTION 4. Does Nscore by sex interaction add significantly over and above Nscore and sex? What is the increment in chi-square compared to the dif.U model? What does this mean in terms of testing for Non-Uniform DIF? dif.NU – dif.U: diff.chi-square (df= __ , N=__ ) = _______, p = _______.
: Nscore by sex interaction does not add significantly to prediction. The increment diff.chi-square (1, N = 1377) =1.21, p = .272. It means that there is no Non-Uniform DIF, regardless of the effect size.

EXQ: 
The first, baseline model, will include the total Nscore as the only predictor of N_80. The second, uniform DIF model, will include the total Nscore and participants' sex as predictors. [We will NOT test for non-uniform DIF]. 

Does sex add significantly over and above Nscore? What is the chi-square increment compared to the baseline model? Report it here.
 

#Evaluating effect sizes for uniform and non-uniform effects of sex - use package fmsb

NagelkerkeR2(Baseline)
NagelkerkeR2(dif.U)
NagelkerkeR2(dif.NU)
Baseline: Nagelkerke R2 = 0.4888; dif.U: Nagelkerke R2 = 0.5237; dif.NU: Nagelkerke R2 = 0.5244

# compare model dif.U against Baseline - Uniform DIF effect size
NagelkerkeR2(dif.U)$R2 - NagelkerkeR2(Baseline)$R2
# compare model dif.NU against dif.U - Non-Uniform DIF effect size
NagelkerkeR2(dif.NU)$R2 - NagelkerkeR2(dif.U)$R2
 
Decision Rule:
Large DIF: Chi-square significant and Nagelkerke R2 change ≥ 0.07
Moderate DIF: Chi-square significant and Nagelkerke R2 change between 0.035 and 0.07
Negligible DIF: Chi-square insignificant or Nagelkerke R2 change < 0.035

: Nagelkerke R2 increment from Baseline model to dif.U model is 0.035. According to the DIF classification rules, this just qualifies for moderate DIF (because the effect was significant – see Q3, and the effect size is exactly at the cut-off for moderate DIF).
Nagelkerke R2 increment from dif.U model to dif.NU model is 0.0007. According to the DIF classification rules, there is no DIF (i.e. DIF is negligible), because the effect was insignificant – see Q4, and the effect size is tiny.

#Describing the effects: regression coefficients
obtain the regression coefficients of the final model : 
summary(dif.NU)
# coefficients in logistic regression are on the log-odds scale and therefore they are not interpreted. Instead, request exp(B) and interpret them as odds ratios.
exp(coef(dif.NU))
 
QUESTION 7. Write sentences describing the odds ratios, in terms of change in the DV accompanying increases in the IV. Report significant effects only. Use the below templates.:
A one-point increase in Nscore was associated with a _______ times _____________________(increase or decrease) in the odds of endorsing item N_19. Male sex was associated with a _______ times ________________(increase or decrease) in the odds of endorsing item N_19.
A one-point increase in Nscore was associated with a 1.359 times increase in the odds of endorsing the item. Male sex was associated with a 0.207 times decrease in the odds of endorsing the item. [NOTE that values above 1 are associated with an increase, and below 1 with a decrease in odds].

QUESTION 8. Finally, try to interpret any moderate or large DIF effects that you found (ignore negligible DIF). Who have higher expected probabilities of endorsing item N_19 – males or females? Can you interpret / explain this finding substantively?
We found moderate Uniform DIF for item N_19. We also found that females have higher odds of endorsing the item given the same Nscore as males (because males have lower odds – see Q7). It appears that females admit to their “feelings being easily hurt” (see text of N_19) easier than males with the same Neuroticism level. This might be because expressing their feeling is more socially acceptable for females.
<Item response modelling of binary test items>
N_data <- EPQ[ ,4:26]
library(ltm)
#Fit a 1-parameter logistic (1PL or Rasch) model
fit1PL <- rasch(N_data)
summary(fit1PL)
coef(fit1PL)    # parameters in convenient format
* You will see the difficulty and discrimination parameters. In 1-parameter and 2-parameter models, difficulty refers to the latent trait score where the probability of ‘YES’ response equals the probability of ‘NO’ response (both P=0.5). Discrimination refers to the steepness (slope) of the probability function (item characteristic curve) at the item difficulty.
EX QUESTION 1. Examine the 1PL difficulty parameters. Do the difficulty parameters vary widely? What is the ‘easiest’ item in this set? What is the most ‘difficult’ item? Examine the phrasing of the corresponding items (refer to the item list on Moodle) – can you see why one item is easier to agree with than the other?
The difficulty parameters of Neuroticism items vary widely. The ‘easiest’ item to endorse is N_88, with the lowest difficulty value (-2.03). N_88 is phrased “Are you touchy about some things?”, and according to the 1PL model, at very low neuroticism level z=–2.03 (remember, the trait score is scaled like z-score), the probability of agreeing with this item is already 0.5. The most ‘difficult’ item to endorse in this set is N_62, with the highest difficulty value (0.97). N_62 is phrased “Do you often feel life is very dull?”, and according to this model, one need to have neuroticism level of at least 0.97 to endorse this item with probability 0.5. The phrasing of this item is indeed more extreme than that of item N_88, and it is therefore more ‘difficult’ to endorse.
 

EX QUESTION 2. Examine the 1PL discrimination parameters. Why is the discrimination parameter the same for the whole set of 23 items?
: Only one discrimination parameter is printed for this set because the 1PL (Rasch) model assumes that all items have equal discriminations. Therefore the model constrains all discriminations to be equal.

plot(fit2PL)
 
#Fit a 2-parameter logistic model

fit2PL <- ltm(N_data ~ z1)
-> it specifies that items in the set N_data are ‘regressed on’ one latent trait (z1). Note that z1 is not an arbitrary name; it is actually fixed in the package. At most, two latent traits can be fitted (z1 + z2). We are only fitting one trait and therefore we specify ~ z1.

summary(fit2PL)
coef(fit2PL)    # parameters in convenient format
EX QUESTION 3. Examine the 2PL difficulty parameters. What is the ‘easiest’ item in this set? What is the most ‘difficult’ item? Are these the same as in the 1PL model? Examine the phrasing of the corresponding items – can you see why one item is much easier to agree with than the other?
: The ‘easiest’ item to endorse in this set is still item N_88, which now has the difficulty value -2.58. The most ‘difficult’ item to endorse in this set is now item N_54, with the difficulty value (1.09). The most difficult item from the 1PL model, N_62, has a similarly high difficulty (1.06). N_54 is phrased “Do you suffer from sleeplessness?”, and according to this model, one needs to have neuroticism level of at least 1.09 to endorse this item with probability 0.5.
 

EX QUESTION 4. Examine the 2PL discrimination parameters. What is the most and least discriminating item in this set? Examine the phrasing of the corresponding items – can you interpret the meaning of the construct we are measuring in relation to the most discriminating item (equivalent to “marker” item in factor analysis)?
: The most discriminating item in this set is N_34 (Dscrmn.=2.33). This item reads “Are you a worrier?”, which seems to be right at the heart of the Neuroticism construct. This is the item which would have the highest factor loading in factor analysis of these data. The least discriminating item is N_47 (Dscrmn.=0.71), reading “Do you worry about your health?”. According to this model, the item is more marginal to the general Neuroticism construct (perhaps it tackles a specific sub-domain of neuroticism).


plot(fit2PL)-> the curves should cross.

#Compare 1PL and 2PL models

anova(fit1PL, fit2PL)
 

EX QUESTION 6. Examine the results of anova() function. “LRT” value is the likelihood ratio test result (which is the chi-square). What are the degrees of freedom? Can you explain why the degrees of freedom as they are? Is the difference between the two models significant? Which model would you retain? (Use the same logic as we used in SEM for judging which model to retain).
: The degrees of freedom = 22. This is made up by the difference in the number of item parameters estimated. The Rasch model estimated 23 difficulty parameters, and only 1 discrimination parameter (one for all items). The 2PL model estimated 23 difficulty parameters, and 23 discrimination parameters. The difference between the two models = 22 parameters. The chi-square value 346.06 on 22 degrees of freedom is highly significant, so the 2PL model fits the data much better and we have to prefer it to the more parsimonious but worse fitting 1PL model.

#Estimate Neuroticism trait scores for people
Scores <- factor.scores(fit2PL, method="EB", resp.patterns=N_data)
* Check out what components are stored in this object by calling head(Scores). It appears that the estimated trait scores (z1) and their standard errors (se.z1) are stored in $score.dat part of the Scores object.
Nscore <- Scores$score.dat$z1
Nse <- Scores$score.dat$se.z1

EX Q: Using function factor.scores() and the Empirical Bayes (EB) method, produce IRT scores for all participants in the Mobility survey. 

What is the estimated z score for participant #2? Enter it here (3 decimal places will be enough).

EX Q: What is the estimated Standard Error of the z score for participant #2? Enter it here (3 decimal places will be enough).


 



+) you can plot the histogram of the estimated IRT scores, by calling hist(Nscore).

Nsum <- rowMeans(N_data, na.rm=TRUE)*23
plot(Nscore, Nsum)
 

#Evaluate the Standard Errors of measurement


plot the IRT estimated scores against their standard errors:
plot(Nscore, Nse)
 
QUESTION 7. Examine the graph. What range of the Neuroticism trait score is measured with most precision? What are the smallest and the largest Standard Errors on this graph, approximately?
[Hint. You can also get the exact values by calling min(Nse) and max(Nse).]
: Most precise measurement is observed in the range between about z=-0.2 and z=0. The smallest standard error was about 0.3 (exact value 0.299). The largest standard error was about 0.57 (exact value 0.573).



<img width="470" height="629" alt="image" src="https://github.com/user-attachments/assets/ea7a780c-d955-4cf8-b3ef-4bcbedc91765" />
