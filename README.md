# R-studio

## <Likert scale>

### package install

>> library(psych) 

### read data

>> load("SDQ.RData") 

### selecting variables

>> items_emotion<-c("somatic","worries","unhappy","clingy","afraid") 

### Computing test score

* ( SDQ = data file name) / computes the sum of specified variables for each row
  
>> rowSums(SDQ[items_emotion])

* (removing NA data (missing data) )

>> rowSums(SDQ[items_emotion], na.rm=TRUE) 


* ( 5: likert scale number)

>> rowMeans(SDQ[items_emotion], na.rm=TRUE)*5 

- set the name of removed missing data

>> SDQ$S_emotion <- rowMeans(SDQ[items_emotion], na.rm=TRUE)*5

- histogram 

>> hist(SDQ$S_emotion) 


<img width="452" height="335" alt="image" src="https://github.com/user-attachments/assets/bdf9792c-3eac-400b-8fa8-ad68f3a4e84e" />


- mean, sd, median (min max range skew kurtosis)

>> describe(SDQ$S_emotion)

<img width="452" height="216" alt="image" src="https://github.com/user-attachments/assets/a1092f66-a02a-44e3-9e72-4127b994ef67" />


### Norm referencing

#### FIRST!!

Check the cutoff: 

EX: 

Normal: 0-5

Borderline: 6

Abnormal: 7-10

>> table(SDQ$S_emotion<=5) 

* note. (<= :  ≤ / >= : ≥ / == : = )


<img width="452" height="302" alt="image" src="https://github.com/user-attachments/assets/fcf9c12f-6b3f-4383-b614-d70a3978003d" />

<img width="452" height="273" alt="image" src="https://github.com/user-attachments/assets/c4c25ebc-25ef-4072-993b-c72894cdda63" />



 
# <Classical test theory: Classical Test Theory analysis of a scale compiled from binary items>

### package install

>> library(psych)

### import the data into a new object (data frame) called EPQ

>> EPQ <- read.delim(file="EPQ_N.dat")

### To see the mean, median, SD …

>> describe(EPQ)

### compute the product -moment (Pearson) correlations

>> lowerCor(EPQ)

### missing values will be treated in a pairwise fashion

>> lowerCor(EPQ, use="pairwise") 

### tetrachoric correlations; These would be more appropriate for binary items on which a NO/YES dichotomy was forced

>> tetrachoric(EPQ)

### compute the average score from non-missing item responses (removing ‘NA’ values from calculation, na.rm=TRUE / 23 (the number of items in the Neuroticism scale)  

N_score <- rowMeans(EPQ, na.rm=TRUE)*23 

<img width="452" height="317" alt="image" src="https://github.com/user-attachments/assets/819cf7c9-d995-434a-b561-b18627eda908" />

<img width="452" height="100" alt="image" src="https://github.com/user-attachments/assets/68c4125d-6770-4045-ab35-79940e483ae3" />

<img width="452" height="119" alt="image" src="https://github.com/user-attachments/assets/4308f18f-7524-475f-b045-124804e7d9d5" />

###  mean, median, SD …  

 >> describe(N_score)


<img width="1274" height="280" alt="Screenshot 2026-05-13 at 1 37 02 pm" src="https://github.com/user-attachments/assets/7e16f49c-100f-45b9-b374-5c62b0e0df75" />

### histogram

>> hist(N_score) 

# Internal consistency reliability

### “internal consistency reliability” (Cronbach’s alpha) of the total score (average score)

>> alpha(EPQ)

<img width="1288" height="106" alt="Screenshot 2026-05-13 at 1 37 54 pm" src="https://github.com/user-attachments/assets/b31825e5-4fb2-4baa-944b-ce91921afc5d" />

<img width="452" height="159" alt="image" src="https://github.com/user-attachments/assets/e1af1295-d1bd-41bb-ba96-febcf265f068" />

### To obtain the mean and SD for *the sum score* 

>> alpha(EPQ, cumulative=TRUE) 

<img width="1084" height="290" alt="Screenshot 2026-05-13 at 1 38 42 pm" src="https://github.com/user-attachments/assets/90d87126-9bb5-40fc-9d4b-ecd1ece5729c" />


### EX Q: Which item has the highest correlation with the remaining items (r.drop value)? Look up this item’s content in the EPQ questionnaire on Moodle.

#### To compute the tetrachoric correlations for the EPQ items

>> EPQtetr <- tetrachoric(EPQ)

#### The function of the correlations rather than the raw scores, no statistics for the “test score” can be computed, and you cannot specify the type of score using the cumulative option 

>> alpha(EPQtetr$rho)

<img width="1182" height="452" alt="Screenshot 2026-05-13 at 1 40 13 pm" src="https://github.com/user-attachments/assets/cc2f641b-698b-4539-81e4-ee5af4ff5c25" />



### EX Q: What is the tetrachoric-based alpha? 

