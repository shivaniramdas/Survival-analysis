# Survival-analysis
Were some passengers more likely to survive the unfortunate?

## About

The widely considered “unsinkable” RMS Titanic sank after colliding with an iceberg. Unfortunately, there weren’t enough lifeboats for everyone onboard, resulting in the death of 1502 out of 2224 passengers and crew.While there was some element of luck involved in surviving, it seems some groups of people were more likely to survive than others.

Here I have worked on building a predictive model that answers the question: “what sorts of people were more likely to survive?” using passenger data (ie name, age, gender, socio-economic class, etc)

## Data

Train.csv contains the details of a subset of the passengers on board (891 to be exact) and importantly, will reveal whether they survived or not, also known as the “ground truth”. The `test.csv` dataset contains similar information but does not disclose the “ground truth” for each passenger.

Variable | Description | Values
---------|-------------|---------
survival | Survival |	0 = No, 1 = Yes
pclass | Ticket class |	1 = 1st, 2 = 2nd, 3 = 3rd
sex |	Sex	
Age |	Age in years	
sibsp |	# of siblings / spouses aboard the Titanic	
parch |	# of parents / children aboard the Titanic	
ticket |	Ticket number	
fare |	Passenger fare	
cabin |	Cabin number	
embarked | Port of Embarkation | C = Cherbourg, Q = Queenstown, S = Southampton

* pclass: A proxy for socio-economic status (SES)
1st = Upper
2nd = Middle
3rd = Lower

* age: Age is fractional if less than 1. If the age is estimated, is it in the form of xx.5

* sibsp: The dataset defines family relations in this way
Sibling = brother, sister, stepbrother, stepsister
Spouse = husband, wife (mistresses and fiancés were ignored)

* parch: The dataset defines family relations in this way...
Parent = mother, father
Child = daughter, son, stepdaughter, stepson
Some children travelled only with a nanny, therefore parch=0 for them

## Findings and Stats

> SEX

* It is evident that only 38.38 % of the population on the ship survived , rest died
* There were 109 males across the ship who survived that accident
* There were 233 females across the ship who survived that accident

> Ticket class 

* It is evident that in overall, the males and females of Pclass 3 died more than others
* The males and female of Pclass 3 showed a remarkable increase in death, showing increasing trend in death as class shifts down
* Females showed a near fall down trend as expected but pclass=2 females survived less than the Pclass=3 females
* The males on contrary showed a dip in between i.e. in males who survived , Plass --> 3 > 1 > 2
* Including both the sexes, 2nd class survived less than the other two clases
* Almost all women in Pclass 1 and 2 survived and nearly all men in Pclass 2 and 3 died

> Embarked

* This shows that those who were embarked S survived more than those who were embarked C and then Q
* Most of the people who died were embarked S
* Also, people survived with embarked Q were mostly from Plass 3 females
* survived axis shows the % which means embarked Q males in Pclass 1 and 2 all died
* embarked females in Pclass 1 and 2 all lived

> AGE

* All female in Pclass 3 and Age_bin = 5 died
* Males in Age_bin >= 2 and Pclass died more than survived or died greater than 50%

> Siblings and Spouse

* Females in Pclass 1 and 2 with siblings upto 3 nearly all survived
* For Pclass 3 , males and females showed a near decreasing trend as number of siblings increased
* For males, no survival rate above 0.5 for any values of SibSp(less than 50%)

> Partents or Children

* For males, all survival rates below 0.5 for any values of Parch, except for Parch = 2 and Pclass = 1
* Maximum people are travelling with no siblings
* More people were travelling with only their 1 parent rather than 2
* Maximum population on the ship was aged between 15 yrs to 50 yrs
* Most of the people only paid upto 50 as their fare

## Algorithms for predicting the survival

A couple of algorithms were trained and their performance was compared:

```
MLA = []
x = [LinearSVC() , DecisionTreeClassifier() , LogisticRegression() , KNeighborsClassifier() , GaussianNB() ,
    RandomForestClassifier() , GradientBoostingClassifier()]

X = ["LinearSVC" , "DecisionTreeClassifier" , "LogisticRegression" , "KNeighborsClassifier" , "GaussianNB" ,
    "RandomForestClassifier" , "GradientBoostingClassifier"]

for i in range(0,len(x)):
    model = x[i]
    model.fit( X_train , y_train )
    pred = model.predict(X_test)
    MLA.append(accuracy_score(pred , y_test))
```

Much of the algorithms are giving the accuracy between 77% to 80% with some above 80%

Finally used KNN:

Accuracy turns out to be 85.074% with n-neighbors = 6

Different values of K were tested:

```
KNNaccu = []
Neighbours = []

for neighbour in range(1,31):
    model = KNeighborsClassifier(n_neighbors=neighbour)
    model.fit( X_train , y_train )
    pred = model.predict(X_test)
    KNNaccu.append(accuracy_score(pred , y_test))
    Neighbours.append(neighbour)
```

Conclusion:

For Neighbours = 6 , the accuracy is the maximum
