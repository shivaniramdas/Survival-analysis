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