# Computing the Standard Error of measurement for the total score

<img width="840" height="178" alt="Screenshot 2026-05-13 at 1 41 40 pm" src="https://github.com/user-attachments/assets/4c565d56-1bdc-421d-9549-16eea335b662" />

<img width="452" height="196" alt="image" src="https://github.com/user-attachments/assets/b0584222-fed5-4636-b22e-7599ffa04452" />

 
# Computing the Confidence Interval around a score

>> N_score[1]-2*SEm

>> N_score[1]+2*SEm

 
# < Testing homogeneity of a psychometric scale>

### package install

>> library(psych)

### read data

>> load("SDQ.RData") 

### selecting variables 

>> items_conduct <- c("tantrum","obeys","fights","lies","steals")

### full correlation matrix

>> lowerCor(SDQ[items_conduct])  

<img width="408" height="118" alt="image" src="https://github.com/user-attachments/assets/7ea4d2ce-21a8-4aa6-90ca-e01c4edf012f" />

### Kaiser-Meyer-Olkin (KMO) index – the measure of sampling adequacy (MSA)

>> KMO(SDQ[items_conduct])

<img width="986" height="362" alt="Screenshot 2026-05-13 at 1 43 37 pm" src="https://github.com/user-attachments/assets/a40288dc-020d-4c08-970a-65f243eae009" />

<img width="452" height="190" alt="image" src="https://github.com/user-attachments/assets/dbde6e6a-fd4f-4557-949a-40bbf19188f9" />

  
### Parallel Analysis Scree

>> fa.parallel(SDQ[items_conduct], fa="pc")	
 
<img width="452" height="42" alt="image" src="https://github.com/user-attachments/assets/fc5a247a-2862-4d74-81b0-934ad9fa00ab" />

 <img width="452" height="401" alt="image" src="https://github.com/user-attachments/assets/ebd886c2-1023-41b1-ad87-ac6ada0930a5" />
 
<img width="1264" height="486" alt="Screenshot 2026-05-13 at 1 44 09 pm" src="https://github.com/user-attachments/assets/a138e3b4-ca13-44ce-b6ae-5ccfa41cf530" />


### Fitting and interpreting a single-factor model

>> fa(SDQ[items_conduct],nfactors=1) 

EX Q: 

<img width="1320" height="1002" alt="Screenshot 2026-05-13 at 1 45 06 pm" src="https://github.com/user-attachments/assets/9507229d-d87e-4161-9165-95afab36f542" />

<img width="452" height="248" alt="image" src="https://github.com/user-attachments/assets/3f0b03d6-daad-4c6c-8d2b-23851f18956d" />

### Q. Is the chi-square for the tested model significant? Do you accept or reject the single-factor model? [Look for “Likelihood Chi Square” in the output.]  

<img width="452" height="171" alt="image" src="https://github.com/user-attachments/assets/82eee3ce-5cb9-4a0a-9450-ed8700495942" />

<img width="1276" height="710" alt="Screenshot 2026-05-13 at 1 45 45 pm" src="https://github.com/user-attachments/assets/e1986548-2baf-4510-acb9-d6b4032f29b4" />

Note. The hypothesis cannot be rejected{=accept} (prob > 0.05); the scale is homogeneous

### Residuals 

>> F_conduct <- fa(SDQ[items_conduct], nfactors=1)

### without removing diagonal

>> residuals.psych(F_conduct)

<img width="375" height="123" alt="image" src="https://github.com/user-attachments/assets/fcedaf0c-3ca1-44b9-a038-b67f31510506" />

### removing diagonal

residuals.psych(F_conduct, diag=FALSE)

 <img width="363" height="123" alt="image" src="https://github.com/user-attachments/assets/6234558d-1cf4-4abe-8fe8-58691f837116" />

- Standards are the same as correlation; therefore, consider r < 0.3: small, r < 0.5: medium, r < 0.7: large. Consider that the error rate is high, if it exceeds 0.3 or is close to that.

### reverse coding

Note. *Obey the negative sign in the correlation matrix*, need to reverse the coding

>> R_conduct <- reverse.code(c(1,-1,1,1,1), SDQ[items_conduct])

>>alpha(R_conduct)

<img width="1278" height="450" alt="Screenshot 2026-05-13 at 1 51 05 pm" src="https://github.com/user-attachments/assets/2186e464-88c2-4175-8a19-4e8ff81c1c4c" />

 
### install package

>> library(GPArotation) 

### omega total

>> omega(R_conduct, nfactors=1)
 
<img width="1268" height="484" alt="Screenshot 2026-05-13 at 1 52 36 pm" src="https://github.com/user-attachments/assets/d93a0b12-7068-47cc-9362-7dcb6900c72a" />


# <Exploratory Factor Analysis of personality test scores>

### package install

>> library(psych)

### read data

>> load("neo.RData") 

### measure of sampling adequacy (MSA)

>> KMO(neo)

<img width="1316" height="278" alt="Screenshot 2026-05-13 at 1 53 13 pm" src="https://github.com/user-attachments/assets/80d819c3-4b30-4c56-aba1-432a07c19027" />


### scree plots

>> fa.parallel(neo, n.obs=1000, fm="ml", fa="pc")
 
<img width="1280" height="88" alt="Screenshot 2026-05-13 at 1 53 44 pm" src="https://github.com/user-attachments/assets/91b7e088-1368-465a-af40-5197357faa24" />

<img width="452" height="291" alt="image" src="https://github.com/user-attachments/assets/73d9d318-28c7-4291-b967-1161e7399025" />


* if you don’t need the n.observation:

<img width="452" height="154" alt="image" src="https://github.com/user-attachments/assets/f6687672-a130-46ea-b036-972667a3aba2" />


# Result of chi-square statistic testing the 5-factor model, Fitting an exploratory 5-factor model

## {NEED GPA rotation package}

>> fa(neo, nfactors=5, n.obs=1000, fm="ml")

↳ nfactors : neo have 5 factors in their survey script 


QUESTION: Find the result of the chi-square statistic testing the 5-factor model (look for “Likelihood Chi Square”). How many degrees of freedom are there? What is the chi square statistic, and p value, for the tested model? Would you retain or reject this model based on the chi-square test? Why?


<img width="1292" height="300" alt="Screenshot 2026-05-13 at 1 55 06 pm" src="https://github.com/user-attachments/assets/372c5427-f369-4b52-9f5c-5ce2aaea7a96" />


# Model residuals, evaluate the root mean square of the residuals (RMSR), which is a summary of all residuals

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


### QUESTION 6. Examine the standardised factor loadings (pattern matrix), and name the factors you obtained based on which facets load on them.
= ML1=Neuroticism; ML4=Conscientiousness, ML3=Agreeableness, ML2=Extraversion, ML5=Openness (see the salient loadings marked in Q7) 

- When you see Neo PI Description, ordered in neuroticisim -> extraversion -> agreeableness -> conscientiousness -> openness

<img width="1276" height="652" alt="Screenshot 2026-05-13 at 1 56 10 pm" src="https://github.com/user-attachments/assets/a7720291-7b90-4e8a-9f04-616b7cf42886" />


### QUESTION 7. Examine the factor loadings again, this time looking for cross-loading facets (facets with loadings greater than 0.32 on factor(s) other than its own). Refer to the NEO facet descriptions in the supplementary document to hypothesise why these cross-loadings may have occurred.

<img width="259" height="342" alt="image" src="https://github.com/user-attachments/assets/ae4be032-5078-4cb5-b345-e0b351371c79" />


 
* ML2: Extraversion and E4 is extraversion question, so when you compared {correlation between ML4 and E4}, {correlation between ML3 and E4}, and {correlation between ML2 and E4} correlation between ML2 and E4 need to be largest, but it isn’t


∴ There are several cross-loadings for facets of Agreeableness (factor ML3) and Extraversion (factor ML2) - see the loadings below. For instance, E4 (Activity), described as ‘pace of living’ loads on Extraversion as expected (0.36) but even slightly stronger on Conscientiousness (0.39) and negatively on Agreeableness (-0.38). Perhaps the need to meet deadlines and achieve (part of Conscientiousness) has an effect on the ‘pace of living’, as well as the need to ‘get ahead’ (the low end of Agreeableness).



### QUESTION 8. Examine the columns h2 and u2 of the factor loadings (pattern matrix). The h2 column is the facet’s communality (proportion of variance due to all of the common factors), and u2 is the uniqueness (proportion of variance unique to this facet). The communality and uniqueness must sum to 1. Based on communalities, which facets are the least explained by the factor model we just tested? Which are the best explained? 

<img width="1206" height="1162" alt="Screenshot 2026-05-13 at 1 57 24 pm" src="https://github.com/user-attachments/assets/3264a89d-f373-49be-ada0-e384acc9705d" />


∴ Facets O6 (Values) and O4 (Ideas) are the least explained by the factors in this model. Their communalities (see column “h2”) are only 15% and 28%, respectively. O6 Values is an unusual scale, quite different from other NEO scales. It has attitudinal rather than behavioural statements, such as “I believe letting students hear controversial speakers can only confuse and mislead them’.
+) Facets N3 (Depression) and C5 (Self-Discipline) are best explained by the factors in this model.



### QUESTION 9. Find and interpret the factor correlation matrix. Which factors correlate the strongest? 

<img width="806" height="374" alt="Screenshot 2026-05-13 at 1 58 34 pm" src="https://github.com/user-attachments/assets/e4b4f2a2-050e-463e-b602-ca94e795017f" />


∴ Overall, the five factors correlate quite weakly, but they are not orthogonal. ML1 (Neuroticism) correlates negatively with all other factors; the rest of the factors correlate positively with each other. The strongest correlation is between ML1 (Neuroticism) and ML4 (Conscientiousness) (r=–.41).
 
# <Confirmatory Factor Analysis> 

### Package install

>> library(psych)
>> library(lavaan)

### Read data

>> load("Thurstone.RData")

### Specifying and fitting a measurement model
<img width="452" height="113" alt="image" src="https://github.com/user-attachments/assets/bfaa1cb1-8964-455f-af27-2174c7dcc444" />
<img width="403" height="133" alt="image" src="https://github.com/user-attachments/assets/5d839934-5a19-4543-ab7b-1e337cfe2831" />

<img width="880" height="168" alt="Screenshot 2026-05-12 at 10 17 59 pm" src="https://github.com/user-attachments/assets/8730fbe9-7268-4b66-a0d0-6543f46760aa" />


             
### Fit the model with default scaling, and ask for summary output 

>> fit <- cfa(model=T.model, sample.cov=Thurstone, sample.nobs=215)

### Factor loading, Std.Err, z-values or p-values, latent variables, parameters
   
>> summary(fit)

<img width="452" height="209" alt="image" src="https://github.com/user-attachments/assets/1ca5034d-6fde-4d2e-97e2-e947be77d27b" />

### Factor loading, Std.Err, z-values or p-values
  
∴ The factor loadings for s1, s4 and s7 were not actually estimated; instead, they were fixed to 1 to set the scale of the latent factors (latent factors then simply take the scale of these particular measured variables). That is why there is no usual estimation statistics reported for these. Factor loadings for the remaining 6 subtests (9-3=6) are free parameters in the model to estimate.

 <img width="452" height="359" alt="image" src="https://github.com/user-attachments/assets/9688e04e-e878-4d99-92fc-ded5f8d5dadc" />

### Latent variables
  
∴ There are 12 unobserved (latent) variables – 3 common factors (Verbal, WordFluency and Reasoning), and 9 unique factors /errors (these are labelled by the prefix ‘.’ in front of the observed variable to which this error term is attached, for example .s1, .s2, etc. It so happens that in this model, all the latent variables are exogenous (independent), and for that reason variances for them are estimated. In addition, covariances are estimated between the 3 common factors (3 covariances, one for each pair of factors). Of course, the errors are assumed uncorrelated (remember the local independence assumption in factor analysis?), and so their covariances are fixed to 0 (not estimated and not printed in the output).

<img width="1198" height="346" alt="Screenshot 2026-05-13 at 2 00 27 pm" src="https://github.com/user-attachments/assets/0f2100c2-ec7a-4a60-952c-e6b04d124711" />


### Parameters

∴ You can look this up in lavaan output. It says: “Number of free parameters 21”. To work out how this number is derived, you can look how many rows of values are printed in ‘Parameter Estimates’ under each category. The model estimates: 6 factor loadings (see Q1) + 3 factor variances (see Q2) + 3 factor covariances (see Q2) + 9 error variances (see Q2). That’s it. So we have 6+3+3+9=21 parameters.

#### ‘Sample moments’ refers to the number of variances and covariances in our observed data
  
: m(m+1)/2 = ex: 9 observed variables, therefore there are 9(9+1)/2=45


<img width="452" height="87" alt="image" src="https://github.com/user-attachments/assets/9016bcb7-661a-412f-ae99-d872231e8822" />

### Chi-square
 
∴ Chi-square is 38.737 (df=24). We have to reject the model, because the test indicates that the probability of this factor model holding in the population is less than .05 (P = .029).

### Extended output

#### SRMR, CFI and RMSEA.  

>> summary(fit, fit.measures=TRUE)

<img width="452" height="72" alt="image" src="https://github.com/user-attachments/assets/ed628340-c34f-476c-8fa6-309a604276f0" />

<img width="436" height="78" alt="image" src="https://github.com/user-attachments/assets/fd586f3e-7760-4fe7-b718-8c5a505fcbf4" />
 
<img width="420" height="138" alt="image" src="https://github.com/user-attachments/assets/a50693b8-6b44-4289-b487-5e55e360f72a" />

∴ Comparative Fit Index (CFI) = 0.986, which is larger than 0.95, indicating good fit. Root Mean Square Error of Approximation (RMSEA) = 0.053, just outside of the cut-off .05 for close fit. The 90% confidence interval for RMSEA is (0.017, 0.083), which just includes the cut-off 0.08 for adequate fit. Overall, RMSEA indicates close to adequate fit. Standardized Root Mean Square Residual (SRMR) = 0.044 is small as we would hope for a well-fitting model. All indices indicate close fit of this model, despite the significant chi-square.


### Alternative scaling of latent factors
>> fit.2 <- cfa(T.model, sample.cov=Thurstone, sample.nobs=215, std.lv=TRUE)

### Factor loading, factor covariances, error variances.

>> summary(fit.2)

<img width="442" height="256" alt="image" src="https://github.com/user-attachments/assets/1976e107-fb6b-402f-afd9-d24aa67ef52b" />

 
### Factor loading

∴ All factor loadings are positive as would be expected with ability variables, since ability subtests should be positive indicators of the ability domains. The SEs are low (magnitude of 1/SQRT(N), as they should be in a properly identified model). All factor loadings are significantly different from 0 (p-values are very small).
 
 <img width="441" height="150" alt="image" src="https://github.com/user-attachments/assets/e90f3f33-e2d3-4a53-aaac-c32ddc32b9ee" />


### factor covariance

∴ The factor covariances are easy to interpret in terms of size, because we set the factors’ variances =1, and therefore, factor covariances are correlations. The correlations between the 3 ability domains are positive and large, as expected.

<img width="452" height="174" alt="image" src="https://github.com/user-attachments/assets/4a3e4538-37b2-40f7-8296-272b170df092" />

 
### Error variance

∴ The error variances are certainly quite small – considering that the observed variables had a variance 1 (remember, we analysed the correlation matrix, with 1 on the diagonal?), the error variance is less than half that for most subtests. The remaining proportion of variance is due to the common factors. For example, for s1, the error variance is 0.18, and this means 18% of the variance is due to error, and the remaining 82% (1-0.18) is due to the common factors.


### Standardised solution (in which EVERYTHING is standardised - the latent and observed variables)

#### Factor loading, covariance, error variance

>> summary(fit.2, standardized=TRUE)

### Examining residuals and local areas of misfit

>> fitted(fit.2)

>> residuals(fit.2)


### standardised residuals

>> residuals(fit.2, type="standardized")

### modification indices

>> modindices(fit.2)


# <Path analysis>
  
### read data

>> load("Wellbeing.RData")

### package install

>> library(lavaan)

### Specifying and fitting the model

 <img width="403" height="133" alt="image" src="https://github.com/user-attachments/assets/bc1c792f-b3dd-4792-8330-d643a3082ca8" />

 <img width="496" height="474" alt="Screenshot 2026-05-12 at 10 23 56 pm" src="https://github.com/user-attachments/assets/e19f8163-aa8c-4657-9fa2-d824c4416956" />

###  Number of model parameters  

#### Number of free parameters(number of model parameters)

>> sem(W.model, sample.cov=Wellbeing, sample.nobs=149)

<img width="1200" height="598" alt="Screenshot 2026-05-13 at 2 07 15 pm" src="https://github.com/user-attachments/assets/b8e92526-e319-4b25-a267-0908dc01da91" />


>> fit <- sem(W.model, sample.cov=Wellbeing, sample.nobs=149)

#### Regression, covariances, variances

>> summary(fit, fit.measures=TRUE) 

<img width="1168" height="544" alt="Screenshot 2026-05-13 at 2 08 03 pm" src="https://github.com/user-attachments/assets/b84658c6-3fcd-49ee-9660-ae4717799de0" />

 
### QUESTION 3. Interpret the chi-square. Do you retain or reject the model?

∴ The chi-square test (Chi-square = 10.682, Degrees of freedom = 2, P-value = .005) suggests rejecting the model because the test is significant (p-value is very low). In this case, we cannot “blame” the poor chi-square result on the large sample size (our sample is not that large).

### R esiduals covariance

>> residuals(fit)

<img width="916" height="526" alt="Screenshot 2026-05-13 at 2 08 31 pm" src="https://github.com/user-attachments/assets/abb6c60c-5127-4c41-936b-49354424cca2" />

 
>> residuals(fit, type="standardized")

<img width="1056" height="512" alt="Screenshot 2026-05-13 at 2 09 13 pm" src="https://github.com/user-attachments/assets/d209505a-1027-440b-81bb-283805cfb2b3" />


Note. We usually interpret a correlation of 0.1 as small; and correlations below 0.1 as trivial. Use the same logic for interpreting the residual correlations.) The residuals for these omitted paths are small in magnitude (just under 0.1), but one borderline residual PS/SWB (=0.096) is significantly different from zero (stdz value = 2.051 is larger than the critical value 1.96).



###  Computing indirect and total effects

 <img width="452" height="186" alt="image" src="https://github.com/user-attachments/assets/71c207ea-0366-4c06-82cb-1e74cc593095" />
 
>> <img width="1202" height="864" alt="Screenshot 2026-05-13 at 2 10 34 pm" src="https://github.com/user-attachments/assets/47b70344-4371-4acc-8f0c-83dcc37c9b0b" />


<img width="452" height="195" alt="image" src="https://github.com/user-attachments/assets/b8b10596-ab16-426f-b092-ceada9f23a1e" />

<img width="1098" height="306" alt="Screenshot 2026-05-13 at 2 11 01 pm" src="https://github.com/user-attachments/assets/173ddc9e-8273-4e3b-a3c2-002d161eb849" />

### QUESTION 7. What is the indirect effect of PS on SWB via WA? What is the indirect effect of PS on SWB via CT? What is the total indirect effect of PS on SWB (the sum of the indirect paths via WA and CT)? How do the numbers correspond to the observed covariance of PS and SWB?

<img width="1236" height="182" alt="Screenshot 2026-05-13 at 2 11 24 pm" src="https://github.com/user-attachments/assets/1ff422da-3d44-4a97-b01a-2e6904b6964e" />


# <Structural models for repeated measures>

### Creating project and examining data

### Reading data

>> SDQ <- read.csv(file="SDQ_repeated.csv")
>> library(psych)

#### full descriptive statistics for all variables

>> describe(SDQ)

>> library(lavaan)

### Fitting a basic structural model for repeated measures


<img width="1060" height="494" alt="Screenshot 2026-05-13 at 2 12 57 pm" src="https://github.com/user-attachments/assets/d04f5e85-d99c-464d-aca2-7864e87ae1c7" />


### Ask for summary output including fit indices

#### chi-square test, SRMR, CFI and RMSE

>> summary(fit0, fit.measures=TRUE)

<img width="452" height="98" alt="image" src="https://github.com/user-attachments/assets/18d4e3f9-c8dd-4615-be4b-41833666033c" />

<img width="415" height="65" alt="image" src="https://github.com/user-attachments/assets/41723c8c-f7fe-4f4b-9d41-f10dd1afb64d" />

<img width="420" height="97" alt="image" src="https://github.com/user-attachments/assets/f3052d02-cb39-432d-b1bd-222c7dfcbc18" />

<img width="433" height="135" alt="image" src="https://github.com/user-attachments/assets/09daff12-a354-4be6-be16-ab52c81e7fa0" />


### Modification indices

>> modindices(fit0)

<img width="452" height="323" alt="image" src="https://github.com/user-attachments/assets/c82c0ce0-a63f-48d8-b433-46c2b4fe7f58" />


### EX Q: What do the modification indices tell you? Which two changes in the model would produce the greatest decrease in the chi-square? How do you interpret these model changes?

A: Two largest modification indices (MI) by far can be found in the covariance ~~ statements: p1_hyper~~ p2_hyper (mi=248.422) and p1_prosoc~~p2_prosoc (mi=156.286).

The first MI tells you that if you repeat the analysis, allowing p1_hyper and p2_hyper to correlate (actually, because these are DVs, the correlation will be between their errors/unique factors), the chi-square will fall by about 248. 

But is this reasonable to allow errors/unique factors for the same measures at Time 1 and Time 2 to correlate? Consider how the variance on the Hyperactivity facet is explained by both the common Externalising factor and the remaining unique content of the facet (the unique factor). Because the same Hyperactivity scale was administered on two different occasions, its unique content not explained by the common Externalising factor would be still shared between the occasions. 

Therefore, the unique factors at Time 1 and Time 2 cannot be considered independent. The correlated errors will correct for this lack of local independence. Similarly, we should allow correlated errors across time for the Pro-social construct (p1_prosoc and p2_prosoc). A correlated error for p1_conduct and p2_conduct is not needed since M.I. did not suggest it.

### Modify the model to allow the unique factors (errors) of p1_hyper and p2_hyper, and errors of p1_prosoc and p2_prosoc to correlate.

<img width="1082" height="712" alt="Screenshot 2026-05-13 at 2 15 59 pm" src="https://github.com/user-attachments/assets/2d6eeedb-3b1f-4736-a06c-c8d165abfc31" />

### Q: chi-square for the model with correlated errors for repeated measures (Model 1). 

<img width="437" height="109" alt="image" src="https://github.com/user-attachments/assets/e77d00af-438e-457a-95de-f76d117e6ce3" />

### Fitting a full measurement invariance model for repeated measures

<img width="930" height="1158" alt="image" src="https://github.com/user-attachments/assets/df2bd61c-83d3-4d3e-8085-037059070d03" />

>> fit2 <- sem(model = Model2, data = SDQ, meanstructure=TRUE)

### For chi-square test, SRMR, CFI and RMSE

>> summary(fit2, fit.measures=TRUE) 

<img width="422" height="98" alt="image" src="https://github.com/user-attachments/assets/503f0c3c-e848-4bf3-8a2a-0567784f4b56" />
 
>> modindices(fit2)

<img width="452" height="378" alt="image" src="https://github.com/user-attachments/assets/86d9ddd3-aefa-4517-aedc-1d7310b7c9b1" />

=> 24, 25

### Carry out the chi-square difference test to compare nested models Model 2 and Model 3. Report the chi-square difference statistic here as a number. 

<img width="321" height="80" alt="image" src="https://github.com/user-attachments/assets/efd5e048-7e9f-4429-88aa-11d3c3a02a1d" />


<img width="452" height="136" alt="image" src="https://github.com/user-attachments/assets/c10cc088-9827-4047-82ee-e5cba6ee0487" />



# <Fitting measurement models to multiple groups>

## Creating project and examining data

### reading data

>> library(lavaan)

>> library(psych)

### Data import

>> data(HolzingerSwineford1939)

: A new object HolzingerSwineford1939 should appear in your Environment tab

### sampling out the target population

>> sample <- HolzingerSwineford1939[HolzingerSwineford1939$school=="Grant-White", ]

: a new object called sample with only children from school Grant-White included

### give value labels for sex variable
                    
<img width="487" height="87" alt="image" src="https://github.com/user-attachments/assets/dc35fa24-64dc-4e4d-af4a-8a309e088461" />

### Descriptives by sex: Descriptive statistics by group

>> describeBy(sample, group="sex")


Ex QUESTION 1. Examine the means of the six test variables for boys and girls. Note the mean differences for x3 (spatial orientation), and all verbal tests (x4-x6). Who scores higher on what tests?

<img width="1274" height="1078" alt="Screenshot 2026-05-16 at 1 54 18 pm" src="https://github.com/user-attachments/assets/c79c02a2-1b49-4ce8-ad2c-4d56f150f44d" />

A: Boys scored higher than girls on x3, but girls scored higher than boys on all verbal tests (x4, x5 and x6).


# Fitting a baseline measurement model to two subgroups (boys and girls)

## Describe the measurement (confirmatory factor analysis, or CFA) model

<img width="487" height="68" alt="image" src="https://github.com/user-attachments/assets/6d42b706-76bd-4966-8e46-f87ef87f4e0c" />

# Fitting Baseline (Configural) model

>> fit.b <- cfa(HS.model, data = sample, group = "sex")
>> summary(fit.b, fit.measures=TRUE): chi-square, df, p-value, CFI, RMSEA,SRMR


## QUESTION 2. How many sample moments are there in the data? Why? {Hint. When counting sample moments, do not forget that we split the data into 2 groups, so observed means, variances and covariances are available for both groups}.

A: There are 6 observed variables, therefore 6 means, plus 6(6+1)/2=21 variances and covariances; 27 moments in total for each group. So we have 27*2=54 sample moments in both groups.

## QUESTION 3. How many parameters does the baseline (configural) model estimate? What are they? {Hint. You can look up the total number of parameters in the output, but try to work out how these are made up. The output will help you, if you look in ‘Parameter Estimates’. Remember that values printed there are parameters.}

A: Baseline model estimates 38 parameters in total. Boys and girls groups estimate the same parameters (i.e. there are 19 parameters in each group)

<img width="452" height="105" alt="image" src="https://github.com/user-attachments/assets/d06fbba5-0ed2-4198-a92e-9d2e74d0b682" />

## QUESTION 4. Interpret the chi-square, and SRMR. Do we retain or reject the baseline model?

A: Chi-square for the baseline model is insignificant (chisq = 16.710; Degrees of freedom = 16; p = .405). The SRMR is 0.040 – nice and small.

# Fitting a full measurement invariance model to subgroups

# Fitting the Measurement Invariance model

<img width="487" height="105" alt="image" src="https://github.com/user-attachments/assets/495607a3-a901-4daf-9092-0644b1b27527" />

-> What you have just done is fit a full measurement invariance model. The model tests the following combined hypothesis:

H1. The measure is fully invariant across groups. Factor loadings, intercepts and error variances for corresponding indicators are equal.

## QUESTION 5. Interpret the chi-square and SRMR. Do we retain or reject the full measurement invariance model?

A: Chi-square for the measurement invariance model is again insignificant (chisq = 27.482, Degrees of freedom = 30, P-value = 0.598). The SRMR is 0.058 – small again. The almost equal chi-square values for both groups (boy chisq = 13.693, girl chisq = 13.789) indicate that the measurement invariance model is equally appropriate for boys and girls.

<img width="452" height="333" alt="image" src="https://github.com/user-attachments/assets/bd8429a0-3e2d-42ce-b83e-c8a7b5476c11" />
<img width="452" height="203" alt="image" src="https://github.com/user-attachments/assets/b9fc71fc-b0a6-47a2-bb7b-f7a4ba8ef409" />


## QUESTION 6. How many parameters does the measurement invariance model estimate? What are they? {Hint. Again, look up the total number of parameters in the output, and then try to work out how these are made up. The ‘Parameter Estimates’ output and the above explanation will help you.}

A: The output says that ‘Number of free parameters’ is 40, and ‘Number of equality constraints’ is 16. This means that 40-16=24 unique parameters are estimated

<img width="413" height="126" alt="image" src="https://github.com/user-attachments/assets/135f8f62-1ccf-4545-8619-b315c63972d9" />


# Testing Equality of means of latent factors : All you need to do is to add one more group equality constraint, for latent variable "means"

<img width="487" height="83" alt="image" src="https://github.com/user-attachments/assets/7a1ae17a-91d2-471d-8d36-811eb7e2562e" />

## EX Q: Now fit the HS.model separately to boys and girls of Pasteur school, imposing equality constraints on the factor loadings only (i.e. fit a Metric invariance model). What is the chi-square statistic for the boy subgroup? 

A: The correct answer is: 18.081

<img width="1260" height="352" alt="Screenshot 2026-05-16 at 2 23 27 pm" src="https://github.com/user-attachments/assets/78b28a8b-84e0-4041-a8d8-798394c8843c" />

### Note. Because the two models are nested (one is a special case of the other), you can conduct the chi-square difference test using the R base function anova(), which will compute the difference of the models’ chi-square statistics and the difference of their degrees of freedom, and print out the resulting p-value.

>> anova(fit.mi, fit.mi.e)

## QUESTION 8. Conduct the chi-square difference test of models with and without the equality constraints as described above, and interpret the results. Are the models significantly different? Which model will you retain?

The model with additional constraints (fit.mi.e) has the Chi-square = 35.786; Degrees of freedom = 32. Testing the difference between this model and the previous model (fit.mi), we obtain Diff(Chi-square) = 35.786–27.482= 8.304 and Diff(DF) = 32–30 = 2.

=> Chi-square of 8.304 on 2 degrees of freedom is significant at the 0.05 level, with the p-value=0.016. Restricting the model with additional equality constraints resulted in a significantly different (worse) fit. The fit is worse is because the chi-square is greater (and constraining some free parameters cannot make the fit better!). We conclude that the means for boys and girls on the Spatial and Verbal tests are significantly different, and that our measurement invariance model with free means is better than the model with means constrained to be equal.


 * Note. How the fit can be ‘significantly worse’ if it is still very good, according to the chi-square test (the SRMR, not being a ‘significance’ measure but an ‘effect size’ measure, picked up the worsening fit). Here, the small sample works against us – there is not enough power to reject the ‘wrong’ model (it has too many parameters), but just enough power to detect the elements of the model that make a difference.

<img width="452" height="114" alt="image" src="https://github.com/user-attachments/assets/51c3c1b5-c513-41d1-855d-a4dcfca3eed7" />


# <Logistic regression – application to DIF analysis>


## Data set - preliminary examination

EPQ <- read.delim(file="EPQ_N_demo.txt", header=TRUE)

## Screening EPQ Neuroticism items for gender DIF

## Creating the trait (matching) variable, and the grouping variable

### Compute the Neuroticism trait score (call it Nscore), and append it to the dataset as a new variable

>> PQ$Nscore <- rowMeans(EPQ[ ,4:26], na.rm=TRUE)*23

* item responses are located in columns 4 to 26


## The variable sex is coded as 0 = female; 1 = male. ATTENTION: this means that “male” is the focal group


<img width="487" height="87" alt="image" src="https://github.com/user-attachments/assets/f705ccda-adaf-438d-9d95-64597dc5733f" />

>> library(psych)

### Descriptive statistics by group

>> describeBy(EPQ, group="sex")

## EX Q: Who has the higher proportion of endorsing item N_19 – males or females? (Hint. Remember that for binary items coded 0/1, the item mean is also the proportion of endorsement.) Who score higher on the Neuroticism scale (Nscore) on average – males or females? (Interpret the means for N_19 in the light of the Nscore means)

<img width="1308" height="1174" alt="Screenshot 2026-05-16 at 2 30 57 pm" src="https://github.com/user-attachments/assets/f4056c87-f683-48cb-ba58-dc9da4d414f2" />


# Specifying logistic regression models

## Baseline model 

>> Baseline <- glm(N_19 ~ Nscore, data = EPQ, family = binomial(link="logit"))

## Uniform DIF model 

>> dif.U <- glm(N_19 ~ Nscore + sex, data = EPQ, family = binomial(link="logit"))

## Non-Uniform DIF model

>> dif.NU <- glm(N_19 ~ Nscore + sex + Nscore:sex, data = EPQ, family = binomial(link="logit"))

## Testing for the significance of uniform and non-uniform effects of sex

>> anova(dif.NU, test= "Chisq")

<img width="914" height="1152" alt="Screenshot 2026-05-16 at 2 32 59 pm" src="https://github.com/user-attachments/assets/f31e8a07-32b0-48ee-b76b-a4c35a0f2f00" />


## EXQ: Does sex add significantly over and above Nscore? What is the chi-square increment compared to the baseline model? 

Note. The first, baseline model, will include the total Nscore as the only predictor of N_80. The second, uniform DIF model, will include the total Nscore and participants' sex as predictors. [We will NOT test for non-uniform DIF]. 

<img width="1284" height="610" alt="Screenshot 2026-05-16 at 2 34 40 pm" src="https://github.com/user-attachments/assets/4f04b770-5412-4a48-b96b-9283c63dd69f" />


#Evaluating effect sizes for uniform and non-uniform effects of sex - use package "fmsb"


